---
title: ASP.NET Core ile React proje şablonu kullanın
author: SteveSandersonMS
description: React ve oluşturma-react-uygulama için ASP.NET Core tek sayfa uygulama (SPA) proje şablonu ile çalışmaya başlama hakkında bilgi edinin.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/react
ms.openlocfilehash: c83b119e81d7d0abfd727cb8c72abb09763d9448
ms.sourcegitcommit: b2723654af4969a24545f09ebe32004cb5e84a96
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46011438"
---
# <a name="use-the-react-project-template-with-aspnet-core"></a>ASP.NET Core ile React proje şablonu kullanın

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> Bu belge hakkında React proje şablonu, ASP.NET Core 2.0 sürümünde dahil değildir. Bu, el ile güncelleştirebilirsiniz yeni React hakkında şablonudur. Şablon içinde ASP.NET Core 2.1 varsayılan olarak dahil edilir.

::: moniker-end

Güncelleştirilmiş React proje şablonu uygun bir başlama noktası ASP.NET Core için React kullanan uygulamalar sağlar ve [oluşturma-react-app](https://github.com/facebookincubator/create-react-app) (CRA) kuralları, istemci tarafı zengin kullanıcı arabirimi (UI) uygulamak için.

Şablon, hem bir API arka ucu görev yapacak bir ASP.NET Core projesi ve bir kullanıcı Arabirimi, ancak her ikisi de oluşturduğu ve tek bir birim olarak yayımlanan tek uygulama projesinde barındırma birlikte yapması standart bir CRA React proje oluşturmaya eşdeğerdir.

## <a name="create-a-new-app"></a>Yeni uygulama oluştur

::: moniker range="= aspnetcore-2.0"

ASP.NET Core 2.0 kullanıyorsanız, seçtiğiniz olun [güncelleştirilmiş React proje şablonu yüklü](xref:spa/index#installation).

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

ASP.NET Core 2.1 yüklü varsa, React proje şablonu yüklemek için gerek yoktur.

::: moniker-end

Yeni Proje Oluştur komutunu kullanarak bir komut isteminden `dotnet new react` boş bir dizin içinde. Örneğin, aşağıdaki komutları uygulamada oluşturma bir *-yeni-Uygulamam* dizini ve bu dizine geçin:

```console
dotnet new react -o my-new-app
cd my-new-app
```

Visual Studio veya .NET Core CLI uygulamayı çalıştırın:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Oluşturulan açın *.csproj* dosya ve uygulama normal olarak oradan çalıştırın.

Derleme işlemi birkaç dakika sürebilir ilk çalıştırma npm bağımlılıkları yükler. Ardışık derlemeler çok daha hızlıdır.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Adlı bir ortam değişkeni sahip olduğunuzdan emin olun `ASPNETCORE_Environment` değeriyle `Development`. (PowerShell olmayan istemleri içinde) Windows üzerinde çalıştırma `SET ASPNETCORE_Environment=Development`. Linux veya macOS üzerinde çalıştıran `export ASPNETCORE_Environment=Development`.

Çalıştırma [dotnet derleme](/dotnet/core/tools/dotnet-build) uygulamanızı doğrulamak için yapılar doğru. İlk çalıştırılmasında oluşturma işlemi birkaç dakika sürebilir npm bağımlılıkları, geri yükler. Ardışık derlemeler çok daha hızlıdır.

Çalıştırma [çalıştırma dotnet](/dotnet/core/tools/dotnet-run) uygulamasını başlatmak için.

---

Proje şablonu, ASP.NET Core uygulaması ve bir React uygulaması oluşturur. ASP.NET Core uygulaması, veri erişimi, yetkilendirme ve diğer sunucu tarafı sorunları için kullanılmak üzere tasarlanmıştır. Bulunan React uygulama *ClientApp* alt dizini kullanır, tüm kullanıcı Arabirimi sorunları için kullanılmak üzere tasarlanmıştır.

## <a name="add-pages-images-styles-modules-etc"></a>Sayfaları, görüntüler, stil, modüller, vb. ekleyin.

*ClientApp* dizindir CRA React standart bir uygulaması. Resmi görmek [CRA belgeleri](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) daha fazla bilgi için.

Bu şablonla oluşturulan React uygulama ve CRA tarafından oluşturulan arasında küçük farklar vardır; Ancak, uygulama özelliklerini değiştirilmez. Şablon tarafından oluşturulan uygulama içeren bir [önyükleme](https://getbootstrap.com/)-temel düzen ve basit bir yönlendirme örneği.

## <a name="install-npm-packages"></a>Npm paketlerini yükle

Üçüncü taraf npm paketlerini yüklemek için bir komut isteminde kullanmak *ClientApp* alt. Örneğin:

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a>Yayımlama ve dağıtma

Geliştirmede uygulama geliştiriciye kolaylık sağlamak için en iyi duruma getirilmiş bir modda çalışır. Örneğin, (hata ayıklama sırasında özgün kaynak kodunuzu görebilmeniz için) kaynak eşlemeleri JavaScript paketleri içerir. Uygulama JavaScript, HTML ve CSS diskte dosya değişiklikleri izler ve otomatik olarak yeniden derler ve bu dosyaları değiştirmek gördüğünde yeniden yükler.

Üretim ortamında, uygulamanızın performansını en iyi duruma getirilmiş bir sürümünü işlevi görür. Bu, otomatik olarak gerçekleştirilmesi için yapılandırılır. Yayımladığınızda, istemci tarafı kodunuzu küçültülmüş, transpiled yapısı derleme yapılandırmasını gösterir. Geliştirme derleme, üretim yapı sunucusunda yüklü olması Node.js gerektirmez.

Standart kullanabileceğiniz [ASP.NET Core barındırma ve dağıtma yöntemleri](xref:host-and-deploy/index).

## <a name="run-the-cra-server-independently"></a>CRA sunucunun bağımsız olarak çalıştırın

Proje, ASP.NET Core uygulaması geliştirme modunda başlatıldığında, arka planda CRA geliştirme sunucusunu kendi örneğini başlatmak için yapılandırılır. Bu, ayrı bir sunucuya el ile çalıştırmak zorunda olmadığınız anlamına gelir çünkü uygundur.

Bu varsayılan ayarı bir dezavantajı vardır. C# kodunuzu ve ASP.NET Core uygulamasını yeniden başlatmak için gereken her değiştirdiğinizde CRA sunucuyu yeniden başlatır. Birkaç saniyede yedekleme başlatmak için gereklidir. Sık C# kod düzenleme yapıyorsanız ve yeniden başlatmak için CRA sunucusu beklemek istemiyorsanız, harici olarak CRA sunucunun ASP.NET Core işlemden bağımsız olarak çalıştırın. Bunu yapmak için:

1. Komut isteminde, geçiş *ClientApp* alt ve CRA geliştirme sunucusu başlatma:

    ```console
    cd ClientApp
    npm start
    ```

2. ASP.NET Core uygulamanızı biri kendi başlatma yerine dış CRA server örneğini kullanacak şekilde değiştirin. İçinde *başlangıç* sınıfı, yerine `spa.UseReactDevelopmentServer` aşağıdaki çağrı:

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

ASP.NET Core uygulamanızı başlattığınızda CRA sunucusu başlatma olmaz. El ile başlatılan örneği yerine kullanılır. Bu başlatma ve hızlı yeniden başlatma için sağlar. Artık her seferinde yeniden oluşturmasıyla React uygulamanız için bekliyor.
