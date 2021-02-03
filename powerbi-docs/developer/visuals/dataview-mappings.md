---
title: Общие сведения о сопоставлении представлений данных в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, каким образом служба Power BI преобразует данные, прежде чем передавать их в визуальные элементы. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 01/28/2021
ms.openlocfilehash: 0dca634769a7b2779d3ee4168dc2c37f1c33bd9c
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99043167"
---
# <a name="understand-data-view-mapping-in-power-bi-visuals"></a>Общие сведения о сопоставлениях представлений данных в визуальных элементах Power BI

В этой статье рассматриваются представления данных и описывается связь между ролями данных, что позволяет указывать для них условные требования. В этой статье также описываются все типы `dataMappings`.

Каждое допустимое сопоставление создает представление данных, но в настоящее время поддерживается выполнение только одного запроса для одного визуального элемента. Обычно получается только одно представление данных. Однако можно указать несколько сопоставлений данных с разными условиями, что разрешено:

```json
"dataViewMappings": [
    {
        "conditions": [ ... ],
        "categorical": { ... },
        "single": { ... },
        "table": { ... },
        "matrix": { ... }
    }
]
```

Power BI создает сопоставление с представлением данных только в том случае, если допустимое сопоставление указано в `dataViewMappings`.

Иными словами, `categorical` может быть определено в `dataViewMappings`, однако другие сопоставления, такие как `table` или `single`, могут быть не определены. Например:

```json
"dataViewMappings": [
    {
        "categorical": { ... }
    }
]
```

Служба Power BI создает представление данных с одним сопоставлением `categorical`, но при этом `table` и другие сопоставления не определены:

```javascript
{
    "categorical": {
        "categories": [ ... ],
        "values": [ ... ]
    },
    "metadata": { ... }
}
```

## <a name="conditions"></a>Условия

В этом разделе описываются условия для определенного сопоставления данных. Можно предоставить несколько наборов условий, и, если данные совпадают с одним из описанных наборов, визуальный элемент примет данные как допустимые.

В настоящее время для каждого поля можно указать минимальное и максимальное значения. Они представляют количество полей, которые можно привязать к этой роли данных. 

> [!NOTE]
> Если роль данных в условии опущена, она может иметь любое количество полей.

### <a name="example-1"></a>Пример 1

В каждую роль данных можно перетащить несколько полей. В этом примере мы ограничим категорию одним полем данных, а меру — двумя.

```json
"conditions": [
    { "category": { "max": 1 }, "y": { "max": 2 } },
]
```

### <a name="example-2"></a>Пример 2

В этом примере требуется соблюдение любого из двух условий:
* Точно одно поле данных категории и точно две меры.
* Точно две категории и точно одна мера.

```json
"conditions": [
    { "category": { "min": 1, "max": 1 }, "measure": { "min": 2, "max": 2 } },
    { "category": { "min": 2, "max": 2 }, "measure": { "min": 1, "max": 1 } }
]
```

## <a name="single-data-mapping"></a>Одиночное сопоставление данных

Одиночное сопоставление данных — это простейшая форма сопоставления данных. Оно принимает одно поле меры и выдает итог. Если поле является числовым, то выдается сумма. В противном случае выдается количество уникальных значений.

Чтобы использовать одиночное сопоставление данных, нужно определить имя роли данных, которую требуется сопоставить. Это сопоставление работает только с одним полем меры. Если присвоено второе поле, представление данных не будет создаваться. В связи с этим рекомендуется включать условие, которое будет ограничивать данные одним полем.

> [!NOTE]
> Это сопоставление данных невозможно использовать совместно с любым другим сопоставлением данных. Оно предназначено для сокращения данных до одного числового значения.

### <a name="example-3"></a>Пример 3

```json
{
    "dataRoles": [
        {
            "displayName": "Y",
            "name": "Y",
            "kind": "Measure"
        }
    ],
    "dataViewMappings": [
        {
            "conditions": [
                {
                    "Y": {
                        "max": 1
                    }
                }
            ],
            "single": {
                "role": "Y"
            }
        }
    ]
}
```

