---
title: Devre kartına ASP.NET Core SignalR ölçek genişletme için redis
author: tdykstra
description: Bir ASP.NET Core SignalR uygulama için ölçek genişletme etkinleştirmek için bir Redis devre kartı kurmayı öğrenin.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/redis-backplane
ms.openlocfilehash: 343cb5b2c7ed7162bae7865553a783fea45f0cfb
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284482"
---
# <a name="set-up-a-redis-backplane-for-aspnet-core-signalr-scale-out"></a>Bir Redis devre kartı ASP.NET Core SignalR genişleme için ayarlama

Tarafından [Andrew Stanton-Nurse](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), ve [Tom Dykstra](https://github.com/tdykstra),

Bu makalede, SignalR özgü yönlerini ayarlama açıklanmaktadır bir [Redis](https://redis.io/) bir ASP.NET Core SignalR uygulamayı kullanıma ölçeklendirme için kullanılacak sunucusu.

## <a name="set-up-a-redis-backplane"></a>Bir Redis devre kartı ayarlayın

* Bir Redis sunucusuna dağıtın.

  Üretim kullanımı için yalnızca şirket içi altyapı için bir Redis devre kartı önerilir. Gecikme süresini en aza indirmek için aynı veri merkezinde SignalR uygulama olarak Redis sunucusu olmalıdır. SignalR uygulamanızı Azure bulutunda çalışır durumdaysa bir Redis devre kartı yerine Azure SignalR hizmeti öneririz. Azure Redis Cache hizmeti kullanmak için geliştirme ve test ortamları. Daha fazla bilgi için aşağıdaki kaynaklara bakın:

  * <xref:signalr/scale>
  * [Redis belgeleri](https://redis.io/)
  * [Azure Redis Cache belgeleri](https://docs.microsoft.com/en-us/azure/redis-cache/)

::: moniker range="= aspnetcore-2.1"

* SignalR uygulamada, yükleme `Microsoft.AspNetCore.SignalR.Redis` NuGet paketi. (Ayrıca bir `Microsoft.AspNetCore.SignalR.StackExchangeRedis` ASP.NET Core 2.2 ve daha sonra biridir ancak bu, paket.)

* İçinde `Startup.ConfigureServices` yöntemi, çağrı `AddRedis` sonra `AddSignalR`:

  ```csharp
  services.AddSignalR().AddRedis("<your_Redis_connection_string>");
  ```

* Seçenekleri gerektiği gibi yapılandırın:
 
  Bağlantı dizesi veya çoğu seçenekler ayarlanabilir [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) nesne. Belirtilen seçenekler `ConfigurationOptions` bağlantı dizesinde olanları geçersiz kılar.

  Aşağıdaki örnekte de seçeneklerini ayarlama işlemi gösterilmektedir `ConfigurationOptions` nesne. Birden çok uygulama aynı Redis örneği paylaşabileceği Bu örnek aşağıdaki adımda açıklandığı gibi bir kanal önek ekler.

  ```csharp
  services.AddSignalR()
    .AddRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  Önceki kodda, `options.Configuration` ne olursa olsun bağlantı dizesinde belirtilmedi ile başlatılır.

::: moniker-end

::: moniker range="> aspnetcore-2.1"

* SignalR uygulamasında aşağıdaki NuGet paketlerini yükleyin:

  * `Microsoft.AspNetCore.SignalR.StackExchangeRedis` -StackExchange.Redis 2.X.X üzerinde bağlıdır. Bu daha sonra ve ASP.NET Core 2.2 için önerilen pakettir.
  * `Microsoft.AspNetCore.SignalR.Redis` -StackExchange.Redis 1.X.X üzerinde bağlıdır. Bu paket, ASP.NET Core 3. 0'sevkiyat değil.

* İçinde `Startup.ConfigureServices` yöntemi, çağrı `AddStackExchangeRedis` sonra `AddSignalR`:

  ```csharp
  services.AddSignalR().AddStackExchangeRedis("<your_Redis_connection_string>");
  ```

* Seçenekleri gerektiği gibi yapılandırın:
 
  Bağlantı dizesi veya çoğu seçenekler ayarlanabilir [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) nesne. Belirtilen seçenekler `ConfigurationOptions` bağlantı dizesinde olanları geçersiz kılar.

  Aşağıdaki örnekte de seçeneklerini ayarlama işlemi gösterilmektedir `ConfigurationOptions` nesne. Birden çok uygulama aynı Redis örneği paylaşabileceği Bu örnek aşağıdaki adımda açıklandığı gibi bir kanal önek ekler.

  ```csharp
  services.AddSignalR()
    .AddStackExchangeRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  Önceki kodda, `options.Configuration` ne olursa olsun bağlantı dizesinde belirtilmedi ile başlatılır.

  Redis seçenekleri hakkında daha fazla bilgi için bkz. [StackExchange Redis belgeleri](https://stackexchange.github.io/StackExchange.Redis/Configuration.html).

::: moniker-end

* Birden fazla SignalR uygulama için bir Redis sunucusu kullanıyorsanız, her bir SignalR uygulama için farklı bir kanal önek kullanın.

  Bir kanal önek ayarı bir SignalR uygulamadan farklı bir kanal önekleri kullanan diğer yalıtır. Farklı önekler atamazsanız, tümü kendi istemcileri bir uygulamadan gönderilen ileti devre kartı olarak Redis sunucusunu kullanan tüm uygulamalar, tüm istemcilere geçer.

* Yazılım Yapışkan oturumlar için sunucu grubunda yük dengelemeyi yapılandırın. Bunu yapmak ilgili belgeler bazı örnekleri aşağıda verilmiştir:

  * [IIS](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing)
  * [HAProxy](https://www.haproxy.com/blog/load-balancing-affinity-persistence-sticky-sessions-what-you-need-to-know/)
  * [Nginx](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/#sticky)
  * [pfSense](https://www.netgate.com/docs/pfsense/loadbalancing/inbound-load-balancing.html#sticky-connections)

## <a name="redis-server-errors"></a>Redis sunucu hataları

Bir Redis sunucusuna çıktığında SignalR iletileri teslim olmaz gösteren özel durum oluşturur. Bazı tipik bir özel durum iletileri:

* *Başarısız yazma iletisi*
* *'MethodName' hub'yöntemini çağırmak başarısız oldu*
* *Redis bağlantısı başarısız oldu*

SignalR sunucunun geri geldiğinde bunları gönderilecek iletileri arabelleğe almayan. Redis sunucusu çalışmadığında gönderilen tüm iletiler kaybolur.

SignalR Redis sunucusuna yeniden kullanılabilir olduğunda otomatik olarak yeniden bağlanır.

### <a name="custom-behavior-for-connection-failures"></a>Bağlantı hataları için özel davranış

Redis bağlantısı hatası olaylarının nasıl ele alınacağını gösteren bir örnek aşağıda verilmiştir.

::: moniker range="= aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

::: moniker range="> aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddMessagePackProtocol()
        .AddStackExchangeRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

## <a name="clustering"></a>Kümeleme

Kümeleme, birden çok Redis sunucuları kullanarak yüksek kullanılabilirlik elde etmek için kullanabileceğiniz bir yöntemdir. Kümeleme resmi olarak desteklenmez ancak işe yarayabilir.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

* <xref:signalr/scale>
* [Redis belgeleri](https://redis.io/documentation)
* [StackExchange Redis belgeleri](https://stackexchange.github.io/StackExchange.Redis/)
* [Azure Redis Cache belgeleri](https://docs.microsoft.com/en-us/azure/redis-cache/)
