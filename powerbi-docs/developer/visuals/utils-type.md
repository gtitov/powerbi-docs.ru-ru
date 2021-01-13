---
title: Общие сведения об использовании типов служебных программ в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается использование средств SVG для расширения базовых типов в визуальных элементах Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
manager: rkarlin
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: 4f81f55f8d5cfc54020b3b4e02e8be55fb65b0d1
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888128"
---
# <a name="type-utils"></a>Инструменты для типов

TypeUtils — это набор функций и классов, расширяющих базовые типы для визуальных элементов Power BI.

## <a name="installation"></a>Установка

Чтобы установить пакет, выполните следующую команду в каталоге с текущим пользовательским визуальным элементом:

npm install powerbi-visuals-utils-typeutils --save Эта команда устанавливает пакет и добавляет его в качестве зависимости в файл package.json.

## <a name="double"></a>Double

`Double` предоставляет возможности управления точностью чисел.

Этот модуль предоставляет следующие функции:

### <a name="pow10"></a>pow10

Эта функция возвращает число, возведенное в десятую степень.

```typescript
function pow10(exp: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.pow10(25);

// returns: 1e+25
```

### <a name="log10"></a>log10

Эта функция возвращает логарифм числа по основанию 10.

```typescript
function log10(val: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.log10(25);

// returns: 1
```

## <a name="getprecision"></a>getPrecision

Эта функция возвращает степень 10, представляющую точность числа.

```typescript
function getPrecision(x: number, decimalDigits?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.getPrecision(562344, 6);

// returns: 0.1
```

### <a name="equalwithprecision"></a>equalWithPrecision

Эта функция проверяет, является ли разница между двумя числами меньшей, чем указанная точность.

```typescript
function equalWithPrecision(x: number, y: number, precision?: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.equalWithPrecision(1, 1.005, 0.01);

// returns: true
```

### <a name="lesswithprecision"></a>lessWithPrecision

Эта функция проверяет, меньше ли первое значение второго.

```typescript
function lessWithPrecision(x: number, y: number, precision?: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.lessWithPrecision(0.995, 1, 0.001);

// returns: true
```

### <a name="lessorequalwithprecision"></a>lessOrEqualWithPrecision

Эта функция проверяет, является ли первое значение меньшим, чем второе, или равным ему.

```typescript
function lessOrEqualWithPrecision(x: number, y: number, precision?: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.lessOrEqualWithPrecision(1.005, 1, 0.01);

// returns: true
```

### <a name="greaterwithprecision"></a>greaterWithPrecision

Эта функция проверяет, больше ли первое значение второго.

```typescript
function greaterWithPrecision(x: number, y: number, precision?: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.greaterWithPrecision(1, 0.995, 0.01);

// returns: false
```

### <a name="greaterorequalwithprecision"></a>greaterOrEqualWithPrecision

Эта функция проверяет, является ли первое значение большим, чем второе, или равным ему.

```typescript
function greaterOrEqualWithPrecision(x: number, y: number, precision?: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.greaterOrEqualWithPrecision(1, 1.005, 0.01);

// returns: true
```

### <a name="floorwithprecision"></a>floorWithPrecision

Эта функция округляет число в меньшую сторону с указанной точностью.

```typescript
function floorWithPrecision(x: number, precision?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.floorWithPrecision(5.96, 0.001);

// returns: 5
```

### <a name="ceilwithprecision"></a>ceilWithPrecision

Эта функция округляет число в большую сторону (`ceils`) с указанной точностью.

```typescript
function ceilWithPrecision(x: number, precision?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.ceilWithPrecision(5.06, 0.001);

// returns: 6
```

### <a name="floortoprecision"></a>floorToPrecision

Эта функция округляет число в меньшую сторону до указанной точности.

```typescript
function floorToPrecision(x: number, precision?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.floorToPrecision(5.96, 0.1);

// returns: 5.9
```

### <a name="ceiltoprecision"></a>ceilToPrecision

Эта функция округляет число в большую сторону (`ceils`) до указанной точности.

```typescript
function ceilToPrecision(x: number, precision?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.ceilToPrecision(-506, 10);

// returns: -500
```