Итоговое представление данных по-прежнему содержит другие типы (табличные, категориальные и т. д.), но каждое сопоставление будет содержать только одно значение. Рекомендуется просто обращаться к значению по отдельности.

```JSON
{
    "dataView": [
        {
            "metadata": null,
            "categorical": null,
            "matrix": null,
            "table": null,
            "tree": null,
            "single": {
                "value": 94163140.3560001
            }
        }
    ]
}
```

Пример кода для обработки простого сопоставления представления данных

```typescript
"use strict";
import powerbi from "powerbi-visuals-api";
import DataView = powerbi.DataView;
import DataViewSingle = powerbi.DataViewSingle;
// standart imports
// ...

export class Visual implements IVisual {
    private target: HTMLElement;
    private host: IVisualHost;
    private valueText: HTMLParagraphElement;

    constructor(options: VisualConstructorOptions) {
        // constructor body
        this.target = options.element;
        this.host = options.host;
        this.valueText = document.createElement("p");
        this.target.appendChild(this.valueText);
        // ...
    }

    public update(options: VisualUpdateOptions) {
        const dataView: DataView = options.dataViews[0];
        const singleDataView: DataViewSingle = dataView.single;

        if (!singleDataView ||
            !singleDataView.value ) {
            return
        }

        this.valueText.innerText = singleDataView.value.toString();
    }
}
```

В результате в визуальном элементе отображается одно значение из Power BI:

![Пример визуального элемента с одним сопоставлением представления данных](media/dataview-mappings/visual-simple-dataview-mapping.png)

## <a name="categorical-data-mapping"></a>Категориальное сопоставление данных

Категориальное сопоставление данных используется для получения одного или двух независимых группирований данных.

### <a name="example-4"></a>Пример 4

Ниже приведено определение из нашего предыдущего примера для ролей данных:

```json
"dataRole":[
    {
        "displayName": "Category",
        "name": "category",
        "kind": "Grouping"
    },
    {
        "displayName": "Y Axis",
        "name": "measure",
        "kind": "Measure"
    }
]
```

А теперь для сопоставления:

```json
"dataViewMappings": {
    "categorical": {
        "categories": {
            "for": { "in": "category" }
        },
        "values": {
            "select": [
                { "bind": { "to": "measure" } }
            ]
        }
    }
}
```

Это простой пример. В общем виде он означает следующее: "сопоставить мою роль данных `category`, чтобы для каждого поля, которое я перетаскиваю в `category`, его данные сопоставлялись с `categorical.categories`. Кроме того, сопоставить мою роль данных `measure` с `categorical.values`".

* **for...in** — включение всех элементов в этой роли данных в запрос данных.
* **bind...to** — дает тот же результат, что и *for...in*, но ожидает, что роль данных будет иметь условие, ограничивающее его до одного поля.

### <a name="example-5"></a>Пример 5

В этом примере мы будем использовать две первых роли данных из предыдущего примера, а также дополнительно определим `grouping` и `measure2`.

```json
"dataRole":[
    {
        "displayName": "Category",
        "name": "category",
        "kind": "Grouping"
    },
    {
        "displayName": "Y Axis",
        "name": "measure",
        "kind": "Measure"
    },
    {
        "displayName": "Grouping with",
        "name": "grouping",
        "kind": "Grouping"
    },
    {
        "displayName": "X Axis",
        "name": "measure2",
        "kind": "Grouping"
    }
]
```

А теперь для сопоставления:

```json
"dataViewMappings":{
    "categorical": {
        "categories": {
            "for": { "in": "category" }
        },
        "values": {
            "group": {
                "by": "grouping",
                "select":[
                    { "bind": { "to": "measure" } },
                    { "bind": { "to": "measure2" } }
                ]
            }
        }
    }
}
```

Разница заключается в том, как мы сопоставляем categorical.values. Мы предписываем: "сопоставить мои роли данных `measure` и `measure2` для группирования по роли данных `grouping`".

### <a name="example-6"></a>Пример 6

Вот эти роли данных:

```json
"dataRoles": [
    {
        "displayName": "Categories",
        "name": "category",
        "kind": "Grouping"
    },
    {
        "displayName": "Measures",
        "name": "measure",
        "kind": "Measure"
    },
    {
        "displayName": "Series",
        "name": "series",
        "kind": "Measure"
    }
]
```

