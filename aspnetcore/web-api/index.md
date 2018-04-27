---
title: Web API ile ASP.NET çekirdek oluşturma
author: scottaddie
description: Bir web API ASP.NET Core ve her özelliği kullanmak, uygun olduğunda oluşturmak için kullanılabilen özellikler hakkında bilgi edinin.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: web-api/index
ms.openlocfilehash: 017bcc1ed65b1baa92408db07201d1c7bab2849d
ms.sourcegitcommit: 01db73f2f7ac22b11ea48a947131d6176b0fe9ad
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="72bed-103">Web API ile ASP.NET çekirdek oluşturma</span><span class="sxs-lookup"><span data-stu-id="72bed-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="72bed-104">Tarafından [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="72bed-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="72bed-105">[Görüntülemek veya karşıdan örnek kod](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([nasıl indirileceğini](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="72bed-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="72bed-106">Bu belge, bir web API ASP.NET Core ve her özelliği kullanmak en uygun olduğunda oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72bed-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="72bed-107">ControllerBase sınıf türetin</span><span class="sxs-lookup"><span data-stu-id="72bed-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="72bed-108">Devralınan [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) web API'si hizmet vermek için amaçlanan bir denetleyicide sınıfı.</span><span class="sxs-lookup"><span data-stu-id="72bed-108">Inherit from the [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="72bed-109">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="72bed-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="72bed-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="72bed-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="72bed-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="72bed-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end

<span data-ttu-id="72bed-112">`ControllerBase` Sınıfı çok sayıda özellikleri ve yöntemleri erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="72bed-112">The `ControllerBase` class provides access to numerous properties and methods.</span></span> <span data-ttu-id="72bed-113">Önceki örnekte, bu tür bir yöntemleri dahil [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) ve [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span><span class="sxs-lookup"><span data-stu-id="72bed-113">In the preceding example, some such methods include [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) and [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span></span> <span data-ttu-id="72bed-114">Bu yöntemler HTTP 400 ve 201 durum kodları, sırasıyla döndürmek için eylem yöntemlerinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="72bed-114">These methods are invoked within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="72bed-115">[ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) de tarafından sağlanan özellik, `ControllerBase`, istek model doğrulama gerçekleştirmek için erişilir.</span><span class="sxs-lookup"><span data-stu-id="72bed-115">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property, also provided by `ControllerBase`, is accessed to perform request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="72bed-116">ApiControllerAttribute sınıfıyla açıklama ekleme</span><span class="sxs-lookup"><span data-stu-id="72bed-116">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="72bed-117">ASP.NET Core 2.1 tanıtır `[ApiController]` bir web API denetleyicisi sınıfı belirtmek için öznitelik.</span><span class="sxs-lookup"><span data-stu-id="72bed-117">ASP.NET Core 2.1 introduces the `[ApiController]` attribute to denote a web API controller class.</span></span> <span data-ttu-id="72bed-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="72bed-118">For example:</span></span>

<span data-ttu-id="72bed-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="72bed-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span></span>

<span data-ttu-id="72bed-120">Bu öznitelik genellikle ile birlikte `ControllerBase` yararlı yöntemlere ve özelliklere erişmek için.</span><span class="sxs-lookup"><span data-stu-id="72bed-120">This attribute is commonly coupled with `ControllerBase` to gain access to useful methods and properties.</span></span> <span data-ttu-id="72bed-121">`ControllerBase` yöntemleri erişim gibi sağlar [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) ve [dosya](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span><span class="sxs-lookup"><span data-stu-id="72bed-121">`ControllerBase` provides access to methods such as [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) and [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span></span>

<span data-ttu-id="72bed-122">İle açıklanan özel temel denetleyici sınıfını oluşturmak için başka bir yaklaşımdır `[ApiController]` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="72bed-122">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

<span data-ttu-id="72bed-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span><span class="sxs-lookup"><span data-stu-id="72bed-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span></span>

<span data-ttu-id="72bed-124">Aşağıdaki bölümlerde özniteliği tarafından eklenen kullanışlı özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72bed-124">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="72bed-125">Otomatik HTTP 400 yanıtlar</span><span class="sxs-lookup"><span data-stu-id="72bed-125">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="72bed-126">Doğrulama hatalarını otomatik olarak bir HTTP 400 yanıt tetikler.</span><span class="sxs-lookup"><span data-stu-id="72bed-126">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="72bed-127">Aşağıdaki kod, Eylemler gereksiz olur:</span><span class="sxs-lookup"><span data-stu-id="72bed-127">The following code becomes unnecessary in your actions:</span></span>

<span data-ttu-id="72bed-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span><span class="sxs-lookup"><span data-stu-id="72bed-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span></span>

<span data-ttu-id="72bed-129">Aşağıdaki kod ile bu varsayılan davranışı devre dışı bırakılır *Startup.ConfigureServices*:</span><span class="sxs-lookup"><span data-stu-id="72bed-129">This default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="72bed-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span><span class="sxs-lookup"><span data-stu-id="72bed-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span></span>

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="72bed-131">Kaynak parametresi çıkarım bağlama</span><span class="sxs-lookup"><span data-stu-id="72bed-131">Binding source parameter inference</span></span>

<span data-ttu-id="72bed-132">Bağlama kaynak özniteliği, bir eylem parametresinin değeri bulunan konumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="72bed-132">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="72bed-133">Aşağıdaki bağlama kaynak öznitelikleri mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="72bed-133">The following binding source attributes exist:</span></span>

|<span data-ttu-id="72bed-134">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="72bed-134">Attribute</span></span>|<span data-ttu-id="72bed-135">Bağlama kaynağı</span><span class="sxs-lookup"><span data-stu-id="72bed-135">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="72bed-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span><span class="sxs-lookup"><span data-stu-id="72bed-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span></span>     | <span data-ttu-id="72bed-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="72bed-137">Request body</span></span> |
|<span data-ttu-id="72bed-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span><span class="sxs-lookup"><span data-stu-id="72bed-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span></span>     | <span data-ttu-id="72bed-139">İstek gövdesini form verilerini</span><span class="sxs-lookup"><span data-stu-id="72bed-139">Form data in the request body</span></span> |
|<span data-ttu-id="72bed-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span><span class="sxs-lookup"><span data-stu-id="72bed-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span></span> | <span data-ttu-id="72bed-141">İstek üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="72bed-141">Request header</span></span> |
|<span data-ttu-id="72bed-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span><span class="sxs-lookup"><span data-stu-id="72bed-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span></span>   | <span data-ttu-id="72bed-143">Sorgu dizesi parametresi isteği</span><span class="sxs-lookup"><span data-stu-id="72bed-143">Request query string parameter</span></span> |
|<span data-ttu-id="72bed-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span><span class="sxs-lookup"><span data-stu-id="72bed-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span></span>   | <span data-ttu-id="72bed-145">Geçerli isteğin rota verileri</span><span class="sxs-lookup"><span data-stu-id="72bed-145">Route data from the current request</span></span> |
|<span data-ttu-id="72bed-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="72bed-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="72bed-147">Bir eylem parametresi olarak eklenen isteği hizmeti</span><span class="sxs-lookup"><span data-stu-id="72bed-147">The request service injected as an action parameter</span></span> |

<span data-ttu-id="72bed-148">Olmadan `[ApiController]` öznitelikleri açıkça tanımlanmış kaynak bağlama özniteliği.</span><span class="sxs-lookup"><span data-stu-id="72bed-148">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="72bed-149">Aşağıdaki örnekte, `[FromQuery]` öznitelik gösterir `discontinuedOnly` istek URL'SİNDEKİ sorgu dizesinde sağlanan parametre değeri:</span><span class="sxs-lookup"><span data-stu-id="72bed-149">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

<span data-ttu-id="72bed-150">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="72bed-150">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span></span>

<span data-ttu-id="72bed-151">Çıkarım kuralları eylem parametrelerini varsayılan veri kaynakları için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="72bed-151">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="72bed-152">Bu kurallar, aksi takdirde eylem parametrelerini el ile uygulamak büyük olasılıkla bağlama kaynaklarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72bed-152">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="72bed-153">Bağlama kaynak öznitelikleri gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="72bed-153">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="72bed-154">**[FromBody]**  karmaşık tür parametreleri için algılanır.</span><span class="sxs-lookup"><span data-stu-id="72bed-154">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="72bed-155">Bu kural için bir özel gibi karmaşık, yerleşik ile herhangi bir türü özel bir anlamı olan [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) ve [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span><span class="sxs-lookup"><span data-stu-id="72bed-155">An exception to this rule is any complex, built-in type with a special meaning, such as [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) and [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span></span> <span data-ttu-id="72bed-156">Bağlama kaynak çıkarım kodu, bu özel türleri yok sayar.</span><span class="sxs-lookup"><span data-stu-id="72bed-156">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="72bed-157">Birden fazla parametre açıkça belirtilen bir eylem sahip olduğunda (aracılığıyla `[FromBody]`) veya isteği gövdesinden bağlı olarak çıkarımı yapılan, bir özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="72bed-157">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="72bed-158">Örneğin, aşağıdaki eylemi imzaları bir özel durum neden:</span><span class="sxs-lookup"><span data-stu-id="72bed-158">For example, the following action signatures cause an exception:</span></span>

<span data-ttu-id="72bed-159">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span><span class="sxs-lookup"><span data-stu-id="72bed-159">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span></span>

* <span data-ttu-id="72bed-160">**[FromForm]**  için eylem parametrelerini tür çıkarımı yapılan [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) ve [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span><span class="sxs-lookup"><span data-stu-id="72bed-160">**[FromForm]** is inferred for action parameters of type [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span></span> <span data-ttu-id="72bed-161">Tüm basit veya kullanıcı tanımlı türler için olayla değil.</span><span class="sxs-lookup"><span data-stu-id="72bed-161">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="72bed-162">**[FromRoute]**  rota şablonu içindeki bir parametre eşleşen herhangi bir eylem parametresi adını algılanır.</span><span class="sxs-lookup"><span data-stu-id="72bed-162">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="72bed-163">Birden çok yol bir eylem parametresinin eşleştiğinde, herhangi bir rota değeri olarak kabul edilir `[FromRoute]`.</span><span class="sxs-lookup"><span data-stu-id="72bed-163">When multiple routes match an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="72bed-164">**[FromQuery]**  için başka bir eylem parametrelerini algılanır.</span><span class="sxs-lookup"><span data-stu-id="72bed-164">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="72bed-165">Aşağıdaki kod ile varsayılan çıkarım kuralları devre dışı *Startup.ConfigureServices*:</span><span class="sxs-lookup"><span data-stu-id="72bed-165">The default inference rules are disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="72bed-166">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span><span class="sxs-lookup"><span data-stu-id="72bed-166">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span></span>

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="72bed-167">Multipart/form-data isteği çıkarımı</span><span class="sxs-lookup"><span data-stu-id="72bed-167">Multipart/form-data request inference</span></span>

<span data-ttu-id="72bed-168">Ne zaman bir eylem parametresine açıklama ile [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) özniteliği `multipart/form-data` içerik türü çıkarımı yapılan istek.</span><span class="sxs-lookup"><span data-stu-id="72bed-168">When an action parameter is annotated with the [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="72bed-169">Aşağıdaki kod ile varsayılan davranışı devre dışı bırakılır *Startup.ConfigureServices*:</span><span class="sxs-lookup"><span data-stu-id="72bed-169">The default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="72bed-170">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="72bed-170">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span></span>

### <a name="attribute-routing-requirement"></a><span data-ttu-id="72bed-171">Yönlendirme gereksinim özniteliği</span><span class="sxs-lookup"><span data-stu-id="72bed-171">Attribute routing requirement</span></span>

<span data-ttu-id="72bed-172">Öznitelik yönlendirme gereksinimi olur.</span><span class="sxs-lookup"><span data-stu-id="72bed-172">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="72bed-173">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="72bed-173">For example:</span></span>

<span data-ttu-id="72bed-174">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span><span class="sxs-lookup"><span data-stu-id="72bed-174">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span></span>

<span data-ttu-id="72bed-175">Eylemler aracılığıyla erişilemez [geleneksel yolları](xref:mvc/controllers/routing#conventional-routing) tanımlanan [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) veya [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) içinde *Startup.Configure*.</span><span class="sxs-lookup"><span data-stu-id="72bed-175">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) or by [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) in *Startup.Configure*.</span></span>
::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="72bed-176">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="72bed-176">Additional resources</span></span>

* [<span data-ttu-id="72bed-177">Denetleyici eylem dönüş türleri</span><span class="sxs-lookup"><span data-stu-id="72bed-177">Controller action return types</span></span>](xref:web-api/action-return-types)
* [<span data-ttu-id="72bed-178">Özel biçimlendiriciler</span><span class="sxs-lookup"><span data-stu-id="72bed-178">Custom formatters</span></span>](xref:web-api/advanced/custom-formatters)
* [<span data-ttu-id="72bed-179">Yanıt verilerini biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="72bed-179">Format response data</span></span>](xref:web-api/advanced/formatting)
* [<span data-ttu-id="72bed-180">Swagger kullanarak yardım sayfalarına</span><span class="sxs-lookup"><span data-stu-id="72bed-180">Help pages using Swagger</span></span>](xref:tutorials/web-api-help-pages-using-swagger)
* [<span data-ttu-id="72bed-181">Denetleyici eylemlerine yönlendirme</span><span class="sxs-lookup"><span data-stu-id="72bed-181">Routing to controller actions</span></span>](xref:mvc/controllers/routing)