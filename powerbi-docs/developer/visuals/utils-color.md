---
title: Общие сведения об использовании средств для работы с цветом в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В ней описывается, как с помощью средств для работы с цветом упростить применение тем и палитр к точкам данных визуального элемента в Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 02/14/2020
ms.openlocfilehash: cc75188d806d653766860b2fada9028477a75f71
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887852"
---
# <a name="color-utils"></a>Инструменты для работы с цветом
Эта статья поможет вам установить, импортировать и использовать средства для работы с цветом. В ней описывается, как с помощью средств для работы с цветом упростить применение тем и палитр к точкам данных визуального элемента в Power BI.

## <a name="requirements"></a>Требования
Чтобы использовать пакет, необходимо выполнить некоторые действия.
* [node.js](https://nodejs.org) (рекомендуется использовать последнюю версию LTS)
* [npm](https://www.npmjs.com/) (минимальная поддерживаемая версия — 3.0.0)
* Пользовательский визуальный элемент, созданный [PowerBI-visuals-tools](https://www.npmjs.com/package/powerbi-visuals-tools)

## <a name="installation"></a>Установка

Чтобы установить пакет, выполните следующую команду в каталоге с текущим визуальным элементом:

```bash
npm install powerbi-visuals-utils-colorutils --save
```
Эта команда устанавливает пакет и добавляет его в качестве зависимости в ```package.json```

## <a name="usage"></a>Использование

Для работы со средствами для взаимодействия визуальных элементов следует импортировать необходимый компонент в исходный код визуального элемента.
```typescript
import { ColorHelper } from "powerbi-visuals-utils-colorutils";
```

Узнайте, как установить и использовать средства для работы с цветом в визуальных элементах Power BI.

* [Руководство по использованию] В руководстве по использованию описывается общедоступный API пакета. Вы увидите описание и несколько примеров для каждого общедоступного интерфейса пакета.

Этот пакет содержит следующие классы и модули:
* [ColorHelper](#colorhelper) — помогает создавать разные цвета для значений на диаграмме;
* [colorUtils](#colorutils) — помогает преобразовывать цветовые форматы.

## `ColorHelper`
Класс `ColorHelper` предоставляет следующие функции и методы.

### `getColorForSeriesValue` 
Этот метод возвращает цвет для заданного значения ряда. Если не задан явный цвет или цвет по умолчанию, то цвет выделяется из цветовой шкалы для этого ряда.
```typescript
getColorForSeriesValue(objects: IDataViewObjects, value: PrimitiveValue, themeColorName?: ThemeColorName): string;
```
#### <a name="example"></a>Пример
```typescript
import powerbi from "powerbi-visuals-api";
import { ColorHelper } from "powerbi-visuals-utils-colorutils";

import DataViewObjects = powerbi.DataViewObjects;

import DataViewValueColumns = powerbi.DataViewValueColumns;
import DataViewValueColumnGroup = powerbi.DataViewValueColumnGroup;
import DataViewObjectPropertyIdentifier = powerbi.DataViewObjectPropertyIdentifier;

import IVisual = powerbi.extensibility.visual.IVisual;
import IColorPalette = powerbi.extensibility.IColorPalette;
import VisualUpdateOptions = powerbi.extensibility.visual.VisualUpdateOptions;
import VisualConstructorOptions = powerbi.extensibility.visual.VisualConstructorOptions;

export class YourVisual implements IVisual {
    // Implementation of IVisual

    private colorPalette: IColorPalette;

    constructor(options: VisualConstructorOptions) {
        this.colorPalette = options.host.colorPalette;
    }

    public update(visualUpdateOptions: VisualUpdateOptions): void {
        const valueColumns: DataViewValueColumns = visualUpdateOptions.dataViews[0].categorical.values,
            grouped: DataViewValueColumnGroup[] = valueColumns.grouped(),
            defaultDataPointColor: string = "green",
            fillProp: DataViewObjectPropertyIdentifier = {
                objectName: "objectName",
                propertyName: "propertyName"
            };

        let colorHelper: ColorHelper = new ColorHelper(
            this.colorPalette,
            fillProp,
            defaultDataPointColor);

        for (let i = 0; i < grouped.length; i++) {
            let grouping: DataViewValueColumnGroup = grouped[i];

            let color = colorHelper.getColorForSeriesValue(grouping.objects, grouping.name); // returns a color of the series
        }
    }
}
```

### `getColorForMeasure`
Этот метод возвращает цвет для заданной меры.
```typescript
 getColorForMeasure(objects: IDataViewObjects, measureKey: any, themeColorName?: ThemeColorName): string;
```
#### <a name="example"></a>Пример
```typescript
import powerbi from "powerbi-visuals-api";
import { ColorHelper } from "powerbi-visuals-utils-colorutils";

import DataViewObjects = powerbi.DataViewObjects;
import IVisual = powerbi.extensibility.visual.IVisual;
import IColorPalette = powerbi.extensibility.IColorPalette;
import VisualUpdateOptions = powerbi.extensibility.visual.VisualUpdateOptions;
import DataViewObjectPropertyIdentifier = powerbi.DataViewObjectPropertyIdentifier;
import VisualConstructorOptions = powerbi.extensibility.visual.VisualConstructorOptions;

export class YourVisual implements IVisual {
    // Implementation of IVisual

    private colorPalette: IColorPalette;

    constructor(options: VisualConstructorOptions) {
        this.colorPalette = options.host.colorPalette;
    }

    public update(visualUpdateOptions: VisualUpdateOptions): void {
        const objects: DataViewObjects = visualUpdateOptions.dataViews[0].categorical.categories[0].objects[0],
            defaultDataPointColor: string = "green",
            fillProp: DataViewObjectPropertyIdentifier = {
                objectName: "objectName",
                propertyName: "propertyName"
            };

        let colorHelper: ColorHelper = new ColorHelper(
            this.colorPalette,
            fillProp,
            defaultDataPointColor);

        let color = colorHelper.getColorForMeasure(objects, ""); // returns a color
    }
}
```

### <a name="static-normalizeselector"></a>static `normalizeSelector`
Этот метод возвращает нормализованный селектор.
```typescript
static normalizeSelector(selector: Selector, isSingleSeries?: boolean): Selector;
```
#### <a name="example"></a>Пример
```typescript
import ISelectionId = powerbi.visuals.ISelectionId;
import { ColorHelper } from "powerbi-visuals-utils-colorutils";

let selectionId: ISelectionId = ...;
let selector = ColorHelper.normalizeSelector(selectionId.getSelector(), false);
```

Методы `getThemeColor` и `getHighContrastColor` связаны с цветами цветовой темы.
Кроме того, `ColorHelper` имеет свойство `isHighContrast`, которое должно быть полезно для проверки.

### `getThemeColor`
Этот метод возвращает цвет темы.
```typescript
 getThemeColor(themeColorName?: ThemeColorName): string;
```
### `getHighContrastColor`
 Этот метод возвращает цвет для режима высокой контрастности.
```typescript
getHighContrastColor(themeColorName?: ThemeColorName, defaultColor?: string): string;
```
#### <a name="example-related-to-high-contrast-mode-usage"></a>Пример, связанный с использованием режима высокой контрастности.
```typescript

import { ColorHelper } from "powerbi-visuals-utils-colorutils";

export class MyVisual implements IVisual {
        private colorHelper: ColorHelper;

        private init(options: VisualConstructorOptions): void {
            this.colors = options.host.colorPalette;
            this.colorHelper = new ColorHelper(this.colors);
        } 

            private createViewport(element: HTMLElement): void {
                const fontColor: string = "#131aea";
                const axisBackgroundColor: string = this.colorHelper.getThemeColor();
                
                // some d3 code before
                d3ElementName.attr("fill", colorHelper.getHighContrastColor("foreground", fontColor);
            }
                
            public static parseSettings(dataView: DataView, colorHelper: ColorHelper): VisualSettings {
                // some code that should be applied on formatting settings
                if (colorHelper.isHighContrast) {
                        this.settings.fontColor = colorHelper.getHighContrastColor("foreground", this.settings.fontColor);
                    }
            }
}
```


## `ColorUtils`
 Этот модуль предоставляет следующие функции:

* [hexToRGBString](#hextorgbstring)
* [rotate](#rotate)
* [parseColorString](#parsecolorstring)
* [calculateHighlightColor](#calculatehighlightcolor)
* [createLinearColorScale](#createlinearcolorscale)
* [shadeColor](#shadecolor)
* [rgbBlend](#rgbblend)
* [channelBlend](#channelblend)
* [hexBlend](#hexblend)

### <a name="hextorgbstring"></a>hexToRGBString
Преобразовывает шестнадцатеричный цвет в строку RGB.

```typescript
function hexToRGBString(hex: string, transparency?: number): string
```

#### <a name="example"></a>Пример

```typescript
import  { hexToRGBString } from "powerbi-visuals-utils-colorutils";

hexToRGBString('#112233');

// returns: "rgb(17,34,51)"
```

### <a name="rotate"></a>поворот
Поворачивает цвет RGB.

```typescript
function rotate(rgbString: string, rotateFactor: number): string
```

#### <a name="example"></a>Пример

```typescript
import { rotate } from "powerbi-visuals-utils-colorutils";

rotate("#CC0000", 0.25); // returns: #66CC00
```

### <a name="parsecolorstring"></a>parseColorString
Анализирует любую строку цвета для получения формата RGB.

```typescript
function parseColorString(color: string): RgbColor
```

#### <a name="example"></a>Пример

```typescript
import { parseColorString } from "powerbi-visuals-utils-colorutils";

parseColorString('#09f');
// returns: {R: 0, G: 153, B: 255 }

parseColorString('rgba(1, 2, 3, 1.0)');
// returns: {R: 1, G: 2, B: 3, A: 1.0 }
```

### <a name="calculatehighlightcolor"></a>calculateHighlightColor
Вычисляет цвет выделения из rgbColor на основе lumianceThreshold и разницы.

```typescript
function calculateHighlightColor(rgbColor: RgbColor, lumianceThreshold: number, delta: number): string
```

#### <a name="example"></a>Пример

```typescript
import { calculateHighlightColor } from "powerbi-visuals-utils-colorutils";

let yellow = "#FFFF00",
    yellowRGB = parseColorString(yellow);

calculateHighlightColor(yellowRGB, 0.8, 0.2);

// returns: '#CCCC00'
```

### <a name="createlinearcolorscale"></a>createLinearColorScale
Возвращает линейную цветовую шкалу для заданной области чисел.

```typescript
function createLinearColorScale(domain: number[], range: string[], clamp: boolean): LinearColorScale
```

#### <a name="example"></a>Пример

```typescript
import { createLinearColorScale } from "powerbi-visuals-utils-colorutils";

let scale = ColorUtility.createLinearColorScale(
    [0, 1, 2, 3, 4],
    ["red", "green", "blue", "black", "yellow"],
    true);

scale(1); // returns: green
scale(10); // returns: yellow
```

### <a name="shadecolor"></a>shadeColor
Преобразовывает шестнадцатеричное строковое выражение в число, вычисляя процентное значение и каналы R, G, B.
Применяет процентное значение для каждого канала и возвращает шестнадцатеричное значение в виде строки со знаком фунта.

```typescript
function shadeColor(color: string, percent: number): string
```

#### <a name="example"></a>Пример

```typescript
import { shadeColor } from "powerbi-visuals-utils-colorutils";

shadeColor('#000000', 0.1); // returns '#1a1a1a'
shadeColor('#FFFFFF', -0.5); // returns '#808080'
shadeColor('#00B8AA', -0.25); // returns '#008a80'
shadeColor('#00B8AA', 0); // returns '#00b8aa'
```

### <a name="rgbblend"></a>rgbBlend
Накладывает цвет с непрозрачностью на цвет фона. Альфа-каналы не учитываются.

```typescript
function rgbBlend(foreColor: RgbColor, opacity: number, backColor: RgbColor): RgbColor
```

#### <a name="example"></a>Пример

```typescript
import { rgbBlend} from "powerbi-visuals-utils-colorutils";

rgbBlend({R: 100, G: 100, B: 100}, 0.5, {R: 200, G: 200, B: 200});

// returns: {R: 150, G: 150, B: 150}
```

### <a name="channelblend"></a>channelBlend
Смешивает один канал для двух цветов.

```typescript
function channelBlend(foreChannel: number, opacity: number, backChannel: number): number
```

#### <a name="example"></a>Пример

```typescript
import { channelBlend} from "powerbi-visuals-utils-colorutils";

channelBlend(0, 1, 255); // returns: 0
channelBlend(128, 1, 255); // returns: 128
channelBlend(255, 0, 0); // returns: 0
channelBlend(88, 0, 88); // returns: 88
```

### <a name="hexblend"></a>hexBlend
Накладывает цвет с непрозрачностью на цвет фона.

```typescript
function hexBlend(foreColor: string, opacity: number, backColor: string): string
```

#### <a name="example"></a>Пример

```typescript
import { hexBlend} from "powerbi-visuals-utils-colorutils";

let yellow = "#FFFF00",
    black = "#000000",
    white = "#FFFFFF";

hexBlend(yellow, 0.5, white); // returns: "#FFFF80"
hexBlend(white, 0.5, yellow); // returns: "#FFFF80"

hexBlend(yellow, 0.5, black); // returns: "#808000"
hexBlend(black, 0.5, yellow); // returns: "#808000"
```