---
title: Общие сведения об использовании средств форматирования в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается использование средств форматирования для форматирования значений и применения к ним локализации в визуальном элементе Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
manager: rkarlin
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: 564f6587ff361e3b2860bafb4ae43bc19ad8c2ba
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887806"
---
# <a name="formatting-utils"></a>Инструменты форматирования

Средства форматирования содержат классы, интерфейсы и методы для форматирования значений. Они также содержат методы расширения для обработки строк и измерения размера текста в документе SVG или HTML.

## <a name="text-measurement-service"></a>Служба измерения текста

Этот модуль предоставляет следующие функции и интерфейсы.

### <a name="textproperties-interface"></a>Интерфейс TextProperties

Этот интерфейс описывает общие свойства текста.

```typescript
interface TextProperties {
    text?: string;
    fontFamily: string;
    fontSize: string;
    fontWeight?: string;
    fontStyle?: string;
    fontVariant?: string;
    whiteSpace?: string;
}
```

### <a name="measuresvgtextwidth"></a>measureSvgTextWidth

Эта функция измеряет ширину текста с заданными свойствами текста SVG.

```typescript
function measureSvgTextWidth(textProperties: TextProperties, text?: string): number;
```

Пример использования `measureSvgTextWidth`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...

let textProperties: TextProperties = {
    text: "Microsoft PowerBI",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.measureSvgTextWidth(textProperties);

// returns: 194.71875
```

### <a name="measuresvgtextrect"></a>measureSvgTextRect

Эта функция возвращает прямоугольник с заданными свойствами текста SVG.

```typescript
function measureSvgTextRect(textProperties: TextProperties, text?: string): SVGRect;
```

Пример использования `measureSvgTextRect`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...

let textProperties: TextProperties = {
    text: "Microsoft PowerBI",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.measureSvgTextRect(textProperties);

// returns: { x: 0, y: -22, width: 194.71875, height: 27 }
```

### <a name="measuresvgtextheight"></a>measureSvgTextHeight

Эта функция измеряет высоту текста с заданными свойствами текста SVG.

```typescript
function measureSvgTextHeight(textProperties: TextProperties, text?: string): number;
```

Пример использования `measureSvgTextHeight`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...


let textProperties: TextProperties = {
    text: "Microsoft PowerBI",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.measureSvgTextHeight(textProperties);

// returns: 27
```

### <a name="estimatesvgtextbaselinedelta"></a>estimateSvgTextBaselineDelta

Эта функция возвращает направляющую с заданными свойствами текста SVG.

```typescript
function estimateSvgTextBaselineDelta(textProperties: TextProperties): number;
```

Пример

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...

let textProperties: TextProperties = {
    text: "Microsoft PowerBI",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.estimateSvgTextBaselineDelta(textProperties);

// returns: 5
```

### <a name="estimatesvgtextheight"></a>estimateSvgTextHeight

Эта функция оценивает высоту текста с заданными свойствами текста SVG.

```typescript
function estimateSvgTextHeight(textProperties: TextProperties, tightFightForNumeric?: boolean): number;
```

Пример использования `estimateSvgTextHeight`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...

let textProperties: TextProperties = {
    text: "Microsoft PowerBI",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.estimateSvgTextHeight(textProperties);

// returns: 27
```

Пример кода пользовательского визуального элемента см. [здесь](https://github.com/Microsoft/powerbi-visuals-sankey/blob/4d544ea145b4e15006083a3610dfead3da5f61a4/src/visual.ts#L372).

### <a name="measuresvgtextelementwidth"></a>measureSvgTextElementWidth

Эта функция измеряет ширину элемента svgElement.

```typescript
function measureSvgTextElementWidth(svgElement: SVGTextElement): number;
```

Пример использования measureSvgTextElementWidth:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
// ...

let svg: D3.Selection = d3.select("body").append("svg");

svg.append("text")
    .text("Microsoft PowerBI")
    .attr({
        "x": 25,
        "y": 25
    })
    .style({
        "font-family": "sans-serif",
        "font-size": "24px"
    });

let textElement: D3.Selection = svg.select("text");

textMeasurementService.measureSvgTextElementWidth(textElement.node());

// returns: 194.71875
```

### <a name="getmeasurementproperties"></a>getMeasurementProperties

Эта функция получает свойства измерения текста для указанного элемента модели DOM.

```typescript
function getMeasurementProperties(element: Element): TextProperties;
```

Пример использования `getMeasurementProperties`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
// ...

let element: JQuery = $(document.createElement("div"));

element.text("Microsoft PowerBI");

element.css({
    "width": 500,
    "height": 500,
    "font-family": "sans-serif",
    "font-size": "32em",
    "font-weight": "bold",
    "font-style": "italic",
    "white-space": "nowrap"
});

textMeasurementService.getMeasurementProperties(element.get(0));

/* returns: {
    fontFamily:"sans-serif",
    fontSize: "32em",
    fontStyle: "italic",
    fontVariant: "",
    fontWeight: "bold",
    text: "Microsoft PowerBI",
    whiteSpace: "nowrap"
}*/
```

### <a name="getsvgmeasurementproperties"></a>getSvgMeasurementProperties

Эта функция получает свойства измерения текста для указанного текстового элемента SVG.

```typescript
function getSvgMeasurementProperties(svgElement: SVGTextElement): TextProperties;
```

Пример использования `getSvgMeasurementProperties`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
// ...

let svg: D3.Selection = d3.select("body").append("svg");

let textElement: D3.Selection = svg.append("text")
    .text("Microsoft PowerBI")
    .attr({
        "x": 25,
        "y": 25
    })
    .style({
        "font-family": "sans-serif",
        "font-size": "24px"
    });

textMeasurementService.getSvgMeasurementProperties(textElement.node());

/* returns: {
    "text": "Microsoft PowerBI",
    "fontFamily": "sans-serif",
    "fontSize": "24px",
    "fontWeight": "normal",
    "fontStyle": "normal",
    "fontVariant": "normal",
    "whiteSpace": "nowrap"
}*/
```

## <a name="getdivelementwidth"></a>getDivElementWidth

Эта функция возвращает ширину элемента div.

```typescript
function getDivElementWidth(element: JQuery): string;
```

Пример использования `getDivElementWidth`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
// ...

let svg: Element = d3.select("body")
    .append("div")
    .style({
        "width": "150px",
        "height": "150px"
    })
    .node();

textMeasurementService.getDivElementWidth(svg)

// returns: 150px
```

### <a name="gettailoredtextordefault"></a>getTailoredTextOrDefault

Сравнивает размер текста меток с доступным размером и отрисовывает многоточие, если доступный размер меньше.

```typescript
function getTailoredTextOrDefault(textProperties: TextProperties, maxWidth: number): string;
```

Пример использования `getTailoredTextOrDefault`:

```typescript
import { textMeasurementService } from "powerbi-visuals-utils-formattingutils";
import TextProperties = textMeasurementService.TextProperties;
// ...

let textProperties: TextProperties = {
    text: "Microsoft PowerBI!",
    fontFamily: "sans-serif",
    fontSize: "24px"
};

textMeasurementService.getTailoredTextOrDefault(textProperties, 100);

// returns: Micros...
```

## <a name="string-extensions"></a>Расширения для работы со строками

Этот модуль предоставляет следующие функции:

## <a name="endswith"></a>endsWith

Эта функция проверяет, заканчивается ли строка определенной подстрокой.

```typescript
function endsWith(str: string, suffix: string): boolean;
```

Пример использования `endsWith`:

```typescript
import { stringExtensions } from "powerbi-visuals-utils-formattingutils";
// ...

stringExtensions.endsWith("Power BI", "BI");

// returns: true
```

### <a name="equalignorecase"></a>equalIgnoreCase

Эта функция сравнивает строки без учета регистра.

```typescript
function equalIgnoreCase(a: string, b: string): boolean;
```

Пример использования `equalIgnoreCase`:

```typescript
import { stringExtensions } from "powerbi-visuals-utils-formattingutils";
// ...

stringExtensions.equalIgnoreCase("Power BI", "power bi");

// returns: true
```

### <a name="startswith"></a>startsWith

Эта функция проверяет, начинается ли строка с определенной подстроки.

```typescript
function startsWith(a: string, b: string): boolean;
```

Пример использования `startsWith`:

```typescript
import { stringExtensions } from "powerbi-visuals-utils-formattingutils";
// ...

stringExtensions.startsWith("Power BI", "Power");

// returns: true
```

### <a name="contains"></a>contains

Эта функция проверяет, содержит ли строка определенную подстроку.

```typescript
function contains(source: string, substring: string): boolean;
```

Пример использования метода `contains`:

```typescript
import { stringExtensions } from "powerbi-visuals-utils-formattingutils";
// ...

stringExtensions.contains("Microsoft Power BI Visuals", "Power BI");

// returns: true
```

### <a name="isnullorempty"></a>isNullOrEmpty

Проверяет, имеет ли строка значение NULL, является ли она пустой или неопределенной.

```typescript
function isNullOrEmpty(value: string): boolean;
```

Пример метода `isNullOrEmpty`:

```typescript
import { stringExtensions } from "powerbi-visuals-utils-formattingutils";
// ...

stringExtensions.isNullOrEmpty(null);

// returns: true
```

## <a name="value-formatter"></a>Модуль форматирования значений

Этот модуль предоставляет следующие функции, интерфейсы и классы.

## <a name="ivalueformatter"></a>IValueFormatter

Этот интерфейс описывает открытые методы и свойства модуля форматирования.

```typescript
interface IValueFormatter {
    format(value: any): string;
    displayUnit?: DisplayUnit;
    options?: ValueFormatterOptions;
}
```

### <a name="ivalueformatterformat"></a>IValueFormatter.format

Этот метод форматирует заданное значение.

```typescript
function format(value: any, format?: string, allowFormatBeautification?: boolean): string;
```

Примеры `IValueFormatter.format`.

#### <a name="the-thousand-formats"></a>Формат для тысяч

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ value: 1001 });

iValueFormatter.format(5678);

// returns: "5.68K"
```

#### <a name="the-million-formats"></a>Формат для миллионов

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ value: 1e6 });

iValueFormatter.format(1234567890);

// returns: "1234.57M"
```

#### <a name="the-billion-formats"></a>Формат для миллиардов

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ value: 1e9 });

iValueFormatter.format(1234567891236);

// returns: 1234.57bn
```

#### <a name="the-trillion-format"></a>Формат для триллионов

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ value: 1e12 });

