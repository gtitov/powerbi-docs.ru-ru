---
title: Параметры URL-адресов в отчетах с разбивкой на страницы (построитель отчетов Power BI)
description: Узнайте, как отправлять команды в отчеты с разбивкой на страницы в Power BI, добавив параметр к URL-адресу, который можно включить в электронную почту или на веб-страницу.
author: maggiesMSFT
ms.author: maggies
ms.service: powerbi
ms.subservice: report-builder
ms.topic: conceptual
ms.reviewer: cfinlan
ms.custom: ''
ms.date: 12/15/2020
ms.openlocfilehash: 4dc7d3dbb68a06f1b18714d2070b7c305390ef6b
ms.sourcegitcommit: fef29a5c5bf1e0dae663c42c9ce5ae50e29ae9be
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/16/2020
ms.locfileid: "97558477"
---
# <a name="url-parameters-in-paginated-reports-in-power-bi"></a>Параметры URL-адреса в отчетах с разбивкой на страницы в Power BI

[!INCLUDE [applies-to](../includes/applies-to.md)] [!INCLUDE [yes-service](../includes/yes-service.md)] [!INCLUDE [yes-paginated](../includes/yes-paginated.md)] [!INCLUDE [yes-premium](../includes/yes-premium.md)] [!INCLUDE [no-desktop](../includes/no-desktop.md)] 

Вы можете отправлять команды в отчеты с разбивкой на страницы в Power BI, добавив параметр в URL-адрес. Например, вы просмотрели отчет, используя конкретный набор значений параметров отчета. Вы инкапсулируете эти сведения в URL-адрес с помощью предопределенных параметров доступа к URL-адресу. Затем вы настраиваете обработку отчета в Power BI путем внедрения параметров для форматов отрисовки или для отображения панели инструментов отчета. После этого вы вставляете этот URL-адрес непосредственно в сообщение электронной почты или на веб-страницу, чтобы другие пользователи могли так же как вы работать с отчетом в браузере. 

Ниже приводятся действия, которые можно выполнять с помощью параметров доступа к URL-адресу. 

- Отправка параметров отчета в отчет. 
- Инициация экспорта содержимого отчета в поддерживаемом формате файла. 
- Скрытие или просмотр панели параметров. 
- Задание параметра DeviceInfo. 

