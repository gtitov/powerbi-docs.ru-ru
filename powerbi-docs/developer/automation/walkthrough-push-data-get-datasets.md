---
title: Получение набора данных для добавления строк во встроенной аналитике Power BI для получения оптимальной встроенной бизнес-аналитики
description: Пошаговое руководство по отправке данных — получение набора данных для добавления строк в таблицу Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: madia
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: tutorial
ms.date: 02/05/2019
ms.openlocfilehash: e1be761f68dfcd58de8623618acd859694b95bde
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887461"
---
# <a name="step-4-get-a-dataset-to-add-rows-into-a-power-bi-table"></a>Шаг 4. Получение набора данных для добавления строк в таблицу Power BI

Эта статья является частью пошагового руководства по [принудительной отправке данных в набор данных](walkthrough-push-data.md).

На **шаге 3** ([Создание набора данных в панели мониторинга Power BI](walkthrough-push-data-create-dataset.md)) руководства по принудительной отправке данных в набор данных вы вызвали операцию [Создание набора данных](/rest/api/power-bi/datasets), чтобы создать набор данных в Power BI. На этом шаге вы будете использовать операцию [Получение наборов данных](/rest/api/power-bi/datasets/getdatasets) и Newtonsoft.Json, чтобы получить идентификатор набора данных. Идентификатор набора данных потребуется на шаге 4 для добавления строк в набор данных. 