iValueFormatter.format(1234567891236);

// returns: 1.23T
```

#### <a name="the-exponent-format"></a>Экспоненциальный формат

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ format: "E" });

iValueFormatter.format(1234567891236);

// returns: 1.234568E+012
```

### <a name="the-culture-selector"></a>Выбор языка и региональных параметров

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let valueFormatterUK = valueFormatter.create({ cultureSelector: "en-GB" });

valueFormatterUK.format(new Date(2007, 2, 3, 17, 42, 42));

// returns: 03/03/2007 17:42:42

let valueFormatterUSA = valueFormatter.create({ cultureSelector: "en-US" });

valueFormatterUSA.format(new Date(2007, 2, 3, 17, 42, 42));

// returns: 3/3/2007 5:42:42 PM
```

#### <a name="the-percentage-format"></a>Процентный формат

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ format: "0.00 %;-0.00 %;0.00 %" });

iValueFormatter.format(0.54);

// returns: 54.00 %
```

#### <a name="the-dates-format"></a>Формат дат

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let date = new Date(2016, 10, 28, 15, 36, 0),
    iValueFormatter = valueFormatter.create({});

iValueFormatter.format(date);

// returns: 11/28/2016 3:36:00 PM
```

#### <a name="the-boolean-format"></a>Логический формат

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({});

iValueFormatter.format(true);

// returns: True
```

