---
title: Свойства набора данных Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Дополнительные сведения о свойствах API набора данных Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 06/08/2018
ms.openlocfilehash: b4bd173c2f3730a0a6082214afbfdf5760048102
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887691"
---
# <a name="dataset-properties"></a>Свойства набора данных

В текущей версии 1 API набора данных можно создать только набор данных с именем и коллекцией таблиц. У каждой таблицы есть имя и коллекция объектов столбцов. У каждого столбца есть имя и тип данных. Мы существенно расширяем возможности соответствующих свойств главным образом за счет поддержки мер и связей между таблицами. Ниже приведен полный список свойств, поддерживаемых в этом выпуске.

> [!IMPORTANT]
> Он доступен на странице [Группы операций наборов данных](/rest/api/power-bi/datasets).

## <a name="dataset"></a>Набор данных

Имя  |Тип  |Описание  |Только для чтения  |Обязательно
---------|---------|---------|---------|---------
идентификатор     |  Guid       | Системный идентификатор набора данных.        | Верно        | Неверно        
name     | Строка        | Определяемое пользователем имя набора данных.        | False        | Да        
таблицы     | Table[]        | Коллекция таблиц.        |  False       | False        
relationships     | Relationship[]        | Коллекция связей между таблицами.        | False        |  False  
defaultMode     | Строка        | Определяет действие, выполняемое с набором данных, — отправка или передача в потоковом режиме (или и то и другое). Значения: "Push" и "Streaming".         | False        |  False

## <a name="table"></a>Таблица

Имя  |Тип  |Описание  |Только для чтения  |Обязательно
---------|---------|---------|---------|---------
name     | Строка        |  Определяемое пользователем имя таблицы. Также может использоваться в качестве ее идентификатора.       | False        |  Да       
столбцы     |  column[]       |  Коллекция столбцов.       | False        |  Да       
measures     | measure[]        |  Коллекция мер.       | False        |  False       
isHidden     | Логическое        | Если это свойство имеет значение true, таблица скрыта в клиентских средствах.        | False        | False        

## <a name="column"></a>Столбец

Имя  |Тип  |Описание  |Только для чтения  |Обязательно
---------|---------|---------|---------|---------
name     |  Строка        | Определяемое пользователем имя столбца.        |  False       | Да       
dataType     |  Строка       |  Поддерживаемые [типы данных EDM](/dotnet/framework/data/adonet/entity-data-model-primitive-data-types) и ограничения. См. раздел [Ограничения типов данных](#data-type-restrictions).      |  False       | Да        
formatString     | Строка        | Строка, описывающая формат отображаемого значения. Сведения о форматах строк см. в разделе [Содержимое FORMAT_STRING](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents).      | False        | False        
sortByColumn    | Строка        |   Строка, представляющая собой название столбца в той же таблице, который нужно использовать для сортировки текущего столбца.     | False        | False       
dataCategory     | Строка        |  Строковое значение, которое следует использовать в качестве категории данных, описывающей данные в столбце. Вот несколько типичных значений: Address, City, Continent, Country, Image, ImageUrl, Latitude, Longitude, Organization, Place, PostalCode, StateOrProvince, WebUrl       |  False       | False        
isHidden    |  Логическое       |  Свойство, указывающее, является ли столбец скрытым. Значение по умолчанию — false.       | False        | False        
summarizeBy     | Строка        |  Метод агрегирования по умолчанию для столбца. Доступны следующие значения: default, none, sum, min, max, count, average, distinctCount     |  False       | False

## <a name="measure"></a>Мера

Имя  |Тип  |Описание  |Только для чтения  |Обязательно
---------|---------|---------|---------|---------
name     | Строка        |  Определяемое пользователем имя меры.       |  False       | Да        
expression     | Строка        | Допустимое выражение DAX.        | False        |  Да       
formatString     | Строка        |  Строка, описывающая формат отображаемого значения. Сведения о форматах строк см. в разделе [Содержимое FORMAT_STRING](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents).       | False        | False        
isHidden     | Строка        |  Если это свойство имеет значение true, таблица скрыта в клиентских средствах.       |  False       | False       

## <a name="relationship"></a>Relationship

Имя  |Тип  |Описание  |Только для чтения  |Обязательно 
---------|---------|---------|---------|---------
name     | Строка        | Определяемое пользователем имя связи. Также может использоваться в качестве ее идентификатора.        | False       | Да        
crossFilteringBehavior     | Строка        |    Направление фильтрации связи: OneDirection (по умолчанию), BothDirections, Automatic       | False        | False        
fromTable     | Строка        | Имя таблицы внешнего ключа.        | False        | Да         
fromColumn    | Строка        | Имя столбца внешнего ключа.        | False        | Да         
toTable    | Строка        | Имя таблицы первичного ключа.        | False        | Да         
toColumn     | Строка        | Имя столбца первичного ключа.        | False        | Да        

## <a name="data-type-restrictions"></a>Ограничения типов данных

Эти ограничения относятся только к свойству dataType.

Тип данных  |Ограничения  
---------|---------
Int64     |   Int64.MaxValue и Int64.MinValue не допускаются.      
Double     |  Значения Double.MaxValue и Double.MinValue не допускается. NaN не поддерживается. В некоторых функциях не поддерживаются +Infinity и -Infinity (например, Min, Max).       
Логическое     |   Верно или неверно.
Datetime    |   Во время загрузки данных мы квантуем значения с частями суток на целые значения, кратные 1/300 секунды (3,33 мс).      
Строка     |  Текущее ограничение длины строкового значения: 4000 символов.
Decimal|точность = 28, шкала = 4

## <a name="example"></a>Пример
В приведенном ниже коде продемонстрированы некоторые из этих свойств.

```json
{

  "name": "PushAdvanced",

  "tables": [

    {

      "name": "Date",

      "columns": [

        {

          "name": "Date",

          "dataType": "dateTime",

          "formatString": "dddd\\, mmmm d\\, yyyy",

          "summarizeBy": "none"

        }

      ]

    },

    {

      "name": "sales",

      "columns": [

        {

          "name": "Date",

          "dataType": "dateTime",

          "formatString": "dddd\\, mmmm d\\, yyyy",

          "summarizeBy": "none"

        },

        {

          "name": "Sales",

          "dataType": "int64",

          "formatString": "0",

          "summarizeBy": "sum"

        }

      ],

      "measures": [

        {

          "name": "percent to forecast",

          "expression": "SUM(sales[Sales])/SUM(forecast[forecast])",

          "formatString": "0.00 %;-0.00 %;0.00 %"

        }

      ]

    },

    {

      "name": "forecast",

      "columns": [

        {

          "name": "date",

          "dataType": "dateTime",

          "formatString": "m/d/yyyy",

          "summarizeBy": "none"

        },

        {

          "name": "forecast",

          "dataType": "int64",

          "formatString": "0",

          "summarizeBy": "sum"

        }

      ]

    }

  ],

  "relationships": [

    {

      "name": "2ea345ce-b147-436e-8ac2-9d3c4d82af8d",

      "fromTable": "sales",

      "fromColumn": "Date",

      "toTable": "Date",

      "toColumn": "Date",

      "crossFilteringBehavior": "bothDirections"

    },

    {

      "name": "5d95f419-e589-4345-9581-6e70670b1bba",

      "fromTable": "forecast",

      "fromColumn": "date",

      "toTable": "Date",

      "toColumn": "Date",

      "crossFilteringBehavior": "bothDirections"

    }

  ]

}
```