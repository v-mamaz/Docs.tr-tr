---
title: "ASP.NET Core MVC EF temel - Gelişmiş - 10, 10"
author: tdykstra
description: "Bu öğretici Entity Framework Çekirdek kullanan ASP.NET web uygulamaları geliştirme temellerini gittiğiniz zaman uyumlu olması için kullanışlı olan çeşitli konular tanıtır."
keywords: "ASP.NET Core, Entity Framework Çekirdek, ham sql, sql, havuz deseni, çalışma deseni, otomatik değişikliği algılama biriminin var olan veritabanı inceleyin"
ms.author: tdykstra
manager: wpickett
ms.date: 03/15/2017
ms.topic: get-started-article
ms.assetid: 92a2986a-d005-4ff6-9559-6657fd466bb7
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-mvc/advanced
ms.openlocfilehash: d63502a32e38eb192b40f21f5cd57d20048154e3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
# <a name="advanced-topics---ef-core-with-aspnet-core-mvc-tutorial-10-of-10"></a><span data-ttu-id="4d1ad-104">Gelişmiş konular - EF çekirdek ASP.NET Core MVC Öğreticisi (10 / 10)</span><span class="sxs-lookup"><span data-stu-id="4d1ad-104">Advanced topics - EF Core with ASP.NET Core MVC tutorial (10 of 10)</span></span>

