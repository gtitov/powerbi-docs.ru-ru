---
title: Программная настройка учетных данных для Power BI
description: Порядок программной настройки учетных данных при автоматизации Power BI
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.date: 06/23/2020
ms.openlocfilehash: 902fb0534eee307a84b24fe30496a32cccadb147
ms.sourcegitcommit: bbf7e9341a4e1cc96c969e24318c8605440282a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97097991"
---
# <a name="configure-credentials-programmatically-for-power-bi"></a>Программная настройка учетных данных для Power BI

Выполните описанные в этой статье действия, чтобы программно настроить учетные данные для Power BI.

>[!NOTE]
>* Вызывающий пользователь должен быть владельцем набора данных или администратором шлюза. Вы также можете использовать [субъект-службу](../embedded/embed-service-principal.md). Например, субъектом-службой может быть владелец набора данных.
>* Управление облачными источниками данных и их соответствующими учетными данными осуществляется на уровне пользователя.

## <a name="update-credentials-flow-for-data-sources"></a>Обновление потока учетных данных для источников данных

1. Вызовите интерфейс [получения источников данных](/rest/api/power-bi/datasets/getdatasourcesingroup), чтобы обнаружить источники данных для набора данных. Текст ответа для каждого источника данных содержит тип, сведения о подключении, шлюз и идентификатор источника данных.

    ```csharp
    // Select a datasource
    var datasources = pbiClient.Datasets.GetDatasources(datasetId).Value;
    var datasource = datasources.First();
    ```

2. Создайте строку учетных данных в соответствии с [примерами обновления источника данных](/rest/api/power-bi/gateways/updatedatasource) в зависимости от типа учетных данных.

    # <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

    ```csharp
    var credentials =  new BasicCredentials(username: "username", password :"*****");
    ```

    # <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

     ```csharp
    var credentials = "{\"credentialData\":[{\"name\":\"username\", \"value\":\"john\"},{\"name\":\"password\", \"value\":\"*****\"}]}";
    ```

    ---

    >[!NOTE]
    >Если вы используете облачные источники данных, не выполняйте дальнейшие действия в этом разделе. Задайте учетные данные, использовав идентификаторы шлюза и источника данных из шага 1 и вызвав команду [Обновить источник данных](/rest/api/power-bi/gateways/updatedatasource). 

3. Вызовите интерфейс [получения шлюза](/rest/api/power-bi/gateways/getgateways) для извлечения открытого ключа шлюза.

    ```csharp
    var gateway = pbiClient.Gateways.GetGatewayById(datasource.GatewayId);
    ```