Полный список команд и параметров, доступных через доступ к URL-адресу, см. в разделе  [Справочник по параметрам доступа к URL-адресу](#url-access-parameter-reference) далее в этой статье. 

## <a name="url-access-concepts"></a>Основные понятия доступа к URL-адресу 

Запросы URL-адресов к Power BI содержат параметры, обрабатываемые службой. Способ, которым служба обрабатывает запросы URL-адресов, зависит от параметров, префиксов параметров и типов элементов, включенных в URL-адрес. Функции URL-адресов в отчетах с разбивкой на страницы совместимы с большинством браузеров и приложений, поддерживающих стандартную URL-адресацию. 

## <a name="url-access-syntax"></a>Синтаксис доступа к URL-адресу 

Запросы URL-адресов могут содержать несколько параметров, указанных в любом порядке. Параметры разделяются символом амперсанда (&). Пары "имя-значение" разделяются знаком равенства (=). Например:

```
powerbiserviceurl?rp:parametervalueh&rdl:parameter=value  
```

## <a name="syntax-description"></a>Описание синтаксиса 

### <a name="powerbiserviceurl"></a>powerbiserviceurl 

URL-адрес веб-службы клиента Power BI. Например: 

**&** Используется для разделения пар "имя-значение" в параметрах доступа к URL-адресу.

**префикс** — префикс для параметра URL-адреса (например, rp: или rdl:), указывающий действие в службе Power BI. 

> [!NOTE]
> Параметры отчета должны иметь префикс параметра и указываются с учетом регистра. 

**параметр** — имя параметра. 

### <a name="value"></a>Значение 

Текст URL-адреса, соответствующий значению используемого параметра. 

Примеры передачи параметров отчета в URL-адресе см. в статье о  [передаче параметра отчета в URL-адресе](report-builder-url-pass-parameters.md).

## <a name="url-access-parameter-reference"></a>Справочник по параметрам доступа к URL-адресу

Следующие параметры можно использовать как часть URL-адреса для настройки внешнего вида отчетов с разбивкой на страницы в Power BI. В этом разделе перечислены наиболее распространенные параметры. Параметры не учитывают регистр и начинаются с префикса параметра  `rdl:` , если они связаны с выходным форматом.  

### <a name="report-commands-rdl"></a>Команды отчета (`rdl:`) 

**Формат экспорта** — задает формат отображения и экспорта отчета.

Пример: rdl:format=PDF

Доступные значения:
 
- PPTX (PowerPoint)
- MHTML 
- ИЗОБРАЖЕНИЕ 
- EXCELOPENXML (EXCEL) 
- WORDOPENXML (WORD) 
- CSV 
- PDF 
- ACCESSIBLEPDF (PDF)
- XML 

**Представление отчета** указывает тип представления, используемого для отображения отчета.

-   rdl:reportView

    - "interactive" (по умолчанию): загружает отчет в интерактивном режиме.
    - "pageView": загружает отчет в режиме представления страницы.

**Панель параметров** определяет, будет ли панель параметров закрыта, открыта или полностью скрыта при загрузке отчета.

-   rdl:parameterPanel

    - collapsed — при загрузке отчета панель параметров закрыта. Пользователи могут развернуть панель, нажав кнопку.
    - hidden — при загрузке отчета панель параметров закрыта и кнопка неактивна.
    - expanded (по умолчанию) — при загрузке отчета панель параметров открыта и кнопка активна.

**Сведения об устройстве**. Можно указать дополнительные выходные параметры для следующих форматов экспорта. 

PDF / ACCESSIBLEPDF:

- rdl:AccessiblePDF=true/false
- rdl:Columns=целое число
- rdl:ColumnSpacing=десятичное число (дюймы)
- rdl:DpiX=целое число
- rdl:DpiY=целое число
- rdl:EndPage=целое число
- rdl:HumanReadablePDF=true/false
- rdl:MarginBottom=десятичное число (дюймы)
- rdl:MarginLeft=десятичное число (дюймы)
- rdl:MarginRight=десятичное число (дюймы)
- rdl:MarginTop=десятичное число (дюймы)
- rdl:PageHeight=десятичное число (дюймы)
- rdl:PageWidth=десятичное число (дюймы)
    - rdl:StartPage=целое число
    
CSV:

- rdl:Encoding=строка
- rdl:ExcelMode=true/false
- rdl:FieldDelimiter=строка
- rdl:NoHeader=true/false
- rdl:Qualifier=строка
- rdl:RecordDelimiter=строка
- rdl:SuppressLineBreaks=true/false
    - rdl:UseFormattedValues=true/false
    
WORDOPENXML (WORD):

- rdl:AutoFit=строка -> True/False/Never/Default
- rdl:ExpandToggles=true/false
- rdl:FixedPageWidth=true/false
- rdl:OmitHyperlinks=true/false
- rdl:OmitDrillthroughs=true/false

EXCELOPENXML (EXCEL):

- rdl:OmitDocumentMap=true/false
- rdl:OmitFormulas=true/false
    - rdl:SimplePageHeaders=true/false
    
PPTX (PowerPoint):
 
- rdl:Columns=целое число
- rdl:ColumnSpacing=десятичное число (дюймы)
- rdl:DpiX=целое число
- rdl:DpiY=целое число
- rdl:EndPage=целое число
- rdl:MarginBottom=десятичное число (дюймы)
- rdl:MarginLeft=десятичное число (дюймы)
- rdl:MarginRight=десятичное число (дюймы)
- rdl:MarginTop=десятичное число (дюймы)
- rdl:PageHeight=десятичное число (дюймы)
- rdl:PageWidth=десятичное число (дюймы)
- rdl:StartPage=целое число
    - rdl:UseReportPageSize=true/false

XML:

- rdl:UseFormattedValues=true/false
- rdl:Indented=true/false
- rdl:OmitNamespace=true/false
- rdl:OmitSchema=true/false
- rdl:Encoding=строка
- rdl:Schema=true/false

**Открыть гиперссылку в том же окне браузера** Добавьте "rdl:targetSameWindow=true" в URL-адрес гиперссылки в отчете, чтобы служба Power BI открывала эту гиперссылку в том же окне браузера. Сведения о добавлении гиперссылок в отчет см. в статье [Добавление гиперссылки на URL-адрес](/sql/reporting-services/report-design/add-a-hyperlink-to-a-url-report-builder-and-ssrs) в документации по SQL Server Reporting Services.

## <a name="next-steps"></a>Дальнейшие действия

- [Передача параметра отчета в URL-адресе для отчета с разбивкой на страницы в Power BI](report-builder-url-pass-parameters.md)
- [Сведения об отчетах с разбивкой на страницы в Power BI Premium](paginated-reports-report-builder-power-bi.md)