Это сопоставление представления данных:

```json
"dataViewMappings": [
    {
        "categorical": {
            "categories": {
                "for": {
                    "in": "category"
                }
            },
            "values": {
                "group": {
                    "by": "series",
                    "select": [{
                            "for": {
                                "in": "measure"
                            }
                        }
                    ]
                }
            }
        }
    }
]
```

Категориальное представление данных можно визуализировать указанным образом:

| Страна или регион | 2013 | 2014 | 2015 | 2016 |
|---------|------|------|------|------|
| США | x | x | 650 | 350 |
| Canada | x | 630 | 490 | x |
| Мексика | 645 | x | x | x |
| Великобритания | x | x | 831 | x |


Служба Power BI создает его как категориальное представление данных. Это набор категорий.

```JSON
{
    "categorical": {
        "categories": [
            {
                "source": {...},
                "values": [
                    "Canada",
                    "USA",
                    "UK",
                    "Mexico"
                ],
                "identity": [...],
                "identityFields": [...],
            }
        ]
    }
}
```

Каждая категория также сопоставляется с набором значений. Каждое из этих значений сгруппировано по рядам, то есть по годам.

Например, каждый массив `values` представляет данные за каждый год.
Кроме того, каждый массив `values` имеет 4 значения для Канады, США, Великобритании и Мексики соответственно:

```JSON
{
    "values": [
        // Values for 2013 year
        {
            "source": {...},
            "values": [
                null, // Value for `Canada` category
                null, // Value for `USA` category
                null, // Value for `UK` category
                645 // Value for `Mexico` category
            ],
            "identity": [...],
        },
        // Values for 2014 year
        {
            "source": {...},
            "values": [
                630, // Value for `Canada` category
                null, // Value for `USA` category
                null, // Value for `UK` category
                null // Value for `Mexico` category
            ],
            "identity": [...],
        },
        // Values for 2015 year
        {
            "source": {...},
            "values": [
                490, // Value for `Canada` category
                650, // Value for `USA` category
                831, // Value for `UK` category
                null // Value for `Mexico` category
            ],
            "identity": [...],
        },
        // Values for 2016 year
        {
            "source": {...},
            "values": [
                null, // Value for `Canada` category
                350, // Value for `USA` category
                null, // Value for `UK` category
                null // Value for `Mexico` category
            ],
            "identity": [...],
        }
    ]
}
```

Пример кода для обработки сопоставления представления категориальных данных описывается ниже. В примере создается иерархическая структура `Country => Year => Value`.

```typescript
"use strict";
import powerbi from "powerbi-visuals-api";
import DataView = powerbi.DataView;
import DataViewCategorical = powerbi.DataViewCategorical;
import DataViewValueColumnGroup = powerbi.DataViewValueColumnGroup;
import PrimitiveValue = powerbi.PrimitiveValue;
// standart imports
// ...

export class Visual implements IVisual {
    private target: HTMLElement;
    private host: IVisualHost;
    private categories: HTMLElement;

    constructor(options: VisualConstructorOptions) {
        // constructor body
        this.target = options.element;
        this.host = options.host;
        this.categories = document.createElement("pre");
        this.target.appendChild(this.categories);
        // ...
    }

    public update(options: VisualUpdateOptions) {
        const dataView: DataView = options.dataViews[0];
        const categoricalDataView: DataViewCategorical = dataView.categorical;

        if (!categoricalDataView ||
            !categoricalDataView.categories ||
            !categoricalDataView.categories[0] ||
            !categoricalDataView.values) {
            return;
        }

        // Categories have only one column in data buckets
        // If you want to support several columns of categories data bucket, you should iterate categoricalDataView.categories array.
        const categoryFieldIndex = 0;
        // Measure has only one column in data buckets.
        // If you want to support several columns on data bucket, you should iterate years.values array in map function
        const measureFieldIndex = 0;
        let categories: PrimitiveValue[] = categoricalDataView.categories[categoryFieldIndex].values;
        let values: DataViewValueColumnGroup[] = categoricalDataView.values.grouped();

        let data = {};
        // iterate categories/countries
        categories.map((category: PrimitiveValue, categoryIndex: number) => {
            data[category.toString()] = {};
            // iterate series/years
            values.map((years: DataViewValueColumnGroup) => {
                if (!data[category.toString()][years.name] && years.values[measureFieldIndex].values[categoryIndex]) {
                    data[category.toString()][years.name] = []
                }
                if (years.values[0].values[categoryIndex]) {
                    data[category.toString()][years.name].push(years.values[measureFieldIndex].values[categoryIndex]);
                }
            });
        });

        this.categories.innerText = JSON.stringify(data, null, 6);
        console.log(data);
    }
}
```

