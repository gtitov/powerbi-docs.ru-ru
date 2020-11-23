---
title: Внедрение содержимого в приложение для клиентов
description: Узнайте, как правильно интегрировать (внедрять) в приложение нужные клиентам отчеты, информационные панели или плитки с помощью API Power BI для встроенной аналитики. Узнайте, как выполнять интеграцию Power BI в приложение с помощью программного обеспечения и средств встроенной аналитики, а также средств встроенной бизнес-аналитики.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
ms.topic: tutorial
ms.service: powerbi
ms.subservice: powerbi-developer
ms.custom: seodec18
ms.date: 06/02/2020
ms.openlocfilehash: dab16218406a4b97c9e2aa01974380ba09dde003
ms.sourcegitcommit: 5240990f998851c4854eb565de681099264c5a61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "94719013"
---
# <a name="tutorial-embed-power-bi-content-into-an-application-for-your-customers"></a>Руководство. Внедрение содержимого Power BI в приложение для клиентов

С помощью **Power BI Embedded в Azure** или **внедрения Power BI в Office** вы можете встраивать отчеты, панели мониторинга или плитки в приложение с помощью данных, принадлежащих ему. Модель **данных, принадлежащих приложению**, позволяет приложению использовать Power BI как встроенную платформу аналитики. Как **независимый поставщик программного обеспечения** или **разработчик** вы можете создавать содержимое Power BI, отображающее отчеты, информационные панели или плитки в приложении. При этом приложение будет полностью интегрированным и интерактивным, а пользователям не потребуется лицензия Power BI. Из этого руководства вы узнаете, как интегрировать отчет в приложение с помощью пакета SDK Power BI для .NET и API JavaScript для Power BI.

![Внедрение отчета Power BI](media/embed-sample-for-customers/embed-sample-for-customers-035.png)

Из этого руководства вы узнаете, как выполнять следующие задачи:
> [!div class="checklist"]
> * регистрация приложения в Azure;
> * внедрение отчета Power BI в приложение.

## <a name="prerequisites"></a>Предварительные требования

Для работы вам понадобятся:

* [учетная запись Power BI Pro](../../fundamentals/service-self-service-signup-for-power-bi.md) (главная учетная запись, то есть имя пользователя и пароль для входа в учетную запись Power BI Pro) или [субъект-служба (токен только для приложения)](embed-service-principal.md);
* собственная установка [клиента Azure Active Directory](create-an-azure-active-directory-tenant.md).