### <a name="roundtoprecision"></a>roundToPrecision

Эта функция округляет число до указанной точности.

```typescript
function roundToPrecision(x: number, precision?: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.roundToPrecision(596, 10);

// returns: 600
```

### <a name="ensureinrange"></a>ensureInRange

Эта функция возвращает число в диапазоне от минимума до максимума.

```typescript
function ensureInRange(x: number, min: number, max: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.ensureInRange(-27.2, -10, -5);

// returns: -10
```

### <a name="round"></a>round

Эта функция округляет число.

```typescript
function round(x: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.round(27.45);

// returns: 27
```

### <a name="removedecimalnoise"></a>removeDecimalNoise

Эта функция устраняет десятичный шум.

```typescript
function removeDecimalNoise(value: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.removeDecimalNoise(21.493000000000002);

// returns: 21.493
```

### <a name="isinteger"></a>isInteger

Эта функция проверяет, является ли число целым.

```typescript
function isInteger(value: number): boolean;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.isInteger(21.493000000000002);

// returns: false
```

### <a name="toincrement"></a>toIncrement

Эта функция увеличивает число на указанное число и возвращает округленное число.

```typescript
function toIncrement(value: number, increment: number): number;
```

Пример

```typescript
import { double } from "powerbi-visuals-utils-typeutils";
// ...

double.toIncrement(0.6383723, 0.05);

// returns: 0.65
```

## <a name="prototype"></a>Прототип

`Prototype` предоставляет возможности наследования объектов.

Этот модуль предоставляет следующие функции:

## <a name="inherit"></a>inherit

Эта функция возвращает новый объект, прототипом которого является указанный объект.

```typescript
function inherit<T>(obj: T, extension?: (inherited: T) => void): T;
```

Пример

```typescript
import { prototype } from "powerbi-visuals-utils-typeutils";
// ...

let base = { Microsoft: "Power BI" };

prototype.inherit(base);

/* returns: {
    __proto__: {
        Microsoft: "Power BI"
    }
}*/
```

## <a name="inheritsingle"></a>inheritSingle

Эта функция возвращает новый объект, прототипом которого является указанный объект, только в том случае, если прототип не задан.

```typescript
function inheritSingle<T>(obj: T): T;
```

Пример

```typescript
import { prototype } from "powerbi-visuals-utils-typeutils";
// ...

let base = { Microsoft: "Power BI" };

prototype.inheritSingle(base);

/* returns: {
    __proto__: {
        Microsoft: "Power BI"
    }
}*/
```

## <a name="pixelconverter"></a>PixelConverter

`PixelConverter` предоставляет возможность преобразования пикселей в точки и точек в пиксели.

Этот модуль предоставляет следующие функции:

## <a name="tostring"></a>toString

Эта функция преобразует значение пикселя в строку.

```typescript
function toString(px: number): string;
```

Пример

```typescript
import { pixelConverter } from "powerbi-visuals-utils-typeutils";
// ...

pixelConverter.toString(25);

// returns: 25px
```

## <a name="frompoint"></a>fromPoint

Эта функция преобразует указанное значение точки в значение пикселя и возвращает строковую интерпретацию.

```typescript
function fromPoint(pt: number): string;
```

Пример

```typescript
import { pixelConverter } from "powerbi-visuals-utils-typeutils";
// ...

pixelConverter.fromPoint(8);

// returns: 33.33333333333333px
```

## <a name="frompointtopixel"></a>fromPointToPixel

Эта функция преобразует указанное значение точки в значение пикселя.

```typescript
function fromPointToPixel(pt: number): number;
```

Пример

```typescript
import { pixelConverter } from "powerbi-visuals-utils-typeutils";
// ...

pixelConverter.fromPointToPixel(8);

// returns: 10.666666666666666
```

## <a name="topoint"></a>toPoint

Эта функция преобразует указанное значение пикселя в значение точки.

```typescript
function toPoint(px: number): number;
```

Пример

```typescript
import { pixelConverter } from "powerbi-visuals-utils-typeutils";
// ...

pixelConverter.toPoint(8);

// returns: 6
```
