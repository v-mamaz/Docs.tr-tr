---
title: ASP.NET Core ile Açısal proje şablonu kullanın
author: SteveSandersonMS
description: Angular ve Açısal CLI için ASP.NET Core tek sayfa uygulama (SPA) proje şablonu ile başlayacağınızı öğrenin.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/angular
ms.openlocfilehash: 811e28af2b67c356ff038d8d673e2164bb56578e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291602"
---
# <a name="use-the-angular-project-template-with-aspnet-core"></a><span data-ttu-id="4d467-103">ASP.NET Core ile Açısal proje şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="4d467-103">Use the Angular project template with ASP.NET Core</span></span>

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="4d467-104">Bu belge hakkında Açısal proje şablonu ASP.NET Core 2. 0 ' dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="4d467-104">This documentation isn't about the Angular project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="4d467-105">Bunu el ile güncelleştirme yapabilmeniz için daha yeni Açısal hakkında şablonudur.</span><span class="sxs-lookup"><span data-stu-id="4d467-105">It's about the newer Angular template to which you can update manually.</span></span> <span data-ttu-id="4d467-106">Şablon ASP.NET Core 2.1 içinde varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="4d467-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

::: moniker-end

<span data-ttu-id="4d467-107">Güncelleştirilmiş Açısal proje şablonu, zengin, istemci tarafı kullanıcı arabirimini (UI) uygulamak için Angular ve Açısal CLI kullanarak uygulamaları ASP.NET Core için uygun bir başlama noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d467-107">The updated Angular project template provides a convenient starting point for ASP.NET Core apps using Angular and the Angular CLI to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="4d467-108">Bir API arka ucu olarak görev yapması için bir ASP.NET Core proje ve bir kullanıcı Arabirimi hareket edecek bir Açısal CLI projesi oluşturmak için şablon eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="4d467-108">The template is equivalent to creating an ASP.NET Core project to act as an API backend and an Angular CLI project to act as a UI.</span></span> <span data-ttu-id="4d467-109">Şablon tek uygulama projesinde her iki proje türleri barındırma rahatlık sunar.</span><span class="sxs-lookup"><span data-stu-id="4d467-109">The template offers the convenience of hosting both project types in a single app project.</span></span> <span data-ttu-id="4d467-110">Sonuç olarak, uygulama projesi oluşturulur ve tek bir birim olarak yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="4d467-110">Consequently, the app project can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="4d467-111">Yeni uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="4d467-111">Create a new app</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="4d467-112">ASP.NET Core 2.0 kullanıyorsanız, seçtiğiniz olun [güncelleştirilmiş tepki proje şablonu yüklü](xref:spa/index#installation).</span><span class="sxs-lookup"><span data-stu-id="4d467-112">If using ASP.NET Core 2.0, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span>

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4d467-113">ASP.NET Core 2.1 yüklü değilse Açısal proje şablonu yüklemeye gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="4d467-113">If you have ASP.NET Core 2.1 installed, there's no need to install the Angular project template.</span></span>

::: moniker-end

