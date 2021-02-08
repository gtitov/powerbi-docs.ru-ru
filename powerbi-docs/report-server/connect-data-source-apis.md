---
title: Изменение строк подключения к источникам данных с помощью PowerShell
description: Изменение строк подключения к источникам данных с помощью API в PowerShell — сервер отчетов Microsoft Power BI
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 10/26/2020
ms.openlocfilehash: b7f431ba6b8f559380916c17689d0eab74a0c9a7
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99044317"
---
# <a name="change-data-source-connection-strings-in-power-bi-reports-with-powershell---power-bi-report-server"></a>Изменение строк подключения к источникам данных в отчетах Power BI с помощью PowerShell — сервер отчетов Microsoft Power BI


Начиная с выпуска Сервера отчетов Power BI за октябрь 2020 г., мы предоставляем возможность обновлять подключения к отчетам Power BI для DirectQuery.

> [!IMPORTANT]
> Это также является критическим изменением по сравнению с тем, как аналогичную настройку можно выполнить в предыдущих выпусках. Если вы используете версию Сервера отчетов Power BI, выпущенную до октября 2020 г., см. раздел [Изменение строк подключения к источникам данных в отчетах Power BI с помощью PowerShell — Сервер отчетов Power BI (до октября 2020 г.)](connect-data-source-apis-pre-oct-2020.md).

## <a name="prerequisites"></a>Предварительные требования.
- Скачайте выпуск [Сервера отчетов Power BI и приложения Power BI Desktop для Сервера отчетов Power BI](https://powerbi.microsoft.com/report-server/) за октябрь 2020 г. или более поздний.
- Отчет, сохраненный в выпуске Power BI Desktop для Сервера отчетов за октябрь 2020 г. или более позднем, с включенными **расширенными метаданными наборов данных**.
- Отчет, использующий параметризованные соединения. Только отчеты с параметризованными соединениями и базами данных могут быть обновлены после публикации.
- В этом примере используются инструменты PowerShell Reporting Services. Вы можете добиться того же результата с помощью новых REST API.

## <a name="create-a-report-with-parameterized-connections"></a>Создание отчета с параметризованными соединениями
    
1. Создайте подключение SQL Server к серверу. В приведенном ниже примере мы подключаемся к localhost для базы данных ReportServer и извлекаем данные из ExecutionLog.

    :::image type="content" source="media/connect-data-source-apis/sql-server-connect-database.png" alt-text="Подключение к базе данных SQL Server":::

    Вот как выглядит запрос M на этом этапе.

    ```
    let
        Source = Sql.Database("localhost", "ReportServer"),
        dbo_ExecutionLog3 = Source{[Schema="dbo",Item="ExecutionLog3"]}[Data]
    in
        dbo_ExecutionLog3
    ```

2. Выберите **Управление параметрами** на ленте Редактора Power Query.

    :::image type="content" source="media/connect-data-source-apis/power-query-manage-parameters.png" alt-text="Выбор элемента &quot;Управление параметрами&quot;":::

1.  Создайте параметры для имени сервера servername и имени базы данных databasename.

    :::image type="content" source="media/connect-data-source-apis/report-server-manage-parameters.png" alt-text="Управление параметрами, задание servername и databasename":::


3. Измените запрос для первого подключения и сопоставьте базу данных и имя сервера.

    :::image type="content" source="media/connect-data-source-apis/report-server-map-database-server.png" alt-text="Сопоставление имени сервера и имени базы данных":::

    Теперь запрос выглядит следующим образом.

    ```
    let
        Source = Sql.Database(ServerName, Databasename),
        dbo_ExecutionLog3 = Source{[Schema="dbo",Item="ExecutionLog3"]}[Data]
    in
        dbo_ExecutionLog3
    ```
    
    4. Опубликуйте этот отчет на сервере. В этом примере отчет называется executionlogparameter. На следующем рисунке показан пример страницы управления источником данных.

    :::image type="content" source="media/connect-data-source-apis/report-server-manage-data-source-credentials.png" alt-text="Страница управления источником данных":::

## <a name="update-parameters-using-the-powershell-tools"></a>Обновление параметров с помощью инструментов PowerShell

1. Откройте PowerShell и установите новейшие инструменты Reporting Services, следуя инструкциям по адресу [https://github.com/microsoft/ReportingServicesTools](https://github.com/microsoft/ReportingServicesTools).
    
2.  Чтобы получить параметр для отчета, используйте новый REST DataModelParameters API DataModelParameters, применив следующий вызов PowerShell.

    ```powershell
    Get-RsRestItemDataModelParameters '/executionlogparameter'

        Name         Value
        ----         -----
        ServerName   localhost
        Databasename ReportServer
    ```

3. Мы сохраняем результат этого вызова в переменной.

    ```powershell
    $parameters = Get-RsRestItemDataModelParameters '/executionlogparameter'
    ```

4. Эта переменная обновляется значениями, которые необходимо изменить.
5. Мы сохраняем результат этого вызова в переменной.

    ```powershell
    $parameters[0].Value = 'myproductionserver'
    $parameters[1].Value = 'myproductiondatabase'
    ```

6. Располагая обновленными значениями, можно использовать командлет `Set-RsRestItemDataModelParameters` для обновления значений на сервере.

    ```powershell
    Set-RsRestItemDataModelParameters -RsItem '/executionlogparameter' -DataModelParameters $parameters
    ```

7. После обновления параметров сервер обновляет все источники данных, привязанные к этим параметрам. Вернувшись к диалоговому окну **Изменение источника данных**, вы сможете задать учетные данные для обновленного сервера и базы данных.

    :::image type="content" source="media/connect-data-source-apis/report-server-manage-executionlogparameter-dialog.png" alt-text="Задание учетных данных для обновленного сервера и базы данных":::

## <a name="next-steps"></a>Дальнейшие действия

[Источники данных для отчетов с разбивкой на страницы в решении "Сервер отчетов Power BI"](connect-data-sources.md) 

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