Результат визуального элемента:

![Визуальный элемент с сопоставлением представления категориальных данных](media/dataview-mappings/categorical-data-view-mapping-visual.png)

## <a name="table-data-mapping"></a>Сопоставление табличных данных

Представление табличных данных — это простое сопоставление данных. По сути, это список точек данных, где можно агрегировать точки числовых данных.

### <a name="example-7"></a>Пример 7

Учитывая доступные возможности:

```json
"dataRoles": [
    {
        "displayName": "Column",
        "name": "column",
        "kind": "Grouping"
    },
    {
        "displayName": "Value",
        "name": "value",
        "kind": "Measure"
    }
]
```

```json
"dataViewMappings": [
    {
        "table": {
            "rows": {
                "select": [
                    {
                        "for": {
                            "in": "column"
                        }
                    },
                    {
                        "for": {
                            "in": "value"
                        }
                    }
                ]
            }
        }
    }
]
```

Представление табличных данных можно визуализировать следующим образом:  

Пример данных:

| Страна или регион| Year; | Sales |
|-----|-----|------|
| США | 2016 | 100 |
| США | 2015 | 50 |
| Canada | 2015 | 200 |
| Canada | 2015 | 50 |
| Мексика | 2013 | 300 |
| Великобритания | 2014 | 150 |
| США | 2015 | 75 |

Привязка данных:

![Привязки данных в сопоставлении представления табличных данных](media/dataview-mappings/table-dataview-mapping-data.png)

Служба Power BI отображает данные в представлении табличных данных. Изначально предполагать, что данные упорядочены, не следует.

```JSON
{
    "table" : {
        "columns": [...],
        "rows": [
            [
                "Canada",
                2014,
                630
            ],
            [
                "Canada",
                2015,
                490
            ],
            [
                "Mexico",
                2013,
                645
            ],
            [
                "UK",
                2014,
                831
            ],
            [
                "USA",
                2015,
                650
            ],
            [
                "USA",
                2016,
                350
            ]
        ]
    }
}
```

Вы можете выполнить статистическую обработку данных, выбрав нужное поле и затем указав операцию суммирования.  

![Агрегация данных](media/dataview-mappings/data-aggregation.png)

Пример кода для обработки сопоставления представления табличных данных.

```typescript
"use strict";
import "./../style/visual.less";
import powerbi from "powerbi-visuals-api";
// ...
import DataViewMetadataColumn = powerbi.DataViewMetadataColumn;
import DataViewTable = powerbi.DataViewTable;
import DataViewTableRow = powerbi.DataViewTableRow;
import PrimitiveValue = powerbi.PrimitiveValue;
// other imports
// ...

export class Visual implements IVisual {
    private target: HTMLElement;
    private host: IVisualHost;
    private table: HTMLParagraphElement;

    constructor(options: VisualConstructorOptions) {
        // constructor body
        this.target = options.element;
        this.host = options.host;
        this.table = document.createElement("table");
        this.target.appendChild(this.table);
        // ...
    }

    public update(options: VisualUpdateOptions) {
        const dataView: DataView = options.dataViews[0];
        const tableDataView: DataViewTable = dataView.table;

        if (!tableDataView) {
            return
        }
        while(this.table.firstChild) {
            this.table.removeChild(this.table.firstChild);
        }

        //draw header
        const tableHeader = document.createElement("th");
        tableDataView.columns.forEach((column: DataViewMetadataColumn) => {
            const tableHeaderColumn = document.createElement("td");
            tableHeaderColumn.innerText = column.displayName
            tableHeader.appendChild(tableHeaderColumn);
        });
        this.table.appendChild(tableHeader);

        //draw rows
        tableDataView.rows.forEach((row: DataViewTableRow) => {
            const tableRow = document.createElement("tr");
            row.forEach((columnValue: PrimitiveValue) => {
                const cell = document.createElement("td");
                cell.innerText = columnValue.toString();
                tableRow.appendChild(cell);
            })
            this.table.appendChild(tableRow);
        });
    }
}
```

