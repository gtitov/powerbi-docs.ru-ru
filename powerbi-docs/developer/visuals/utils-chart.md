---
title: Общие сведения об использовании средств для создания диаграмм в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается использование средств диаграмм для рисования осей и условных обозначений в визуальном элементе Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
manager: rkarlin
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: 9094d639225eb82cbcf427346d1ad78943ddc90f
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887875"
---
# <a name="chart-utils"></a>Инструменты для диаграмм

ChartUtils — это набор интерфейсов и методов для создания осей, меток данных и условных обозначений в визуальных элементах Power BI.

## <a name="installation"></a>Установка

Чтобы установить пакет, выполните следующую команду в каталоге с текущим визуальным элементом:

```bash
npm install powerbi-visuals-utils-chartutils --save
```

## <a name="axis-helper"></a>Вспомогательный модуль для осей

Вспомогательный модуль для осей (объект `axis`) предоставляет функции, упрощающие работу с осью.

Этот модуль предоставляет следующие функции:

### <a name="getrecommendednumberofticksforxaxis"></a>getRecommendedNumberOfTicksForXAxis

Эта функция возвращает рекомендуемое число делений в соответствии с шириной диаграммы.

```typescript
function getRecommendedNumberOfTicksForXAxis(availableWidth: number): number;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...
axis.getRecommendedNumberOfTicksForXAxis(1024);

// returns: 8
```

### <a name="getrecommendednumberofticksforyaxis"></a>getRecommendedNumberOfTicksForYAxis

Эта функция возвращает рекомендуемое число делений в соответствии с высотой диаграммы.

```typescript
function getRecommendedNumberOfTicksForYAxis(availableWidth: number);
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...
axis.getRecommendedNumberOfTicksForYAxis(100);

// returns: 3
```

### <a name="getbestnumberofticks"></a>getBestNumberOfTicks

Возвращает оптимальное число делений в соответствии с минимальным значением, максимальным значением, а также метаданными и максимальным числом делений меры.

```typescript
function getBestNumberOfTicks(
  min: number,
  max: number,
  valuesMetadata: DataViewMetadataColumn[],
  maxTickCount: number,
  isDateTime?: boolean
): number;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...
var dataViewMetadataColumnWithIntegersOnly: powerbi.DataViewMetadataColumn[] = [
  {
    displayName: "col1",
    isMeasure: true,
    type: ValueType.fromDescriptor({ integer: true })
  },
  {
    displayName: "col2",
    isMeasure: true,
    type: ValueType.fromDescriptor({ integer: true })
  }
];
var actual = axis.getBestNumberOfTicks(
  0,
  3,
  dataViewMetadataColumnWithIntegersOnly,
  6
);

// returns: 4
```

### <a name="getticklabelmargins"></a>getTickLabelMargins

Эта функция возвращает поля для меток делений.

```typescript
function getTickLabelMargins(
  viewport: IViewport,
  yMarginLimit: number,
  textWidthMeasurer: ITextAsSVGMeasurer,
  textHeightMeasurer: ITextAsSVGMeasurer,
  axes: CartesianAxisProperties,
  bottomMarginLimit: number,
  properties: TextProperties,
  scrollbarVisible?: boolean,
  showOnRight?: boolean,
  renderXAxis?: boolean,
  renderY1Axis?: boolean,
  renderY2Axis?: boolean
): TickLabelMargins;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

axis.getTickLabelMargins(
  plotArea,
  marginLimits.left,
  TextMeasurementService.measureSvgTextWidth,
  TextMeasurementService.estimateSvgTextHeight,
  axes,
  marginLimits.bottom,
  textProperties,
  /*scrolling*/ false,
  showY1OnRight,
  renderXAxis,
  renderY1Axis,
  renderY2Axis
);

// returns:  xMax, yLeft, yRight, stackHeigh;
```

### <a name="isordinal"></a>isOrdinal

Проверяет, имеет ли строка значение NULL, является ли она пустой или неопределенной.

```typescript
function isOrdinal(type: ValueTypeDescriptor): boolean;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...
let type = ValueType.fromDescriptor({ misc: { barcode: true } });
axis.isOrdinal(type);

// returns: true
```

### <a name="isdatetime"></a>isDateTime

Проверяет, имеет ли значение тип DateTime.

```typescript
function isDateTime(type: ValueTypeDescriptor): boolean;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

axis.isDateTime(ValueType.fromDescriptor({ dateTime: true }));

// returns: true
```

### <a name="getcategorythickness"></a>getCategoryThickness

Использует шкалу D3 для получения фактической толщины категории.

