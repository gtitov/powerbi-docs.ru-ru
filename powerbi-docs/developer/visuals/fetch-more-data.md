---
title: Получение дополнительных данных из Power BI
description: В этой статье описывается включение сегментированного получения больших наборов данных для визуальных элементов Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 06/18/2019
ms.openlocfilehash: b8be5b68603f818e26e7f731e4f163bc626b5053
ms.sourcegitcommit: 132b3f6ba6d2b1948ddc15969d64cf629f7fb280
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "94483703"
---
# <a name="fetch-more-data-from-power-bi"></a>Получение дополнительных данных из Power BI

В этой статье описывается, как загрузить дополнительные данные, чтобы обойти установленное для точки данных ограничение в 30 КБ с помощью метода `fetchMoreData`. При таком подходе данные предоставляются в виде блоков. Чтобы повысить производительность, можно настроить размер блока в соответствии с конкретными требованиями.

## <a name="limitations-of-fetchmoredata"></a>Ограничения метода fetchMoreData

* Размер окна находится в диапазоне от 2 до 30 000.
* Общее число строк Dataview ограничено 1 048 576 строками.
* В режиме агрегирования сегментов размер памяти DataView ограничен 100 МБ.

## <a name="enable-a-segmented-fetch-of-large-datasets"></a>Включение сегментированного получения больших наборов данных

Для сегментного режима `dataview` определите размер окна для `dataReductionAlgorithm` в файле *capabilities.json* визуального элемента для требуемого `dataViewMapping`. `count` определяет размер окна, ограничивающий количество новых строк данных, добавляемых к `dataview` при каждом обновлении.

Добавьте следующий код в файл *capabilities.json*:

```typescript
"dataViewMappings": [
    {
        "table": {
            "rows": {
                "for": {
                    "in": "values"
                },
                "dataReductionAlgorithm": {
                    "window": {
                        "count": 100
                    }
                }
            }
    }
]
```

Новые сегменты добавляются к существующему `dataview` и предоставляются визуальному элементу в виде вызова `update`.

## <a name="usage-in-the-power-bi-visual"></a>Использование в визуальном элементе Power BI

В Power BI `fetchMoreData` можно использовать в режиме агрегирования сегментов по умолчанию или в режиме добавочных накоплений. 

### <a name="using-segments-aggregation-mode-default"></a>Использование режима агрегирования сегментов (по умолчанию)

В этом режиме DataView, предоставленный визуальному элементу, содержит накопленные данные для всех предыдущих `fetchMoreData requests`. Таким образом, размер DataView должен увеличиваться при каждом обновлении. Например, если ожидается всего 100 000 строк, а размер окна равен 10 000, то первое обновление DataView должно включать в себя 10 000 строк, второе обновление DataView должно включать 20 000 строк и т. д.

Для выбора этого режима следует вызвать `fetchMoreData` с `aggregateSegments = true`.

Чтобы определить, существуют ли данные, проверьте наличие `dataView.metadata.segment`.

```typescript
    public update(options: VisualUpdateOptions) {
        const dataView = options.dataViews[0];
        console.log(dataView.metadata.segment);
        // output: __proto__: Object
    }
```

С помощью `options.operationKind` вы также можете проверить, является ли это обновление первичным или очередным. В следующем коде `VisualDataChangeOperationKind.Create` ссылается на первый сегмент, а `VisualDataChangeOperationKind.Append` — на последующие сегменты.

Пример реализации см. в следующем фрагменте кода:

```typescript
// CV update implementation
public update(options: VisualUpdateOptions) {
    // indicates this is the first segment of new data.
    if (options.operationKind == VisualDataChangeOperationKind.Create) {

    }

    // on second or subsequent segments:
    if (options.operationKind == VisualDataChangeOperationKind.Append) {

    }

    // complete update implementation
}
```

Можно также вызвать метод `fetchMoreData` из обработчика событий пользовательского интерфейса, как показано ниже:

```typescript
btn_click(){
{
    // check if more data is expected for the current data view
    if (dataView.metadata.segment) {
        //request for more data if available; as a response, Power BI will call update method
        let request_accepted: bool = this.host.fetchMoreData(true);
        // handle rejection
        if (!request_accepted) {
            // for example, when the 100 MB limit has been reached
        }
    }
}
```

В ответ на вызов метода `this.host.fetchMoreData` Power BI вызывает метод `update` визуального элемента с новым сегментом данных.

> [!NOTE]
> Power BI ограничит общий объем получаемых данных значением 100 МБ, чтобы предотвратить нехватку памяти на клиенте. Когда будет достигнуто ограничение, метод `fetchMoreData()` возвратит `false`.

### <a name="using-incremental-updates-mode"></a>Использование режима добавочных обновлений

В этом режиме DataView, предоставленный визуальному элементу, содержит только добавочные данные. Таким образом, размер DataView не будет передавать определенный размер окна. Например, если ожидается всего 101 000 строк, а размер окна равен 10 000, то визуальный элемент будет получать 10 обновлений с размером DataView, равным 10 000, и одно обновление с размером DataView, равным 1000.

Для выбора этого режима следует вызвать `fetchMoreData` с `aggregateSegments = false`.

Чтобы определить, существуют ли данные, проверьте наличие `dataView.metadata.segment`.

```typescript
    public update(options: VisualUpdateOptions) {
        const dataView = options.dataViews[0];
        console.log(dataView.metadata.segment);
        // output: __proto__: Object
    }
```

С помощью `options.operationKind` вы также можете проверить, является ли это обновление первичным или очередным. В следующем коде `VisualDataChangeOperationKind.Create` ссылается на первый сегмент, а `VisualDataChangeOperationKind.Segment` — на последующие сегменты.

Пример реализации см. в следующем фрагменте кода:

```typescript
// CV update implementation
public update(options: VisualUpdateOptions) {
    // indicates this is the first segment of new data.
    if (options.operationKind == VisualDataChangeOperationKind.Create) {

    }

    // on second or subsequent segments:
    if (options.operationKind == VisualDataChangeOperationKind.Segment) {
        
    }

    // skip overlapping rows 
    const rowOffset = (dataView.table['lastMergeIndex'] === undefined) ? 0 : dataView.table['lastMergeIndex'] + 1;

    // Process incoming data
    for (var i = rowOffset; i < dataView.table.rows.length; i++) {
        var val = <number>(dataView.table.rows[i][0]); // Pick first column               
            
     }
     
    // complete update implementation
}
```

Можно также вызвать метод `fetchMoreData` из обработчика событий пользовательского интерфейса, как показано ниже:

```typescript
btn_click(){
{
    // check if more data is expected for the current data view
    if (dataView.metadata.segment) {
        //request for more data if available; as a response, Power BI will call update method
        let request_accepted: bool = this.host.fetchMoreData(false);
        // handle rejection
        if (!request_accepted) {
            // for example, when the 100 MB limit has been reached
        }
    }
}
```

В ответ на вызов метода `this.host.fetchMoreData` Power BI вызывает метод `update` визуального элемента с новым сегментом данных.

> [!NOTE]
> Несмотря на то что данные DataView в разных обновлениях являются в основном исключительными, последующие DataView будут частично перекрываться.
> Для сопоставления табличных и категориальных данных предполагается, что первые N строк DataView будут содержать данные, скопированные из предыдущего DataView.
> N можно определить следующим образом: `(dataView.table['lastMergeIndex'] === undefined) ? 0 : dataView.table['lastMergeIndex'] + 1`