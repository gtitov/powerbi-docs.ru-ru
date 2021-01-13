---
title: Проверка подлинности пользователей и получение маркера доступа Azure AD для приложения встроенной аналитики Power BI для улучшения возможностей использования бизнес-аналитики клиентами
description: Узнайте, как зарегистрировать приложение в Azure Active Directory для использования внедренного содержимого Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.date: 06/04/2019
ms.openlocfilehash: 8001dd0e15ef713fa67256a45f645b0d7a0890c0
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888450"
---
# <a name="get-an-azure-ad-access-token-for-your-power-bi-application"></a>Получение маркера доступа Azure AD для приложения Power BI

Эта статья описывает, как проверить подлинность пользователей в приложении Power BI и получить маркер доступа для использования с [REST API Power BI](/rest/api/power-bi/).

Прежде чем приложение вызовет REST API, нужно получить **маркер доступа для проверки подлинности** Azure Active Directory (Azure AD). Ваше приложение использует этот маркер, чтобы обращаться к панелям мониторинга, плиткам и отчетам Power BI. Дополнительные сведения см. в разделе [Авторизация доступа к веб-приложениям Azure Active Directory с помощью потока предоставления кода OAuth 2.0](/azure/active-directory/develop/v1-protocols-oauth-code).

Способ получения маркера доступа зависит от того, каким образом внедряется содержимое. Эта статья описывает два разных подхода.

## <a name="access-token-for-power-bi-users-user-owns-data"></a>Маркер доступа для пользователей Power BI (данные принадлежат пользователю)

В этом примере пользователи входят в Azure AD вручную, используя имя для входа, предоставленное организацией. Этот вариант используется при внедрении содержимого для пользователей, имеющих доступ к Power BI.

### <a name="get-an-azure-ad-authorization-code"></a>Получение кода авторизации Azure AD

Первый шаг при получении **токена доступа** заключается в получении кода авторизации из **Azure AD**. Создайте строку запроса с указанными ниже свойствами и выполните перенаправление в **Azure AD**.

#### <a name="authorization-code-query-string"></a>Строка запроса для кода авторизации

```csharp
var @params = new NameValueCollection
{
    //Azure AD will return an authorization code. 
    //See the Redirect class to see how "code" is used to AcquireTokenByAuthorizationCode
    {"response_type", "code"},

    //Client ID is used by the application to identify themselves to the users that they are requesting permissions from.
    //You get the client id when you register your Azure app.
    {"client_id", Properties.Settings.Default.ClientID},

    //Resource uri to the Power BI resource to be authorized
    // https://analysis.windows.net/powerbi/api
    {"resource", Properties.Settings.Default.PowerBiAPI},

    //After user authenticates, Azure AD will redirect back to the web app
    {"redirect_uri", "https://localhost:13526/Redirect"}
};
```

После создания строки запроса выполните перенаправление в **Azure AD** для получения **кода авторизации**.  Ниже приведен полный метод C# для создания строки запроса **кода авторизации** и перенаправления в **Azure AD**. После этого воспользуйтесь **кодом авторизации** для получения **маркера доступа**.

