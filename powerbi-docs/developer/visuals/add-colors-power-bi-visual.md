---
title: Добавление цветов в визуальные элементы Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, как добавлять цвета в визуальные элементы Power BI? и как управлять точками данных для визуального элемента с цветом. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 03/27/2020
ms.openlocfilehash: e6b6fb1dbc1397b93ac12692c8610e6f36d0b8bf
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887990"
---
# <a name="add-colors-to-your-power-bi-visuals"></a>Добавление цветов в визуальные элементы службы Power BI

В этой статье описывается, как добавить цвета в визуальные элементы и как управлять точками данных для визуального элемента цвета.

`IVisualHost` выставляет цвет в качестве одной из своих служб.
В примере кода в этой статье изменяется [визуальный элемент SampleBarChart](https://github.com/microsoft/PowerBI-visuals-sampleBarChart).
Исходный код см. в разделе файле [barChart.ts](https://github.com/microsoft/PowerBI-visuals-sampleBarChart/blob/master/src/barChart.ts).

Чтобы приступить к созданию визуализаций, см. руководство [Разработка визуализации "Круговая карточка" в Power BI](develop-circle-card.md).

## <a name="add-color-to-data-points"></a>Добавление цвета к точкам данных

Каждая точка данных представляется другим цветом.
Добавьте цвет в интерфейс `BarChartDataPoint`, как показано в следующем примере:

```typescript
/**
 * Interface for BarChart data points.
 *
 * @interface
 * @property {number} value    - Data value for point.
 * @property {string} category - Corresponding category of data value.
 * @property {string} color    - Color corresponding to data point.
 */
interface BarChartDataPoint {
    value: number;
    category: string;
    color: string;
};
```

## <a name="use-the-color-palette-service"></a>Использование службы цветовой палитры

Служба `colorPalette` управляет цветами, используемыми в визуальном элементе.
Экземпляр службы доступен на `IVisualHost`.

Определите его в методе `update`.

```typescript
constructor(options: VisualConstructorOptions) {
        this.host = options.host; // host: IVisualHost
        ...
    }

public update(options: VisualUpdateOptions) {

    let colorPalette: IColorPalette = host.colorPalette;
    ...
}
```

## <a name="assigning-color-to-data-points"></a>Назначение цвета точкам данных

Затем укажите `dataPoints`.
В этом примере каждая из `dataPoints` включает значение, категорию и цвет.
`dataPoints` может также включать другие свойства.

В `SampleBarChart` метод `visualTransform` инкапсулирует вычисление `dataPoints`.
Этот метод является частью линейчатой диаграммы viewmodel.
Поскольку метод выполняет итерацию через вычисление `dataPoints` в `visualTransform`, это идеальное место для назначения цветов, как показано в следующем коде:

```typescript

public update(options: VisualUpdateOptions) {
    ....
    let viewModel: BarChartViewModel = visualTransform(options, this.host);
    ....
}

function visualTransform(options: VisualUpdateOptions, host: IVisualHost): BarChartViewModel {
    let colorPalette: IColorPalette = host.colorPalette; // host: IVisualHost
    for (let i = 0, len = Math.max(category.values.length, dataValue.values.length); i < len; i++) {
        barChartDataPoints.push({
            category: category.values[i],
            value: dataValue.values[i],
            color: colorPalette.getColor(category.values[i]).value,
        });
    }
}
```

Затем примените данные из `dataPoints` в выбор [d3](https://d3js.org/) `barSelection` в методе `update`:

```typescript
// This code is actual for d3 v5
// in d3 v5 for this case we should use merge() after enter() and apply changes on barSelectionMerged
this.barSelection = this.barContainer
    .selectAll('.bar')
    .data(this.barDataPoints);

const barSelectionMerged = this.barSelection
    .enter()
    .append('rect')
    .merge(<any>this.barSelection);

barSelectionMerged.classed('bar', true);

barSelectionMerged
.attr("width", xScale.bandwidth())
.attr("height", d => height - yScale(<number>d.value))
.attr("y", d => yScale(<number>d.value))
.attr("x", d => xScale(d.category))
.style("fill", (dataPoint: BarChartDataPoint) => dataPoint.color)
.style("stroke", (dataPoint: BarChartDataPoint) => dataPoint.strokeColor)
.style("stroke-width", (dataPoint: BarChartDataPoint) => `${dataPoint.strokeWidth}px`);

this.barSelection
    .exit()
    .remove();
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о визуальных элементах Power BI см. в статье [Возможности и свойства визуальных элементов Power BI](capabilities.md).

Дополнительные сведения о разработке визуальных элементов Power BI см. в статьях [Отладка визуальных элементов Power BI](visuals-how-to-debug.md) и [Устранение неполадок визуальных элементов Power BI](power-bi-custom-visuals-troubleshoot.md).