Файл стилей визуальных элементов `style/visual.less` содержит макет для таблицы:

```less
table {
    display: flex;
    flex-direction: column;
}

tr, th {
    display: flex;
    flex: 1;
}

td {
    flex: 1;
    border: 1px solid black;
}
```

![Визуальный элемент с сопоставлением представления табличных данных](media/dataview-mappings/table-dataview-mapping-visual.png)

## <a name="matrix-data-mapping"></a>Сопоставление матричных данных

Сопоставление матричных данных похоже на сопоставление табличных данных, однако строки в нем представляются иерархически. Кроме того, любое из значений роли данных можно использовать в качестве заголовка столбца.

```json
{
    "dataRoles": [
        {
            "name": "Category",
            "displayName": "Category",
            "displayNameKey": "Visual_Category",
            "kind": "Grouping"
        },
        {
            "name": "Column",
            "displayName": "Column",
            "displayNameKey": "Visual_Column",
            "kind": "Grouping"
        },
        {
            "name": "Measure",
            "displayName": "Measure",
            "displayNameKey": "Visual_Values",
            "kind": "Measure"
        }
    ],
    "dataViewMappings": [
        {
            "matrix": {
                "rows": {
                    "for": {
                        "in": "Category"
                    }
                },
                "columns": {
                    "for": {
                        "in": "Column"
                    }
                },
                "values": {
                    "select": [
                        {
                            "for": {
                                "in": "Measure"
                            }
                        }
                    ]
                }
            }
        }
    ]
}
```

Служба Power BI создает иерархическую структуру данных. Корневой элемент иерархии дерева включает данные из столбца **Parents** (Родители) роли данных `Category` и столбца **Children** (Дети) табличной роли данных.

Набор данных:

| Parents | Дети | Grandchildren | Столбцы | Значения |
|-----|-----|------|-------|-------|
| Parent1 | Child1 | Grand child1 | Col1 | 5 |
| Parent1 | Child1 | Grand child1 | Col2 | 6 |
| Parent1 | Child1 | Grand child2 | Col1 | 7 |
| Parent1 | Child1 | Grand child2 | Col2 | 8 |
| Parent1 | Child2 | Grand child3 | Col1 | 5 |
| Parent1 | Child2 | Grand child3 | Col2 | 3 |
| Parent1 | Child2 | Grand child4 | Col1 | 4 |
| Parent1 | Child2 | Grand child4 | Col2 | 9 |
| Parent1 | Child2 | Grand child5 | Col1 | 3 |
| Parent1 | Child2 | Grand child5 | Col2 | 5 |
| Parent2 | Child3 | Grand child6 | Col1 | 1 |
| Parent2 | Child3 | Grand child6 | Col2 | 2 |
| Parent2 | Child3 | Grand child7 | Col1 | 7 |
| Parent2 | Child3 | Grand child7 | Col2 | 1 |
| Parent2 | Child3 | Grand child8 | Col1 | 10 |
| Parent2 | Child3 | Grand child8 | Col2 | 13 |

Базовый визуальный элемент матрицы Power BI отрисовывает данные как таблицу.

![Визуальный элемент матрицы](media/dataview-mappings/matrix-visual-smaple.png)

Визуальный элемент получает структуру данных, как описывается в следующем коде (здесь показаны только две первые строки таблицы):

