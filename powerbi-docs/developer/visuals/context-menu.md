---
title: Добавление контекстного меню в визуальный элемент Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Узнайте, как добавить контекстное меню в визуальный элемент Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
manager: rkarlin
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 06/18/2019
ms.openlocfilehash: 1c19ba94588628e002cdb9e65f59bd4182020e1c
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888703"
---
# <a name="add-context-menu-to-power-bi-visual"></a>Добавление контекстного меню к визуальному элементу Power BI

Вы можете использовать `selectionManager.showContextMenu()` с параметрами `selectionId` и положением (в качестве объекта `{x:, y:}`), чтобы Power BI отображал контекстное меню для визуального элемента.

> [!IMPORTANT]
> `selectionManager.showContextMenu()` появился в API визуальных элементов 2.2.0.

Обычно он добавляется как событие щелчка правой кнопкой мыши (или длительное нажатие для сенсорных устройств). Контекстное меню было добавлено в образец BarChart для справки:

```typescript
    public update(options: VisualUpdateOptions) {
        //...
        //handle context menu
        this.svg.on('contextmenu', () => {
            const mouseEvent: MouseEvent = d3.event as MouseEvent;
            const eventTarget: EventTarget = mouseEvent.target;
            let dataPoint = d3.select(eventTarget).datum();
            this.selectionManager.showContextMenu(dataPoint? dataPoint.selectionId : {}, {
                x: mouseEvent.clientX,
                y: mouseEvent.clientY
            });
            mouseEvent.preventDefault();
        });
```