Если вы не зарегистрированы в **Power BI**, перед началом работы [пройдите бесплатную регистрацию](https://powerbi.microsoft.com/pricing/).

>[!NOTE]
>[Premium на пользователя (PPU)](../../admin/service-premium-per-user-faq.md) не поддерживается. Вы можете использовать PPU, чтобы поэкспериментировать с решением *внедрения для клиентов*, но вы не сможете [перенести его в рабочую среду](embed-sample-for-customers.md#move-to-production).

## <a name="set-up-your-embedded-analytics-development-environment"></a>Настройка среды разработки для встроенной аналитики

Чтобы внедрить в приложение отчеты, панели мониторинга и плитки, необходимо убедиться, что среда допускает внедрение с помощью Power BI.

Воспользуйтесь [средством настройки внедрения](https://app.powerbi.com/embedsetup), чтобы быстро приступить к работе и скачать пример приложения с пошаговой инструкцией для создания среды и внедрения отчета.

Если вы решили настроить среду вручную, см. инструкции ниже.

### <a name="register-an-application-in-azure-active-directory-azure-ad"></a>Регистрация приложения в Azure Active Directory

[Зарегистрируйте приложение](register-app.md) в Azure Active Directory, чтобы предоставить ему доступ к [REST API Power BI](/rest/api/power-bi/). Регистрация приложения позволит создать удостоверение для приложения и предоставить ему [разрешения на доступ к ресурсам REST Power BI](/azure/active-directory/develop/v2-permissions-and-consent). Способ регистрации приложения зависит от того, используете ли вы главную учетную запись или [субъект-службу](embed-service-principal.md).

Выбранный метод влияет на тип приложения, регистрируемого в Azure.

Если вы продолжаете использовать главную учетную запись, зарегистрируйте **собственное** приложение, так как в этом случае применяется неинтерактивный вход.

Если же вы используете субъект-службу, необходимо зарегистрировать **веб-приложение на стороне сервера**, чтобы создать секрет приложения.

## <a name="set-up-your-power-bi-environment"></a>Настройка рабочей среды Power BI

### <a name="create-a-workspace"></a>Создать рабочую область

Если вы планируете внедрять отчеты, панели мониторинга и плитки в приложение для клиентов, необходимо разместить содержимое в рабочей области. Можно настроить рабочие области разных типов: [традиционные](../../collaborate-share/service-create-workspaces.md) или [новые](../../collaborate-share/service-create-the-new-workspaces.md). Если вы используете *главную* учетную запись, тип рабочих областей может быть любым. Однако если вы применяете *[субъект-службу](embed-service-principal.md)* для входа в приложение, необходимо использовать новые рабочие области. И *главная* учетная запись, и *субъект-служба* должны быть администраторами рабочих областей, в которые входит приложение.

### <a name="create-and-publish-your-reports"></a>Создание и публикация отчетов

Вы можете создавать отчеты и наборы данных с помощью Power BI Desktop, а затем публиковать эти отчеты в рабочей области. Эту задачу можно выполнять двумя способами. Конечный пользователь может публиковать отчеты в традиционной рабочей области с помощью главной учетной записи (с лицензией Power BI Pro). Если вы используете субъект-службу, то можете публиковать отчеты в новых рабочих областях с помощью [REST API Power BI](/rest/api/power-bi/imports/postimportingroup).

Ниже приведены пошаговые инструкции по публикации отчета PBIX в рабочей области Power BI.

1. Скачайте пример [демонстрационной версии блога](https://github.com/Microsoft/powerbi-desktop-samples) из GitHub.

    ![Образец отчета](media/embed-sample-for-customers/embed-sample-for-customers-026-1.png)

2. Откройте PBIX-файл с образцом отчета в **Power BI Desktop**.

   ![Отчет в PBI Desktop](media/embed-sample-for-customers/embed-sample-for-customers-027.png)

3. Опубликуйте его в **рабочих областях**. Этот процесс зависит от того, используете ли вы главную учетную запись (с лицензией Power Pro) или субъект-службу. Если вы используете главную учетную запись, отчет можно опубликовать через Power BI Desktop.  Если же вы используете субъект-службу, необходимо применять REST API Power BI.

## <a name="embed-content-using-the-sample-application"></a>Внедрение содержимого с помощью примера приложения

Этот пример намеренно упрощен в целях наглядности. За защиту секрета приложения или учетных данных главной учетной записи отвечаете вы или ваши разработчики.

Чтобы приступить к внедрению содержимого, используя пример приложения, выполните указанные ниже действия.

1. Скачайте [Visual Studio](https://www.visualstudio.com/) (версии 2013 или более поздней). Обязательно скачайте последнюю версию [пакета NuGet](https://www.nuget.org/profiles/powerbi).

2. Чтобы приступить к работе, скачайте [пример с данными, принадлежащими приложению](https://github.com/Microsoft/PowerBI-Developer-Samples) из GitHub.

    ![Пример приложения с данными, принадлежащими приложению](media/embed-sample-for-customers/embed-sample-for-customers-026.png)

3. Откройте файл **Web.config** из примера приложения. Здесь есть поля, которые нужно заполнить, чтобы успешно запустить приложение. Для поля **AuthenticationType** можно выбрать значение **MasterUser** или **ServicePrincipal**. Выбранный метод проверки подлинности влияет на заполняемые поля.

    > [!Note]
    > По умолчанию в этом примере поле **AuthenticationType** имеет значение MasterUser.

    <center>

    | **MasterUser** <br> (лицензия Power BI Pro) | **ServicePrincipal** <br> (токен только для приложения)|
    |---------------|-------------------|
    | [applicationId](#application-id) | [applicationId](#application-id) |
    | [workspaceId](#workspace-id) | [workspaceId](#workspace-id) |
    | [reportId](#report-id) | [reportId](#report-id) |
    | [pbiUsername](#power-bi-username-and-password) |  |
    | [pbiPassword](#power-bi-username-and-password) |  |
    |  | [applicationsecret](#application-secret) |
    |  | [tenant](#tenant) |

   </center>

    ![Файл веб-конфигурации](media/embed-sample-for-customers/embed-sample-for-customers-030.png)

### <a name="application-id"></a>Идентификатор приложения

Этот атрибут необходим для обоих типов проверки подлинности (главной учетной записи и [субъекта-службы](embed-service-principal.md)).

Укажите в поле **applicationId** значение **идентификатора приложения** из **Azure**. Поле **applicationId** используется приложением для его идентификации для пользователей, у которых запрашиваются разрешения.

Чтобы получить значение **applicationId**, сделайте следующее.

1. Войдите на [портал Azure](https://portal.azure.com).

2. В области навигации слева выберите **Все службы**, а затем — **Регистрация приложений**.

    ![Поиск приложений для регистрации](media/embed-sample-for-customers/embed-sample-for-customers-003.png)

3. Выберите приложение, для которого требуется **applicationId**.

    ![Выбор приложения](media/embed-sample-for-customers/embed-sample-for-customers-006.png)

4. В поле **Идентификатор приложения** указан GUID. Используйте этот **идентификатор приложения** как значение параметра **applicationId** приложения.

    ![applicationId](media/embed-sample-for-customers/embed-sample-for-customers-007.png)

### <a name="workspace-id"></a>Идентификатор рабочей области

Этот атрибут необходим для обоих типов проверки подлинности (главной учетной записи и [субъекта-службы](embed-service-principal.md)).

Укажите в поле **workspaceId** GUID рабочей области (группы) из Power BI. Эти данные можно получить из URL-адреса после входа в службу Power BI или с помощью PowerShell.

URL-адрес <br>

![workspaceId](media/embed-sample-for-customers/embed-sample-for-customers-031.png)

PowerShell <br>

```powershell
Get-PowerBIworkspace -name "App Owns Embed Test"
```

   ![workspaceId из PowerShell](media/embed-sample-for-customers/embed-sample-for-customers-031-ps.png)

### <a name="report-id"></a>Идентификатор отчета

Этот атрибут необходим для обоих типов проверки подлинности (главной учетной записи и [субъекта-службы](embed-service-principal.md)).

Укажите в поле **reportId** значение GUID отчета из Power BI. Эти данные можно получить из URL-адреса после входа в службу Power BI или с помощью PowerShell.

URL-адрес<br>

![reportId](media/embed-sample-for-customers/embed-sample-for-customers-032.png)

PowerShell <br>

```powershell
Get-PowerBIworkspace -name "App Owns Embed Test" | Get-PowerBIReport
```

![reportId из PowerShell](media/embed-sample-for-customers/embed-sample-for-customers-032-ps.png)

### <a name="power-bi-username-and-password"></a>Имя пользователя и пароль Power BI

Эти атрибуты необходимы, только если в качестве типа проверки подлинности выбрана главная учетная запись.

Если для проверки подлинности используется [субъект-служба](embed-service-principal.md), заполнять атрибуты имени пользователя и пароля не нужно.

* Укажите в поле **pbiUsername** главную учетную запись Power BI.
* Укажите в поле **pbiPassword** пароль для главной учетной записи Power BI.

### <a name="application-secret"></a>Секрет приложения

Этот атрибут необходим только для типа проверки подлинности [субъект-служба](embed-service-principal.md).

Заполните сведения **ApplicationID** из раздела **Ключи** раздела **Регистрация приложений** в **Azure**.  Этот атрибут действует при использовании [субъекта-службы](embed-service-principal.md).

Чтобы получить значение **ApplicationSecret**, сделайте следующее.

1. Войдите на [портал Azure](https://portal.azure.com).

2. В области навигации слева выберите **Все службы**, а затем — **Регистрация приложений**.

    ![Поиск приложений для регистрации](media/embed-sample-for-customers/embed-sample-for-customers-003.png)

3. Выберите приложение, для которого нужно использовать **ApplicationSecret**.

    ![Выбор приложения](media/embed-sample-for-customers/embed-sample-for-customers-0038.png)

4. Выберите **Сертификаты и секреты** в разделе **Управление**.

5. Выберите **Новые секреты клиента**.

6. Введите имя в поле **Описание** и выберите длительность. Затем выберите **Сохранить**, чтобы получить **Значение** для вашего приложения. Когда вы закроете панель **Ключи** после сохранения значения ключа, поле значения отображается только как скрытое. На этом этапе вы не можете получить значение ключа. Если вы потеряете значение ключа, потребуется создать новое на портале Azure.

    ![Значение ключа](media/embed-sample-for-customers/embed-sample-for-customers-042.png)

### <a name="tenant"></a>Клиент

Этот атрибут необходим только для типа проверки подлинности [субъект-служба](embed-service-principal.md).

Укажите в поле **tenant** идентификатор клиента Azure. Эти данные можно получить в [центре администрирования Azure AD](/onedrive/find-your-office-365-tenant-id) после входа в службу Power BI или с помощью PowerShell.

### <a name="run-the-application"></a>Запуск приложения

1. Выберите **Запуск** в **Visual Studio**.

    ![Выполнение приложения](media/embed-sample-for-customers/embed-sample-for-customers-033.png)

2. Теперь выберите **Внедрить отчет**. В зависимости от того, какое содержимое вы хотите проверить (отчеты, панели мониторинга или плитки), выберите нужный вариант в приложении.

    ![Выберите содержимое](media/embed-sample-for-customers/embed-sample-for-customers-034.png)

3. Теперь вы можете просмотреть отчет в примере приложения.

    ![Просмотр приложения](media/embed-sample-for-customers/embed-sample-for-customers-035.png)

## <a name="embed-content-within-your-application"></a>Внедрение содержимого в приложении

Несмотря на то, что шаги по внедрению содержимого выполняются с помощью [интерфейсов REST API Power BI](/rest/api/power-bi/), примеры кода, описанные в этой статье, созданы с помощью **пакета SDK для .NET**.

Чтобы внедрять содержимое для клиентов в приложении, вам нужно получить **маркер доступа** для главной учетной записи или [субъекта-службы](embed-service-principal.md) из **Azure AD**. [Маркер доступа Azure AD](get-azuread-access-token.md#access-token-for-non-power-bi-users-app-owns-data) для приложения Power BI необходимо получить, прежде чем выполнять вызовы [REST API Power BI](/rest/api/power-bi/).

Для создания клиента Power BI с помощью **маркера доступа** потребуется создать объект клиента Power BI, что позволит работать с интерфейсами [REST API Power BI](/rest/api/power-bi/). Для создания объекта клиента Power BI маркер **AccessToken** упаковывается в объект **_Microsoft.Rest.TokenCredentials_* _.

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Rest;
using Microsoft.PowerBI.Api.V2;

var tokenCredentials = new TokenCredentials(authenticationResult.AccessToken, "Bearer");

// Create a Power BI Client object. it's used to call Power BI APIs.
using (var client = new PowerBIClient(new Uri(ApiUrl), tokenCredentials))
{
    // Your code to embed items.
}
```

### <a name="get-the-content-item-you-want-to-embed"></a>Получение элемента содержимого, который нужно внедрить

Вы можете использовать объект клиента Power BI, чтобы получить ссылку на элемент, который требуется внедрить.

Ниже приведен пример кода для получения первого отчета из определенной рабочей области.

_Пример получения элемента содержимого (отчета, панели мониторинга или плитки), который вы хотите внедрить, можно найти в файле Services\EmbedService.cs в [примере приложения](https://github.com/Microsoft/PowerBI-Developer-Samples).*

```csharp
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;

// You need to provide the workspaceId where the dashboard resides.
ODataResponseListReport reports = await client.Reports.GetReportsInGroupAsync(workspaceId);

// Get the first report in the group.
Report report = reports.Value.FirstOrDefault();
```

### <a name="create-the-embed-token"></a>Создание маркера внедрения
Создайте токен внедрения, который можно использовать из API JavaScript. Существует два типа API; первая группа содержит пять API, каждый из которых создает токен внедрения для определенного элемента. Вторая группа, которая содержит только один API, создает токен, который можно использовать для внедрения нескольких элементов.

**Интерфейсы API для создания токена внедрения для определенного элемента**

Токен внедрения, созданный этими API, будет связан только с внедряемым элементом. При каждом внедрении элемента Power BI (такого как отчет, панель мониторинга или плитка) при помощи этих API необходимо создать для него новый токен внедрения.
* [Панели мониторинга: GenerateTokenInGroup](/rest/api/power-bi/embedtoken/dashboards_generatetokeningroup)
* [Наборы данных: GenerateTokenInGroup](/rest/api/power-bi/embedtoken/datasets_generatetokeningroup)
* [Отчеты: GenerateTokenForCreateInGroup](/rest/api/power-bi/embedtoken/reports_generatetokenforcreateingroup)
* [Отчеты: GenerateTokenInGroup](/rest/api/power-bi/embedtoken/reports_generatetokeningroup)
* [Плитки: GenerateTokenInGroup](/rest/api/power-bi/embedtoken/tiles_generatetokeningroup)

Примеры создания токена внедрения для отчета, панели мониторинга или плитки доступны в следующих файлах [примеров приложений](https://github.com/Microsoft/PowerBI-Developer-Samples).
* Services\EmbedService.cs
* Models\EmbedConfig.cs
* Models\TileEmbedConfig.cs

Ниже приведен пример кода для использования API при создании токена внедрения отчетов GenerateTokenInGroup.
```csharp
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;

// Generate Embed Token.
var generateTokenRequestParameters = new GenerateTokenRequest(accessLevel: "view");
EmbedToken tokenResponse = client.Reports.GenerateTokenInGroup(workspaceId, report.Id, generateTokenRequestParameters);

// Generate Embed Configuration.
var embedConfig = new EmbedConfig()
{
    EmbedToken = tokenResponse,
    EmbedUrl = report.EmbedUrl,
    Id = report.Id
};
```

**API для создания и внедрения токена для нескольких элементов**<a id="multiEmbedToken"></a>

API [создания токена](/rest/api/power-bi/embedtoken/generatetoken) внедрения создает токен, который можно использовать для внедрения нескольких элементов.

Он также допускает динамический выбор набора данных при внедрении отчета. Дополнительные сведения о таком использовании API см. в разделе [Динамическая привязка](embed-dynamic-binding.md).


Ниже приведен пример использования этого API.
 
```csharp
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;

var reports = new List<GenerateTokenRequestV2Report>()
{ 
    new GenerateTokenRequestV2Report()
    {
        AllowEdit = false,
        Id = report1.Id
    },
    new GenerateTokenRequestV2Report()
    {
        AllowEdit = true,
        Id = report2.Id
    }
};

var datasets= new List<GenerateTokenRequestV2Dataset>()
{
    new GenerateTokenRequestV2Dataset(dataset1.Id),
    new GenerateTokenRequestV2Dataset(dataset2.Id),
    new GenerateTokenRequestV2Dataset(dataset3.Id),
};

var targetWorkspaces = new List<GenerateTokenRequestV2TargetWorkspace>()
{
    new GenerateTokenRequestV2TargetWorkspace(workspace1.Id),
    new GenerateTokenRequestV2TargetWorkspace(workspace2.Id),
};

var request = new GenerateTokenRequestV2()
{
    Datasets = datasets,
    Reports = reports,
    TargetWorkspaces = targetWorkspaces,
};

var token = client.GetClient().EmbedToken.GenerateToken(request);
```

### <a name="load-an-item-using-javascript"></a>Загрузка элемента с помощью JavaScript

Чтобы загрузить отчет в элемент div веб-страницы, вы можете использовать JavaScript.

С полнофункциональным примером на основе API JavaScript вы можете ознакомиться на странице [средства "Площадка"](https://microsoft.github.io/PowerBI-JavaScript/demo). Средство "Тестовая площадка" — это очень удобный способ быстро протестировать разные примеры Power BI Embedded. Дополнительные сведения об API JavaScript вы найдете на странице [вики-сайта PowerBI-JavaScript](https://github.com/Microsoft/powerbi-javascript/wiki).

В примере используются модели **EmbedConfig** и **TileEmbedConfig** и представления отчета.

*Пример добавления представления для отчета, панели мониторинга или плитки доступен в файлах Views\Home\EmbedReport.cshtml, Views\Home\EmbedDashboard.cshtml или Views\Home\Embedtile.cshtml в [примере приложения](#embed-content-using-the-sample-application).*

```javascript
<script src="~/scripts/powerbi.js"></script>
<div id="reportContainer"></div>
<script>
    // Read embed application token from Model
    var accessToken = "@Model.EmbedToken.Token";

    // Read embed URL from Model
    var embedUrl = "@Html.Raw(Model.EmbedUrl)";

    // Read report Id from Model
    var embedReportId = "@Model.Id";

    // Get models. models contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config = {
        type: 'report',
        tokenType: models.TokenType.Embed,
        accessToken: accessToken,
        embedUrl: embedUrl,
        id: embedReportId,
        permissions: models.Permissions.All,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
</script>
```

## <a name="move-to-production"></a>Начало эксплуатации в рабочей среде

Завершив разработку приложения, вернитесь к рабочей области с емкостью.

> [!Important]
> Для перехода к рабочей среде требуется емкость. Все рабочие области, содержащие отчеты и панели мониторинга, а также содержащие наборы данных, должны быть назначены емкости.

### <a name="create-a-capacity"></a>Создание емкости

Создав емкость, вы сможете пользоваться ресурсом для клиента. Можно использовать два типа емкости.
* **Power BI Premium** — это подписка Office 356 уровня клиента, доступная в двух семействах SKU: *EM* и *P*. При внедрении содержимого Power BI это решение называется *внедрением Power BI*. Дополнительные сведения об этой подписке см. в разделе [Что такое Power BI Premium?](../../admin/service-premium-what-is.md).
* **Azure Power BI Embedded** — вы можете приобрести емкость на [портале Microsoft Azure](https://portal.azure.com). Эта подписка использует номера SKU *A*. Дополнительные сведения о создании емкости Power BI Embedded см. в статье [Создание емкости Power BI Embedded на портале Azure](azure-pbie-create-capacity.md).
> [!NOTE]
> С номерами SKU A вы не можете получить доступ к содержимому Power BI с бесплатной лицензией Power BI.

В следующей таблице описаны ресурсы и ограничения для каждого SKU. Чтобы определить, какая емкость лучше соответствует вашим потребностям, ознакомьтесь с таблицей [Какой номер SKU следует приобрести для моего сценария](./embedded-faq.md#which-solution-should-i-choose).

| Узлы емкости | Число виртуальных ядер | Серверные виртуальные ядра | ОЗУ (ГБ) | Интерфейсные виртуальные ядра | Подключения DirectQuery и активные подключения (в секунду) | Параллелизм обновления модели |
| --- | --- | --- | --- | --- | --- | --- |
| EM1/A1 | 1 | 0,5 | 2.5 | 0,5 | 3,75 % | 1 |
| EM2/A2 | 2 | 1 | 5 | 1 | 7,5 % | 2 |
| EM3/A3 | 4 | 2 | 10 | 2 | 15 | 3 |
| P1/A4 | 8 | 4 | 25 | 4 | 30 | 6 |
| P2/A5 | 16 | 8 | 50 | 8 | 60 | 12 |
| P3/A6 | 32 | 16 | 100 | 16 | 120 | 24 |
| | | | | | | |

### <a name="development-testing"></a>Тестирование в ходе разработки

Для тестирования в процессе разработки можно использовать токены внедрения пробной версии с лицензией Pro. Для внедрения в рабочей среде используйте емкость.

Число токенов внедрения пробной версии, которые можно создать в субъекте-службе или основной учетной записи Power BI, ограниченно. Используйте API [доступных компонентов](/rest/api/power-bi/availablefeatures/getavailablefeatures), чтобы просмотреть текущий объем использования сценариев внедрения в процентном соотношении. Объем использования приводится для отдельного субъекта-службы или главной учетной записи.

Если во время тестирования токены внедрения закончились, необходимо приобрести [емкость](embedded-capacity.md) Power BI Embedded или Premium. В этом случае не будет ограничения на количество создаваемых токенов.


### <a name="assign-a-workspace-to-a-capacity"></a>Назначение рабочей области для емкости

Созданной емкости можно назначить рабочую область.

Все рабочие области, которые содержат ресурсы Power BI, связанные с внедренным содержимым (включая наборы данных, отчеты и панели мониторинга), должны быть назначены емкостям. Например, если внедренный отчет и связанный с ним набор данных размещаются в разных рабочих областях, обе эти рабочие области должны быть назначены емкостям.

Чтобы назначить емкость рабочей области с помощью [субъекта-службы](embed-service-principal.md), используйте [REST API Power BI](/rest/api/power-bi/capacities/groups_assigntocapacity). Если применяется REST API Power BI, необходимо использовать [идентификатор объекта субъекта-службы](embed-service-principal.md).

Чтобы назначить емкость рабочей области с помощью **главной учетной записи**, выполните указанные ниже действия.

1. В **службе Power BI** разверните рабочие области и щелкните многоточие возле рабочей области, которую вы используете для внедрения содержимого. Затем выберите команду **Изменить рабочие области**.

    ![Изменение рабочей области](media/embed-sample-for-customers/embed-sample-for-customers-036.png)

2. Разверните элемент **Дополнительно**, затем включите параметр **Емкость** и выберите созданную емкость. Затем выберите **Сохранить**.

    ![Назначение емкости](media/embed-sample-for-customers/embed-sample-for-customers-024.png)

3. После нажатия кнопки **Сохранить** рядом с именем рабочей области должен появиться **ромб**.

    ![Рабочая область, связанная с емкостью](media/embed-sample-for-customers/embed-sample-for-customers-037.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы узнали, как внедрить содержимое Power BI в свое приложение для клиентов. Кроме того, вы можете попробовать внедрить содержимое Power BI для своей организации.

> [!div class="nextstepaction"]
>[Внедрение для организации](embed-sample-for-your-organization.md)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)