```typescript
function getCategoryThickness(scale: any): number;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

let range = [0, 100];
let domain = [0, 10];
let scale = d3.scale
  .linear()
  .domain(domain)
  .range(range);
let actualThickness = axis.getCategoryThickness(scale);
```

### <a name="invertordinalscale"></a>invertOrdinalScale

Эта функция инвертирует порядковую шкалу. Если x < scale.range()[0], возвращается scale.domain()[0].
В противном случае возвращается самый большой элемент в scale.domain(), который <= x.

```typescript
function invertOrdinalScale(scale: d3.scale.Ordinal<any, any>, x: number);
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

let domain: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
  pixelSpan: number = 100,
  ordinalScale: d3.scale.ordinal = axis.createOrdinalScale(
    pixelSpan,
    domain,
    0.4
  );

axis.invertOrdinalScale(ordinalScale, 49);

// returns: 4
```

### <a name="findclosestxaxisindex"></a>findClosestXAxisIndex

Эта функция находит и возвращает индекс, ближайший к оси x.

```typescript
function findClosestXAxisIndex(
  categoryValue: number,
  categoryAxisValues: AxisHelperCategoryDataPoint[]
): number;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

/**
 * Finds the index of the category of the given x coordinate given.
 * pointX is in non-scaled screen-space, and offsetX is in render-space.
 * offsetX does not need any scaling adjustment.
 * @param {number} pointX The mouse coordinate in screen-space, without scaling applied
 * @param {number} offsetX Any left offset in d3.scale render-space
 * @return {number}
 */
private findIndex(pointX: number, offsetX?: number): number {
    // we are using mouse coordinates that do not know about any potential CSS transform scale
    let xScale = this.scaleDetector.getScale().x;
    if (!Double.equalWithPrecision(xScale, 1.0, 0.00001)) {
        pointX = pointX / xScale;
    }
    if (offsetX) {
        pointX += offsetX;
    }

    let index = axis.invertScale(this.xAxisProperties.scale, pointX);
    if (this.data.isScalar) {
        // When we have scalar data the inverted scale produces a category value, so we need to search for the closest index.
        index = axis.findClosestXAxisIndex(index, this.data.categoryData);
    }

    return index;
}
```

### <a name="diffscaled"></a>diffScaled

Эта функция вычисляет и возвращает разность значений на шкале.

```typescript
function diffScaled(
  scale: d3.scale.Linear<any, any>,
  value1: any,
  value2: any
): number;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

var scale: d3.scale.Linear<number, number>,
    range = [0, 999],
    domain = [0, 1, 2, 3, 4, 5, 6, 7, 8, 999];

scale = d3.scale.linear()
    .range(range)
    .domain(domain);

return axis.diffScaled(scale, 0, 0));

// returns: 0
```

### <a name="createdomain"></a>createDomain

Эта функция создает домен значений для оси.

```typescript
function createDomain(
  data: any[],
  axisType: ValueTypeDescriptor,
  isScalar: boolean,
  forcedScalarDomain: any[],
  ensureDomain?: NumberRange
): number[];
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

var cartesianSeries = [
  {
    data: [
      { categoryValue: 7, value: 11, categoryIndex: 0, seriesIndex: 0 },
      {
        categoryValue: 9,
        value: 9,
        categoryIndex: 1,
        seriesIndex: 0
      },
      {
        categoryValue: 15,
        value: 6,
        categoryIndex: 2,
        seriesIndex: 0
      },
      { categoryValue: 22, value: 7, categoryIndex: 3, seriesIndex: 0 }
    ]
  }
];

var domain = axis.createDomain(
  cartesianSeries,
  ValueType.fromDescriptor({ text: true }),
  false,
  []
);

// returns: [0, 1, 2, 3]
```

### <a name="getcategoryvaluetype"></a>getCategoryValueType

Эта функция возвращает `ValueType` для столбца категории. Если тип отсутствует, значение по умолчанию — `Text`.

```typescript
function getCategoryValueType(
  data: any[],
  axisType: ValueTypeDescriptor,
  isScalar: boolean,
  forcedScalarDomain: any[],
  ensureDomain?: NumberRange
): number[];
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

var cartesianSeries = [
  {
    data: [
      { categoryValue: 7, value: 11, categoryIndex: 0, seriesIndex: 0 },
      {
        categoryValue: 9,
        value: 9,
        categoryIndex: 1,
        seriesIndex: 0
      },
      {
        categoryValue: 15,
        value: 6,
        categoryIndex: 2,
        seriesIndex: 0
      },
      { categoryValue: 22, value: 7, categoryIndex: 3, seriesIndex: 0 }
    ]
  }
];

axis.getCategoryValueType(
  cartesianSeries,
  ValueType.fromDescriptor({ text: true }),
  false,
  []
);

// returns: [0, 1, 2, 3]
```

