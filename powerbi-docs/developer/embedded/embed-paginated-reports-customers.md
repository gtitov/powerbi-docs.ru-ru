---
title: Внедрение отчетов с разбивкой на страницы в приложение встроенной аналитики Power BI для более эффективной бизнес-аналитики для ваших клиентов
description: Узнайте, как интегрировать (внедрить) отчет Power BI с разбивкой на страницы в приложение с помощью API-интерфейсов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
ms.topic: tutorial
ms.service: powerbi
ms.subservice: powerbi-developer
ms.custom: seodec18
ms.date: 01/04/2019
ms.openlocfilehash: b9623b91555efe01817e4ffca3c6f80bd73c5243
ms.sourcegitcommit: c86ce723d5db16fb960d1731795d84f4654e4b4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "98110896"
---
# <a name="tutorial-embed-power-bi-paginated-reports-into-an-application-for-your-customers"></a>Руководство. Внедрение отчетов Power BI с разбивкой на страницы в приложение для клиентов

С помощью **Power BI Embedded в Azure** или **внедрения Power BI в Office** вы можете внедрять отчеты с разбивкой на страницы в приложение с помощью данных, принадлежащих ему. Модель **данных, принадлежащих приложению**, позволяет приложению использовать Power BI как встроенную платформу аналитики. Как **независимый поставщик программного обеспечения** или **разработчик** вы можете создавать содержимое Power BI, отображающее отчеты с разбивкой на страницы в приложении. При этом приложение будет полностью интегрированным и интерактивным, а пользователям не потребуется лицензия Power BI. Из этого руководства вы узнаете, как интегрировать отчет с разбивкой на страницы в приложение с помощью пакета SDK Power BI для .NET и API JavaScript для Power BI.

![Внедрение отчета Power BI](media/embed-paginated-reports-for-customers/embedded-paginated-report.png)

Из этого руководства вы узнаете, как выполнять следующие задачи:
> [!div class="checklist"]
> * регистрация приложения в Azure;
> * внедрение отчета Power BI с разбивкой на страницы в приложение.

## <a name="prerequisites"></a>Предварительные требования

Для работы вам понадобятся:

* [субъект-служба (маркер только для приложения)](embed-service-principal.md);
* подписка [Microsoft Azure](https://azure.microsoft.com/);
* собственная установка [клиента Azure Active Directory](create-an-azure-active-directory-tenant.md);
* По крайней мере [емкости](#create-a-capacity) A4 или P1 с включенной рабочей нагрузкой [отчетов с разбивкой на страницы](../../admin/service-admin-premium-workloads.md#paginated-reports).

Если у вас нет подписки Azure, перед началом работы [создайте бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

> [!IMPORTANT]
> * Необходимо использовать **субъект-службу**. Главный пользователь не поддерживается.
>* [Premium на пользователя (PPU)](../../admin/service-premium-per-user-faq.md) не поддерживается. Вы можете использовать PPU, чтобы поэкспериментировать с решением, но вы не сможете [перенести его в рабочую среду](move-to-production.md).
> * Источники данных, для которых требуется единый вход, не поддерживаются. Список поддерживаемых наборов данных и способов проверки их подлинности см. в статье [Поддерживаемые источники данных для отчетов с разбивкой на страницы Power BI](../../paginated-reports/paginated-reports-data-sources.md). 
> * Набор данных Power BI не поддерживается в качестве [источника данных](../../connect-data/service-get-data.md).

## <a name="set-up-your-power-bi-environment"></a>Настройка рабочей среды Power BI

Для внедрения отчета с разбивкой на страницы необходимо назначить рабочую область емкости и отправить отчет в рабочую область.

### <a name="create-an-app-workspace"></a>Создание рабочей области приложения

Поскольку для входа в приложение вы применяете [субъект-службу](embed-service-principal.md), необходимо использовать [новые рабочие области](../../collaborate-share/service-create-the-new-workspaces.md). При использовании *субъекта-службы* также необходимо быть администратором или членом рабочих областей приложения, участвующим в приложении.

### <a name="create-a-capacity"></a>Создание емкости

Прежде чем импортировать или передать отчет с разбивкой на страницы для внедрения, рабочая область, содержащая отчет, должна быть назначена по меньшей мере емкости A4 или P1. Вы можете выбрать из двух типов емкости.
* **Power BI Premium** — для внедрения отчета с разбиением на страницы требуется емкость SKU *P*. При внедрении содержимого Power BI это решение называется *внедрением Power BI*. Дополнительные сведения об этой подписке см. в разделе [Что такое Power BI Premium?](../../admin/service-premium-what-is.md).
* **Azure Power BI Embedded** — вы можете приобрести емкость на [портале Microsoft Azure](https://portal.azure.com). Эта подписка использует номера SKU *A*. Для внедрения отчетов с разбивкой на страницы требуется по крайней мере подписка *A4*. Дополнительные сведения о создании емкости Power BI Embedded см. в статье [Создание емкости Power BI Embedded на портале Azure](azure-pbie-create-capacity.md).

    >[!NOTE]
    >Недавно была выпущена новая версия Power BI Embedded, которая называется **Embedded 2-го поколения**. Embedded 2-го поколения упрощает управление внедренными емкостями и улучшает работу Power BI Embedded. Дополнительные сведения см. в разделе [Power BI Embedded 2-го поколения](power-bi-embedded-generation-2.md).

В следующей таблице описаны ресурсы и ограничения для каждого SKU. Чтобы определить, какая емкость лучше соответствует вашим потребностям, ознакомьтесь с таблицей [Какой номер SKU следует приобрести для моего сценария](./embedded-faq.md#which-solution-should-i-choose).

| Узлы емкости | Число виртуальных ядер | Серверные виртуальные ядра | ОЗУ (ГБ) | Интерфейсные виртуальные ядра | 
| --- | --- | --- | --- | --- |
| A1 с [Embedded 2-го поколения](power-bi-embedded-generation-2.md) | 1 | 0,5 | 2.5 | 0,5 |
| A2 с [Embedded 2-го поколения](power-bi-embedded-generation-2.md) | 2 | 1 | 5 | 1 |
| A3 с [Embedded 2-го поколения](power-bi-embedded-generation-2.md) | 4 | 2 | 10 | 2 |
| P1/A4 | 8 | 4 | 25 | 4 |
| P2/A5 | 16 | 8 | 50 | 8 |
| P3/A6 | 32 | 16 | 100 | 16 |
| | | | | |

### <a name="assign-an-app-workspace-to-a-capacity"></a>Назначение рабочей области приложения для емкости

Создав емкость, вы можете назначить ей рабочую область приложения.

Чтобы назначить емкость рабочей области с помощью [субъекта-службы](embed-service-principal.md), используйте [REST API Power BI](/rest/api/power-bi/capacities/groups_assigntocapacity). Если применяется REST API Power BI, необходимо использовать [идентификатор объекта субъекта-службы](embed-service-principal.md).

### <a name="create-and-upload-your-paginated-reports"></a>Создание и передача отчетов с разбивкой на страницы

Отчет с разбивкой на страницы можно создать с помощью [построителя отчетов Power BI](../../paginated-reports/paginated-reports-report-builder-power-bi.md#create-reports-in-power-bi-report-builder), а затем [передать отчет в службу](../../paginated-reports/paginated-reports-quickstart-aw.md#upload-the-report-to-the-service).

Отчеты с разбивкой на страницы можно импортировать в новые рабочие области с помощью [REST API Power BI](/rest/api/power-bi/imports/postimportingroup).

## <a name="embed-content-using-the-sample-application"></a>Внедрение содержимого с помощью примера приложения

Этот пример намеренно упрощен в целях наглядности. Вы или ваши разработчики отвечаете за защиту секретного ключа приложения.

Чтобы приступить к внедрению содержимого, используя пример приложения, выполните указанные ниже действия.

1. Скачайте [Visual Studio](https://www.visualstudio.com/) (версии 2013 или более поздней). Обязательно скачайте последнюю версию [пакета NuGet](https://www.nuget.org/profiles/powerbi).

2. Чтобы приступить к работе, скачайте [пример с данными, принадлежащими приложению](https://github.com/Microsoft/PowerBI-Developer-Samples) из GitHub.

    ![Пример приложения с данными, принадлежащими приложению](media/embed-sample-for-customers/embed-sample-for-customers-026.png)

3. Откройте файл **Web.config** из примера приложения. Здесь есть поля, которые нужно заполнить, чтобы успешно запустить приложение. Выберите значение **ServicePrincipal** для поля **AuthenticationType**.

    Заполните следующие поля:
    * [applicationId](#application-id)
    * [workspaceId](#workspace-id)
    * [reportId](#report-id)
    * [applicationsecret](#application-secret)
    * [tenant](#tenant)

    > [!Note]
    > По умолчанию в этом примере поле **AuthenticationType** имеет значение MasterUser. Убедитесь, что вы изменили его на **ServicePrincipal**. 


    ![Файл веб-конфигурации](media/embed-sample-for-customers/embed-sample-for-customers-030.png)

### <a name="application-id"></a>Идентификатор приложения

Укажите в поле **applicationId** значение **идентификатора приложения** из **Azure**. Поле **applicationId** используется приложением для его идентификации для пользователей, у которых запрашиваются разрешения.

Чтобы получить значение **applicationId**, сделайте следующее.

1. Войдите на [портал Azure](https://portal.azure.com).

2. В области навигации слева выберите **Все службы** и выполните поиск пункта **Регистрация приложений**.

    ![Поиск приложений для регистрации](media/embed-paginated-reports-for-customers/app-registration.png)

3. Выберите приложение, для которого требуется **applicationId**.

    ![Снимок экрана: отображаемые имена приложений с одним выбранным приложением, для которого требуется идентификатор приложения.](media/embed-paginated-reports-for-customers/display-name.png)

4. В поле **Идентификатор приложения** указан GUID. Используйте этот **идентификатор приложения** как значение параметра **applicationId** приложения.

    ![applicationId](media/embed-paginated-reports-for-customers/application-id.png)

### <a name="workspace-id"></a>Идентификатор рабочей области

Укажите в поле **workspaceId** GUID рабочей области (группы) приложения из Power BI. Эти данные можно получить из URL-адреса после входа в службу Power BI или с помощью PowerShell.

URL-адрес <br>

![workspaceId](media/embed-paginated-reports-for-customers/groups-red-url.png)

PowerShell <br>

```powershell
Get-PowerBIworkspace -name "Paginated Report Embed"
```

   ![workspaceId из PowerShell](media/embed-paginated-reports-for-customers/powershell.png)

### <a name="report-id"></a>Идентификатор отчета

Укажите в поле **reportId** значение GUID отчета из Power BI. Эти данные можно получить из URL-адреса после входа в службу Power BI или с помощью PowerShell.

URL-адрес<br>

![reportId](media/embed-paginated-reports-for-customers/rdl-report-url.png)

PowerShell <br>

```powershell
Get-PowerBIworkspace -name "Paginated Report Embed" | Get-PowerBIReport
```

![reportId из PowerShell](media/embed-paginated-reports-for-customers/powershell-report-id.png)

### <a name="application-secret"></a>Секрет приложения

Заполните сведения **ApplicationID** из раздела **Ключи** раздела **Регистрация приложений** в **Azure**.

Чтобы получить значение **ApplicationSecret**, сделайте следующее.

1. Войдите на [портал Azure](https://portal.azure.com).

2. В области навигации слева выберите **Все службы** и выполните поиск пункта **Регистрация приложений**.

    ![Поиск приложений для регистрации](media/embed-paginated-reports-for-customers/app-registration.png)

3. Выберите приложение, для которого нужно использовать **ApplicationSecret**.

    ![Снимок экрана: отображаемые имена приложений с одним выбранным приложением, для которого требуется секрет приложения.](media/embed-paginated-reports-for-customers/display-name-2.png)

4. Выберите **Сертификаты и секреты** в разделе **Управление**.

5. Выберите **Новые секреты клиента**.

6. Введите имя в поле **Описание** и выберите длительность. Затем выберите **Сохранить**, чтобы получить **Значение** для вашего приложения. Когда вы закроете панель **Ключи** после сохранения значения ключа, поле значения отображается только как скрытое. На этом этапе вы не можете получить значение ключа. Если вы потеряете значение ключа, потребуется создать новое на портале Azure.

    ![Значение ключа](media/embed-paginated-reports-for-customers/client-secret.png)

### <a name="tenant"></a>Клиент

Укажите в поле **tenant** идентификатор клиента Azure. Эти данные можно получить в [центре администрирования Azure AD](/onedrive/find-your-office-365-tenant-id) после входа в службу Power BI или с помощью PowerShell.

### <a name="run-the-application"></a>Запуск приложения

1. Выберите **Запуск** в **Visual Studio**.

    ![Выполнение приложения](media/embed-sample-for-customers/embed-sample-for-customers-033.png)

2. Теперь выберите **Внедрить отчет**.

    ![Выберите содержимое](media/embed-sample-for-customers/embed-sample-for-customers-034.png)

3. Теперь вы можете просмотреть отчет в примере приложения.

    ![Просмотр приложения](media/embed-paginated-reports-for-customers/embedded-paginated-report.png)

## <a name="embed-power-bi-paginated-reports-within-your-application"></a>Внедрение отчетов Power BI с разбивкой на страницы в приложении

Несмотря на то, что шаги по внедрению отчетов Power BI с разбивкой на страницы выполняются с помощью [REST API Power BI](/rest/api/power-bi/), примеры кода, описанные в этой статье, созданы с помощью **пакета SDK для .NET**.

При внедрении отчетов Power BI с разбивкой на страницы для ваших клиентов в приложении в **Azure AD** необходимо иметь [субъект-службу](embed-service-principal.md) и получить [маркер доступа Azure AD](get-azuread-access-token.md#access-token-for-non-power-bi-users-app-owns-data) для приложения Power BI, прежде чем выполнять вызовы к [интерфейсам REST API Power BI](/rest/api/power-bi/).

Для создания клиента Power BI с помощью **маркера доступа** создайте объект клиента Power BI, что позволит работать с интерфейсами [REST API Power BI](/rest/api/power-bi/). Для создания объекта клиента Power BI маркер **AccessToken** упаковывается в объект **_Microsoft.Rest.TokenCredentials_* _.

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

### <a name="get-the-paginated-report-you-want-to-embed"></a>Получение отчета с разбивкой на страницы, который необходимо внедрить

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

Создайте маркер внедрения, который можно использовать из API JavaScript. Чтобы создать маркер внедрения для внедрения отчетов Power BI с разбивкой на страницы, используйте API [Reports GenerateTokenInGroup](/rest/api/power-bi/embedtoken/reports_generatetokeningroup).

Пример создания токена внедрения можно найти в файле *Services\EmbedService.cs* в [примере приложения](https://github.com/Microsoft/PowerBI-Developer-Samples).

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

### <a name="load-an-item-using-javascript"></a>Загрузка элемента с помощью JavaScript

Чтобы загрузить отчет с разбивкой на страницы в элемент div веб-страницы, можно использовать JavaScript.

С полнофункциональным примером на основе API JavaScript вы можете ознакомиться на странице [средства "Площадка"](https://microsoft.github.io/PowerBI-JavaScript/demo). Средство "Тестовая площадка" — это очень удобный способ быстро протестировать разные примеры Power BI Embedded. Дополнительные сведения об API JavaScript вы найдете на странице [вики-сайта PowerBI-JavaScript](https://github.com/Microsoft/powerbi-javascript/wiki).

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы узнали, как внедрить отчет с разбивкой на страницы Power BI в свое приложение для клиентов. Кроме того, вы можете попробовать внедрить содержимое Power BI для своих клиентов или организации.

> [!div class="nextstepaction"]
>[Внедрение содержимого для клиентов](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Внедрение содержимого для организации](embed-sample-for-your-organization.md)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)