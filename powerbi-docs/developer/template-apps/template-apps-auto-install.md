---
title: Автоматизация настройки установки приложения-шаблона для клиентов
description: Сведения об автоматизации настройки установки приложения-шаблона.
author: paulinbar
ms.author: painbar
ms.topic: conceptual
ms.service: powerbi
ms.subservice: powerbi-developer
ms.date: 11/23/2020
ms.openlocfilehash: ca5db6ed7a07d5a6fb10133285378e8318527464
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96386099"
---
# <a name="automated-configuration-of-a-template-app-installation"></a>Автоматическая настройка установки приложения-шаблона

Приложения-шаблоны — это отличный способ начать получать ценную информацию из своих данных. Приложения-шаблоны позволяют сделать это быстро и просто, обеспечивая подключение к данным и предоставляя готовые отчеты, которые затем можно настроить, если это потребуется.

Клиенты не всегда знают, как настроить подключение к своим данным, а необходимость предоставлять эти сведения при установке приложения-шаблона может оказаться для них проблематичным.

Если вы являетесь поставщиком служб данных и создали приложение-шаблон, чтобы помочь своим клиентам начать работу с данными в своей службе, можно упростить установку приложения-шаблона, автоматизировав настройку его параметров. Когда клиент входит на портал, он переходит по специальной ссылке, которую вы подготовили. При этом запускается служба автоматизации, которая собирает необходимые сведения, предварительно настраивает параметры приложения-шаблона и перенаправляет клиента в учетную запись Power BI, где можно установить приложение. Все, что нужно сделать, — это нажать "Установить", пройти проверку подлинности в источнике данных, и все готово! 

Этот пользовательский интерфейс показан ниже.

![Иллюстрация автоматической установки приложения для пользователя.](media/template-apps-auto-install/high-level-flow.png)

В этой статье описывается базовый порядок действий, предварительные требования и основные этапы и API, необходимые для автоматизации настройки установки приложения-шаблона. Тем не менее, если вы предпочитаете быстро начать работу, можно перейти к [учебнику](template-apps-auto-install-tutorial.md), где вы автоматизируете настройку установки приложения-шаблона с помощью простого примера подготовленного приложения, использующего функцию Azure.

## <a name="basic-flow"></a>Базовый поток действий

Ниже приведена основная последовательность автоматизации настройки установки приложения-шаблона.

1. Пользователь входит на портал ISV и щелкает ссылку. Инициируется автоматический поток. На этом этапе портал ISV подготавливает конфигурацию пользователя.

2. ISV получает маркер **только для приложения** на основе [субъекта-службы (маркера только для приложения)](../embedded/embed-service-principal.md), который зарегистрирован в клиенте ISV.