### <a name="createaxis"></a>createAxis

Эта функция создает ось D3 со шкалой. Ось может быть вертикальной или горизонтальной, а также иметь числовой, текстовый тип или тип даты и времени.

```typescript
function createAxis(options: CreateAxisOptions): IAxisProperties;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";
// ...

var dataPercent = [0.0, 0.33, 0.49];

var formatStringProp: powerbi.DataViewObjectPropertyIdentifier = {
  objectName: "general",
  propertyName: "formatString"
};
let metaDataColumnPercent: powerbi.DataViewMetadataColumn = {
  displayName: "Column",
  type: ValueType.fromDescriptor({ numeric: true }),
  objects: {
    general: {
      formatString: "0 %"
    }
  }
};

var os = axis.createAxis({
  pixelSpan: 100,
  dataDomain: [dataPercent[0], dataPercent[2]],
  metaDataColumn: metaDataColumnPercent,
  formatString: valueFormatter.getFormatString(
    metaDataColumnPercent,
    formatStringProp
  ),
  outerPadding: 0.5,
  isScalar: true,
  isVertical: true
});
```

### <a name="applycustomizeddomain"></a>applyCustomizedDomain

Эта функция задает настроенный домен, но не производит изменений, если ничего не задано.

```typescript
function applyCustomizedDomain(customizedDomain, forcedDomain: any[]): any[];
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

let customizedDomain = [undefined, 20],
  existingDomain = [0, 10];

axis.applyCustomizedDomain(customizedDomain, existingDomain);

// returns: {0:0, 1:20}
```

### <a name="combinedomain"></a>combineDomain

Эта функция объединяет принудительный домен с фактическим, если было задано одно из значений.
Принудительный домен имеет первоочередной приоритет. Расширяет домен, если этого требует какая-либо опорная точка.

```typescript
function combineDomain(
  forcedDomain: any[],
  domain: any[],
  ensureDomain?: NumberRange
): any[];
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

let forcedYDomain = this.valueAxisProperties
  ? [this.valueAxisProperties["secStart"], this.valueAxisProperties["secEnd"]]
  : null;

let xDomain = [minX, maxX];

axis.combineDomain(forcedYDomain, xDomain, ensureXDomain);
```

### <a name="poweroften"></a>powerOfTen

Эта функция указывает, является ли число степенью числа 10.

```typescript
function powerOfTen(d: any): boolean;
```

Пример

```typescript
import { axis } from "powerbi-visuals-utils-chartutils";
// ...

axis.powerOfTen(10);

// returns: true
```

## <a name="datalabelmanager"></a>DataLabelManager

`DataLabelManager` помогает создавать метки и работать с ними. Элементы меток упорядочиваются с помощью точки привязки или прямоугольника. Возможно автоматическое обнаружение конфликтов для изменения положения или скрытия элементов.

Класс `DataLabelManager` предоставляет следующие методы:

## <a name="hidecollidedlabels"></a>hideCollidedLabels

Этот метод упорядочивает положение меток и настраивает их видимость на холсте в соответствии с их размерами и перекрытием.

```typescript
function hideCollidedLabels(
  viewport: IViewport,
  data: any[],
  layout: any,
  addTransform: boolean = false
): LabelEnabledDataPoint[];
```

Пример

```typescript
let dataLabelManager = new DataLabelManager();
let filteredData = dataLabelManager.hideCollidedLabels(
  this.viewport,
  values,
  labelLayout,
  true
);
```

## <a name="isvalid"></a>IsValid

Этот статический метод проверяет, допустим ли указанный прямоугольник (имеет ли он положительные значения ширины и высоты).

```typescript
function isValid(rect: IRect): boolean;
```

Пример

```typescript
let rectangle = {
  left: 150,
  top: 130,
  width: 120,
  height: 110
};

DataLabelManager.isValid(rectangle);

// returns: true
```

## <a name="datalabelutils"></a>DataLabelUtils

`DataLabelUtils` предоставляет средства для работы с метками данных.

Этот модуль предоставляет следующие функции, интерфейсы и классы.

### <a name="getlabelprecision"></a>getLabelPrecision

Эта функция вычисляет точность исходя из указанного формата.

```typescript
function getLabelPrecision(precision: number, format: string): number;
```

### <a name="getlabelformattedtext"></a>getLabelFormattedText

Эта функция возвращает точность для указанного формата.

```typescript
function getLabelFormattedText(options: LabelFormattedTextOptions): string;
```

Пример