#### <a name="the-customized-precision"></a>Настроенная точность

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

let iValueFormatter = valueFormatter.create({ value: 0, precision: 3 });

iValueFormatter.format(3.141592653589793);

// returns: 3.142
```

Пример кода пользовательского визуального элемента см. [здесь](https://github.com/Microsoft/powerbi-visuals-sankey/blob/4d544ea145b4e15006083a3610dfead3da5f61a4/src/visual.ts#L359).

## <a name="valueformatteroptions"></a>ValueFormatterOptions

Этот интерфейс описывает `options` интерфейса IValueFormatter и параметры функции create.

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";
import ValueFormatterOptions = valueFormatter.ValueFormatterOptions;

interface ValueFormatterOptions {
    /** The format string to use. */
    format?: string;
    /** The data value. */
    value?: any;
    /** The data value. */
    value2?: any;
    /** The number of ticks. */
    tickCount?: any;
    /** The display unit system to use */
    displayUnitSystemType?: DisplayUnitSystemType;
    /** True if we are formatting single values in isolation (e.g. card), as opposed to multiple values with a common base (e.g. chart axes) */
    formatSingleValues?: boolean;
    /** True if we want to trim off unnecessary zeroes after the decimal and remove a space before the % symbol */
    allowFormatBeautification?: boolean;
    /** Specifies the maximum number of decimal places to show*/
    precision?: number;
    /** Detect axis precision based on value */
    detectAxisPrecision?: boolean;
    /** Specifies the column type of the data value */
    columnType?: ValueTypeDescriptor;
    /** Specifies the culture */
    cultureSelector?: string;
}
```

## <a name="create"></a>create

Этот метод создает экземпляр интерфейса IValueFormatter.

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";
import create = valueFormatter.create;

function create(options: ValueFormatterOptions): IValueFormatter;
```

### <a name="example-of-using-create"></a>Пример использования функции create

```typescript
import { valueFormatter } from "powerbi-visuals-utils-formattingutils";

valueFormatter.create({});

// returns: an instance of IValueFormatter.
```

## <a name="next-steps"></a>Дальнейшие действия

[Добавление локализаций в пользовательский визуальный элемент Power BI](localization.md)  