В redirect.aspx.cs выполняется вызов [AuthenticationContext.AcquireTokenByAuthorizationCode](/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenbyauthorizationcodeasync#Microsoft_IdentityModel_Clients_ActiveDirectory_AuthenticationContext_AcquireTokenByAuthorizationCodeAsync_System_String_System_Uri_Microsoft_IdentityModel_Clients_ActiveDirectory_ClientCredential_System_String_) для создания маркера.

#### <a name="get-authorization-code"></a>Получение кода авторизации

```csharp
protected void signInButton_Click(object sender, EventArgs e)
{
    //Create a query string
    //Create a sign-in NameValueCollection for query string
    var @params = new NameValueCollection
    {
        //Azure AD will return an authorization code. 
        //See the Redirect class to see how "code" is used to AcquireTokenByAuthorizationCode
        {"response_type", "code"},

        //Client ID is used by the application to identify themselves to the users that they are requesting permissions from. 
        //You get the client id when you register your Azure app.
        {"client_id", Properties.Settings.Default.ClientID},

        //Resource uri to the Power BI resource to be authorized
        // https://analysis.windows.net/powerbi/api
        {"resource", Properties.Settings.Default.PowerBiAPI},

        //After user authenticates, Azure AD will redirect back to the web app
        {"redirect_uri", "https://localhost:13526/Redirect"}
    };

    //Create sign-in query string
    var queryString = HttpUtility.ParseQueryString(string.Empty);
    queryString.Add(@params);

    //Redirect authority
    //Authority Uri is an Azure resource that takes a client id to get an Access token
    // AADAuthorityUri = https://login.microsoftonline.com/common/
    string authorityUri = Properties.Settings.Default.AADAuthorityUri;
    var authUri = String.Format("{0}?{1}", authorityUri, queryString);
    Response.Redirect(authUri);
}
```

### <a name="get-an-access-token-from-authorization-code"></a>Получение маркера доступа из кода авторизации

Когда **Azure AD** выполняет перенаправление обратно в веб-приложение с помощью **кода авторизации**, можно воспользоваться им для получения маркера доступа. Ниже приведен пример C#, который вы можете использовать на странице перенаправления и в событии `Page_Load` для default.aspx.

Вы можете извлечь пространство имен **Microsoft.IdentityModel.Clients.ActiveDirectory** из пакета NuGet [Библиотеки проверки подлинности Active Directory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="redirectaspxcs"></a>Redirect.aspx.cs

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;

protected void Page_Load(object sender, EventArgs e)
{
    //Redirect uri must match the redirect_uri used when requesting Authorization code.
    string redirectUri = String.Format("{0}Redirect", Properties.Settings.Default.RedirectUrl);
    string authorityUri = Properties.Settings.Default.AADAuthorityUri;

    // Get the auth code
    string code = Request.Params.GetValues(0)[0];

    // Get auth token from auth code
    TokenCache TC = new TokenCache();

    AuthenticationContext AC = new AuthenticationContext(authorityUri, TC);
    ClientCredential cc = new ClientCredential
        (Properties.Settings.Default.ClientID,
        Properties.Settings.Default.ClientSecret);

    AuthenticationResult AR = AC.AcquireTokenByAuthorizationCode(code, new Uri(redirectUri), cc);

    //Set Session "authResult" index string to the AuthenticationResult
    Session[_Default.authResultString] = AR;

    //Redirect back to Default.aspx
    Response.Redirect("/Default.aspx");
}
```

#### <a name="defaultaspx"></a>Default.aspx

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;

protected void Page_Load(object sender, EventArgs e)
{

    //Test for AuthenticationResult
    if (Session[authResultString] != null)
    {
        //Get the authentication result from the session
        authResult = (AuthenticationResult)Session[authResultString];

        //Show Power BI Panel
        signInStatus.Visible = true;
        signInButton.Visible = false;

        //Set user and token from authentication result
        userLabel.Text = authResult.UserInfo.DisplayableId;
        accessTokenTextbox.Text = authResult.AccessToken;
    }
}
```

## <a name="access-token-for-non-power-bi-users-app-owns-data"></a>Маркер доступа для пользователей, не работающих с Power BI (данные принадлежат приложению)

Этот подход обычно используется для приложений независимых поставщиков программного обеспечения, когда права на доступ к данным принадлежат такому приложению. Пользователи могут быть не зарегистрированы в Power BI, поэтому приложение управляет проверкой подлинности и доступом для пользователей.

### <a name="access-token-with-a-master-account"></a>Маркер доступа с главной учетной записью

Для этого подхода используется одна *главная* учетная запись пользователя Power BI Pro. Учетные данные для этой учетной записи сохраняются в приложении. Приложение выполняет проверку подлинности в Azure AD с помощью этих сохраненных учетных данных. Следующий образец кода взят из [примера с данными, принадлежащими приложению](https://github.com/guyinacube/PowerBI-Developer-Samples)

### <a name="access-token-with-service-principal"></a>Маркер доступа с субъектом-службой

Для этого подхода используется [субъект-служба](embed-service-principal.md), то есть токен **только для приложения**. Приложение выполняет проверку подлинности в Azure AD с помощью субъекта-службы. Следующий образец кода взят из [примера с данными, принадлежащими приложению](https://github.com/guyinacube/PowerBI-Developer-Samples)

#### <a name="embedservicecs"></a>EmbedService.cs

```csharp
var AuthorityURL  = "https://login.microsoftonline.com/<TenantId>/"
var ResourceURL  = "https://analysis.windows.net/powerbi/api"
var authenticationContext = new AuthenticationContext(AuthorityUrl);
       AuthenticationResult authenticationResult = null;
       if (AuthenticationType.Equals("MasterUser"))
       {
              // Authentication using master user credentials
              var credential = new UserPasswordCredential(Username, Password);
              authenticationResult = authenticationContext.AcquireTokenAsync(ResourceUrl, ApplicationId, credential).Result;
       }
       else
       {
             // Authentication using app credentials
             var credential = new ClientCredential(ApplicationId, ApplicationSecret);
             authenticationResult = await authenticationContext.AcquireTokenAsync(ResourceUrl, credential);
       }


m_tokenCredentials = new TokenCredentials(authenticationResult.AccessToken, "Bearer");
```

## <a name="troubleshoot"></a>Диагностика

Сообщение об ошибке: "AuthenticationContext" не содержит определения для "AcquireToken", и не удалось найти доступный метод расширения "AcquireToken", принимающий тип "AuthenticationContext" в качестве первого аргумента (возможно, пропущена директива using или ссылка на сборку).

   При возникновении этой ошибки попробуйте скачать [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.22.302111727).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда у вас есть маркер доступа, можно вызвать REST API Power BI, чтобы внедрить содержимое.

У вас имеются и другие вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)