<span data-ttu-id="4d1ad-105">Tarafından [zel Dykstra](https://github.com/tdykstra) ve [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4d1ad-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4d1ad-106">Contoso University örnek web uygulaması Entity Framework Çekirdek ve Visual Studio kullanarak ASP.NET Core MVC web uygulamalarının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-106">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="4d1ad-107">Eğitmen serisi hakkında daha fazla bilgi için bkz: [serideki ilk öğreticide](intro.md).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-107">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="4d1ad-108">Önceki öğreticide tablo başına hiyerarşisi devralma uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-108">In the previous tutorial, you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="4d1ad-109">Bu öğretici Entity Framework Çekirdek kullanan ASP.NET Core web uygulamaları geliştirme temellerini gittiğiniz zaman uyumlu olması için kullanışlı olan çeşitli konular tanıtır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-109">This tutorial introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET Core web applications that use Entity Framework Core.</span></span>

## <a name="raw-sql-queries"></a><span data-ttu-id="4d1ad-110">Ham SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="4d1ad-110">Raw SQL Queries</span></span>

<span data-ttu-id="4d1ad-111">Entity Framework kullanmanın yararları, veri depolamanın çok yakından belirli bir yöntem kodunuzu bağlamadan önler biridir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-111">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="4d1ad-112">SQL sorguları ve komutlar, ayrıca bunları kendiniz yazmak zorunda kalmaktan boşaltır oluşturarak bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-112">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="4d1ad-113">Ancak el ile oluşturduğunuz belirli SQL sorguları çalıştırmak gerektiğinde olağanüstü senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-113">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created.</span></span> <span data-ttu-id="4d1ad-114">Bu senaryolar için Entity Framework kod ilk API, SQL komutlarını veritabanına doğrudan geçirmenizi sağlayan yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-114">For these scenarios, the Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="4d1ad-115">EF çekirdek 1.0 aşağıdaki seçenekleriniz vardır:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-115">You have the following options in EF Core 1.0:</span></span>

* <span data-ttu-id="4d1ad-116">Kullanım `DbSet.FromSql` varlık türleri döndüren sorgular için yöntem.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-116">Use the `DbSet.FromSql` method for queries that return entity types.</span></span> <span data-ttu-id="4d1ad-117">Döndürülen nesneleri tarafından beklenen türde olmalıdır `DbSet` nesne ve otomatik olarak izlenir tarafından veritabanı bağlamı sürece, [izleme kapatmak](crud.md#no-tracking-queries).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-117">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you [turn tracking off](crud.md#no-tracking-queries).</span></span>

* <span data-ttu-id="4d1ad-118">Kullanım `Database.ExecuteSqlCommand` sorgu dışı komutları için.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-118">Use the `Database.ExecuteSqlCommand` for non-query commands.</span></span>

<span data-ttu-id="4d1ad-119">Varlık olmayan türleri döndüren bir sorgu çalıştırmanız gerekiyorsa, EF tarafından sağlanan veritabanı bağlantısı ile ADO.NET kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-119">If you need to run a query that returns types that aren't entities, you can use ADO.NET with the database connection provided by EF.</span></span> <span data-ttu-id="4d1ad-120">Varlık türlerini almak için bu yöntemi kullanmak olsa bile döndürülen verileri veritabanı bağlamı tarafından izlenen değil.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-120">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>

<span data-ttu-id="4d1ad-121">Bir web uygulamasında SQL komutlarını yürüttüğünüzde her zaman true olarak, siteniz SQL ekleme saldırılarına karşı korumak için önlemler almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-121">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="4d1ad-122">Bunu yapmanın bir yolu, bir web sayfası tarafından gönderilen dizeleri SQL komutlarını yorumlanan emin olmak için parametreli sorgular kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-122">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="4d1ad-123">Bu öğreticide kullanıcı girişi bir sorgu tümleştirdiğinizde parametreli sorgular kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-123">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

## <a name="call-a-query-that-returns-entities"></a><span data-ttu-id="4d1ad-124">Varlık döndüren bir sorgu arayın</span><span class="sxs-lookup"><span data-stu-id="4d1ad-124">Call a query that returns entities</span></span>

<span data-ttu-id="4d1ad-125">`DbSet<TEntity>` Sınıfı türünde bir varlık döndüren bir sorgu çalıştırmak için kullanabileceğiniz bir yöntem sağlar `TEntity`.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-125">The `DbSet<TEntity>` class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="4d1ad-126">Bu, nasıl çalıştığını görmek için kodda değiştireceğiz `Details` departmanı denetleyicisinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-126">To see how this works you'll change the code in the `Details` method of the Department controller.</span></span>

<span data-ttu-id="4d1ad-127">İçinde *DepartmentsController.cs*, `Details` yöntemi, bir bölüm ile alan kodu değiştirin bir `FromSql` vurgulanan aşağıdaki kodda gösterildiği gibi yöntem çağrısı:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-127">In *DepartmentsController.cs*, in the `Details` method, replace the code that retrieves a department with a `FromSql` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_RawSQL&highlight=8,9,10,13)]

<span data-ttu-id="4d1ad-128">Yeni kod düzgün çalıştığını doğrulamak için seçin **Departmanlar** sekmesini ve ardından **ayrıntıları** Departmanlar biri için.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-128">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![Departman ayrıntıları](advanced/_static/department-details.png)

## <a name="call-a-query-that-returns-other-types"></a><span data-ttu-id="4d1ad-130">Diğer türleri döndüren bir sorgu arayın</span><span class="sxs-lookup"><span data-stu-id="4d1ad-130">Call a query that returns other types</span></span>

<span data-ttu-id="4d1ad-131">Daha önce bir öğrenci istatistikleri kılavuz Öğrenciler sayısı için her kayıt tarihi gösterdi hakkında sayfası için oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-131">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="4d1ad-132">Veri Öğrenciler varlık kümesinde var (`_context.Students`) ve sonuçları bir liste halinde projeye LINQ kullanılan `EnrollmentDateGroup` model nesneleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-132">You got the data from the Students entity set (`_context.Students`) and used LINQ to project the results into a list of `EnrollmentDateGroup` view model objects.</span></span> <span data-ttu-id="4d1ad-133">SQL kendisi yerine LINQ kullanarak yazma istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-133">Suppose you want to write the SQL itself rather than using LINQ.</span></span> <span data-ttu-id="4d1ad-134">Bir SQL sorgusu çalıştırması gerekecek yapmak için varlık nesnesi dışında bir şey döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-134">To do that you need to run a SQL query that returns something other than entity objects.</span></span> <span data-ttu-id="4d1ad-135">EF çekirdek 1. 0'bunu yapmak için bir ADO.NET kod yazma ve veritabanı bağlantısı EF elde yoludur.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-135">In EF Core 1.0, one way to do that is write ADO.NET code and get the database connection from EF.</span></span>

<span data-ttu-id="4d1ad-136">İçinde *HomeController.cs*, yerine `About` aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-136">In *HomeController.cs*, replace the `About` method with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseRawSQL&highlight=3-32)]

<span data-ttu-id="4d1ad-137">Kullanarak bir ekleme deyimi:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-137">Add a using statement:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings2)]

<span data-ttu-id="4d1ad-138">Uygulamayı çalıştırın ve hakkında sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-138">Run the app and go to the About page.</span></span> <span data-ttu-id="4d1ad-139">Uygulama önceden olduğu aynı verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-139">It displays the same data it did before.</span></span>

![Sayfa hakkında](advanced/_static/about.png)

## <a name="call-an-update-query"></a><span data-ttu-id="4d1ad-141">Güncelleştirme sorgusu çağırın</span><span class="sxs-lookup"><span data-stu-id="4d1ad-141">Call an update query</span></span>

<span data-ttu-id="4d1ad-142">Contoso University yöneticiler her indirmelere için iadeleri sayısını değiştirme veritabanındaki genel değişiklikler gerçekleştirmek istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-142">Suppose Contoso University administrators want to perform global changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="4d1ad-143">Çok sayıda kurslar university varsa, tüm varlıklar almak ve bunları tek tek değiştirmek için verimsiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-143">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="4d1ad-144">Bu bölümde, tüm kurslara krediler sayısını değiştirmek bir faktör belirtmesini sağlayan bir web sayfası uygulamak ve SQL UPDATE deyimi yürüterek değişiklik.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-144">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL UPDATE statement.</span></span> <span data-ttu-id="4d1ad-145">Web sayfasını aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-145">The web page will look like the following illustration:</span></span>

![Güncelleştirme indirmelere krediler sayfası](advanced/_static/update-credits.png)

<span data-ttu-id="4d1ad-147">İçinde *CoursesContoller.cs*, HttpGet ve HttpPost için UpdateCourseCredits yöntemleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-147">In *CoursesContoller.cs*, add UpdateCourseCredits methods for HttpGet and HttpPost:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdateGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdatePost)]

<span data-ttu-id="4d1ad-148">Denetleyici HttpGet isteği işlediğinde, hiçbir şey döndürülür `ViewData["RowsAffected"]`, yukarıdaki çizimde gösterildiği gibi görünümün boş bir metin kutusu ve bir gönderme düğmesi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-148">When the controller processes an HttpGet request, nothing is returned in `ViewData["RowsAffected"]`, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="4d1ad-149">Zaman **güncelleştirme** düğmesine tıklandığında, HttpPost yöntemi çağrılır ve çarpanı metin kutusuna girilen değere sahip.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-149">When the **Update** button is clicked, the HttpPost method is called, and multiplier has the value entered in the text box.</span></span> <span data-ttu-id="4d1ad-150">Kodu sonra kurslar güncelleştirir ve görünümüne etkilenen satır sayısını döndürür SQL yürütür `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-150">The code then executes the SQL that updates courses and returns the number of affected rows to the view in `ViewData`.</span></span> <span data-ttu-id="4d1ad-151">Görünüm zaman alır bir `RowsAffected` değeri, güncelleştirilmiş satır sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-151">When the view gets a `RowsAffected` value, it displays the number of rows updated.</span></span>

<span data-ttu-id="4d1ad-152">İçinde **Çözüm Gezgini**, sağ *görünümler/kurslar* klasörünü ve ardından **Ekle > Yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-152">In **Solution Explorer**, right-click the *Views/Courses* folder, and then click **Add > New Item**.</span></span>

<span data-ttu-id="4d1ad-153">İçinde **Yeni Öğe Ekle** iletişim kutusunda, tıklatın **ASP.NET** altında **yüklü** sol bölmede **MVC görünüm sayfası**ve YeniGörünümadı *UpdateCourseCredits.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-153">In the **Add New Item** dialog, click **ASP.NET** under **Installed** in the left pane, click **MVC View Page**, and name the new view *UpdateCourseCredits.cshtml*.</span></span>

<span data-ttu-id="4d1ad-154">İçinde *Views/Courses/UpdateCourseCredits.cshtml*, şablon kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-154">In *Views/Courses/UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-html[Main](intro/samples/cu/Views/Courses/UpdateCourseCredits.cshtml)]

<span data-ttu-id="4d1ad-155">Çalıştırma `UpdateCourseCredits` seçerek yöntemi **kurslar** sonra ekleyerek sekmesinde, "/ UpdateCourseCredits" sonuna kadar tarayıcının adres çubuğundaki URL'yi (örneğin: `http://localhost:5813/Courses/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-155">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:5813/Courses/UpdateCourseCredits`).</span></span> <span data-ttu-id="4d1ad-156">Metin kutusuna bir sayı girin:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-156">Enter a number in the text box:</span></span>

![Güncelleştirme indirmelere krediler sayfası](advanced/_static/update-credits.png)

<span data-ttu-id="4d1ad-158">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-158">Click **Update**.</span></span> <span data-ttu-id="4d1ad-159">Etkilenen satırların sayısını bakın:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-159">You see the number of rows affected:</span></span>

![Etkilenen Satırlar güncelleştirme indirmelere krediler sayfası](advanced/_static/update-credits-rows-affected.png)

<span data-ttu-id="4d1ad-161">Tıklatın **listesine dön** krediler düzenlenen sayısıyla kurslar listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-161">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="4d1ad-162">Üretim kodu her zaman geçerli bir veri kümesinde güncelleştirmelerinin sağlar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-162">Note that production code would ensure that updates always result in valid data.</span></span> <span data-ttu-id="4d1ad-163">Burada gösterilen Basitleştirilmiş kodu 5'ten büyük sayılar elde etmek yeterince krediler sayısı çarpabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-163">The simplified code shown here could multiply the number of credits enough to result in numbers greater than 5.</span></span> <span data-ttu-id="4d1ad-164">( `Credits` Özelliğine sahip bir `[Range(0, 5)]` özniteliği.) Güncelleştirme sorgusu çalışır ancak geçersiz veriler, krediler sayısı 5 veya daha az olduğunu varsayalım diğer bölümlerinde sistem beklenmeyen sonuçlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-164">(The `Credits` property has a `[Range(0, 5)]` attribute.) The update query would work but the invalid data could cause unexpected results in other parts of the system that assume the number of credits is 5 or less.</span></span>

<span data-ttu-id="4d1ad-165">Ham SQL sorguları hakkında daha fazla bilgi için bkz: [ham SQL sorguları](https://docs.microsoft.com/ef/core/querying/raw-sql).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-165">For more information about raw SQL queries, see [Raw SQL Queries](https://docs.microsoft.com/ef/core/querying/raw-sql).</span></span>

## <a name="examine-sql-sent-to-the-database"></a><span data-ttu-id="4d1ad-166">SQL veritabanına gönderilen inceleyin</span><span class="sxs-lookup"><span data-stu-id="4d1ad-166">Examine SQL sent to the database</span></span>

<span data-ttu-id="4d1ad-167">Bazen veritabanına gönderilen gerçek SQL sorguları görebilmek için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-167">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="4d1ad-168">Yerleşik günlük işlevselliği için ASP.NET Core içeren SQL sorguları ve güncelleştirmeleri için günlükler yazmak için EF çekirdek tarafından otomatik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-168">Built-in logging functionality for ASP.NET Core is automatically used by EF Core to write logs that contain the SQL for queries and updates.</span></span> <span data-ttu-id="4d1ad-169">Bu bölümde bazı örnekler SQL günlüğü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-169">In this section you'll see some examples of SQL logging.</span></span>

<span data-ttu-id="4d1ad-170">Açık *StudentsController.cs* ve `Details` yöntemi açık bir kesme noktası ayarlayın `if (student == null)` deyimi.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-170">Open *StudentsController.cs* and in the `Details` method set a breakpoint on the `if (student == null)` statement.</span></span>

<span data-ttu-id="4d1ad-171">Uygulamayı hata ayıklama modunda çalıştırın ve bir öğrenci için ayrıntıları sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-171">Run the app in debug mode, and go to the Details page for a student.</span></span>

<span data-ttu-id="4d1ad-172">Git **çıkış** hata ayıklama gösteren penceresi çıkış ve sorgu bakın:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-172">Go to the **Output** window showing debug output, and you see the query:</span></span>

```
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (56ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT TOP(2) [s].[ID], [s].[Discriminator], [s].[FirstName], [s].[LastName], [s].[EnrollmentDate]
FROM [Person] AS [s]
WHERE ([s].[Discriminator] = N'Student') AND ([s].[ID] = @__id_0)
ORDER BY [s].[ID]
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (122ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT [s.Enrollments].[EnrollmentID], [s.Enrollments].[CourseID], [s.Enrollments].[Grade], [s.Enrollments].[StudentID], [e.Course].[CourseID], [e.Course].[Credits], [e.Course].[DepartmentID], [e.Course].[Title]
FROM [Enrollment] AS [s.Enrollments]
INNER JOIN [Course] AS [e.Course] ON [s.Enrollments].[CourseID] = [e.Course].[CourseID]
INNER JOIN (
    SELECT TOP(1) [s0].[ID]
    FROM [Person] AS [s0]
    WHERE ([s0].[Discriminator] = N'Student') AND ([s0].[ID] = @__id_0)
    ORDER BY [s0].[ID]
) AS [t] ON [s.Enrollments].[StudentID] = [t].[ID]
ORDER BY [t].[ID]
```

<span data-ttu-id="4d1ad-173">Burada herhangi bir şey, beklenmedik fark edeceksiniz: SQL en çok 2 satırları seçer (`TOP(2)`) Kişi tablosundan.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-173">You'll notice something here that might surprise you: the SQL selects up to 2 rows (`TOP(2)`) from the Person table.</span></span> <span data-ttu-id="4d1ad-174">`SingleOrDefaultAsync` Yöntemi, sunucu üzerindeki 1 satır için çözümlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-174">The `SingleOrDefaultAsync` method doesn't resolve to 1 row on the server.</span></span> <span data-ttu-id="4d1ad-175">Neden şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-175">Here's why:</span></span>

* <span data-ttu-id="4d1ad-176">Sorgu birden çok satır döndürürse, bu yöntem null değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-176">If the query would return multiple rows, the method returns null.</span></span>
* <span data-ttu-id="4d1ad-177">Sorgu birden çok satır döndürecekti olup olmadığını belirlemek için en az 2 döndürür denetlemek EF sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-177">To determine whether the query would return multiple rows, EF has to check if it returns at least 2.</span></span>

<span data-ttu-id="4d1ad-178">Hata ayıklama modunu kullanın ve günlük çıktısı almak için bir kesme noktasında durdurmak yok Not **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-178">Note that you don't have to use debug mode and stop at a breakpoint to get logging output in the **Output** window.</span></span> <span data-ttu-id="4d1ad-179">Bu günlük çıktıyı görünmesini istediğiniz noktada durdurmak için yalnızca bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-179">It's just a convenient way to stop the logging at the point you want to look at the output.</span></span> <span data-ttu-id="4d1ad-180">Bunu yok ise, günlük kaydı devam eder ve geri ilgilendiğiniz bölümleri bulmak için kaydırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-180">If you don't do that, logging continues and you have to scroll back to find the parts you're interested in.</span></span>

## <a name="repository-and-unit-of-work-patterns"></a><span data-ttu-id="4d1ad-181">Depo ve iş desenleri birimi</span><span class="sxs-lookup"><span data-stu-id="4d1ad-181">Repository and unit of work patterns</span></span>

<span data-ttu-id="4d1ad-182">Çoğu geliştiricinin depo ve iş desenleri biriminin Entity Framework ile çalışan kod çevresinde bir sarmalayıcı olarak uygulamak için kod yazma.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-182">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="4d1ad-183">Bu düzenleri, veri erişim katmanı ve bir uygulamanın iş mantığı katmanı arasındaki bir Soyutlama Katmanı oluşturmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-183">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="4d1ad-184">Bu desenleri uygulama veri deposunda değişiklik uygulamanızdan verenlerden yardımcı olabilir ve otomatik birim testi veya teste dayalı geliştirme (TDD) kolaylaştırabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-184">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="4d1ad-185">Ancak, bu desenleri uygulamak için ek kod yazma her zaman en iyi seçenek EF, çeşitli nedenlerle kullanan uygulamalar için değil:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-185">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

* <span data-ttu-id="4d1ad-186">EF bağlamı sınıfının kendisi veri deposu özel kod kodunuzdan korunmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-186">The EF context class itself insulates your code from data-store-specific code.</span></span>

* <span data-ttu-id="4d1ad-187">EF bağlam sınıfını EF kullanarak bunu veritabanı için bir iş birimi sınıf güncelleştirmeleri olarak davranamaz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-187">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>

* <span data-ttu-id="4d1ad-188">EF deposu kod yazmadan TDD uygulamaya yönelik özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-188">EF includes features for implementing TDD without writing repository code.</span></span>

<span data-ttu-id="4d1ad-189">Depo ve iş desenleri ölçü uygulama hakkında daha fazla bilgi için bkz: [Bu öğretici seri Entity Framework 5 sürümünü](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-189">For information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span></span>

<span data-ttu-id="4d1ad-190">Entity Framework Çekirdek test etmek için kullanılan bir bellek içi veritabanı sağlayıcısı uygular.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-190">Entity Framework Core implements an in-memory database provider that can be used for testing.</span></span> <span data-ttu-id="4d1ad-191">Daha fazla bilgi için bkz: [Inmemory ile test](https://docs.microsoft.com/ef/core/miscellaneous/testing/in-memory).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-191">For more information, see [Testing with InMemory](https://docs.microsoft.com/ef/core/miscellaneous/testing/in-memory).</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="4d1ad-192">Otomatik değiştirme algılama</span><span class="sxs-lookup"><span data-stu-id="4d1ad-192">Automatic change detection</span></span>

<span data-ttu-id="4d1ad-193">Entity Framework bir varlık nasıl değiştiğini (ve bu nedenle hangi veritabanına gönderilmesi gereken güncelleştirmeler) geçerli bir varlık değerleri özgün değerlerle karşılaştırarak belirler.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-193">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="4d1ad-194">Varlık sorgulanan ya da bağlı olduğunda özgün değerler depolanır.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-194">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="4d1ad-195">Otomatik değiştirme algılama neden yöntemlerin bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-195">Some of the methods that cause automatic change detection are the following:</span></span>

* <span data-ttu-id="4d1ad-196">DbContext.SaveChanges</span><span class="sxs-lookup"><span data-stu-id="4d1ad-196">DbContext.SaveChanges</span></span>

* <span data-ttu-id="4d1ad-197">DbContext.Entry</span><span class="sxs-lookup"><span data-stu-id="4d1ad-197">DbContext.Entry</span></span>

* <span data-ttu-id="4d1ad-198">ChangeTracker.Entries</span><span class="sxs-lookup"><span data-stu-id="4d1ad-198">ChangeTracker.Entries</span></span>

<span data-ttu-id="4d1ad-199">Çok sayıda varlık takip ettiğiniz ve aşağıdaki yöntemlerden birini birçok kez bir döngüde çağırmanız, algılama otomatik değişiklik kullanarak geçici olarak kapatarak önemli performans geliştirmeleri alabilirsiniz `ChangeTracker.AutoDetectChangesEnabled` özelliği.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-199">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the `ChangeTracker.AutoDetectChangesEnabled` property.</span></span> <span data-ttu-id="4d1ad-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-200">For example:</span></span>

```csharp
_context.ChangeTracker.AutoDetectChangesEnabled = false;
```

## <a name="entity-framework-core-source-code-and-development-plans"></a><span data-ttu-id="4d1ad-201">Entity Framework Çekirdek kaynak kodu ve Geliştirme planları</span><span class="sxs-lookup"><span data-stu-id="4d1ad-201">Entity Framework Core source code and development plans</span></span>

<span data-ttu-id="4d1ad-202">Entity Framework Çekirdek için kaynak kodunu şu adresten edinilebilir [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-202">The source code for Entity Framework Core is available at [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span></span> <span data-ttu-id="4d1ad-203">Kaynak kodu yanı sıra, her gece derlemeleri almak, sorun izleme, özellik belirtimlerin, toplantı notları tasarım [ileride geliştirme için yol haritası](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap)ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-203">Besides source code, you can get nightly builds, issue tracking, feature specs, design meeting notes, [the roadmap for future development](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap), and more.</span></span> <span data-ttu-id="4d1ad-204">Hatalar dosya ve kendi geliştirmeler EF kaynak kodu katkıda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-204">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="4d1ad-205">Kaynak kodu açık olsa da, Entity Framework Çekirdek tam bir Microsoft ürünü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-205">Although the source code is open, Entity Framework Core is fully supported as a Microsoft product.</span></span> <span data-ttu-id="4d1ad-206">Microsoft Entity Framework takım üzerinde Katkıları kabul edilen denetim tutar ve her sürümle kalitesini emin olmak için tüm kod değişiklikleri sınar.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-206">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="reverse-engineer-from-existing-database"></a><span data-ttu-id="4d1ad-207">Varolan veritabanından ters mühendislik</span><span class="sxs-lookup"><span data-stu-id="4d1ad-207">Reverse engineer from existing database</span></span>

<span data-ttu-id="4d1ad-208">Varolan bir veritabanını varlık sınıflardan dahil olmak üzere bir veri modeli ters mühendislik için kullanmak [iskele dbcontext](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) komutu.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-208">To reverse engineer a data model including entity classes from an existing database, use the [scaffold-dbcontext](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) command.</span></span> <span data-ttu-id="4d1ad-209">Bkz: [başlangıç Öğreticisi](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-209">See the [getting-started tutorial](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span></span>

<a id="dynamic-linq"></a>
## <a name="use-dynamic-linq-to-simplify-sort-selection-code"></a><span data-ttu-id="4d1ad-210">Sıralama seçimi kodu basitleştirmek için dinamik LINQ kullanma</span><span class="sxs-lookup"><span data-stu-id="4d1ad-210">Use dynamic LINQ to simplify sort selection code</span></span>

<span data-ttu-id="4d1ad-211">[Bu serideki üçüncü öğretici](sort-filter-page.md) LINQ kodunun kodlama sabit sütun adları tarafından nasıl yazılacağını gösterir bir `switch` deyimi.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-211">The [third tutorial in this series](sort-filter-page.md) shows how to write LINQ code by hard-coding column names in a `switch` statement.</span></span> <span data-ttu-id="4d1ad-212">Aralarından seçim yapabileceğiniz iki sütunlarla bu düzgün çalışır, ancak çok sayıda sütun varsa, kodu ayrıntılı alabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-212">With two columns to choose from, this works fine, but if you have many columns the code could get verbose.</span></span> <span data-ttu-id="4d1ad-213">Bu sorunu çözmek için kullanabileceğiniz `EF.Property` yöntemi bir dize olarak özellik adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-213">To solve that problem, you can use the `EF.Property` method to specify the name of the property as a string.</span></span> <span data-ttu-id="4d1ad-214">Bu yaklaşım denemek için değiştirme `Index` yönteminde `StudentsController` aşağıdaki kod ile.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-214">To try out this approach, replace the `Index` method in the `StudentsController` with the following code.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DynamicLinq)]

## <a name="next-steps"></a><span data-ttu-id="4d1ad-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d1ad-215">Next steps</span></span>

<span data-ttu-id="4d1ad-216">Bu, bir ASP.NET MVC uygulamasındaki Entity Framework Çekirdek kullanma öğreticileri bu dizi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-216">This completes this series of tutorials on using the Entity Framework Core in an ASP.NET MVC application.</span></span>

<span data-ttu-id="4d1ad-217">EF çekirdek hakkında daha fazla bilgi için bkz: [Entity Framework Core belgeleri](https://docs.microsoft.com/ef/core).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-217">For more information about EF Core, see the [Entity Framework Core documentation](https://docs.microsoft.com/ef/core).</span></span> <span data-ttu-id="4d1ad-218">Kitap da kullanılabilir: [Entity Framework Çekirdek eylem](https://www.manning.com/books/entity-framework-core-in-action).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-218">A book is also available: [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span></span>

<span data-ttu-id="4d1ad-219">Temel aldık sonra web uygulamanızı dağıtma hakkında daha fazla bilgi için bkz: [yayımlama ve dağıtım](../../publishing/index.md).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-219">For information about how to deploy your web application after you've built it, see [Publishing and deployment](../../publishing/index.md).</span></span>

<span data-ttu-id="4d1ad-220">ASP.NET Core MVC için kimlik doğrulama ve yetkilendirme gibi ilgili diğer konular hakkında bilgi için bkz: [ASP.NET Core belgeleri](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="4d1ad-220">For information about other topics related to ASP.NET Core MVC, such as authentication and authorization, see the [ASP.NET Core documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="4d1ad-221">İlgili kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4d1ad-221">Acknowledgments</span></span>

<span data-ttu-id="4d1ad-222">Zel Dykstra ve Rick Anderson (twitter @RickAndMSFT) Bu öğretici yazıldı.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-222">Tom Dykstra and Rick Anderson (twitter @RickAndMSFT) wrote this tutorial.</span></span> <span data-ttu-id="4d1ad-223">Rowan Mert, Diego Vega ve diğer Entity Framework ekibi üyelerinin kod incelemeleri destekli ve biz öğreticileri için kod yazma sırada, çıkan hatalarını ayıklamanıza yardımcı oldu.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-223">Rowan Miller, Diego Vega, and other members of the Entity Framework team assisted with code reviews and helped debug issues that arose while we were writing code for the tutorials.</span></span>

## <a name="common-errors"></a><span data-ttu-id="4d1ad-224">Sık karşılaşılan hataları</span><span class="sxs-lookup"><span data-stu-id="4d1ad-224">Common errors</span></span>  

### <a name="contosouniversitydll-used-by-another-process"></a><span data-ttu-id="4d1ad-225">Başka bir işlem tarafından kullanılan ContosoUniversity.dll</span><span class="sxs-lookup"><span data-stu-id="4d1ad-225">ContosoUniversity.dll used by another process</span></span>

<span data-ttu-id="4d1ad-226">Hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-226">Error message:</span></span>

> <span data-ttu-id="4d1ad-227">Açılamıyor '... bin\Debug\netcoreapp1.0\ContosoUniversity.dll' yazma--' işlem dosya erişemiyor '... \bin\Debug\netcoreapp1.0\ContosoUniversity.dll' başka bir işlem tarafından kullanıldığından.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-227">Cannot open '...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' for writing -- 'The process cannot access the file '...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll' because it is being used by another process.</span></span>

<span data-ttu-id="4d1ad-228">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-228">Solution:</span></span>

<span data-ttu-id="4d1ad-229">IIS Express sitede durdurun.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-229">Stop the site in IIS Express.</span></span> <span data-ttu-id="4d1ad-230">Windows sistem tepsisi için IIS Express bulmak ve simgesini sağ tıklatın, Contoso University siteyi seçin ve ardından Git **durdurmak Site**.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-230">Go to the Windows System Tray, find IIS Express and right-click its icon, select the Contoso University site, and then click **Stop Site**.</span></span>

### <a name="migration-scaffolded-with-no-code-in-up-and-down-methods"></a><span data-ttu-id="4d1ad-231">Hiçbir kod bulunan yöntemleri yukarı ve aşağı iskele kurulmuş geçiş</span><span class="sxs-lookup"><span data-stu-id="4d1ad-231">Migration scaffolded with no code in Up and Down methods</span></span>

<span data-ttu-id="4d1ad-232">Olası neden:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-232">Possible cause:</span></span>

<span data-ttu-id="4d1ad-233">EF CLI komutları otomatik olarak kapatmak ve kod dosyaları kaydetmek yok.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-233">The EF CLI commands don't automatically close and save code files.</span></span> <span data-ttu-id="4d1ad-234">Programını çalıştırdığınızda, kaydedilmemiş değişiklikleriniz varsa `migrations add` komutunu EF değişikliklerinizi Bul olmaz.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-234">If you have unsaved changes when you run the `migrations add` command, EF won't find your changes.</span></span>

<span data-ttu-id="4d1ad-235">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-235">Solution:</span></span>

<span data-ttu-id="4d1ad-236">Çalıştırma `migrations remove` komutu, kod değişikliklerinizi kaydedin ve yeniden `migrations add` komutu.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-236">Run the `migrations remove` command, save your code changes and rerun the `migrations add` command.</span></span>

### <a name="errors-while-running-database-update"></a><span data-ttu-id="4d1ad-237">Çalışan veritabanı güncelleştirme sırasında hatalar</span><span class="sxs-lookup"><span data-stu-id="4d1ad-237">Errors while running database update</span></span>

<span data-ttu-id="4d1ad-238">Şema değişiklikleri var olan verileri içeren bir veritabanına yaparken diğer hatalarıyla mümkündür.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-238">It's possible to get other errors when making schema changes in a database that has existing data.</span></span> <span data-ttu-id="4d1ad-239">Çözümlenemiyor Geçiş hataları alırsanız, bağlantı dizesindeki veritabanı adını değiştirin veya veritabanını silin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-239">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="4d1ad-240">Yeni bir veritabanı ile geçirmek için veri yok ve update-database komutunu hatasız tamamlamak çok daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-240">With a new database, there is no data to migrate, and the update-database command is much more likely to complete without errors.</span></span>

<span data-ttu-id="4d1ad-241">Veritabanında yeniden adlandırmak için basit yaklaşımdır *appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-241">The simplest approach is to rename the database in *appsettings.json*.</span></span> <span data-ttu-id="4d1ad-242">Sonraki çalıştırmanızda `database update`, yeni bir veritabanı oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-242">The next time you run `database update`, a new database will be created.</span></span>

<span data-ttu-id="4d1ad-243">SSOX bir veritabanını silmek için veritabanına sağ tıklayın, **silmek**ve ardından **Sil veritabanı** iletişim kutusu seç **var olan bağlantıları kapatın** ve 'ıtıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-243">To delete a database in SSOX, right-click the database, click **Delete**, and then in the **Delete Database** dialog box select **Close existing connections** and click **OK**.</span></span>

<span data-ttu-id="4d1ad-244">CLI kullanarak bir veritabanını silmek için Çalıştır `database drop` CLI komutu:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-244">To delete a database by using the CLI, run the `database drop` CLI command:</span></span>

```console
dotnet ef database drop
```

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="4d1ad-245">Hata bulmayla SQL Server örneği</span><span class="sxs-lookup"><span data-stu-id="4d1ad-245">Error locating SQL Server instance</span></span>

<span data-ttu-id="4d1ad-246">Hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-246">Error Message:</span></span>

> <span data-ttu-id="4d1ad-247">SQL Server bağlantı kurulmaya çalışılırken ağ ile ilişkili veya örneğe özgü bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-247">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="4d1ad-248">Sunucu bulunamadı veya erişilebilir değildi.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-248">The server was not found or was not accessible.</span></span> <span data-ttu-id="4d1ad-249">Örnek adının doğru olduğundan ve SQL Server Uzak bağlantılara izin verecek şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-249">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="4d1ad-250">(sağlayıcısı: SQL ağ arabirimleri, hata: 26 - Server/örnek belirtilen hata bulma)</span><span class="sxs-lookup"><span data-stu-id="4d1ad-250">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="4d1ad-251">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="4d1ad-251">Solution:</span></span>

<span data-ttu-id="4d1ad-252">Bağlantı dizesini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-252">Check the connection string.</span></span> <span data-ttu-id="4d1ad-253">Veritabanı dosyasını el ile sildiyseniz, üzerinde yeni bir veritabanı ile başlatmak için yapım dizesinde veritabanı adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4d1ad-253">If you have manually deleted the database file, change the name of the database in the construction string to start over with a new database.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="4d1ad-254">Önceki</span><span class="sxs-lookup"><span data-stu-id="4d1ad-254">Previous</span></span>](inheritance.md)