3. С помощью [REST API Power BI](https://docs.microsoft.com/rest/api/power-bi/) независимый поставщик программного обеспечения создает **билет установки**, который содержит конфигурацию параметров пользователя, подготовленную поставщиком программного обеспечения.

4. ISV перенаправляет пользователя в Power BI с помощью метода перенаправления ```POST```, содержащего билет установки.

5. Пользователь перенаправляется в учетную запись Power BI с билетом установки и предлагает установить приложение-шаблон. Когда пользователь нажимает кнопку "Установить", выполняется установка приложения-шаблона.

>[!Note]
>Несмотря на то, что значения параметров настраиваются независимым поставщиком программного обеспечения при создании билета установки, учетные данные, связанные с источником данных, предоставляются пользователем на заключительных этапах установки. Это исключает их передачу третьим сторонам, обеспечивая безопасное подключение между пользователем и источниками данных приложения-шаблона.

## <a name="prerequisites"></a>Предварительные требования

Чтобы обеспечить установку приложения-шаблона в полностью автоматическом режиме, требуются следующие необходимые компоненты.

* **Лицензия Power BI Pro**. Если вы не зарегистрированы в Power BI Pro, [зарегистрируйтесь для получения бесплатной пробной версии](https://powerbi.microsoft.com/pricing/), прежде чем начать.

* Собственная установка **клиента Azure Active Directory**. Инструкции по настройке см. в разделе [Создание клиента Azure Active Directory](https://docs.microsoft.com/power-bi/developer/embedded/create-an-azure-active-directory-tenant).

* **Субъект-служба (маркер только для приложения)** , зарегистрированная в указанном выше клиенте. Подробнее см. в статье [Внедрение содержимого Power BI с помощью субъект-службы и секрета приложения](https://docs.microsoft.com/power-bi/developer/embedded/embed-service-principal). Обязательно зарегистрируйте приложение в качестве **серверного веб-приложения**. чтобы создать секрет приложения. В этом процессе необходимо сохранить *идентификатор приложения* (идентификатор клиента) и *секрет приложения* (секрет клиента) для последующих шагов.

* **Параметризованное приложение-шаблон**, готовое к установке. Приложение-шаблон должно быть создано в том же клиенте, в котором вы регистрируете приложение в Azure Active Directory (Azure AD). Дополнительные сведения см. в [советах по работе с приложениями-шаблонами](https://docs.microsoft.com/power-bi/connect-data/service-template-apps-tips.md) или в статье [Создание приложений-шаблонов в Power BI](https://docs.microsoft.com/power-bi/connect-data/service-template-apps-create). В приложении-шаблоне необходимо отметить следующие сведения для следующих шагов:
     * *Идентификатор приложения*, *ключ пакета* и *идентификатор владельца*, поскольку они отображаются в URL-адресе установки в конце процесса [Определение свойств приложения-шаблона](../../connect-data/service-template-apps-create.md#define-the-properties-of-the-template-app) при создании приложения. Вы также можете получить эту же ссылку, щелкнув **Получить ссылку** в разделе [Управление выпусками](../../connect-data/service-template-apps-create.md#manage-the-template-app-release) приложения-шаблона.

    * *Имена параметров*, как они определены в наборе данных приложения-шаблона. В именах параметров используются строки, учитывающие регистр. Их также можно получить на вкладке **Настройки параметров** при [определении свойств приложения-шаблона](../../connect-data/service-template-apps-create.md#define-the-properties-of-the-template-app) или из параметров набора данных в Power BI.

    >[!NOTE]
    >Вы можете протестировать предварительно настроенное приложение в приложении-шаблоне, если последнее готово к установке, даже если оно еще не открыто в AppSource. Однако, чтобы пользователи за пределами клиента могли использовать приложение с автоматической установки для установки приложения-шаблона, последний должен быть общедоступным в [Marketplace для приложений Power BI](https://app.powerbi.com/getdata/services). Поэтому перед распространением приложения-шаблона с помощью создаваемого приложения с автоматической установкой обязательно опубликуйте его в [центре партнеров](https://docs.microsoft.com/azure/marketplace/partner-center-portal/create-power-bi-app-offer).

## <a name="main-steps-and-apis"></a>Основные шаги и API

Основные шаги по автоматизации настройки установки приложения-шаблона и необходимые API описаны в последующих разделах. Несмотря на то, что большинство действий выполняются с помощью [REST API Power BI](https://docs.microsoft.com/rest/api/power-bi/), приведенные ниже примеры кода выполняются с помощью **пакета SDK для .NET**.

## <a name="step-1-create-a-power-bi-client-object"></a>Шаг 1. Создание клиентского объекта Power BI 

Для использования REST API Power BI необходимо получить **маркер доступа** для [субъекта-службы](../embedded/embed-service-principal.md) от **Azure AD**. [Маркер доступа Azure AD](../embedded/get-azuread-access-token.md#access-token-for-non-power-bi-users-app-owns-data) для приложения Power BI необходимо получить, прежде чем выполнять вызовы [REST API Power BI](https://docs.microsoft.com/rest/api/power-bi/).
Для создания клиента Power BI с помощью **маркера доступа** потребуется создать объект клиента Power BI, что позволит работать с интерфейсами [REST API Power BI](https://docs.microsoft.com/rest/api/power-bi/). Для создания объекта клиента Power BI маркер **AccessToken** упаковывается в объект **_Microsoft.Rest.TokenCredentials_* _.

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Rest;
using Microsoft.PowerBI.Api.V2;

var tokenCredentials = new TokenCredentials(authenticationResult.AccessToken, "Bearer");

// Create a Power BI Client object. it's used to call Power BI APIs.
using (var client = new PowerBIClient(new Uri(ApiUrl), tokenCredentials))
{
    // Your code to goes here.
}
```

## <a name="step-2-create-an-install-ticket"></a>Шаг 2. Создание билета установки

Создайте билет установки, который будет использоваться для перенаправления пользователей в Power BI. API, используемый для этой операции, — это API-интерфейс _ *CreateInstallTicket**.
* [Приложения-шаблоны CreateInstallTicket](https://docs.microsoft.com/rest/api/power-bi/templateapps/createinstallticket)

Пример создания билета установки для установки и настройки приложения-шаблона см. в файле [InstallTemplateApp/InstallAppFunction.cs](https://github.com/microsoft/Template-apps-examples/blob/master/Developer%20Samples/Automated%20Install%20Azure%20Function/InstallTemplateAppSample/InstallTemplateApp/InstallAppFunction.cs) в [примере приложения](https://github.com/microsoft/Template-apps-examples/tree/master/Developer%20Samples/Automated%20Install%20Azure%20Function/InstallTemplateAppSample).


Ниже приведен пример кода использования *CreateInstallTicket* REST API приложения-шаблона.
```csharp
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;

// Create Install Ticket Request.
InstallTicket ticketResponse = null;
var request = new CreateInstallTicketRequest()
{
    InstallDetails = new List<TemplateAppInstallDetails>()
    {
        new TemplateAppInstallDetails()
        {
            AppId = Guid.Parse(AppId),
            PackageKey = PackageKey,
            OwnerTenantId = Guid.Parse(OwnerId),
            Config = new TemplateAppConfigurationRequest()
            {
                Configuration = Parameters
                                    .GroupBy(p => p.Name)
                                    .ToDictionary(k => k.Key, k => k.Select(p => p.Value).Single())
            }
        }
    }
};

// Issue the request to the REST API using .NET SDK
InstallTicket ticketResponse = await client.TemplateApps.CreateInstallTicketAsync(request);
```

## <a name="step-3-redirect-users-to-power-bi-with-the-ticket"></a>Шаг 3. Перенаправление пользователей в Power BI с помощью билета

После создания билета установки его можно использовать для перенаправления пользователей в Power BI, чтобы продолжить установку и настройку приложения-шаблона. Для этого используется перенаправление метода ```POST``` в URL-адрес установки приложения-шаблона с билетом установки в тексте запроса.

Существуют различные задокументированные методы выполнения перенаправления с помощью запросов ```POST```. Выбор того или иного метода зависит от сценария и от того, как пользователи взаимодействуют с порталом или службой.

Простой пример, который в основном используется для тестирования, использует форму со скрытым полем, которая автоматически отправляет себя при загрузке.

```javascript
<html>
    <body onload='document.forms["form"].submit()'>
        <!-- form method is POST and action is the app install URL -->
        <form name='form' action='https://app.powerbi.com/....' method='post' enctype='application/json'>
            <!-- value should be the new install ticket -->
            <input type='hidden' name='ticket' value='H4sI....AAA='>
        </form>
    </body>
</html>
```

Ниже приведен пример ответа [примера приложения](https://github.com/microsoft/Template-apps-examples/tree/master/Developer%20Samples/Automated%20Install%20Azure%20Function/InstallTemplateAppSample), который содержит билет установки и автоматически перенаправляет пользователей в Power BI. Ответ для этой функции Azure фактически является той же автоматически отправляемой формой, которая отображается в примере HTML выше.

```csharp
...
    return new ContentResult() { Content = RedirectWithData(redirectUrl, ticket.Ticket), ContentType = "text/html" };
}

...

public static string RedirectWithData(string url, string ticket)
{
    StringBuilder s = new StringBuilder();
    s.Append("<html>");
    s.AppendFormat("<body onload='document.forms[\"form\"].submit()'>");
    s.AppendFormat("<form name='form' action='{0}' method='post' enctype='application/json'>", url);
    s.AppendFormat("<input type='hidden' name='ticket' value='{0}' />", ticket);
    s.Append("</form></body></html>");
    return s.ToString();
}
```

>[!Note]
>Хотя существуют различные методы использования перенаправлений обозревателя ```POST```, всегда следует использовать наиболее безопасный метод, который зависит от потребностей службы и ограничений. Помните, что некоторые формы небезопасного перенаправления могут повлечь за собой проблемы с безопасностью для пользователей или служб.

## <a name="step-4-move-your-automation-to-production"></a>Шаг 4. Перемещение автоматизации в рабочую среду

Когда подготовленная автоматизация готова, обязательно переместите ее в рабочую среду.

## <a name="next-steps"></a>Следующие шаги

* Ознакомьтесь с [руководством](template-apps-auto-install-tutorial.md), в котором используется простая функция Azure для автоматизации настройки установки приложения-шаблона.

* Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
