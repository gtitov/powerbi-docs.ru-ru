---
title: Изменение строк подключения к источникам данных с помощью PowerShell — Сервер отчетов Power BI (до октября 2020 г.)
description: Изменение строк подключения к источникам данных с помощью API в PowerShell — Сервер отчетов Power BI (до октября 2020 г.)
author: maggiesMSFT
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 10/26/2020
ms.author: maggies
ms.openlocfilehash: 9b4d31b2acc3ce7ec43bbd3fdb91df8e32c2e953
ms.sourcegitcommit: a5fa368abad54feb44a267fe26c383a731c7ec0d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93049423"
---
# <a name="change-data-source-connection-strings-in-power-bi-reports-with-powershell---power-bi-report-server-pre-october-2020"></a>Изменение строк подключения к источникам данных в отчетах Power BI с помощью PowerShell — Сервер отчетов Power BI (до октября 2020 г.)


Для взаимодействия с необходимыми API вы можете изменить строки подключения к источнику данных отчетов Power BI, размещенных на Сервере отчетов Power BI, с помощью PowerShell. 

> [!IMPORTANT]
> Если вы используете последнюю версию Сервера отчетов Power BI (октябрь 2020 г.), см. раздел [Изменение строк подключения к источникам данных в отчетах Power BI с помощью PowerShell — Сервер отчетов Power BI](connect-data-source-apis.md).

> [!NOTE]
> Сейчас эта функция работает только для DirectQuery. Поддержка импорта и обновления данных ожидается в ближайшее время.

1. Установите командлеты PowerShell для сервера отчетов Power BI. Командлеты и инструкции по установке см. на странице [https://github.com/Microsoft/ReportingServicesTools](https://github.com/Microsoft/ReportingServicesTools). 

    Установите модуль `ReportingServicesTools` прямо из [коллекции PowerShell](https://www.powershellgallery.com/packages/ReportingServicesTools/), используя следующую команду.

    ```powershell
    Install-Module ReportingServicesTools
    ```

2. Получите сведения о существующем источнике данных для файла Power BI с помощью командлетов PowerShell:

    ```powershell
    Get-RsRestItemDataSource -RsItem '/MyPbixReport'
    ```

    Чтобы просмотреть сведения о первом источнике данных, который содержится в отчете Power BI, используйте следующую строку: 

    ```powershell
    $dataSources[0]
    ```

3. Измените сведения о подключении и учетные данные требуемым образом. Если вы изменяете строку подключения и источник данных использует сохраненные учетные данные, необходимо указать пароль к учетной записи. 

    Чтобы изменить строку подключения к источнику данных, используйте следующую строку:

    ```powershell
    $dataSources[0].ConnectionString = 'data source=myCatalogServer;initial catalog=ReportServer;persist security info=False' 
    ```

    Чтобы изменить тип учетных данных для источника данных, используйте следующую строку:

    ```powershell
    $dataSources[0].DataModelDataSource.AuthType = 'Integrated'
    ```

    Чтобы изменить имя пользователя и пароль для источника данных, используйте следующую строку:

    ```powershell
    $dataSources[0].DataModelDataSource.Username = 'domain\user'
    ```
    ```powershell
    $dataSources[0].DataModelDataSource.Secret = 'password'
    ```

4. Сохраните измененные учетные данные на сервере.

    ```powershell
    Set-RsRestItemDataSource -RsItem '/MyPbixReport' -RsItemType 'PowerBIReport' -DataSources $dataSources
    ```

## <a name="next-steps"></a>Дальнейшие действия

[Источники данных для отчетов с разбивкой на страницы в решении "Сервер отчетов Power BI"](connect-data-sources.md) 

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
