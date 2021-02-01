---
title: Экспортируйте API отчетов с разбивкой на страницы встроенной аналитики Power BI для получения оптимальной встроенной бизнес-аналитики
description: Узнайте, как экспортировать внедренный отчет с разбивкой на страницы из Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.topic: how-to
ms.service: powerbi
ms.subservice: powerbi-developer
ms.date: 04/05/2020
ms.openlocfilehash: befb64ec85c02f8993d828202df06aafc5901482
ms.sourcegitcommit: 84f0e7f31e62cae3bea2dcf2d62c2f023cc2d404
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781518"
---
# <a name="export-paginated-report-to-file-preview"></a>Экспорт отчета с разбивкой на страницы в файл (предварительная версия)

API `exportToFile` позволяет экспортировать отчет Power BI с разбивкой на страницы с помощью вызова REST. Поддерживаются следующие форматы файлов:
* **PPTX** (PowerPoint)
* **PDF**
* **XLSX** (Excel)
* **DOX** (Word)
* **CSV**
* **XML**
* **MHTML**
* **Изображение**
    * При экспорте в изображение задайте формат изображения с помощью параметра формата `OutputFormat`.
    * Поддерживаются следующие значения формата вывода: BMP, EMF, GIF, JPEG, PNG или TIFF (по умолчанию).

## <a name="usage-examples"></a>Примеры использования

Функцию экспорта можно использовать различными способами. Вот несколько примеров.

* **Кнопка Send to print (Отправить на печать)** . В приложении создайте кнопку, которая при нажатии активирует задание экспорта. Задание может экспортировать просматриваемый отчет в формате PDF или PPTX, а после его завершения пользователь может получить его в качестве загружаемого файла. С помощью параметров отчета и параметров формата можно экспортировать отчет в определенном состоянии, включая отфильтрованные данные, пользовательские размеры страниц и другие параметры форматирования. Так как API является асинхронным, для доступа к файлу может потребоваться некоторое время.

* **Вложение электронной почты**. Отправка автоматизированного электронного письма через заданные интервалы с вложенным отчетом в формате PDF. Этот сценарий может быть полезен, если вы хотите автоматизировать отправку еженедельного отчета руководителям.

## <a name="using-the-api"></a>Использование API

API является асинхронным. При вызове API [exportToFile](/rest/api/power-bi/reports/exporttofile) запускает задание экспорта. После запуска задания экспорта используйте [опрос](/rest/api/power-bi/reports/getexporttofilestatus) для отслеживания задания, пока оно не будет завершено.

После завершения экспорта вызов API опроса возвращает [URL-адрес Power BI](/rest/api/power-bi/reports/getfileofexporttofile) для получения файла. URL-адрес будет доступен в течение 24 часов.

## <a name="supported-features"></a>Поддерживаемые функции

### <a name="format-settings"></a>Параметры формата

