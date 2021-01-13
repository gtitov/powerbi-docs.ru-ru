---
title: Регистрация приложения для внедрения содержимого Power BI в приложение встроенной аналитики Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Узнайте, как зарегистрировать приложение в Azure Active Directory для использования внедренного содержимого Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: nishalit
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.date: 04/02/2019
ms.openlocfilehash: c30b8f7ebe403e38fa59fa248aacc4b3086bf9ed
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97885874"
---
# <a name="register-an-azure-ad-application-to-use-with-power-bi"></a>Регистрация приложения Azure AD для использования с Power BI

Чтобы использовать встроенную аналитику Power BI, необходимо зарегистрировать приложение Azure Active Directory (Azure AD) в Azure. Приложение Azure AD задает разрешения ресурсам REST Power BI, а также предоставляет доступ к [API-интерфейсам REST Power BI](/rest/api/power-bi/).

## <a name="determine-your-embedding-solution"></a>Определение решения внедрения

Перед регистрацией приложения определите, какие из следующих решений являются для вас оптимальными.

* Внедрение для клиентов
* Внедрение для организации

### <a name="embed-for-your-customers"></a>Внедрение для клиентов

Если вы планируете создать приложение, предназначенное для клиентов, используйте решение [Внедрение для клиентов](embed-sample-for-customers.md), также известное как *данные приложения*. Для работы с приложением пользователям не потребуется входить в Power BI, им также не нужна лицензия Power BI. Приложение будет использовать один из следующих методов для проверки подлинности в Power BI.

* Учетная запись **главного пользователя** (лицензия Power BI Pro, используемая для входа в Power BI)

* [Субъект-служба](embed-service-principal.md)

Решение "Внедрение для клиентов" обычно используется независимыми поставщиками программного обеспечения (ISV) и разработчиками, создающими приложения для третьих сторон.

### <a name="embed-for-your-organization"></a>Внедрение для организации

Если вы планируете создать приложение, требующее от пользователей использовать свои учетные данные для проверки подлинности в Power BI, используйте решение [Внедрение для организации](embed-sample-for-your-organization.md), также известное как *данные пользователя*.

Решение "Внедрение для организации" обычно используется предприятиями и крупными организациями и предназначено для внутренних пользователей.

## <a name="register-an-azure-ad-app"></a>Регистрация приложения Azure AD