Чтобы принудительно отправить данные в набор данных Power BI, необходимо сослаться на таблицу в наборе данных. Для этого сначала потребуется получить **идентификатор набора данных**. Чтобы получить **идентификатор набора данных**, выполните операцию [получения наборов данных](/rest/api/power-bi/datasets/getdatasets). Операция **получения наборов данных** возвращает строку JSON со списком всех наборов данных в Power BI. Для десериализации строки JSON рекомендуется использовать [Newtonsoft.Json](https://www.newtonsoft.com/json).

Вот как получить набор данных.

## <a name="get-a-power-bi-dataset"></a>Получение набора данных Power BI

> **ПРИМЕЧАНИЕ.** Перед началом работы убедитесь, что выполнены предыдущие шаги из пошагового руководства по [принудительной отправке данных в набор данных](walkthrough-push-data.md).

1. В проекте консольного приложения, созданного на шаге 2 [Получение токена доступа для проверки подлинности](walkthrough-push-data-get-token.md) пошагового руководства по отправке данных, установите пакет NuGet Newtonsoft.Json. Ниже приведены действия по установке пакета.

     а. В Visual Studio 2015 выберите пункты **Сервис** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.

     б. В **консоли диспетчера пакетов** введите команду Install-Package Newtonsoft.Json.
2. После установки пакета добавьте директиву **using Newtonsoft.Json;** в файл Program.cs.
3. В Program.cs добавьте приведенный ниже код для получения **идентификатора набора данных**.
4. Запустите консольное приложение и войдите в свою учетную запись Power BI. В окне консоли вы должны увидеть **идентификатор набора данных**.

**Пример получения набора данных**

Добавьте следующий код в Program.cs.

* В методе static void Main(string[] args):
  
  ```csharp
  static void Main(string[] args)
  {
  
    //Get an authentication access token
    token = GetToken();
  
    //Create a dataset in Power BI
    CreateDataset();
  
    //Get a dataset to add rows into a Power BI table
    string datasetId = GetDataset();
  }
  ```
* Добавьте метод GetDatset():
  
  ```csharp
    #region Get a dataset to add rows into a Power BI table
    private static string GetDataset()
    {
        string powerBIDatasetsApiUrl = "https://api.powerbi.com/v1.0/myorg/datasets";
        //POST web request to create a dataset.
        //To create a Dataset in a group, use the Groups uri: https://api.PowerBI.com/v1.0/myorg/groups/{group_id}/datasets
        HttpWebRequest request = System.Net.WebRequest.Create(powerBIDatasetsApiUrl) as System.Net.HttpWebRequest;
        request.KeepAlive = true;
        request.Method = "GET";
        request.ContentLength = 0;
        request.ContentType = "application/json";
  
        //Add token to the request header
        request.Headers.Add("Authorization", String.Format("Bearer {0}", token));
  
        string datasetId = string.Empty;
        //Get HttpWebResponse from GET request
        using (HttpWebResponse httpResponse = request.GetResponse() as System.Net.HttpWebResponse)
        {
            //Get StreamReader that holds the response stream
            using (StreamReader reader = new System.IO.StreamReader(httpResponse.GetResponseStream()))
            {
                string responseContent = reader.ReadToEnd();
  
                //TODO: Install NuGet Newtonsoft.Json package: Install-Package Newtonsoft.Json
                //and add using Newtonsoft.Json
                var results = JsonConvert.DeserializeObject<dynamic>(responseContent);
  
                //Get the first id
                datasetId = results["value"][0]["id"];
  
                Console.WriteLine(String.Format("Dataset ID: {0}", datasetId));
                Console.ReadLine();
  
                return datasetId;
            }
        }
    }
    #endregion
  ```

Следующим шагом является [добавление строк в таблицу Power BI](walkthrough-push-data-add-rows.md).

Ниже приведен [полный листинг кода](#code).

<a name="code"/>

## <a name="complete-code-listing"></a>Полный листинг кода

```csharp
using System;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Net;
using System.IO;
using Newtonsoft.Json;

namespace walkthrough_push_data
{
    class Program
    {
        private static string token = string.Empty;

        static void Main(string[] args)
        {

            //Get an authentication access token
            token = GetToken();

            //Create a dataset in Power BI
            CreateDataset();

            //Get a dataset to add rows into a Power BI table
            string datasetId = GetDataset();

        }

        #region Get an authentication access token
        private static string GetToken()
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
            string token = authContext.AcquireToken(resourceUri, clientID, new Uri(redirectUri)).AccessToken;

            Console.WriteLine(token);
            Console.ReadLine();

            return token;
        }

        #endregion

        #region Create a dataset in Power BI
        private static void CreateDataset()
        {
            //TODO: Add using System.Net and using System.IO

            string powerBIDatasetsApiUrl = "https://api.powerbi.com/v1.0/myorg/datasets";
            //POST web request to create a dataset.
            //To create a Dataset in a group, use the Groups uri: https://api.PowerBI.com/v1.0/myorg/groups/{group_id}/datasets
            HttpWebRequest request = System.Net.WebRequest.Create(powerBIDatasetsApiUrl) as System.Net.HttpWebRequest;
            request.KeepAlive = true;
            request.Method = "POST";
            request.ContentLength = 0;
            request.ContentType = "application/json";

            //Add token to the request header
            request.Headers.Add("Authorization", String.Format("Bearer {0}", token));

            //Create dataset JSON for POST request
            string datasetJson = "{\"name\": \"SalesMarketing\", \"tables\": " +
                "[{\"name\": \"Product\", \"columns\": " +
                "[{ \"name\": \"ProductID\", \"dataType\": \"Int64\"}, " +
                "{ \"name\": \"Name\", \"dataType\": \"string\"}, " +
                "{ \"name\": \"Category\", \"dataType\": \"string\"}," +
                "{ \"name\": \"IsCompete\", \"dataType\": \"bool\"}," +
                "{ \"name\": \"ManufacturedOn\", \"dataType\": \"DateTime\"}" +
                "]}]}";

            //POST web request
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(datasetJson);
            request.ContentLength = byteArray.Length;

            //Write JSON byte[] into a Stream
            using (Stream writer = request.GetRequestStream())
            {
                writer.Write(byteArray, 0, byteArray.Length);

                var response = (HttpWebResponse)request.GetResponse();

                Console.WriteLine(string.Format("Dataset {0}", response.StatusCode.ToString()));

                Console.ReadLine();
            }
        }
        #endregion

        #region Get a dataset to add rows into a Power BI table
        private static string GetDataset()
        {
            string powerBIDatasetsApiUrl = "https://api.powerbi.com/v1.0/myorg/datasets";
            //POST web request to create a dataset.
            //To create a Dataset in a group, use the Groups uri: https://api.PowerBI.com/v1.0/myorg/groups/{group_id}/datasets
            HttpWebRequest request = System.Net.WebRequest.Create(powerBIDatasetsApiUrl) as System.Net.HttpWebRequest;
            request.KeepAlive = true;
            request.Method = "GET";
            request.ContentLength = 0;
            request.ContentType = "application/json";

            //Add token to the request header
            request.Headers.Add("Authorization", String.Format("Bearer {0}", token));

            string datasetId = string.Empty;
            //Get HttpWebResponse from GET request
            using (HttpWebResponse httpResponse = request.GetResponse() as System.Net.HttpWebResponse)
            {
                //Get StreamReader that holds the response stream
                using (StreamReader reader = new System.IO.StreamReader(httpResponse.GetResponseStream()))
                {
                    string responseContent = reader.ReadToEnd();

                    //TODO: Install NuGet Newtonsoft.Json package: Install-Package Newtonsoft.Json
                    //and add using Newtonsoft.Json
                    var results = JsonConvert.DeserializeObject<dynamic>(responseContent);

                    //Get the first id
                    datasetId = results["value"][0]["id"];

                    Console.WriteLine(String.Format("Dataset ID: {0}", datasetId));
                    Console.ReadLine();

                    return datasetId;
                }
            }
        }
        #endregion
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

* [Добавление строк в таблицу Power BI](walkthrough-push-data-add-rows.md)  
* [Newtonsoft.Json](https://www.newtonsoft.com/json)  
* [Получение наборов данных](/rest/api/power-bi/datasets/getdatasets)  
* [Принудительная отправка данных в Power BI](walkthrough-push-data.md)  
* [Обзор интерфейса REST API Power BI](overview-of-power-bi-rest-api.md)  
* [Справочник по REST API Power BI](/rest/api/power-bi/)  

Остались вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)