Укажите различные параметры форматирования для каждого формата файлов. Поддерживаемые свойства и значения эквивалентны [параметрам сведений об устройстве](../../paginated-reports/report-builder-url-parameters.md#report-commands-rdl) для параметров URL-адреса отчета с разбивкой на страницы.

Ниже приведены два примера: один для экспорта первых четырех страниц отчета, используя размер страницы отчета, в PPTX-файл, а другой — для экспорта третьей страницы отчета в JPEG-файл.

**Экспорт первых четырех страниц в PPTX**

```json
{
      "format": "PPTX",
      "paginatedReportConfiguration":{
            "formatSettings":{
                  "UseReportPageSize": "true",
                  "StartPage": "1",
                  "EndPage": "4"
            }
      }
}
```

**Экспорт третьей страницы в JPEG**

```json
{
      "format": "IMAGE",
      "paginatedReportConfiguration":{
            "formatSettings":{
                  "OutputFormat": "JPEG",
                  "StartPage": "3",
                  "EndPage": "3"
            }
      }
}
```

### <a name="report-parameters"></a>Параметры отчета

API `exportToFile` можно использовать для программного экспорта отчета с набором параметров отчета. Это делается с помощью возможностей [параметра отчета](../../paginated-reports/paginated-reports-parameters.md).

Ниже приведен пример задания значений параметров отчета.

```json
{
      "format": "PDF",
      "paginatedReportConfiguration":{
            "parameterValues":[
                  {"name": "State", "value": "WA"},
                  {"name": "City", "value": "Seattle"},
                  {"name": "City", "value": "Bellevue"},
                  {"name": "City", "value": "Redmond"}
            ]
      }
}
```

### <a name="authentication"></a>Аутентификация

Проверку подлинности можно выполнять с помощью пользователя (главного пользователя) или [субъекта-службы](embed-service-principal.md).

### <a name="row-level-security-rls"></a>Безопасность на уровне строк (RLS)

При использовании набора данных Power BI с безопасностью на уровне строк (RLS), определенного в качестве источника данных, можно экспортировать отчет, содержащий данные, которые видны только определенным пользователям. Например, при экспорте отчета о продажах, определенного с помощью региональных ролей, можно программно фильтровать отчет таким образом, чтобы отображался только определенный регион.

Для экспорта с использованием RLS необходимо иметь разрешение на чтение для набора данных Power BI, который отчет использует в качестве источника данных.

Ниже приведен пример указания действующего имени пользователя для RLS.

```json
{
      "format": "PDF",
      "paginatedReportConfiguration":{
            "identities": [
                  {"username": "john@contoso.com"}
            ]
      }
}
```

### <a name="single-sign-on-sql-and-dataverse-sso"></a>Единый вход SQL и Dataverse (SSO)

В Power BI есть возможность задать OAuth с использованием SSO. При этом для получения данных используются учетные данные пользователя, просматривающего отчет. Маркер доступа в заголовке запроса не используется для доступа к данным. Маркер должен передаваться вместе с действующим удостоверением в тексте сообщения POST.

С маркерами доступа проблема может быть в том, что вам нужно получить правильный маркер для ресурса, к которому вы обращаетесь.

- Ресурс для Azure SQL — `https://database.windows.net`.
- Ресурс для Dataverse — адрес `https://` вашей среды. Например, `https://contoso.crm.dynamics.com`.

Получите доступ к API маркера с помощью метода [AuthenticationContext.AcquireTokenAsync](https://docs.microsoft.com/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync).

Ниже приведен пример предоставления действующего имени пользователя с маркером доступа.

```json
{
       "format":"PDF",
       "paginatedReportConfiguration":{
          "formatSettings":{
             "AccessiblePDF":"true",
             "PageHeight":"11in",
             "PageWidth":"8.5in",
             "MarginBottom":"2in"
          },
          "identities":[
             {
                "username":"john@contoso.com",
                "identityBlob": {
                "value": "eyJ0eX....full access token"
         }
        }
     ]
   }
}
```

## <a name="ppu-concurrent-requests"></a>Количество одновременных запросов в PPU
API `exportToFile` позволяет использовать один запрос в течение пяти минут при использовании [Premium на пользователя (PPU)](../../admin/service-premium-per-user-faq.md). Несколько запросов (более одного) в течение пяти минут приведет к ошибке 429: *Слишком много запросов*.

## <a name="code-examples"></a>Примеры кода

Пакет SDK API Power BI, используемый в примерах кода, можно скачать [здесь](https://www.nuget.org/packages/Microsoft.PowerBI.Api).

При создании задания экспорта необходимо выполнить три шага:

1. отправка запроса на экспорт;
2. опрос;
3. получение файлов.

В этом разделе приводятся примеры для каждого шага.

### <a name="step-1---sending-an-export-request"></a>Шаг 1. Отправка запроса на экспорт

Первый шаг — это отправка запроса на экспорт. В этом примере отправляется запрос на экспорт для определенного диапазона страниц, размера и параметра отчета.

```csharp
private async Task<string> PostExportRequest(
    Guid reportId,
    Guid groupId)
{
    // For documentation purposes the export configuration is created in this method
    // Ordinarily, it would be created outside and passed in
    var paginatedReportExportConfiguration = new PaginatedReportExportConfiguration()
    {
        FormatSettings = new Dictionary<string, string>()
        {
            {"PageHeight", "14in"},
            {"PageWidth", "8.5in" },
            {"StartPage", "1"},
            {"EndPage", "4"},
        },
        ParameterValues = new List<ParameterValue>()
        {
            { new ParameterValue() {Name = "State", Value = "WA"} },
            { new ParameterValue() {Name = "City", Value = "Redmond"} },
        },
    };

    var exportRequest = new ExportReportRequest
    {
        Format = FileFormat.PDF,
        PaginatedReportExportConfiguration = paginatedReportExportConfiguration,
    };

    var export = await Client.Reports.ExportToFileInGroupAsync(groupId, reportId, exportRequest);

    // Save the export ID, you'll need it for polling and getting the exported file
    return export.Id;
}
```

### <a name="step-2---polling"></a>Шаг 2. Опрос

После отправки запроса на экспорт используйте опрос, чтобы узнать, когда файл экспорта, который вы ожидаете, будет готов.

```csharp
private async Task<Export> PollExportRequest(
    Guid reportId,
    Guid groupId,
    string exportId /* Get from the ExportToAsync response */,
    int timeOutInMinutes,
    CancellationToken token)
{
    Export exportStatus = null;
    DateTime startTime = DateTime.UtcNow;
    const int secToMillisec = 1000;
    do
    {
        if (DateTime.UtcNow.Subtract(startTime).TotalMinutes > timeOutInMinutes || token.IsCancellationRequested)
        {
            // Error handling for timeout and cancellations
            return null;
        }

        var httpMessage = 
            await Client.Reports.GetExportToFileStatusInGroupWithHttpMessagesAsync(groupId, reportId, exportId);
            
        exportStatus = httpMessage.Body;
        if (exportStatus.Status == ExportState.Running || exportStatus.Status == ExportState.NotStarted)
        {
            // The recommended waiting time between polling requests can be found in the RetryAfter header
            // Note that this header is only populated when the status is either Running or NotStarted
            var retryAfter = httpMessage.Response.Headers.RetryAfter;
            var retryAfterInSec = retryAfter.Delta.Value.Seconds;

            await Task.Delay(retryAfterInSec * secToMillisec);
        }
    }
    // While not in a terminal state, keep polling
    while (exportStatus.Status != ExportState.Succeeded && exportStatus.Status != ExportState.Failed);

    return exportStatus;
}
```

### <a name="step-3---getting-the-file"></a>Шаг 3. Получение файлов.

После того, как опрос вернет URL, используйте этот пример для получения файла.

```csharp
private async Task<ExportedFile> GetExportedFile(
    Guid reportId,
    Guid groupId,
    Export export /* Get from the GetExportStatusAsync response */)
{
    if (export.Status == ExportState.Succeeded)
    {
        var httpMessage = 
            await Client.Reports.GetFileOfExportToFileInGroupWithHttpMessagesAsync(groupId, reportId, export.Id);

        return new ExportedFile
        {
            FileStream = httpMessage.Body,
            ReportName = export.ReportName,
            FileExtension = export.ResourceFileExtension,
        };
    }

    return null;
}

public class ExportedFile
{
    public Stream FileStream;
    public string ReportName;
    public string FileExtension;
}
```

### <a name="end-to-end-example"></a>Комплексный пример

Это полный пример для экспорта отчета. Этот пример включает следующие этапы:
1. [Отправка запроса на экспорт](#step-1---sending-an-export-request).
2. [Опрос](#step-2---polling).
3. [Получение файлов](#step-3---getting-the-file).

```csharp
private async Task<ExportedFile> ExportPaginatedReport(
    Guid reportId,
    Guid groupId,
    int pollingtimeOutInMinutes,
    CancellationToken token)
{
    try
    {
        var exportId = await PostExportRequest(reportId, groupId);

        var export = await PollExportRequest(reportId, groupId, exportId, pollingtimeOutInMinutes, token);
        if (export == null || export.Status != ExportState.Succeeded)
        {
           // Error, failure in exporting the report
            return null;
        }

        return await GetExportedFile(reportId, groupId, export);
    }
    catch
    {
        // Error handling
        throw;
    }
}
```

## <a name="limitations"></a>Ограничения

Экспорт отчета с разбивкой на страницы, в котором в качестве источника данных используется набор данных Power BI, не поддерживается для субъектов-служб.

## <a name="next-steps"></a>Дальнейшие действия

Ознакомьтесь со сведениями о внедрении содержимого для клиентов и вашей организации:

> [!div class="nextstepaction"]
>[Экспорт отчета в файл](export-to.md)

> [!div class="nextstepaction"]
>[Внедрение для клиентов](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Внедрение для организации](embed-sample-for-your-organization.md)
