---
title: Общие сведения об использовании служебных программ SVG в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается использование средств SVG для упрощения работы с SVG в визуальных элементах Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
manager: rkarlin
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: cf798ae13d874e354f6941d50982bfe26d73424d
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887760"
---
# <a name="svg-utils"></a>Инструменты для SVG

SVGUtils — это набор функций и классов, упрощающих работу с SVG в визуальных элементах Power BI

## <a name="installation"></a>Установка

Чтобы установить пакет, выполните следующую команду в каталоге с текущим визуальным элементом:

```bash
npm install powerbi-visuals-utils-svgutils --save
```

## <a name="cssconstants"></a>CssConstants

Модуль `CssConstants` предоставляет специальную функцию и интерфейс для работы с селекторами классов.

Модуль `powerbi.extensibility.utils.svg.CssConstants` предоставляет следующую функцию и интерфейс:

## <a name="classandselector"></a>ClassAndSelector

Этот интерфейс описывает общие свойства селектора класса.

```typescript
interface ClassAndSelector {
  class: string;
  selector: string;
}
```

### <a name="createclassandselector"></a>createClassAndSelector

Эта функция создает экземпляр ClassAndSelector с указанным именем класса.

```typescript
function createClassAndSelector(className: string): ClassAndSelector;
```

Пример

```typescript
import { CssConstants } from "powerbi-visuals-utils-svgutils";
import createClassAndSelector = CssConstants.createClassAndSelector;
import ClassAndSelector = CssConstants.ClassAndSelector;

let divSelector: ClassAndSelector = createClassAndSelector("sample-block");

divSelector.selector === ".sample-block"; // returns: true
divSelector.class === "sample-block"; // returns: true
```

## <a name="manipulation"></a>manipulation

`manipulation` предоставляет ряд специальных функций для создания строк, используемых со свойством преобразования SVG.

Этот модуль предоставляет следующие функции:

### <a name="translate"></a>translate

Эта функция создает строку перевода, используемую со свойством преобразования SVG.

```typescript
function translate(x: number, y: number): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.translate(100, 100);

// returns: translate(100,100)
```

### <a name="translatexwithpixels"></a>translateXWithPixels

Эта функция создает строку translateX, используемую со свойством преобразования SVG.

```typescript
function translateXWithPixels(x: number): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.translateXWithPixels(100);

// returns: translateX(100px)
```

### <a name="translatewithpixels"></a>translateWithPixels

Эта функция создает строку перевода, используемую со свойством преобразования SVG.

```typescript
function translateWithPixels(x: number, y: number): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.translateWithPixels(100, 100);

// returns: translate(100px,100px)
```

### <a name="translateandrotate"></a>translateAndRotate

Эта функция создает строку translate-rotate, используемую со свойством преобразования SVG.

```typescript
function translateAndRotate(
  x: number,
  y: number,
  px: number,
  py: number,
  angle: number
): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.translateAndRotate(100, 100, 50, 50, 35);

// returns: translate(100,100) rotate(35,50,50)
```

### <a name="scale"></a>scale

Эта функция создает строку масштабирования, используемую со свойством преобразования CSS.

```typescript
function scale(scale: number): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.scale(50);

// returns: scale(50)
```

### <a name="transformorigin"></a>transformOrigin

Эта функция создает строку transform-origin, используемую со свойством преобразования CSS.

```typescript
function transformOrigin(xOffset: string, yOffset: string): string;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.transformOrigin(5, 5);

// returns: 5 5
```

### <a name="flushalld3transitions"></a>flushAllD3Transitions

Эта функция принудительно завершает все переходы D3.

```typescript
function flushAllD3Transitions(): void;
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.flushAllD3Transitions();

// forces every transition of D3 to complete
```

### <a name="parsetranslatetransform"></a>parseTranslateTransform

Эта функция анализирует строку преобразования со значением translate(x,y).

```typescript
function parseTranslateTransform(input: string): { x: string; y: string };
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.parseTranslateTransform("translate(100px,100px)");

// returns: { "x":"100px", "y":"100px" }
```

### <a name="createarrow"></a>createArrow

Эта функция создает стрелку.

```typescript
function createArrow(
  width: number,
  height: number,
  rotate: number
): { path: string; transform: string };
```

