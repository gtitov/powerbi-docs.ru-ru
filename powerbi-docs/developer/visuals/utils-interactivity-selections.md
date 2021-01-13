---
title: Средства для взаимодействия с визуальными элементами в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В статье описывается добавление выделенных элементов в визуальные элементы Power BI с помощью средств для взаимодействия. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
manager: rkarlin
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 02/24/2020
ms.openlocfilehash: 533cf90ed9192a8d9e595cdea6320207b841b559
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887783"
---
# <a name="power-bi-visuals-interactivity-utils"></a>Инструменты для взаимодействия визуальных элементов Power BI

Средства для взаимодействия (`InteractivityUtils`) — это набор функций и классов, позволяющий упростить реализацию перекрестного выделения и перекрестной фильтрации.

> [!NOTE]
> Обновления средств для взаимодействия визуальных элементов поддерживают только последнюю версию средств (3.x.x и более поздние версии).

## <a name="installation"></a>Установка

1. Чтобы установить пакет, выполните следующую команду в каталоге с текущим проектом визуального элемента Power BI.

    ```bash
    npm install powerbi-visuals-utils-interactivityutils --save
    ```

2. Если вы используете версию 3.0 или более позднюю версию средства, установите `powerbi-models` для разрешения зависимостей.

    ```bash
    npm install powerbi-models --save
    ```

3. Для работы со средствами для взаимодействия следует импортировать необходимый компонент в исходный код визуального элемента Power BI.

    ```typescript
    import { interactivitySelectionService } from "powerbi-visuals-utils-interactivityutils";
    ```

### <a name="including-the-css-files"></a>Добавление CSS-файлов

Чтобы использовать пакет с визуальным элементом Power BI, необходимо импортировать CSS-файл в файл с расширением `.less`.

`node_modules/powerbi-visuals-utils-interactivityutils/lib/index.css`

Импортируйте CSS-файл в файл с расширением `.less`, так как средство визуализации Power BI создает оболочку для внешних правил CSS.

```less
@import (less) "node_modules/powerbi-visuals-utils-interactivityutils/lib/index.css";
```

## <a name="selectabledatapoint-properties"></a>Свойства SelectableDataPoint

Обычно точки данных содержат выделения и значения. Этот интерфейс расширяет интерфейс `SelectableDataPoint`.

`SelectableDataPoint` уже содержит свойства, как описано ниже.

```typescript
  /** Flag for identifying that a data point was selected */
  selected: boolean;

  /** Identity for identifying the selectable data point for selection purposes */
  identity: powerbi.extensibility.ISelectionId;

  /*
   * A specific identity for when data points exist at a finer granularity than
   * selection is performed.  For example, if your data points select based
   * only on series, even if they exist as category/series intersections.
   */

  specificIdentity?: powerbi.extensibility.ISelectionId;
```

## <a name="defining-an-interface-for-data-points"></a>Определение интерфейса для точек данных

1. Создайте экземпляр средств для взаимодействия и сохраните этот объект как свойство визуального элемента.

    ```typescript
    export class Visual implements IVisual {
      // ...
      private interactivity: interactivityBaseService.IInteractivityService<VisualDataPoint>;
      // ...
      constructor(options: VisualConstructorOptions) {
          // ...
          this.interactivity = interactivitySelectionService.createInteractivitySelectionService(this.host);
          // ...
      }
    }
    ```

    ```typescript
    import { interactivitySelectionService } from "powerbi-visuals-utils-interactivityutils";

    export interface VisualDataPoint extends interactivitySelectionService.SelectableDataPoint {
        value: powerbi.PrimitiveValue;
    }
    ```