```typescript
import { dataLabelUtils } from "powerbi-visuals-utils-chartutils";
// ...

let options: LabelFormattedTextOptions = {
  text: "some text",
  fontFamily: "sans",
  fontSize: "15",
  fontWeight: "normal"
};

dataLabelUtils.getLabelFormattedText(options);
```

### <a name="enumeratedatalabels"></a>enumerateDataLabels

Эта функция возвращает VisualObjectInstance для меток данных.

```typescript
function enumerateDataLabels(
  options: VisualDataLabelsSettingsOptions
): VisualObjectInstance;
```

### <a name="enumeratecategorylabels"></a>enumerateCategoryLabels

Эта функция добавляет VisualObjectInstance для меток данных категории в объект перечисления.

```typescript
function enumerateCategoryLabels(
  enumeration: VisualObjectInstanceEnumerationObject,
  dataLabelsSettings: VisualDataLabelsSettings,
  withFill: boolean,
  isShowCategory: boolean = false,
  fontSize?: number
): void;
```

### <a name="createcolumnformattercachemanager"></a>createColumnFormatterCacheManager

Эта функция возвращает диспетчер кэша, обеспечивающий быстрый доступ к форматированным меткам.

```typescript
function createColumnFormatterCacheManager(): IColumnFormatterCacheManager;
```

Пример

```typescript
import { dataLabelUtils } from "powerbi-visuals-utils-chartutils";
// ...

let value: number = 200000;

labelSettings.displayUnits = 1000000;
labelSettings.precision = 1;

let formattersCache = DataLabelUtils.createColumnFormatterCacheManager();
let formatter = formattersCache.getOrCreate(null, labelSettings);
let formattedValue = formatter.format(value);

// formattedValue == "0.2M"
```

## <a name="legend-service"></a>Служба условных обозначений

Служба `Legend` предоставляет вспомогательные интерфейсы для создания условных обозначений PBI и управления ими для визуальных элементов Power BI

Этот модуль предоставляет следующие функции и интерфейсы.

### <a name="createlegend"></a>createLegend

Эта вспомогательная функция упрощает создание условных обозначений для пользовательских визуальных элементов Power BI.

```typescript
function createLegend(
  legendParentElement: HTMLElement, // top visual element, container in which legend will be created
  interactive: boolean, // indicates that legend should be interactive
  interactivityService: IInteractivityService, // reference to IInteractivityService interface which need to create legend click events
  isScrollable: boolean = false, // indicates that legend could be scrollable or not
  legendPosition: LegendPosition = LegendPosition.Top // Position of the legend inside of legendParentElement container
): ILegend;
```

Пример

```typescript
public constructor(options: VisualConstructorOptions) {
    this.visualInitOptions = options;
    this.layers = [];

    var element = this.element = options.element;
    var viewport = this.currentViewport = options.viewport;
    var hostServices = options.host;

    //... some other init calls

    if (this.behavior) {
        this.interactivityService = createInteractivityService(hostServices);
    }
    this.legend = createLegend(
        element,
        options.interactivity && options.interactivity.isInteractiveLegend,
        this.interactivityService,
        true);
}
```

### <a name="ilegend"></a>ILegend

Этот интерфейс реализует все методы, необходимые для создания условных обозначений.

```typescript
export interface ILegend {
  getMargins(): IViewport;
  isVisible(): boolean;
  changeOrientation(orientation: LegendPosition): void; // processing legend orientation
  getOrientation(): LegendPosition; // get information about current legend orientation
  drawLegend(data: LegendData, viewport: IViewport); // all legend rendering code is placing here
  /**
   * Reset the legend by clearing it
   */
  reset(): void;
}
```

### <a name="drawlegend"></a>drawLegend

Эта функция измеряет высоту текста с заданными свойствами текста SVG.

```typescript
function drawLegend(data: LegendData, viewport: IViewport): void;
```

Пример

```typescript
private renderLegend(): void {
    if (!this.isInteractive) {
        let legendObjectProperties = this.data.legendObjectProperties;
        if (legendObjectProperties) {
            let legendData = this.data.legendData;
            LegendData.update(legendData, legendObjectProperties);
            let position = <string>legendObjectProperties[legendProps.position];
            if (position)
                this.legend.changeOrientation(LegendPosition[position]);

            this.legend.drawLegend(legendData, this.parentViewport);
        } else {
            this.legend.changeOrientation(LegendPosition.Top);
            this.legend.drawLegend({ dataPoints: [] }, this.parentViewport);
        }
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

- [Как использовать InteractivityUtils для добавления элементов выбора в визуальные элементы Power BI](utils-interactivity-selections.md)