Пример

```typescript
import { manipulation } from "powerbi-visuals-utils-svgutils";
// ...

manipulation.createArrow(10, 20, 5);

/* returns: {
    "path": "M0 0L0 20L10 10 Z",
    "transform": "rotate(5 5 10)"
}*/
```

## <a name="rect"></a>Rect

Модуль `Rect` предоставляет ряд специальных функций для работы с прямоугольниками.

Этот модуль предоставляет следующие функции:

### <a name="getoffset"></a>getOffset

Эта функция возвращает смещение прямоугольника.

```typescript
function getOffset(rect: IRect): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.getOffset({ left: 25, top: 25, width: 100, height: 100 });

/* returns: {
    x: 25,
    y: 25
}*/
```

### <a name="getsize"></a>getSize

Эта функция возвращает размер прямоугольника.

```typescript
function getSize(rect: IRect): ISize;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.getSize({ left: 25, top: 25, width: 100, height: 100 });

/* returns: {
    width: 100,
    height: 100
}*/
```

### <a name="setsize"></a>setSize

Эта функция изменяет размер прямоугольника.

```typescript
function setSize(rect: IRect, value: ISize): void;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

let rectangle = { left: 25, top: 25, width: 100, height: 100 };

Rect.setSize(rectangle, { width: 250, height: 250 });

// rectangle === { left: 25, top: 25, width: 250, height: 250 }
```

### <a name="right"></a>right

Эта функция возвращает положение правого края прямоугольника.

```typescript
function right(rect: IRect): number;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.right({ left: 25, top: 25, width: 100, height: 100 });

// returns: 125
```

### <a name="bottom"></a>снизу

Эта функция возвращает положение нижнего края прямоугольника.

```typescript
function bottom(rect: IRect): number;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.bottom({ left: 25, top: 25, width: 100, height: 100 });

// returns: 125
```

### <a name="topleft"></a>topLeft

Эта функция возвращает положение левого верхнего угла прямоугольника.

```typescript
function topLeft(rect: IRect): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.topLeft({ left: 25, top: 25, width: 100, height: 100 });

// returns: { x: 25, y: 25 }
```

### <a name="topright"></a>topRight

Эта функция возвращает положение правого верхнего угла прямоугольника.

```typescript
function topRight(rect: IRect): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.topRight({ left: 25, top: 25, width: 100, height: 100 });

// returns: { x: 125, y: 25 }
```

### <a name="bottomleft"></a>bottomLeft

Эта функция возвращает положение левого нижнего угла прямоугольника.

```typescript
function bottomLeft(rect: IRect): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.bottomLeft({ left: 25, top: 25, width: 100, height: 100 });

// returns: { x: 25, y: 125 }
```

### <a name="bottomright"></a>bottomRight

Эта функция возвращает положение правого нижнего угла прямоугольника.

```typescript
function bottomRight(rect: IRect): IPoint;
```

### <a name="example"></a>Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.bottomRight({ left: 25, top: 25, width: 100, height: 100 });

// returns: { x: 125, y: 125 }
```

### <a name="clone"></a>clone

Эта функция создает копию прямоугольника.

```typescript
function clone(rect: IRect): IRect;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.clone({ left: 25, top: 25, width: 100, height: 100 });

/* returns: {
    left: 25, top: 25, width: 100, height: 100}
*/
```

### <a name="tostring"></a>toString

Эта функция преобразует прямоугольник в строку.

```typescript
function toString(rect: IRect): string;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.toString({ left: 25, top: 25, width: 100, height: 100 });

// returns: {left:25, top:25, width:100, height:100}
```

### <a name="offset"></a>offset

Эта функция применяет указанное смещение к прямоугольнику.

```typescript
function offset(rect: IRect, offsetX: number, offsetY: number): IRect;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.offset({ left: 25, top: 25, width: 100, height: 100 }, 50, 50);

/* returns: {
    left: 75,
    top: 75,
    width: 100,
    height: 100
}*/
```

### <a name="add"></a>add

Эта функция добавляет первый прямоугольник ко второму.

```typescript
function add(rect: IRect, rect2: IRect): IRect;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.add(
  { left: 25, top: 25, width: 100, height: 100 },
  { left: 50, top: 50, width: 75, height: 75 }
);