4. Зашифруйте учетные данные.

    # <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

    ```csharp
    var credentialsEncryptor = new AsymmetricKeyEncryptor(gateway.publicKey);
    ```

    # <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

    Зашифруйте строку учетных данных с помощью открытого ключа шлюза из шага 2. У разных версий шлюза могут иметься разные размеры открытого ключа. См. следующие примеры в коде пакета SDK, доступные в репозитории [PowerBI-CSharp GitHub](https://github.com/microsoft/PowerBI-CSharp/tree/master/sdk/PowerBI.Api/Extensions).
    * [AsymmetricKeyEncryptor.cs](https://github.com/microsoft/PowerBI-CSharp/blob/master/sdk/PowerBI.Api/Extensions/AsymmetricKeyEncryptor.cs)
    * [Asymmetric1024KeyEncryptionHelper.cs](https://github.com/microsoft/PowerBI-CSharp/blob/master/sdk/PowerBI.Api/Extensions/Asymmetric1024KeyEncryptionHelper.cs)
    * [AsymmetricHigherKeyEncryptionHelper.cs](https://github.com/microsoft/PowerBI-CSharp/blob/master/sdk/PowerBI.Api/Extensions/AsymmetricHigherKeyEncryptionHelper.cs)
    * [AuthenticatedEncryption.cs](https://github.com/microsoft/PowerBI-CSharp/blob/master/sdk/PowerBI.Api/Extensions/AuthenticatedEncryption.cs) 

    ---  

5. Создавайте сведения об учетных данных с зашифрованными учетными данными.

    # <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

    Используйте класс AssymetricKeyEncryptor с открытым ключом, полученным в **шаге 3**.

    ```csharp
    var credentialDetails = new CredentialDetails(
            credentials,
            PrivacyLevel.Private,
            EncryptedConnection.Encrypted,
            credentialsEncryptor);
    ```


    # <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

    ```csharp
    var credentialDetails = new CredentialDetails(
            credentials,
            CredentialTypeEnum.Basic,
            EncryptedConnectionEnum.Encrypted,
            EncryptionAlgorithmEnum.None,
            PrivacyLevelEnum.Private);
    ```

    ---

6. Вызовите интерфейс [обновления источника данных](/rest/api/power-bi/gateways/updatedatasource) для задания учетных данных.

    ```csharp
    pbiClient.Gateways.UpdateDatasource(gatewayId, datasourceId, credentialDetails);
    ```

## <a name="configure-a-new-data-source-for-a-data-gateway"></a>Настройка нового источника данных для шлюза данных

1. Установите [локальный шлюз данных](https://powerbi.microsoft.com/gateway/) на своем компьютере.

2. Вызовите интерфейс [получения шлюза](/rest/api/power-bi/gateways/getgateways) для извлечения открытого ключа и идентификатора шлюза.

    ```csharp
    // Select a gateway
    var gateways = pbiClient.Gateways.GetGateways().Value;
    var gateway = gateways.First();
    ```

3. Создайте сведения об учетных данных так же, как описано в разделе [Обновление потока учетных данных для источников данных](#update-credentials-flow-for-data-sources) с помощью открытого ключа шлюза, полученного на **шаге 2**.

4. Создайте текст запроса.

    ```csharp
    var request = new PublishDatasourceToGatewayRequest(
            dataSourceType: "SQL",
            connectionDetails: "{\"server\":\"myServer\",\"database\":\"myDatabase\"}",
            credentialDetails: credentialDetails,
            dataSourceName: "my sql datasource");
    ```

5. Вызовите API [создания источника данных](/rest/api/power-bi/gateways/createdatasource).

    ```csharp
    pbiClient.Gateways.CreateDatasource(gateway.Id, request);
    ```

## <a name="credential-types"></a>Типы учетных данных

При отправке запроса на [создание источника данных](/rest/api/power-bi/gateways/createdatasource) или [обновление источника данных](/rest/api/power-bi/gateways/updatedatasource) для **корпоративного локального шлюза** с помощью [REST API Power BI](/rest/api/power-bi/) учетные данные должны шифроваться с использованием открытого ключа шлюза.

>[!NOTE]
>Пакет SDK для .NET версии 3 также может выполнять примеры пакета SDK для .NET версии 2, перечисленные ниже.

### <a name="windows-and-basic-credentials"></a>Учетные данные Windows и Basic

# <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

```csharp
// Windows credentials
var credentials = new WindowsCredentials(username: "john", password: "*****");

// Or

// Basic credentials
var credentials = new BasicCredentials(username: "john", password: "*****");

var credentialsEncryptor = new AsymmetricKeyEncryptor(publicKey);
var credentialDetails = new CredentialDetails(credentials, PrivacyLevel.Private, EncryptedConnection.Encrypted, credentialsEncryptor);
```

# <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

```csharp
var credentials = "{\"credentialData\":[{\"name\":\"username\", \"value\":\"john\"},{\"name\":\"password\", \"value\":\"*****\"}]}";
```

---

### <a name="key-credentials"></a>Учетные данные в виде ключей

# <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

```csharp
var credentials = new KeyCredentials("TestKey");
var credentialsEncryptor = new AsymmetricKeyEncryptor(publicKey);
var credentialDetails = new CredentialDetails(credentials, PrivacyLevel.Private, EncryptedConnection.Encrypted, credentialsEncryptor);
```

# <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

```csharp
var credentials = "{\"credentialData\":[{\"name\":\"key\", \"value\":\"ec....LA=\"}]}";
```

---

**Учетные данные OAuth2**

# <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

```csharp
var credentials = new OAuth2Credentials("TestToken");
var credentialsEncryptor = new AsymmetricKeyEncryptor(publicKey);
var credentialDetails = new CredentialDetails(credentials, PrivacyLevel.Private, EncryptedConnection.Encrypted, credentialsEncryptor);
```

# <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

```csharp
var credentials = "{\"credentialData\":[{\"name\":\"accessToken\", \"value\":\"eyJ0....fwtQ\"}]}";
```

---

**Анонимные учетные данные**

# <a name="net-sdk-v3"></a>[Пакет SDK версии 3 для .NET](#tab/sdk3)

```csharp
var credentials = new AnonymousCredentials();
var credentialDetails = new CredentialDetails(credentials, PrivacyLevel.Private, EncryptedConnection.NotEncrypted);
```

# <a name="net-sdk-v2"></a>[Пакет SDK для .NET версии 2](#tab/sdk2)

```csharp
var credentials = "{\"credentialData\":\"\"}";
```

---

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="no-gateway-and-data-source-id-found-when-calling-get-data-sources"></a>Отсутствие идентификатора источника данных и шлюза при вызове интерфейса для получения источников данных

Эта проблема означает, что набор данных не привязан к шлюзу. При создании набора данных для каждого облачного подключения в облачном шлюзе пользователя автоматически создается источник данных без учетных данных. Этот шлюз используется для хранения учетных данных для облачных подключений.

После создания набора данных создается автоматическая привязка между ним и подходящим шлюзом, содержащим соответствующие источники данных для всех подключений. Если подходящие шлюзы отсутствуют или их несколько, автоматическая привязка завершается сбоем.

Если вы используете локальные наборы данных, создайте отсутствующие локальные источники данных и привяжите набор данных к шлюзу вручную с помощью интерфейса [привязки к шлюзу](/rest/api/power-bi/datasets/bindtogateway).

Чтобы обнаружить доступные для привязки шлюзы, используйте интерфейс [обнаружения шлюзов](/rest/api/power-bi/datasets/discovergateways).