2. Расширьте базовый класс поведения.

    > [!NOTE]
    > `BaseBehavior` появился в [версии 5.6.x средств для взаимодействия](https://www.npmjs.com/package/powerbi-visuals-utils-interactivityutils/v/5.6.0). Если используется предыдущая версия, создайте класс поведения из примера ниже.

3. Определите интерфейс для параметров класса поведения.

    ```typescript
    import { SelectableDataPoint } from "./interactivitySelectionService";

    import {
        IBehaviorOptions,
        BaseDataPoint
    } from "./interactivityBaseService";

    export interface BaseBehaviorOptions<SelectableDataPointType extends BaseDataPoint> extends IBehaviorOptions<SelectableDataPointType> {

    /** d3 selection object of the main elements on the chart */
    elementsSelection: Selection<any, SelectableDataPoint, any, any>;

    /** d3 selection object of some elements on backgroup, to hadle click of reset selection */
    clearCatcherSelection: d3.Selection<any, any, any, any>;
    }
    ```

4. Определите класс для `visual behavior`. Или расширьте класс `BaseBehavior`.

    **Определение класса для `visual behavior`**

    Этот класс отвечает за обработку событий мыши `click` и `contextmenu`.

    Когда пользователь щелкает элементы данных, визуальный элемент вызывает обработчик выбора для выбора точек данных. Если пользователь щелкает фоновый элемент визуализации, вызывается обработчик снятия выделения.

    Класс имеет соответствующие методы:
    * `bindClick`
    * `bindClearCatcher`
    * `bindContextMenu`.

    ```typescript
    export class Behavior<SelectableDataPointType extends BaseDataPoint> implements IInteractiveBehavior {

        /** d3 selection object of main elements in the chart */
        protected options: BaseBehaviorOptions<SelectableDataPointType>;
        protected selectionHandler: ISelectionHandler;
    
        protected bindClick() {
          // ...
        }
    
        protected bindClearCatcher() {
          // ...
        }
    
        protected bindContextMenu() {
          // ...
        }
    
        public bindEvents(
            options: BaseBehaviorOptions<SelectableDataPointType>,
            selectionHandler: ISelectionHandler): void {
          // ...
        }
    
        public renderSelection(hasSelection: boolean): void {
          // ...
        }
    }
    ```

    **Расширение класса `BaseBehavior`**

    ```typescript
    import powerbi from "powerbi-visuals-api";
    import { interactivitySelectionService, baseBehavior } from "powerbi-visuals-utils-interactivityutils";

    export interface VisualDataPoint extends interactivitySelectionService.SelectableDataPoint {
        value: powerbi.PrimitiveValue;
    }

    export class Behavior extends baseBehavior.BaseBehavior<VisualDataPoint> {
      // ...
    }
    ```

5. Чтобы выполнить обработку щелчка элементов, вызовите метод `on` объекта выбора *d3*. Это также касается `elementsSelection` и `clearCatcherSelection`.

    ```typescript
    protected bindClick() {
      const {
          elementsSelection
      } = this.options;
    
      elementsSelection.on("click", (datum) => {
          const mouseEvent: MouseEvent = getEvent() as MouseEvent || window.event as MouseEvent;
          mouseEvent && this.selectionHandler.handleSelection(
              datum,
              mouseEvent.ctrlKey);
      });
    }
    ```

6. Добавьте аналогичный обработчик для события `contextmenu`, чтобы вызвать метод диспетчера выбора `showContextMenu`.

    ```typescript
    protected bindContextMenu() {
        const {
            elementsSelection
        } = this.options;
    
        elementsSelection.on("contextmenu", (datum) => {
            const event: MouseEvent = (getEvent() as MouseEvent) || window.event as MouseEvent;
            if (event) {
                this.selectionHandler.handleContextMenu(
                    datum,
                    {
                        x: event.clientX,
                        y: event.clientY
                    });
                event.preventDefault();
            }
        });
    }
    ```

7. Средства для взаимодействия вызывают метод `bindEvents` для назначения функций обработчикам. Добавьте в метод `bindEvents` следующие вызовы.
    * `bindClick`
    * `bindClearCatcher`
    * `bindContextMenu`

    ```typescript
      public bindEvents(
          options: BaseBehaviorOptions<SelectableDataPointType>,
          selectionHandler: ISelectionHandler): void {

          this.options = options;
          this.selectionHandler = selectionHandler;

          this.bindClick();
          this.bindClearCatcher();
          this.bindContextMenu();
      }
    ```

8. Метод `renderSelection` отвечает за обновление состояния визуальных элементов на диаграмме. Ниже приведен пример реализации `renderSelection`.

    ```typescript
    public renderSelection(hasSelection: boolean): void {
        this.options.elementsSelection.style("opacity", (category: any) => {
            if (category.selected) {
                return 0.5;
            } else {
                return 1;
            }
        });
    }
    ```

9. Последним шагом является создание экземпляра `visual behavior` и вызов метода `bind` экземпляра средств для взаимодействия.

    ```typescript
    this.interactivity.bind(<BaseBehaviorOptions<VisualDataPoint>>{
        behavior: this.behavior,
        dataPoints: this.categories,
        clearCatcherSelection: select(this.target),
        elementsSelection: selectionMerge
    });
    ```

    * `selectionMerge` является объектом выбора *d3*, который представляет все элементы визуализации, поддерживающие выбор.
    * `select(this.target)` является объектом выбора *d3*, который представляет основные элементы DOM элемента визуализации.
    * `this.categories` — это точки данных с элементами, для которых интерфейсом является `VisualDataPoint` или `categories: VisualDataPoint[];`.
    * `this.behavior` — это новый экземпляр `visual behavior`, созданный в конструкторе визуального элемента, как показано ниже.

      ```typescript
      export class Visual implements IVisual {
        // ...
        constructor(options: VisualConstructorOptions) {
            // ...
            this.behavior = new Behavior();
        }
        // ...
      }
      ```
## <a name="next-steps"></a>Дальнейшие действия

* [Как управлять элементами выбора при переключении закладок](bookmarks-support.md#visuals-with-selection)

* [Сведения о добавлении контекстного меню для точек данных визуальных элементов](context-menu.md)

* [Использование диспетчера выбора для добавления элементов выбора в визуальные элементы Power BI](selection-api.md)