/* returns: {
    left: 75,
    top: 75,
    height: 175,
    width: 175
}*/
```

### <a name="getclosestpoint"></a>getClosestPoint

Эта функция возвращает точку на прямоугольнике, ближайшую к указанной.

```typescript
function getClosestPoint(rect: IRect, x: number, y: number): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.getClosestPoint({ left: 0, top: 0, width: 100, height: 100 }, 50, 50);

/* returns: {
    x: 50,
    y: 50
}*/
```

### <a name="equal"></a>equal

Эта функция сравнивает прямоугольники и возвращает значение true, если они одинаковы.

```typescript
function equal(rect1: IRect, rect2: IRect): boolean;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.equal(
  { left: 0, top: 0, width: 100, height: 100 },
  { left: 50, top: 50, width: 100, height: 100 }
);

// returns: false
```

### <a name="equalwithprecision"></a>equalWithPrecision

Эта функция сравнивает прямоугольники, учитывая точность значений.

```typescript
function equalWithPrecision(rect1: IRect, rect2: IRect): boolean;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.equalWithPrecision(
  { left: 0, top: 0, width: 100, height: 100 },
  { left: 50, top: 50, width: 100, height: 100 }
);

// returns: false
```

### <a name="isempty"></a>isEmpty

Эта функция проверяет, пуст ли прямоугольник.

```typescript
function isEmpty(rect: IRect): boolean;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.isEmpty({ left: 0, top: 0, width: 0, height: 0 });

// returns: true
```

### <a name="containspoint"></a>containsPoint

Эта функция проверяет, содержит ли прямоугольник указанную точку.

```typescript
function containsPoint(rect: IRect, point: IPoint): boolean;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.containsPoint(
  { left: 0, top: 0, width: 100, height: 100 },
  { x: 50, y: 50 }
);

// returns: true
```

### <a name="isintersecting"></a>isIntersecting

Эта функция проверяет, пересекаются ли прямоугольники.

```typescript
function isIntersecting(rect1: IRect, rect2: IRect): boolean;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.isIntersecting(
  { left: 0, top: 0, width: 100, height: 100 },
  { left: 0, top: 0, width: 50, height: 50 }
);

// returns: true
```

### <a name="intersect"></a>intersect

Эта функция возвращает пересечение прямоугольников.

```typescript
function intersect(rect1: IRect, rect2: IRect): IRect;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.intersect(
  { left: 0, top: 0, width: 100, height: 100 },
  { left: 0, top: 0, width: 50, height: 50 }
);

/* returns: {
    left: 0,
    top: 0,
    width: 50,
    height: 50
}*/
```

### <a name="combine"></a>combine

Эта функция объединяет прямоугольники.

```typescript
function combine(rect1: IRect, rect2: IRect): IRect;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.combine(
  { left: 0, top: 0, width: 100, height: 100 },
  { left: 0, top: 0, width: 50, height: 120 }
);

/* returns: {
    left: 0,
    top: 0,
    width: 100,
    height: 120
}*/
```

### <a name="getcentroid"></a>getCentroid

Эта функция возвращает центральную точку прямоугольника.

```typescript
function getCentroid(rect: IRect): IPoint;
```

Пример

```typescript
import { shapes } from "powerbi-visuals-utils-svgutils";
import Rect = shapes.Rect;
// ...

Rect.getCentroid({ left: 0, top: 0, width: 100, height: 100 });

/* returns: {
    x: 50,
    y: 50
}*/
```

## <a name="pointer"></a>указатель

Модуль `pointer` предоставляет специальную функцию для получения положения указателя.

Этот модуль предоставляет следующую функцию:

### <a name="getcoordinates"></a>getCoordinates

Эта функция возвращает положение указателя.

```typescript
function getCoordinates(rootNode: Element, isPointerEvent: boolean): number[];
```

Пример

```typescript
import { pointer } from "powerbi-visuals-utils-svgutils";

let bodySelection = d3.select("body");

bodySelection
  .append("div")
  .style({
    width: "100px",
    height: "100px",
    "background-color": "green"
  })
  .on("click", () => {
    pointer.getCoordinates(bodySelection.node(), true);
  });

// click element, after that you will get position of the pointer
```