Проще всего зарегистрировать приложение Azure AD с помощью [средства настройки внедрения Power BI](https://app.powerbi.com/embedsetup). Этот инструмент предлагает быстрый процесс регистрации для обоих решений внедрения с помощью простого графического интерфейса.

Если вы создаете приложение *Внедрение для организации* и хотите получить больший контроль над приложением Azure AD, можно зарегистрировать его вручную на портале Azure.

> [!IMPORTANT]
> Для регистрации приложения Power BI вам потребуется [клиент Azure Active Directory и пользователь организации](create-an-azure-active-directory-tenant.md).

# <a name="embed-for-your-customers"></a>[Внедрение для клиентов](#tab/customers)

Здесь приведены действия по регистрации приложения Azure AD для решения Power BI [Внедрение для клиентов](embed-sample-for-customers.md).

[!INCLUDE[registration tool step 1](../../includes/register-tool-step-1.md)]

2. В разделе *Выбор решения внедрения* выберите **Внедрение для клиентов**.

[!INCLUDE[registration tool step 3](../../includes/register-tool-step-3.md)]

4. На этапе *Шаг 2. Регистрация приложения* заполните следующие поля.

    * **Имя приложения**. Задайте приложению имя.

    * **Доступ к API** Выберите API-интерфейсы Power BI (также называемые областями), которые требуются приложению. Для выбора всех API-интерфейсов можно использовать параметр *Выбрать все*. Дополнительные сведения о разрешениях на доступ к Power BI см. в статье [Разрешения и согласие для конечной точки платформы удостоверений Майкрософт](/azure/active-directory/develop/v2-permissions-and-consent).

5. Выберите **Зарегистрировать**.

    **Идентификатор приложения** Azure AD отображается в поле *Сводка*. Скопируйте это значение для последующего использования.

[!INCLUDE[registration tool steps 6-7](../../includes/register-tool-steps-6-7.md)]

8. На этапе *Шаг 5. Предоставление разрешений* выберите **Предоставить разрешения**, а затем во всплывающем окне выберите **Принять**. Приложение Azure AD получит доступ к выбранным вами API-интерфейсам (также известным как области) под учетными данными выполнившего вход пользователя. Этот пользователь также известен как **главный пользователь**.

9. (Необязательно) Если вы создали рабочую область Power BI и отправили в нее содержимое с помощью этого средства, можно выбрать **Скачать пример приложения**. Обязательно скопируйте все данные в поле *Сводка*.

[!INCLUDE[registration tool note](../../includes/register-tool-note.md)]

# <a name="embed-for-your-organization"></a>[Внедрение для организации](#tab/organization)

Здесь приведены действия по регистрации приложения Azure AD для решения Power BI [Внедрение для организации](embed-sample-for-your-organization.md).

[!INCLUDE[registration tool step 1](../../includes/register-tool-step-1.md)]

2. В разделе *Выбор решения внедрения* выберите **Внедрение для организации**.

[!INCLUDE[registration tool step 3](../../includes/register-tool-step-3.md)]

4. На этапе *Шаг 2. Регистрация приложения* заполните следующие поля.

    * **Имя приложения**. Задайте приложению имя.

    * **URL-адрес домашней страницы** Введите URL-адрес домашней страницы.

    * **URL-адрес перенаправления** После регистрации пользователи вашего приложения будут перенаправляться на этот адрес, а приложение получит код проверки подлинности из Azure. Выберите один из следующих вариантов:

        * **Использовать URL-адрес по умолчанию** Этот параметр автоматически создаст и скачает пример приложения встроенной аналитики. URL-адрес по умолчанию — http://localhost:13526/.

        * **Использовать настраиваемый URL-адрес** Выберите этот параметр, если у вас уже есть приложение встроенной аналитики и вы знаете, что хотите использовать в качестве URL-адреса перенаправления.

    * **Доступ к API** Выберите API-интерфейсы Power BI (также называемые областями), которые требуются приложению. Для выбора всех API-интерфейсов можно использовать параметр *Выбрать все*. Дополнительные сведения о разрешениях на доступ к Power BI см. в статье [Разрешения и согласие для конечной точки платформы удостоверений Майкрософт](/azure/active-directory/develop/v2-permissions-and-consent).

5. Выберите **Зарегистрировать**.

    Значения **Идентификатор приложения** и **Секрет приложения** для приложения Azure AD отображаются в поле *Сводка*. Скопируйте эти значения для последующего использования.

[!INCLUDE[registration tool steps 6-7](../../includes/register-tool-steps-6-7.md)]

8. (Необязательно) Если вы создали рабочую область Power BI и отправили в нее содержимое с помощью этого средства, можно выбрать **Скачать пример приложения**. Обязательно скопируйте все данные в поле *Сводка*.

[!INCLUDE[registration tool note](../../includes/register-tool-note.md)]

# <a name="manual-registration"></a>[Регистрация вручную](#tab/manual)

Используйте регистрацию приложений в Azure AD вручную, только если вы создаете одно из следующих решений:

* *Внедрение приложения для организации*.

* *Внедрение приложения для клиентов* с *субъектом-службой*.

    >[!NOTE]
    >Если выбрать этот параметр, после регистрации приложения Azure AD необходимо [добавить в него разрешения Power BI](#change-your-azure-ad-apps-permissions).

Дополнительные сведения о регистрации приложений в Azure Active Directory см. в [этой статье](/azure/active-directory/develop/quickstart-v2-register-an-app).

1. Войдите на [портал Azure](https://portal.azure.com).

2. Выберите клиент Azure AD, щелкнув свою учетную запись в правом верхнем углу страницы.

3. Щелкните **Регистрация приложений**. Если этот параметр не отображается, найдите его.
 
4. В разделе *Регистрация приложений* выберите **Новая регистрация**.

5. Заполните следующие поля:

    * **Имя**. Задайте приложению имя.

    * **Поддерживаемый тип учетной записи**. Выберите, кто может использовать приложение.

6. (Необязательно) В поле **URI перенаправления** добавьте URL-адрес перенаправления.

7. Выберите **Зарегистрировать**. После регистрации приложения вы будете направлены на страницу обзора вашего приложения, где можно получить *идентификатор приложения*.

---

## <a name="change-your-azure-ad-apps-permissions"></a>Изменение разрешений приложения Azure AD

После регистрации приложения можно изменить его разрешения. Изменения разрешений можно вносить программным способом или на портале Azure.

>[!NOTE]
>Разрешения для приложений Azure AD применимы только к решениям *внедрения приложения для клиентов* с методом проверки подлинности с помощью *основного пользователя*.

# <a name="azure"></a>[Azure](#tab/Azure)

На портале Azure можно просмотреть приложение и внести изменения в его разрешения.

1. Войдите на [портал Azure](https://portal.azure.com).

2. Выберите клиент Azure AD, щелкнув свою учетную запись в правом верхнем углу страницы.

3. Щелкните **Регистрация приложений**. Если этот параметр не отображается, найдите его.

4. На вкладке **Собственные приложения** выберите свое приложение. Приложение откроется на вкладке *Обзор*, где можно просмотреть *идентификатор приложения*.

5. Откройте вкладку **Разрешения API**.

6. Для добавления разрешений выполните следующие действия.

    1. Выберите **Добавить разрешение**, а затем выберите **Служба Power BI**.

    2. Выберите **Делегированные разрешения** и добавьте или удалите нужные вам разрешения.

    3. Когда все будет готово, нажмите кнопку **Добавить разрешения**, чтобы сохранить изменения.

7. Чтобы удалить разрешение, выполните следующие действия.

    1. Нажмите кнопку с многоточием (...) справа от разрешения.
    
    2. Выберите **Удалить разрешение**.
    
    3. Во всплывающем окне *Удаление разрешения* выберите **Да, удалить**.

# <a name="http"></a>[HTTP](#tab/HTTP)

Чтобы изменить разрешения приложения Azure AD программным способом, необходимо получить в клиенте существующие субъекты-службы (пользователей). Сведения о том, как это сделать, см. в статье [Тип ресурса servicePrincipal](/graph/api/resources/serviceprincipal).

1. Чтобы получить все субъекты-службы в клиенте, вызовите API `Get servicePrincipal` без `{ID}`.

2. Проверьте наличие субъекта-службы, задав в качестве значения свойства `appId` *идентификатор приложения*.

    ```json
    Post https://graph.microsoft.com/v1.0/servicePrincipals HTTP/1.1
    Authorization: Bearer ey..qw
    Content-Type: application/json
    {
    "accountEnabled" : true,
    "appId" : "{App_Client_ID}",
    "displayName" : "{App_DisplayName}"
    }
    ```

    >[!NOTE]
    >Аргумент `displayName` является необязательным.

3. Предоставьте Power BI разрешения для приложения, назначив параметру `consentType` одно из следующих значений.

    * Значение `AllPrincipals` может использовать только администратор Power BI для предоставления разрешений от имени всех пользователей в клиенте.

    * Значение `Principal` используется для предоставления разрешений от имени определенного пользователя. Если вы используете этот параметр, добавьте в текст запроса свойство `principalId={User_ObjectId}`.

     ```json
     Post https://graph.microsoft.com/v1.0/OAuth2PermissionGrants HTTP/1.1
     Authorization: Bearer ey..qw
     Content-Type: application/json
     {
     "clientId":"{Service_Plan_ID}",
     "consentType":"AllPrincipals",
     "resourceId":"c78a3685-1ce7-52cd-95f7-dc5aea8ec98e",
     "scope":"Dataset.ReadWrite.All Dashboard.Read.All Report.Read.All Group.Read Group.Read.All Content.Create Metadata.View_Any Dataset.Read.All Data.Alter_Any",
     "expiryTime":"2018-03-29T14:35:32.4943409+03:00",
     "startTime":"2017-03-29T14:35:32.4933413+03:00"
     }
     ```

    >[!NOTE]
    >* Если вы используете **главного пользователя**, то, чтобы не получать запрос на согласие от Azure AD, необходимо предоставить разрешения главной учетной записи.
    >* Используемый `resourceId` *c78a3685-1ce7-52cd-95f7-dc5aea8ec98e* не является универсальным, а зависит от клиента. Это значение — *идентификатор объекта* приложения *Служба Power BI* в Azure AD. Чтобы получить это значение на портале Azure, последовательно выберите [Корпоративные приложения > Все приложения](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps) и выполните поиск *службы Power BI*.

4. Предоставьте приложению разрешения на доступ к Azure AD, задав значение параметру `consentType`.

    ```json
    Post https://graph.microsoft.com/v1.0/OAuth2PermissionGrants HTTP/1.1
    Authorization: Bearer ey..qw
    Content-Type: application/json
    {
    "clientId":"{Service_Plan_ID}",
    "consentType":"AllPrincipals",
    "resourceId":"61e57743-d5cf-41ba-bd1a-2b381390a3f1",
    "scope":"User.Read Directory.AccessAsUser.All",
    "expiryTime":"2018-03-29T14:35:32.4943409+03:00",
    "startTime":"2017-03-29T14:35:32.4933413+03:00"
    }
    ```

# <a name="c"></a>[C#](#tab/CSharp)

Вы можете также изменить разрешения приложения Azure AD с помощью C#. Дополнительные сведения см. в разделе об API [oAuth2PermissionGrant](https://docs.microsoft.com/graph/api/oauth2permissiongrant-get). Этот метод может быть полезен, если вы собираетесь автоматизировать некоторые процессы.

Дополнительные сведения об HTTP-запросах см. на [вкладке HTTP](register-app.md?tabs=customers%2CHTTP#change-your-azure-ad-apps-permissions).

```csharp
var graphClient = GetGraphClient();

currentState.createdApp = await graphClient.Applications
    .Request()
    .AddAsync(application);

System.Threading.Thread.Sleep(2000);

var passwordCredential = new PasswordCredential
{
    DisplayName = "Client Secret Created in C#"
};

currentState.createdSecret = await graphClient.Applications[currentState.createdApp.Id]
    .AddPassword(passwordCredential)
    .Request()
    .PostAsync();

var servicePrincipal = new ServicePrincipal
{
    AppId = currentState.createdApp.AppId
};

currentState.createdServicePrincipal = await graphClient.ServicePrincipals
    .Request()
    .AddAsync(servicePrincipal);

GraphServiceClient graphClient = new GraphServiceClient(authProvider);

// Use oAuth2PermissionGrant to change permissions
var oAuth2PermissionGrant = await graphClient.Oauth2PermissionGrants["{id}"]
               .Request()
               .GetAsync();
```

---

## <a name="next-steps"></a>Дальнейшие действия

>[!div class="nextstepaction"]
>[Получение маркера доступа Azure AD для приложения Power BI](get-azuread-access-token.md)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)