<span data-ttu-id="4d467-114">Komutunu kullanarak bir komut isteminden yeni bir proje oluşturun `dotnet new angular` boş bir dizinde.</span><span class="sxs-lookup"><span data-stu-id="4d467-114">Create a new project from a command prompt using the command `dotnet new angular` in an empty directory.</span></span> <span data-ttu-id="4d467-115">Örneğin, aşağıdaki komutları uygulaması oluşturmak bir *-yeni-Uygulamam* dizini ve bu dizine geçin:</span><span class="sxs-lookup"><span data-stu-id="4d467-115">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new angular -o my-new-app
cd my-new-app
```

<span data-ttu-id="4d467-116">Uygulama, Visual Studio veya .NET Core CLI çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4d467-116">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="4d467-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d467-117">Visual Studio</span></span>](#tab/visual-studio/)

<span data-ttu-id="4d467-118">Oluşturulan açmak *.csproj* dosya ve uygulama buradan normal olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d467-118">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="4d467-119">Oluşturma işlemi birkaç dakika sürebilir ilk çalıştırmada npm bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="4d467-119">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="4d467-120">Sonraki derlemeleri çok daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="4d467-120">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="4d467-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="4d467-121">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="4d467-122">Adlı bir ortam değişkeni olduğundan emin olun `ASPNETCORE_Environment` değerini `Development`.</span><span class="sxs-lookup"><span data-stu-id="4d467-122">Ensure you have an environment variable called `ASPNETCORE_Environment` with a value of `Development`.</span></span> <span data-ttu-id="4d467-123">(İçinde olmayan PowerShell komut istemleri) Windows üzerinde çalışan `SET ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="4d467-123">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="4d467-124">Linux veya macOS, çalıştırılan `export ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="4d467-124">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="4d467-125">Çalıştırma [dotnet yapı](/dotnet/core/tools/dotnet-build) uygulama doğrulamak için derlemeler doğru.</span><span class="sxs-lookup"><span data-stu-id="4d467-125">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify the app builds correctly.</span></span> <span data-ttu-id="4d467-126">İlk çalıştırılmasında oluşturma işlemi birkaç dakika sürebilir npm bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="4d467-126">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="4d467-127">Sonraki derlemeleri çok daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="4d467-127">Subsequent builds are much faster.</span></span>

<span data-ttu-id="4d467-128">Çalıştırma [çalıştırmak dotnet](/dotnet/core/tools/dotnet-run) uygulamayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="4d467-128">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span> <span data-ttu-id="4d467-129">Aşağıdakine benzer bir ileti günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="4d467-129">A message similar to the following is logged:</span></span>

```console
Now listening on: http://localhost:<port>
```

<span data-ttu-id="4d467-130">Bu URL'yi bir tarayıcıda gidin.</span><span class="sxs-lookup"><span data-stu-id="4d467-130">Navigate to this URL in a browser.</span></span>

<span data-ttu-id="4d467-131">Arka planda Açısal CLI sunucu örneği oluşturan uygulamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="4d467-131">The app starts up an instance of the Angular CLI server in the background.</span></span> <span data-ttu-id="4d467-132">Aşağıdakine benzer bir ileti günlüğe kaydedilir: *NG Canlı geliştirme sunucusu localhost üzerinde dinleme:&lt;otherport&gt;, tarayıcınızı açmak http://localhost:&lt; otherport&gt; /*  .</span><span class="sxs-lookup"><span data-stu-id="4d467-132">A message similar to the following is logged: *NG Live Development Server is listening on localhost:&lt;otherport&gt;, open your browser on http://localhost:&lt;otherport&gt;/*.</span></span> <span data-ttu-id="4d467-133">Bu iletiyi göz ardı edin&mdash;sahip **değil** birleşik ASP.NET Core ve Açısal CLI uygulama için URL.</span><span class="sxs-lookup"><span data-stu-id="4d467-133">Ignore this message&mdash;it's **not** the URL for the combined ASP.NET Core and Angular CLI app.</span></span>

---

<span data-ttu-id="4d467-134">Proje şablonu, bir ASP.NET Core uygulama ve Açısal bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4d467-134">The project template creates an ASP.NET Core app and an Angular app.</span></span> <span data-ttu-id="4d467-135">ASP.NET Core uygulama veri erişimi, yetkilendirme ve diğer sunucu tarafı sorunları için kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4d467-135">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="4d467-136">Bulunan Açısal uygulama *ClientApp* alt, tüm kullanıcı Arabirimi sorunları için kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4d467-136">The Angular app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="4d467-137">Sayfaları, görüntüler, stil, modüller, vb. ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d467-137">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="4d467-138">*ClientApp* dizini standart Açısal CLI uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="4d467-138">The *ClientApp* directory contains a standard Angular CLI app.</span></span> <span data-ttu-id="4d467-139">Resmi görmek [Açısal belgelerine](https://github.com/angular/angular-cli/wiki) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4d467-139">See the official [Angular documentation](https://github.com/angular/angular-cli/wiki) for more information.</span></span>

<span data-ttu-id="4d467-140">Bu şablonla oluşturulan Açısal uygulama ve Açısal CLI tarafından kendi oluşturduğunuz bir arasında küçük farklar vardır (aracılığıyla `ng new`); ancak, uygulama özelliklerini farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="4d467-140">There are slight differences between the Angular app created by this template and the one created by Angular CLI itself (via `ng new`); however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="4d467-141">Şablon tarafından oluşturulan uygulama içeren bir [önyükleme](https://getbootstrap.com/)-tabanlı düzeni ve temel bir yönlendirme örneği.</span><span class="sxs-lookup"><span data-stu-id="4d467-141">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="run-ng-commands"></a><span data-ttu-id="4d467-142">NG komutlarını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4d467-142">Run ng commands</span></span>

<span data-ttu-id="4d467-143">Bir komut isteminde, geçiş *ClientApp* alt:</span><span class="sxs-lookup"><span data-stu-id="4d467-143">In a command prompt, switch to the *ClientApp* subdirectory:</span></span>

```console
cd ClientApp
```

<span data-ttu-id="4d467-144">Varsa `ng` genel yüklü aracı, çalıştırabilirsiniz kendi komutlardan herhangi birini.</span><span class="sxs-lookup"><span data-stu-id="4d467-144">If you have the `ng` tool installed globally, you can run any of its commands.</span></span> <span data-ttu-id="4d467-145">Örneğin, çalıştırabilirsiniz `ng lint`, `ng test`, ya da herhangi bir diğer [Açısal CLI komutları](https://github.com/angular/angular-cli/wiki#additional-commands).</span><span class="sxs-lookup"><span data-stu-id="4d467-145">For example, you can run `ng lint`, `ng test`, or any of the other [Angular CLI commands](https://github.com/angular/angular-cli/wiki#additional-commands).</span></span> <span data-ttu-id="4d467-146">Çalıştırmak için gerekli `ng serve` yine de uygulamanız sunucu tarafı ve istemci tarafı bölümlerini hizmet veren ile ASP.NET Core uygulamanızı oluşturulmasıyla ilgili olduğu için.</span><span class="sxs-lookup"><span data-stu-id="4d467-146">There's no need to run `ng serve` though, because your ASP.NET Core app deals with serving both server-side and client-side parts of your app.</span></span> <span data-ttu-id="4d467-147">Dahili olarak kullanan `ng serve` geliştirme.</span><span class="sxs-lookup"><span data-stu-id="4d467-147">Internally, it uses `ng serve` in development.</span></span>

<span data-ttu-id="4d467-148">Sahip değilseniz `ng` yüklü, aracı çalıştırmak `npm run ng` yerine.</span><span class="sxs-lookup"><span data-stu-id="4d467-148">If you don't have the `ng` tool installed, run `npm run ng` instead.</span></span> <span data-ttu-id="4d467-149">Örneğin, çalıştırabilirsiniz `npm run ng lint` veya `npm run ng test`.</span><span class="sxs-lookup"><span data-stu-id="4d467-149">For example, you can run `npm run ng lint` or `npm run ng test`.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="4d467-150">Npm paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="4d467-150">Install npm packages</span></span>

<span data-ttu-id="4d467-151">Üçüncü taraf npm paketleri yüklemek için bir komut isteminde kullanın *ClientApp* alt dizin.</span><span class="sxs-lookup"><span data-stu-id="4d467-151">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="4d467-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4d467-152">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="4d467-153">Yayımlama ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="4d467-153">Publish and deploy</span></span>

<span data-ttu-id="4d467-154">Geliştirme, uygulama geliştiriciye kolaylık sağlamak için en iyi hale getirilmiş bir modda çalışır.</span><span class="sxs-lookup"><span data-stu-id="4d467-154">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="4d467-155">Örneğin, (hata ayıklama sırasında özgün TypeScript kodunuzu görebilmeniz için) kaynak eşlemeleri JavaScript paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4d467-155">For example, JavaScript bundles include source maps (so that when debugging, you can see your original TypeScript code).</span></span> <span data-ttu-id="4d467-156">Uygulama diskte TypeScript, HTML ve CSS dosya değişiklikleri izleyen ve otomatik olarak yeniden derler ve bu dosyaları değiştirmek gördüğünde yeniden yükler.</span><span class="sxs-lookup"><span data-stu-id="4d467-156">The app watches for TypeScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="4d467-157">Üretimde, uygulamanızın performansını en iyi duruma getirilmiş sürüm hizmet.</span><span class="sxs-lookup"><span data-stu-id="4d467-157">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="4d467-158">Bu, otomatik olarak gerçekleşecek şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4d467-158">This is configured to happen automatically.</span></span> <span data-ttu-id="4d467-159">Yayımladığınızda, derleme yapılandırmasını bir küçültülmüş yayar, tamamlanan-in-time (Uygulama Nesne Ağacı), istemci-tarafı kodunuzun yapı derlenmiş.</span><span class="sxs-lookup"><span data-stu-id="4d467-159">When you publish, the build configuration emits a minified, ahead-of-time (AoT) compiled build of your client-side code.</span></span> <span data-ttu-id="4d467-160">Geliştirme yapı farklı olarak, üretim yapı sunucuya yüklenmesi Node.js gerektirmez (etkinleştirilmiş olduğu sürece [sunucu tarafı prerendering](#server-side-rendering)).</span><span class="sxs-lookup"><span data-stu-id="4d467-160">Unlike the development build, the production build doesn't require Node.js to be installed on the server (unless you have enabled [server-side prerendering](#server-side-rendering)).</span></span>

<span data-ttu-id="4d467-161">Standart kullanabilirsiniz [ASP.NET Core barındırma ve dağıtma yöntemleri](xref:host-and-deploy/index).</span><span class="sxs-lookup"><span data-stu-id="4d467-161">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-ng-serve-independently"></a><span data-ttu-id="4d467-162">"Ng hizmet vermemesini" bağımsız olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4d467-162">Run "ng serve" independently</span></span>

<span data-ttu-id="4d467-163">Proje ASP.NET Core uygulama geliştirme modunda başlatıldığında Açısal CLI sunucu örneğini arka planda başlatmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4d467-163">The project is configured to start its own instance of the Angular CLI server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="4d467-164">Ayrı bir sunucuya el ile çalıştırmak olmadığından, bu uygundur.</span><span class="sxs-lookup"><span data-stu-id="4d467-164">This is convenient because you don't have to run a separate server manually.</span></span>

<span data-ttu-id="4d467-165">Bu varsayılan kurulum bir dezavantajı yoktur.</span><span class="sxs-lookup"><span data-stu-id="4d467-165">There's a drawback to this default setup.</span></span> <span data-ttu-id="4d467-166">C# kodunuzu ve ASP.NET uygulama yeniden başlatılmalıdır çekirdek her değiştirdiğinizde Açısal CLI sunucuyu yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="4d467-166">Each time you modify your C# code and your ASP.NET Core app needs to restart, the Angular CLI server restarts.</span></span> <span data-ttu-id="4d467-167">Yaklaşık 10 saniye yeniden başlatılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="4d467-167">Around 10 seconds is required to start back up.</span></span> <span data-ttu-id="4d467-168">Sık C# kod düzenlemeleri yapıyorsanız ve yeniden başlatmak Açısal CLI için beklemek istemiyorsanız, harici olarak Açısal CLI sunucunun bağımsız olarak ASP.NET Core işlemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d467-168">If you're making frequent C# code edits and don't want to wait for Angular CLI to restart, run the Angular CLI server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="4d467-169">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="4d467-169">To do so:</span></span>

1. <span data-ttu-id="4d467-170">Bir komut isteminde, geçiş *ClientApp* alt ve başlatma Açısal CLI geliştirme sunucusu:</span><span class="sxs-lookup"><span data-stu-id="4d467-170">In a command prompt, switch to the *ClientApp* subdirectory, and launch the Angular CLI development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4d467-171">Kullanım `npm start` Açısal CLI geliştirme sunucusu değil başlatmak için `ng serve`, böylece yapılandırmada *package.json* dikkate.</span><span class="sxs-lookup"><span data-stu-id="4d467-171">Use `npm start` to launch the Angular CLI development server, not `ng serve`, so that the configuration in *package.json* is respected.</span></span> <span data-ttu-id="4d467-172">Ek parametreleri Açısal CLI sunucuya geçirmek için bunları ilgili Ekle `scripts` satırından, *package.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="4d467-172">To pass additional parameters to the Angular CLI server, add them to the relevant `scripts` line in your *package.json* file.</span></span>

2. <span data-ttu-id="4d467-173">ASP.NET Core uygulamanızı birini kendi başlatmayı yerine dış Açısal CLI örnek kullanacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4d467-173">Modify your ASP.NET Core app to use the external Angular CLI instance instead of launching one of its own.</span></span> <span data-ttu-id="4d467-174">İçinde *başlangıç* sınıfı, yerine `spa.UseAngularCliServer` aşağıdaki çağırmayla:</span><span class="sxs-lookup"><span data-stu-id="4d467-174">In your *Startup* class, replace the `spa.UseAngularCliServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:4200");
    ```

<span data-ttu-id="4d467-175">ASP.NET Core uygulamanızı başlattığınızda Açısal CLI sunucu başlatma olmaz.</span><span class="sxs-lookup"><span data-stu-id="4d467-175">When you start your ASP.NET Core app, it won't launch an Angular CLI server.</span></span> <span data-ttu-id="4d467-176">El ile başlatılan örnek yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d467-176">The instance you started manually is used instead.</span></span> <span data-ttu-id="4d467-177">Bu, başlatma ve hızlı yeniden sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d467-177">This enables it to start and restart faster.</span></span> <span data-ttu-id="4d467-178">Artık her zaman istemci uygulamanızı yeniden Açısal CLI için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="4d467-178">It's no longer waiting for Angular CLI to rebuild your client app each time.</span></span>

## <a name="server-side-rendering"></a><span data-ttu-id="4d467-179">Sunucu tarafı işleme</span><span class="sxs-lookup"><span data-stu-id="4d467-179">Server-side rendering</span></span>

<span data-ttu-id="4d467-180">Bir performans özelliği sunucu yanı sıra istemci üzerinde çalışan Açısal uygulamanıza oluşturma öncesi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d467-180">As a performance feature, you can choose to pre-render your Angular app on the server as well as running it on the client.</span></span> <span data-ttu-id="4d467-181">Bu tarayıcılar bunlar bile indiriliyor ve JavaScript paketleri yürütmeden önce görüntülemek için uygulamanızın ilk UI temsil eden HTML biçimlendirmesi aldığınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4d467-181">This means that browsers receive HTML markup representing your app's initial UI, so they display it even before downloading and executing your JavaScript bundles.</span></span> <span data-ttu-id="4d467-182">Bu uygulama çoğunu gelen adlı bir Açısal özelliğinden [Açısal Evrensel](https://universal.angular.io/).</span><span class="sxs-lookup"><span data-stu-id="4d467-182">Most of the implementation of this comes from an Angular feature called [Angular Universal](https://universal.angular.io/).</span></span>

> [!TIP]
> <span data-ttu-id="4d467-183">Sunucu tarafı işleme etkinleştirme (SSR) geliştirme ve dağıtım sırasında fazladan zorluk hem birtakım sunar.</span><span class="sxs-lookup"><span data-stu-id="4d467-183">Enabling server-side rendering (SSR) introduces a number of extra complications both during development and deployment.</span></span> <span data-ttu-id="4d467-184">Okuma [SSR eksileri](#drawbacks-of-ssr) SSR gereksinimleriniz için iyi bir tercihtir olup olmadığını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="4d467-184">Read [drawbacks of SSR](#drawbacks-of-ssr) to determine if SSR is a good fit for your requirements.</span></span>

<span data-ttu-id="4d467-185">SSR etkinleştirmek için projenize eklemeleri sayısı yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d467-185">To enable SSR, you need to make a number of additions to your project.</span></span>

<span data-ttu-id="4d467-186">İçinde *başlangıç* sınıfı, *sonra* yapılandırır satır `spa.Options.SourcePath`, ve *önce* çağrısı `UseAngularCliServer` veya `UseProxyToSpaDevelopmentServer`, aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4d467-186">In the *Startup* class, *after* the line that configures `spa.Options.SourcePath`, and *before* the call to `UseAngularCliServer` or `UseProxyToSpaDevelopmentServer`, add the following:</span></span>

[!code-csharp[](sample/AngularServerSideRendering/Startup.cs?name=snippet_Call_UseSpa&highlight=5-12)]

<span data-ttu-id="4d467-187">Komut dosyası çalıştırarak SSR paket oluşturmak bu kodu geliştirme modunda çalışır `build:ssr`, içinde tanımlanan *ClientApp\package.json*.</span><span class="sxs-lookup"><span data-stu-id="4d467-187">In development mode, this code attempts to build the SSR bundle by running the script `build:ssr`, which is defined in *ClientApp\package.json*.</span></span> <span data-ttu-id="4d467-188">Bu adlı bir Açısal uygulama derlemeler `ssr`, henüz tanımlı değil.</span><span class="sxs-lookup"><span data-stu-id="4d467-188">This builds an Angular app named `ssr`, which isn't yet defined.</span></span>

<span data-ttu-id="4d467-189">Sonunda `apps` içinde dizi *ClientApp/.angular-cli.json*, ek bir uygulama adıyla tanımlamak `ssr`.</span><span class="sxs-lookup"><span data-stu-id="4d467-189">At the end of the `apps` array in *ClientApp/.angular-cli.json*, define an extra app with name `ssr`.</span></span> <span data-ttu-id="4d467-190">Aşağıdaki seçenekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="4d467-190">Use the following options:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/.angular-cli.json?range=24-41)]

<span data-ttu-id="4d467-191">Bu yeni SSR özellikli uygulama yapılandırma iki ek dosyalar gerektirir: *tsconfig.server.json* ve *main.server.ts*.</span><span class="sxs-lookup"><span data-stu-id="4d467-191">This new SSR-enabled app configuration requires two further files: *tsconfig.server.json* and *main.server.ts*.</span></span> <span data-ttu-id="4d467-192">*Tsconfig.server.json* dosya TypeScript derleme seçeneklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4d467-192">The *tsconfig.server.json* file specifies TypeScript compilation options.</span></span> <span data-ttu-id="4d467-193">*Main.server.ts* dosya sırasında SSR kod giriş noktası olarak hizmet verir.</span><span class="sxs-lookup"><span data-stu-id="4d467-193">The *main.server.ts* file serves as the code entry point during SSR.</span></span>

<span data-ttu-id="4d467-194">Adlı yeni bir dosya ekleme *tsconfig.server.json* içinde *ClientApp/src* (varolan yanında *tsconfig.app.json*), aşağıdakileri içeren:</span><span class="sxs-lookup"><span data-stu-id="4d467-194">Add a new file called *tsconfig.server.json* inside *ClientApp/src* (alongside the existing *tsconfig.app.json*), containing the following:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/src/tsconfig.server.json)]

<span data-ttu-id="4d467-195">Bu dosya adlı bir modül için aranacak Angular'ın Uygulama Nesne Ağacı derleyici yapılandırır `app.server.module`.</span><span class="sxs-lookup"><span data-stu-id="4d467-195">This file configures Angular's AoT compiler to look for a module called `app.server.module`.</span></span> <span data-ttu-id="4d467-196">Bu, yeni bir dosya oluşturarak eklersiniz *ClientApp/src/app/app.server.module.ts* (varolan yanında *app.module.ts*) aşağıdakileri içeren:</span><span class="sxs-lookup"><span data-stu-id="4d467-196">Add this by creating a new file at *ClientApp/src/app/app.server.module.ts* (alongside the existing *app.module.ts*) containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/app/app.server.module.ts)]

<span data-ttu-id="4d467-197">Bu modül istemci-tarafı devralan `app.module` ve ek Açısal modüllerine SSR sırasında kullanılabilir tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4d467-197">This module inherits from your client-side `app.module` and defines which extra Angular modules are available during SSR.</span></span>

<span data-ttu-id="4d467-198">Sözcüğünün yeni `ssr` girişi *.angular cli.json* adlı bir giriş noktası dosyası başvurulan *main.server.ts*.</span><span class="sxs-lookup"><span data-stu-id="4d467-198">Recall that the new `ssr` entry in *.angular-cli.json* referenced an entry point file called *main.server.ts*.</span></span> <span data-ttu-id="4d467-199">Bu dosyayı henüz eklemediniz ve bunu yapmak için zaman sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="4d467-199">You haven't yet added that file, and now is time to do so.</span></span> <span data-ttu-id="4d467-200">En yeni bir dosya oluşturun *ClientApp/src/main.server.ts* (varolan yanında *main.ts*), aşağıdakileri içeren:</span><span class="sxs-lookup"><span data-stu-id="4d467-200">Create a new file at *ClientApp/src/main.server.ts* (alongside the existing *main.ts*), containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/main.server.ts)]

<span data-ttu-id="4d467-201">Bu dosyanın kodu çalıştırıldığında ne ASP.NET Core her istek için yürütür `UseSpaPrerendering` eklediğiniz ara yazılımı *başlangıç* sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4d467-201">This file's code is what ASP.NET Core executes for each request when it runs the `UseSpaPrerendering` middleware that you added to the *Startup* class.</span></span> <span data-ttu-id="4d467-202">Alma ile ilgilenen `params` (örneğin, istenen URL) .NET kodu ve sonuçta elde edilen HTML almak için Açısal SSR API çağrıları yapma.</span><span class="sxs-lookup"><span data-stu-id="4d467-202">It deals with receiving `params` from the .NET code (such as the URL being requested), and making calls to Angular SSR APIs to get the resulting HTML.</span></span>

<span data-ttu-id="4d467-203">Kesinlikle konuşulur, bu SSR geliştirme modunda etkinleştirmek yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="4d467-203">Strictly-speaking, this is sufficient to enable SSR in development mode.</span></span> <span data-ttu-id="4d467-204">Böylece yayımlandığında, uygulamanızın düzgün çalıştığını bir son değişiklik yapmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4d467-204">It's essential to make one final change so that your app works correctly when published.</span></span> <span data-ttu-id="4d467-205">Uygulamanızın ana içinde *.csproj* dosya, ayarlamak `BuildServerSideRenderer` özellik değerine `true`:</span><span class="sxs-lookup"><span data-stu-id="4d467-205">In your app's main *.csproj* file, set the `BuildServerSideRenderer` property value to `true`:</span></span>

[!code-xml[](sample/AngularServerSideRendering/AngularServerSideRendering.csproj?name=snippet_EnableBuildServerSideRenderer)]

<span data-ttu-id="4d467-206">Bu derleme işleminin çalışmasına yapılandırır `build:ssr` yayımlama sırasında ve SSR dosyaları sunucuya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4d467-206">This configures the build process to run `build:ssr` during publishing and deploy the SSR files to the server.</span></span> <span data-ttu-id="4d467-207">Bu etkinleştirmezseniz SSR üretimde başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d467-207">If you don't enable this, SSR fails in production.</span></span>

<span data-ttu-id="4d467-208">Açısal kod HTML olarak sunucuda uygulamanızı geliştirme veya üretim modunda çalışırken, önceden işler.</span><span class="sxs-lookup"><span data-stu-id="4d467-208">When your app runs in either development or production mode, the Angular code pre-renders as HTML on the server.</span></span> <span data-ttu-id="4d467-209">İstemci tarafı kodu normal olarak yürütür.</span><span class="sxs-lookup"><span data-stu-id="4d467-209">The client-side code executes as normal.</span></span>

### <a name="pass-data-from-net-code-into-typescript-code"></a><span data-ttu-id="4d467-210">Veri .NET kodundan TypeScript koda geçirme</span><span class="sxs-lookup"><span data-stu-id="4d467-210">Pass data from .NET code into TypeScript code</span></span>

<span data-ttu-id="4d467-211">SSR sırasında istek başına veri ASP.NET Core uygulamanızdan Açısal uygulamanıza iletmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d467-211">During SSR, you might want to pass per-request data from your ASP.NET Core app into your Angular app.</span></span> <span data-ttu-id="4d467-212">Örneğin, tanımlama bilgileri geçirebilirdiniz veya bir şey bir veritabanından okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="4d467-212">For example, you could pass cookie information or something read from a database.</span></span> <span data-ttu-id="4d467-213">Bunu yapmak için düzenleme, *başlangıç* sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4d467-213">To do this, edit your *Startup* class.</span></span> <span data-ttu-id="4d467-214">İçin geri çağırma içinde `UseSpaPrerendering`, için bir değer ayarlamanız `options.SupplyData` aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4d467-214">In the callback for `UseSpaPrerendering`, set a value for `options.SupplyData` such as the following:</span></span>

```csharp
options.SupplyData = (context, data) =>
{
    // Creates a new value called isHttpsRequest that's passed to TypeScript code
    data["isHttpsRequest"] = context.Request.IsHttps;
};
```

<span data-ttu-id="4d467-215">`SupplyData` Rasgele geçirdiğiniz geri çağırma sağlar, istek başına, JSON seri hale getirilebilir veri (için örnek, dizeleri, Boole değerlerini veya numaralarını).</span><span class="sxs-lookup"><span data-stu-id="4d467-215">The `SupplyData` callback lets you pass arbitrary, per-request, JSON-serializable data (for example, strings, booleans, or numbers).</span></span> <span data-ttu-id="4d467-216">*Main.server.ts* kod aldığında bu olarak `params.data`.</span><span class="sxs-lookup"><span data-stu-id="4d467-216">Your *main.server.ts* code receives this as `params.data`.</span></span> <span data-ttu-id="4d467-217">Örneğin, yukarıdaki kod örneğinde bir Boole değeri olarak geçirir `params.data.isHttpsRequest` içine `createServerRenderer` geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="4d467-217">For example, the preceding code sample passes a boolean value as `params.data.isHttpsRequest` into the `createServerRenderer` callback.</span></span> <span data-ttu-id="4d467-218">Bu, uygulamanızın Angular tarafından desteklenen herhangi bir yolla diğer bölümleri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d467-218">You can pass this to other parts of your app in any way supported by Angular.</span></span> <span data-ttu-id="4d467-219">Örneğin, nasıl *main.server.ts* geçirir `BASE_URL` Oluşturucusu alması bildirilmiş herhangi bir bileşen için değer.</span><span class="sxs-lookup"><span data-stu-id="4d467-219">For example, see how *main.server.ts* passes the `BASE_URL` value to any component whose constructor is declared to receive it.</span></span>

### <a name="drawbacks-of-ssr"></a><span data-ttu-id="4d467-220">SSR eksileri</span><span class="sxs-lookup"><span data-stu-id="4d467-220">Drawbacks of SSR</span></span>

<span data-ttu-id="4d467-221">Tüm uygulamaları SSR yararlanır.</span><span class="sxs-lookup"><span data-stu-id="4d467-221">Not all apps benefit from SSR.</span></span> <span data-ttu-id="4d467-222">Birincil avantajı algılanan performansı.</span><span class="sxs-lookup"><span data-stu-id="4d467-222">The primary benefit is perceived performance.</span></span> <span data-ttu-id="4d467-223">Fetch veya JavaScript paketleri ayrıştırılamıyor biraz uzun sürebilir olsa bile bir yavaş ağ bağlantısı üzerinden veya yavaş mobil cihazlarda uygulamanızı ulaşmasını ziyaretçileri ilk UI hızlı bakın.</span><span class="sxs-lookup"><span data-stu-id="4d467-223">Visitors reaching your app over a slow network connection or on slow mobile devices see the initial UI quickly, even if it takes a while to fetch or parse the JavaScript bundles.</span></span> <span data-ttu-id="4d467-224">Bununla birlikte, birçok SPAs çoğunlukla hızlı bilgisayarlarda hızlı, iç şirket ağları üzerinden uygulama neredeyse anında göründüğü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d467-224">However, many SPAs are mainly used over fast, internal company networks on fast computers where the app appears almost instantly.</span></span>

<span data-ttu-id="4d467-225">Aynı anda SSR etkinleştirme için önemli dezavantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="4d467-225">At the same time, there are significant drawbacks to enabling SSR.</span></span> <span data-ttu-id="4d467-226">Geliştirme sürecinizi karmaşıklık ekler.</span><span class="sxs-lookup"><span data-stu-id="4d467-226">It adds complexity to your development process.</span></span> <span data-ttu-id="4d467-227">Kodunuzu iki farklı ortamlarda çalıştırmanız gerekir: istemci ve sunucu tarafı (ASP.NET çekirdek çağrılan bir ortamda Node.js).</span><span class="sxs-lookup"><span data-stu-id="4d467-227">Your code must run in two different environments: client-side and server-side (in a Node.js environment invoked from ASP.NET Core).</span></span> <span data-ttu-id="4d467-228">De hesaba katılmalıdır gereken bazı şeyler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4d467-228">Here are some things to bear in mind:</span></span>

* <span data-ttu-id="4d467-229">SSR üretim sunucularınızda Node.js yükleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4d467-229">SSR requires a Node.js installation on your production servers.</span></span> <span data-ttu-id="4d467-230">Bu otomatik olarak Azure App Services gibi bazı dağıtım senaryoları için kullanılabilir ancak Azure Service Fabric gibi diğer durumdur.</span><span class="sxs-lookup"><span data-stu-id="4d467-230">This is automatically the case for some deployment scenarios, such as Azure App Services, but not for others, such as Azure Service Fabric.</span></span>
* <span data-ttu-id="4d467-231">Etkinleştirme `BuildServerSideRenderer` bayrağı nedenler yapı, *node_modules* yayımlamak için dizin.</span><span class="sxs-lookup"><span data-stu-id="4d467-231">Enabling the `BuildServerSideRenderer` build flag causes your *node_modules* directory to publish.</span></span> <span data-ttu-id="4d467-232">Bu klasör, hangi dağıtım süresini artırır 20.000 + dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="4d467-232">This folder contains 20,000+ files, which increases deployment time.</span></span>
* <span data-ttu-id="4d467-233">Bir Node.js ortamda kodunuzu çalıştırmak için tarayıcı özel JavaScript API varlığını gibi bağlı olamaz `window` veya `localStorage`.</span><span class="sxs-lookup"><span data-stu-id="4d467-233">To run your code in a Node.js environment, it can't rely on the existence of browser-specific JavaScript APIs such as `window` or `localStorage`.</span></span> <span data-ttu-id="4d467-234">Kodunuzu (veya başvuru bazı üçüncü taraf kitaplık) bu API'leri kullanmaya çalışırsa SSR sırasında bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="4d467-234">If your code (or some third-party library you reference) tries to use these APIs, you'll get an error during SSR.</span></span> <span data-ttu-id="4d467-235">Örneğin, birçok yerde tarayıcıya özgü API başvurduğundan jQuery kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4d467-235">For example, don't use jQuery because it references browser-specific APIs in many places.</span></span> <span data-ttu-id="4d467-236">Hataları önlemek için SSR önlemek veya tarayıcıya özgü API ya da kitaplıkları kaçının gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d467-236">To prevent errors, you must either avoid SSR or avoid browser-specific APIs or libraries.</span></span> <span data-ttu-id="4d467-237">Bu tür API'leri yapılan her çağrı sırasında SSR çağrılan olmayan emin olmak için denetimleri kaydırın.</span><span class="sxs-lookup"><span data-stu-id="4d467-237">You can wrap any calls to such APIs in checks to ensure they aren't invoked during SSR.</span></span> <span data-ttu-id="4d467-238">Örneğin, aşağıdaki gibi bir denetimi JavaScript veya TypeScript kodda kullanın:</span><span class="sxs-lookup"><span data-stu-id="4d467-238">For example, use a check such as the following in JavaScript or TypeScript code:</span></span>

    ```javascript
    if (typeof window !== 'undefined') {
        // Call browser-specific APIs here
    }
    ```