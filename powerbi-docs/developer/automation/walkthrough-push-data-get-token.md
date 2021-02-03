---
title: Получение маркера доступа для проверки подлинности в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Пошаговое руководство по отправке данных — получение маркера доступа для проверки подлинности. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: madia
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: tutorial
ms.date: 05/29/2019
ms.openlocfilehash: 8959a0ac63ff1f182bcb3544b1925529b1ad3663
ms.sourcegitcommit: 2e81649476d5cb97701f779267be59e393460097
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "99422405"
---
# <a name="step-2-get-an-authentication-access-token"></a>Шаг 2. Получение токена доступа для проверки подлинности

Эта статья описывает второй шаг процедуры [Принудительная отправка данных в набор данных Power BI](walkthrough-push-data.md).

В шаге 1 вы [зарегистрировали клиентское приложение в Azure AD](../embedded/register-app.md). На этом шаге вы получите токен доступа для проверки подлинности. Приложения Power BI интегрированы с Azure Active Directory для обеспечения безопасного входа и авторизации в приложении. Ваше приложение использует токен для проверки подлинности в Azure AD и получения доступа к ресурсам Power BI.

## <a name="get-an-authentication-access-token"></a>Получение токена доступа для проверки подлинности

Перед началом работы убедитесь, что выполнен [предыдущий шаг](../embedded/register-app.md) процедуры [Принудительная отправка данных в набор данных Power BI](walkthrough-push-data.md). 

Для этой шага требуется Visual Studio 2015 или более поздней версии.

1. В Visual Studio создайте проект **консольного приложения** на языке C#.

2. Установите [библиотеку проверки подлинности Azure AD для пакета NuGet .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.22.302111727). Этот пакет нужен приложению .NET для получения токена безопасности для проверки подлинности. 

     а. Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.

     б. Введите команду **Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.21.301221612**

     в. В файле Program.cs добавьте `using Microsoft.IdentityModel.Clients.ActiveDirectory;`.

3. Добавьте пример кода, указанный после этих действий, в файл Program.cs.

4. Замените "{ClientID}" на **идентификатор клиента**, который вы получили при регистрации приложения [в предыдущей статье](../embedded/register-app.md).

5. Запустите консольное приложение и войдите в свою учетную запись Power BI. 

   В окне консоли должна отображаться строка токена.

**Пример кода получения токена безопасности для проверки подлинности**

Добавьте этот код в Program {...}.

* Переменная токена для вызова операций: 
  
  ```csharp
  private static string token = string.Empty;
  
  static void Main(string[] args)
  {
  }
  ```
* В методе static void Main(string[] args):
  
  ```csharp
  static void Main(string[] args)
  {
    //Get an authentication access token
    token = GetToken();
  }
  ```
* Добавьте метод GetToken():

```csharp
       #region Get an authentication access token
       private static async Task<string> GetToken()
       {
           // TODO: Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.21.301221612
           // and add using Microsoft.IdentityModel.Clients.ActiveDirectory

           //The client id that Azure AD created when you registered your client app.
           string clientID = "{Client_ID}";

           //RedirectUri you used when you register your app.
           //For a client app, a redirect uri gives Azure AD more details on the application that it will authenticate.
           // You can use this redirect uri for your client app
           string redirectUri = "https://login.live.com/oauth20_desktop.srf";

           //Resource Uri for Power BI API
           string resourceUri = "https://analysis.windows.net/powerbi/api";

           //OAuth2 authority Uri
           string authorityUri = "https://login.microsoftonline.com/common/";

           //Get access token:
           // To call a Power BI REST operation, create an instance of AuthenticationContext and call AcquireToken
           // AuthenticationContext is part of the Active Directory Authentication Library NuGet package
           // To install the Active Directory Authentication Library NuGet package in Visual Studio,
           //  run "Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory" from the nuget Package Manager Console.

           // AcquireToken will acquire an Azure access token
           // Call AcquireToken to get an Azure token from Azure Active Directory token issuance endpoint
           AuthenticationContext authContext = new AuthenticationContext(authorityUri);
           var token = authContext.AcquireTokenAsync(resourceUri, clientID, new Uri(redirectUri)).Result.AccessToken;

           Console.WriteLine(token);
           Console.ReadLine();

           return token;
       }

       #endregion
```

Получив токен проверки подлинности, вы можете вызывать любые операции Power BI.

Следующая статья этой серии описывает [создание набора данных в Power BI](walkthrough-push-data-create-dataset.md).


## <a name="complete-code-listing"></a>Полный листинг кода

```csharp
using System;
using Microsoft.IdentityModel.Clients.ActiveDirectory;

namespace walkthrough_push_data
{
    class Program
    {
        private static string token = string.Empty;

        static void Main(string[] args)
        {

            //Get an authentication access token
            token = GetToken();

        }

        #region Get an authentication access token
        private static async Task<string> GetToken()
        {
            // TODO: Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.21.301221612
            // and add using Microsoft.IdentityModel.Clients.ActiveDirectory

            //The client id that Azure AD created when you registered your client app.
            string clientID = "{Client_ID}";

            //RedirectUri you used when you register your app.
            //For a client app, a redirect uri gives Azure AD more details on the application that it will authenticate.
            // You can use this redirect uri for your client app
            string redirectUri = "https://login.live.com/oauth20_desktop.srf";

            //Resource Uri for Power BI API
            string resourceUri = "https://analysis.windows.net/powerbi/api";

            //OAuth2 authority Uri
            string authorityUri = "https://login.microsoftonline.com/common/";

            //Get access token:
            // To call a Power BI REST operation, create an instance of AuthenticationContext and call AcquireToken
            // AuthenticationContext is part of the Active Directory Authentication Library NuGet package
            // To install the Active Directory Authentication Library NuGet package in Visual Studio,
            //  run "Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory" from the nuget Package Manager Console.

            // AcquireToken will acquire an Azure access token
            // Call AcquireToken to get an Azure token from Azure Active Directory token issuance endpoint
            AuthenticationContext authContext = new AuthenticationContext(authorityUri);
            var token = authContext.AcquireTokenAsync(resourceUri, clientID, new Uri(redirectUri)).Result.AccessToken;

            Console.WriteLine(token);
            Console.ReadLine();

            return token;
        }

        #endregion

    }
}
```



## <a name="next-steps"></a>Дальнейшие действия

* Следующая статья этого цикла: [Создание набора данных в Power BI](walkthrough-push-data-create-dataset.md)
* [Обзор интерфейса REST API Power BI](overview-of-power-bi-rest-api.md)  
* [REST API в Power BI](/rest/api/power-bi/)  

У вас имеются и другие вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)