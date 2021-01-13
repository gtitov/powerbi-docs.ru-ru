---
title: Общие сведения об использовании подсказок по служебным программам в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, как использовать подсказки по служебным программам для упрощения настройки всплывающих подсказок для визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 02/14/2020
ms.openlocfilehash: b2ddc85d9ba2530dc394b4106d72b4af702bd9b4
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888657"
---
# <a name="tooltip-utils"></a>Подсказки по служебным программам
Эта статья поможет вам установить, импортировать и использовать подсказки по служебным программам. Эта служебная программа полезна для любых настроек всплывающих подсказок в визуальных элементах Power BI.

## <a name="requirements"></a>Требования
Чтобы использовать пакет, необходимо выполнить некоторые действия.
* [node.js](https://nodejs.org) (рекомендуется использовать последнюю версию LTS)
* [npm](https://www.npmjs.com/) (минимальная поддерживаемая версия — 3.0.0)
* Пользовательский визуальный элемент, созданный [PowerBI-visuals-tools](https://www.npmjs.com/package/powerbi-visuals-tools)

## <a name="installation"></a>Установка

Чтобы установить пакет, выполните следующую команду в каталоге с текущим визуальным элементом:

```bash
npm install powerbi-visuals-utils-tooltiputils --save
```
Эта команда устанавливает пакет и добавляет его в качестве зависимости в ```package.json```

## <a name="usage"></a>Использование

> В этом разделе описывается общедоступный API пакета. Вы увидите описание и несколько примеров для каждого общедоступного интерфейса пакета.

Этот пакет содержит способ создания `TooltipServiceWrapper` и методы, помогающие управлять действиями подсказок. В нем используются интерфейсы подсказок — `ITooltipServiceWrapper`, `TooltipEventArgs`, `TooltipEnabledDataPoint`. 

Кроме того, в нем есть определенные методы (обработчики событий касания), связанные с разработкой мобильных приложений: `touchEndEventName`, `touchStartEventName`, `usePointerEvents`.

`TooltipServiceWrapper` предоставляет самый простой способ управления подсказками.

Этот модуль предоставляет следующие интерфейсы и функции:
* [ITooltipServiceWrapper](#itooltipservicewrapper)
  * [addTooltip](#itooltipservicewrapperaddtooltip)
  * [скрыть](#itooltipservicewrapperhide)

* [Интерфейсы](#interfaces)
  * [TooltipEventArgs](#tooltipeventargs)
  * [TooltipEnabledDataPoint](#tooltipenableddatapoint)
  * [TooltipServiceWrapperOptions](#tooltipservicewrapperoptions)
* [События касания](#touch-events)

### `createTooltipServiceWrapper`
Эта функция создает экземпляр класса ITooltipServiceWrapper.

```typescript
function createTooltipServiceWrapper(tooltipService: ITooltipService, rootElement: Element, handleTouchDelay?: number,  getEventMethod?: () => MouseEvent): ITooltipServiceWrapper;
```

```ITooltipService``` доступен в [IVisualHost](https://github.com/microsoft/PowerBI-visuals-tools/blob/master/templates/visuals/.api/v2.6.0/PowerBI-visuals.d.ts#L1335).

**Пример**

```typescript
import { createTooltipServiceWrapper } from "powerbi-visuals-utils-tooltiputils";

export class YourVisual implements IVisual {
    // implementation of IVisual.

    constructor(options: VisualConstructorOptions) {
        createTooltipServiceWrapper(
            options.host.tooltipService,
            options.element);

        // returns: an instance of ITooltipServiceWrapper.
    }
}
```

Пример кода пользовательского визуального элемента см. [здесь](https://github.com/microsoft/powerbi-visuals-gantt/blob/master/src/gantt.ts#L391).

### `ITooltipServiceWrapper`
Этот интерфейс описывает открытые методы TooltipService

```typescript
interface ITooltipServiceWrapper {
    addTooltip<T>(selection: d3.Selection<any, any, any, any>, getTooltipInfoDelegate: (args: TooltipEventArgs<T>) => powerbi.extensibility.VisualTooltipDataItem[], getDataPointIdentity?: (args: TooltipEventArgs<T>) => powerbi.visuals.ISelectionId, reloadTooltipDataOnMouseMove?: boolean): void;
    hide(): void;
}
```

#### `ITooltipServiceWrapper.addTooltip`

Этот метод добавляет подсказки к текущему выбору.

```typescript
addTooltip<T>(selection: d3.Selection<any>, getTooltipInfoDelegate: (args: TooltipEventArgs<T>) => VisualTooltipDataItem[], getDataPointIdentity?: (args: TooltipEventArgs<T>) => ISelectionId, reloadTooltipDataOnMouseMove?: boolean): void;
```

**Пример**

```typescript
import { createTooltipServiceWrapper, TooltipEventArgs, ITooltipServiceWrapper, TooltipEnabledDataPoint } from "powerbi-visuals-utils-tooltiputils";

let bodyElement = d3.select("body");

let element = bodyElement
    .append("div")
    .style({
        "background-color": "green",
        "width": "150px",
        "height": "150px"
    })
    .classed("visual", true)
    .data([{
        tooltipInfo: [{
            displayName: "Power BI",
            value: 2016
        }]
    }]);

let tooltipServiceWrapper: ITooltipServiceWrapper = createTooltipServiceWrapper(tooltipService, bodyElement.get(0)); // tooltipService is from the IVisualHost.

tooltipServiceWrapper.addTooltip<TooltipEnabledDataPoint>(element, (eventArgs: TooltipEventArgs<TooltipEnabledDataPoint>) => {
    return eventArgs.data.tooltipInfo;
});

// You will see a tooltip if you mouseover the element.
```

Пример кода пользовательского визуального элемента см. [здесь](https://github.com/microsoft/powerbi-visuals-gantt/blob/master/src/gantt.ts#L2931).

Также обратите внимание на следующий пример настройки подсказки в пользовательском визуальном элементе [на диаграмме Ганта](https://github.com/microsoft/powerbi-visuals-gantt/blob/master/src/gantt.ts#L573-L648)

### `ITooltipServiceWrapper.hide`

Этот метод скрывает подсказку.

```typescript
hide(): void;
```

**Пример**

```typescript
import {createTooltipServiceWrapper} from "powerbi-visuals-utils-tooltiputils";

let tooltipServiceWrapper = createTooltipServiceWrapper(options.host.tooltipService, options.element); // options are from the VisualConstructorOptions.

tooltipServiceWrapper.hide();
```
### `Interfaces`
Эти интерфейсы используются при создании TooltipServiceWrapper и его использовании. Кроме того, они были упомянуты в примерах из предыдущего раздела — [здесь](#itooltipservicewrapperaddtooltip).

#### `TooltipEventArgs`
```typescript
interface TooltipEventArgs<TData> {
    data: TData;
    coordinates: number[];
    elementCoordinates: number[];
    context: HTMLElement;
    isTouchEvent: boolean;
}
```

#### `TooltipEnabledDataPoint`
```typescript
interface TooltipEnabledDataPoint {
    tooltipInfo?: powerbi.extensibility.VisualTooltipDataItem[];
}
```

#### `TooltipServiceWrapperOptions`
```typescript
interface TooltipServiceWrapperOptions {
    tooltipService: ITooltipService;
    rootElement: Element;
    handleTouchDelay: number;
    getEventMethod?: () => MouseEvent;
```

### `Touch events`

Теперь подсказки позволяют управлять несколькими событиями касания, которые полезны для разработки мобильных приложений.

#### `touchStartEventName`
```typescript
function touchStartEventName(): string
```
Этот метод возвращает имя события запуска касания.

#### `touchEndEventName`
```typescript
function touchEndEventName(): string
```
Этот метод возвращает имя события запуска касания.

#### `usePointerEvents`
```typescript
function usePointerEvents(): boolean
```
Этот метод возвращает текущее событие touchStart, связанное с указателем.