```json
{
    "metadata": {...},
    "matrix": {
        "rows": {
            "levels": [...],
            "root": {
                "childIdentityFields": [...],
                "children": [
                    {
                        "level": 0,
                        "levelValues": [...],
                        "value": "Parent1",
                        "identity": {...},
                        "childIdentityFields": [...],
                        "children": [
                            {
                                "level": 1,
                                "levelValues": [...],
                                "value": "Child1",
                                "identity": {...},
                                "childIdentityFields": [...],
                                "children": [
                                    {
                                        "level": 2,
                                        "levelValues": [...],
                                        "value": "Grand child1",
                                        "identity": {...},
                                        "values": {
                                            "0": {
                                                "value": 5 // value for Col1
                                            },
                                            "1": {
                                                "value": 6 // value for Col2
                                            }
                                        }
                                    },
                                    ...
                                ]
                            },
                            ...
                        ]
                    },
                    ...
                ]
            }
        },
        "columns": {
            "levels": [...],
            "root": {
                "childIdentityFields": [...],
                "children": [
                    {
                        "level": 0,
                        "levelValues": [...],
                        "value": "Col1",
                        "identity": {...}
                    },
                    {
                        "level": 0,
                        "levelValues": [...],
                        "value": "Col2",
                        "identity": {...}
                    },
                    ...
                ]
            }
        },
        "valueSources": [...]
    }
}
```

## <a name="data-reduction-algorithm"></a>Алгоритм сокращения данных

Чтобы контролировать объем данных, получаемых представлением, можно применить алгоритм сокращения данных.

По умолчанию для всех визуальных элементов Power BI применяется верхний алгоритм сокращения данных, для которого задано значение *count* в 1000 точек данных. Это эквивалентно установке следующих свойств в файле *capabilities.json*:

```json
"dataReductionAlgorithm": {
    "top": {
        "count": 1000
    }
}
```

Вы можете изменить параметр *count* на любое целое значение не более 30 000. Визуальные элементы Power BI на основе R могут поддерживать до 150 000 строк.

## <a name="data-reduction-algorithm-types"></a>Типы алгоритмов для сокращения данных

Предусмотрено четыре типа параметров для алгоритма сокращения данных:

* `top`: если требуется ограничить данные значениями, взятыми из верхней части набора данных. Из набора данных будут взяты первые *count* значений.
* `bottom`: если требуется ограничить данные значениями, взятыми из нижней части набора данных. Из набора данных будут взяты последние "count" значений.
* `sample`: сокращение набора данных с помощью простого алгоритма выборки, ограниченного количеством элементов (*count*). Это означает, что включаются первый и последний элементы, а элементы в количестве *count* располагаются между ними с равными интервалами.
Например, если получен набор данных [0, 1, 2, ... 100] и *count* равно 9, вы получите значения [0, 10, 20 ... 100].
* `window`: загружает одно *окно* точек данных за раз, содержащее определенное число (*count*) элементов. На данный момент `top` и `window` эквивалентны. Сейчас мы работаем над тем, чтобы обеспечить полноценную поддержку настройки окон.

## <a name="data-reduction-algorithm-usage"></a>Использование алгоритма сокращения данных

Алгоритм сокращения данных можно использовать в сопоставлениях представлений категориальных, табличных или матричных данных.

Этот алгоритм можно задать в `categories` и (или) в разделе группы объекта `values` для категориального сопоставления данных.

### <a name="example-8"></a>Пример 8

```json
"dataViewMappings": {
    "categorical": {
        "categories": {
            "for": { "in": "category" },
            "dataReductionAlgorithm": {
                "window": {
                    "count": 300
                }
            }  
        },
        "values": {
            "group": {
                "by": "series",
                "select": [{
                        "for": {
                            "in": "measure"
                        }
                    }
                ],
                "dataReductionAlgorithm": {
                    "top": {
                        "count": 100
                    }
                }  
            }
        }
    }
}
```

Алгоритм сокращения данных можно применить к разделу `rows` таблицы сопоставления представления данных.

### <a name="example-9"></a>Пример 9

```json
"dataViewMappings": [
    {
        "table": {
            "rows": {
                "for": {
                    "in": "values"
                },
                "dataReductionAlgorithm": {
                    "top": {
                        "count": 2000
                    }
                }
            }
        }
    }
]
```

Алгоритм сокращения данных можно применить к разделам `rows` и `columns` матрицы сопоставления представления данных.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как [добавить поддержку детализации для сопоставлений представлений данных в визуальных элементах Power BI](drill-down-support.md).
