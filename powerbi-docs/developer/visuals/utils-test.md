---
title: Общие сведения об использовании служебных программ тестирования визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, как использовать служебные программы тестирования для упрощения макетов и использования конкретных методов в модульном тестировании для визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 02/14/2020
ms.openlocfilehash: 4b2a846f4905c4cb28fe92043cf3c71750b40f11
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888059"
---
# <a name="power-bi-visuals-test-utils"></a>Служебные программы тестирования визуальных элементов Power BI

В этой статье подробно описано, как установить, импортировать и использовать служебные программы тестирования визуальных элементов Power BI. Эти служебные программы тестирования используются для модульного тестирования и включают макеты и методы для таких элементов, как представления данных, выбранные элементы и цветовые схемы.

## <a name="requirements"></a>Требования

Чтобы использовать этот пакет, необходимо установить следующие ресурсы:

* [node.js](https://nodejs.org) — рекомендуется использовать версию LTS.
* [npm](https://www.npmjs.com/) — версия 3.0.0 или более поздняя.
* Пакет [powerbi-visuals-tools](https://github.com/Microsoft/PowerBI-visuals-tools).

## <a name="installation"></a>Установка

Чтобы установить служебные программы тестирования и добавить зависимости в *package.json*, выполните следующую команду из каталога визуальных элементов Power BI:

```bash
npm install powerbi-visuals-utils-testutils --save
```

Ниже приведены описания и примеры для общедоступного API служебных программ тестирования.

## <a name="visualbuilderbase"></a>VisualBuilderBase

Используется в **VisualBuilder** в модульных тестах с наиболее часто используемыми методами `build`, `update` и `updateRenderTimeout`. 

Метод `build` возвращает созданный экземпляр визуального элемента.

Методы `enumerateObjectInstances` и `updateEnumerateObjectInstancesRenderTimeout` необходимы для проверки изменений в контейнере и параметрах форматирования.

```typescript
abstract class VisualBuilderBase<T extends IVisual> {
    element: JQuery;
    viewport: IViewport;
    visualHost: IVisualHost;
    protected visual: T;
    constructor(width?: number, height?: number, guid?: string, element?: JQuery);
    protected abstract build(options: VisualConstructorOptions): T;
     nit(): void;
    destroy(): void;
    update(dataView: DataView[] | DataView): void;
    updateRenderTimeout(dataViews: DataView[] | DataView, fn: Function, timeout?: number): number;
    updateEnumerateObjectInstancesRenderTimeout(dataViews: DataView[] | DataView, options: EnumerateVisualObjectInstancesOptions, fn: (enumeration: VisualObjectInstance[]) => void, timeout?: number): number;
    updateFlushAllD3Transitions(dataViews: DataView[] | DataView): void;
    updateflushAllD3TransitionsRenderTimeout(dataViews: DataView[] | DataView, fn: Function, timeout?: number): number;
    enumerateObjectInstances(options: EnumerateVisualObjectInstancesOptions): VisualObjectInstance[];
}
```

> [!NOTE]
> Дополнительные примеры см. в разделе [о написании модульного теста VisualBuilderBase](./unit-tests-introduction.md#create-a-visual-instance-builder) и сценарии [реального использования VisualBuilderBase](https://github.com/microsoft/powerbi-visuals-gantt/blob/master/test/visualBuilder.ts).

## <a name="dataviewbuilder"></a>DataViewBuilder

Этот модуль, используемый в **TestDataViewBuilder**, предоставляет класс **CategoricalDataViewBuilder**, используемый в методе `createCategoricalDataViewBuilder`. В нем также указываются интерфейсы и методы, необходимые для работы с макетом **DataView** в модульных тестах.

* `withValues` добавляет столбцы статических рядов, а `withGroupedValues` добавляет столбцы динамических рядов.

  Не применяйте динамические и статические ряды в визуальном элементе **DataViewCategorical**. Их можно использовать только в запросе **DataViewCategorical**, где **DataViewTransform** должен разбивать их на отдельные объекты визуальных элементов **DataViewCategorical**.

* `build` возвращает DataView с метаданными и DataViewCategorical

  `build` возвращает значение **Undefined**, если сочетание параметров является недопустимым, например включение динамического и статического ряда при построении визуального элемента **DataView**.

```typescript
class CategoricalDataViewBuilder implements IDataViewBuilderCategorical {
    withCategory(options: DataViewBuilderCategoryColumnOptions): IDataViewBuilderCategorical;
    withCategories(categories: DataViewCategoryColumn[]): IDataViewBuilderCategorical;
    withValues(options: DataViewBuilderValuesOptions): IDataViewBuilderCategorical;
    withGroupedValues(options: DataViewBuilderGroupedValuesOptions): IDataViewBuilderCategorical;
    build(): DataView;
}

function createCategoricalDataViewBuilder(): IDataViewBuilderCategorical;
```

## <a name="testdataviewbuilder"></a>TestDataViewBuilder

Используется для создания **VisualData** в модульных тестах. При помещении данных в контейнеры полей данных Power BI создает категориальный объект **DataView** на основе данных. **TestDataViewBuilder** помогает имитировать создание категориального объекта **DataView**.

```typescript
abstract class TestDataViewBuilder {
    static DataViewName: string;
    private aggregateFunction;
    static setDefaultQueryName(source: DataViewMetadataColumn): DataViewMetadataColumn;
    static getDataViewBuilderColumnIdentitySources(options: TestDataViewBuilderColumnOptions[] | TestDataViewBuilderColumnOptions): DataViewBuilderColumnIdentitySource[];
    static getValuesTable(categories?: DataViewCategoryColumn[], values?: DataViewValueColumn[]): any[][];
    static createDataViewBuilderColumnOptions(categoriesColumns: (TestDataViewBuilderCategoryColumnOptions | TestDataViewBuilderCategoryColumnOptions[])[], valuesColumns: (DataViewBuilderValuesColumnOptions | DataViewBuilderValuesColumnOptions[])[], filter?: (options: TestDataViewBuilderColumnOptions) => boolean, customizeColumns?: CustomizeColumnFn): DataViewBuilderAllColumnOptions;
    static setUpDataViewBuilderColumnOptions(options: DataViewBuilderAllColumnOptions, aggregateFunction: (array: number[]) => number): DataViewBuilderAllColumnOptions;
    static setUpDataView(dataView: DataView, options: DataViewBuilderAllColumnOptions): DataView;
    protected createCategoricalDataViewBuilder(categoriesColumns: (TestDataViewBuilderCategoryColumnOptions | TestDataViewBuilderCategoryColumnOptions[])[], valuesColumns: (DataViewBuilderValuesColumnOptions | DataViewBuilderValuesColumnOptions[])[], columnNames: string[], customizeColumns?: CustomizeColumnFn): IDataViewBuilderCategorical;
    abstract getDataView(columnNames?: string[]): DataView;
}
```

  Ниже перечислены наиболее часто используемые интерфейсы при создании `testDataView`.

  ```typescript
  interface TestDataViewBuilderColumnOptions extends DataViewBuilderColumnOptions {
      values: any[];
  }

  interface TestDataViewBuilderCategoryColumnOptions extends TestDataViewBuilderColumnOptions {
      objects?: DataViewObjects[];
      isGroup?: boolean;
  }

  interface DataViewBuilderColumnOptions {
      source: DataViewMetadataColumn;
  }

  interface DataViewBuilderSeriesData {
      values: PrimitiveValue[];
      highlights?: PrimitiveValue[];
      /** Client-computed maximum value for a column. */
      maxLocal?: any;
      /** Client-computed maximum value for a column. */
      minLocal?: any;
  }

  interface DataViewBuilderColumnIdentitySource {
      fields: any[];
      identities?: CustomVisualOpaqueIdentity[];
  }
  ```
   
> [!NOTE]
> Дополнительные примеры см. в разделе о [написании модульных тестов TestDataViewBuilder](./unit-tests-introduction.md#how-to-add-static-data-for-unit-tests) и сценарии [использования TestDataViewBuilder](https://github.com/microsoft/powerbi-visuals-gantt/blob/master/test/visualData.ts).

## <a name="mocks"></a>Макеты

### <a name="mockivisualhost"></a>MockIVisualHost

Реализует **IVisualHost** для проверки визуальных элементов Power BI без внешних зависимостей, таких как Power BI Framework.

К полезным методам относятся свойства `createSelectionIdBuilder`, `createSelectionManager`, `createLocalizationManager` и getter.

```typescript
import powerbi from "powerbi-visuals-api";

import VisualObjectInstancesToPersist = powerbi.VisualObjectInstancesToPersist;
import ISelectionIdBuilder = powerbi.visuals.ISelectionIdBuilder;
import ISelectionManager = powerbi.extensibility.ISelectionManager;
import IColorPalette = powerbi.extensibility.IColorPalette;
import IVisualEventService = powerbi.extensibility.IVisualEventService;
import ITooltipService = powerbi.extensibility.ITooltipService;
import IVisualHost = powerbi.extensibility.visual.IVisualHost;

class MockIVisualHost implements IVisualHost {
      constructor(
          colorPalette?: IColorPalette,
          selectionManager?: ISelectionManager,
          tooltipServiceInstance?: ITooltipService,
          localeInstance?: MockILocale,
          allowInteractionsInstance?: MockIAllowInteractions,
          localizationManager?: powerbi.extensibility.ILocalizationManager,
          telemetryService?: powerbi.extensibility.ITelemetryService,
          authService?: powerbi.extensibility.IAuthenticationService,
          storageService?: ILocalVisualStorageService,
          eventService?: IVisualEventService);
      createSelectionIdBuilder(): ISelectionIdBuilder;
      createSelectionManager(): ISelectionManager;
      createLocalizationManager(): ILocalizationManager;
      colorPalette: IColorPalette;
      locale: string;
      telemetry: ITelemetryService;
      tooltipService: ITooltipService;
      allowInteractios: boolean;
      storageService: ILocalVisualStorageService;
      eventService: IVisualEventService;
      persistProperties(changes: VisualObjectInstancesToPersist): void;
}
```
   
- `createVisualHost` создает и возвращает экземпляр **IVisualHost**, фактически **MockIVisualHost**
  ```typescript
  function createVisualHost(locale?: Object, allowInteractions?: boolean, colors?: IColorInfo[], isEnabled?: boolean, displayNames?: any, token?: string): IVisualHost;
  ```

    Пример
    ```typescript
    import { createVisualHost } from "powerbi-visuals-utils-testutils"

    let host: IVisualHost = createVisualHost();
    ```

> [!IMPORTANT]
> **MockIVisualHost** является фиктивной реализацией **IVisualHost** и должен использоваться только с модульными тестами.

### <a name="mockicolorpalette"></a>MockIColorPalette

Реализует **IColorPalette** для проверки визуальных элементов Power BI без внешних зависимостей, таких как Power BI Framework.

**MockIColorPalette** предоставляет полезные свойства для проверки цветовой схемы или режима высокой контрастности в модульных тестах.

  ```typescript
  import powerbi from "powerbi-visuals-api";
  import IColorPalette = powerbi.extensibility.ISandboxExtendedColorPalette;
  import IColorInfo = powerbi.IColorInfo;

  class MockIColorPalette implements IColorPalette {
      constructor(colors?: IColorInfo[]);
      getColor(key: string): IColorInfo;
      reset(): IColorPalette;
      isHighContrastMode: boolean;
      foreground: {value: string};
      foregroundLight: {value: string};
      ...
      background: {value: string};
      backgroundLight: {value: string};
      ...
      shapeStroke: {value: string};
  }
  ```
  - `createColorPalette` создает и возвращает экземпляр **IColorPalette**, фактически **MockIColorPalette**
    ```typescript
    function createColorPalette(colors?: IColorInfo[]): IColorPalette;
    ```

    Пример
    ```typescript
    import { createColorPalette } from "powerbi-visuals-utils-testutils"

    let colorPalette: IColorPalette = createColorPalette();
    ```
    
> [!IMPORTANT]
> **MockIColorPalette** является фиктивной реализацией **IColorPalette** и должен использоваться только с модульными тестами.

### <a name="mockiselectionid"></a>MockISelectionId

Реализует **ISelectionId** для проверки визуальных элементов Power BI без внешних зависимостей, таких как Power BI Framework.

  ```typescript
  import powerbi from "powerbi-visuals-api";
  import Selector = powerbi.data.Selector;
  import ISelectionId = powerbi.visuals.ISelectionId;

  class MockISelectionId implements ISelectionId {
      constructor(key: string);
      equals(other: ISelectionId): boolean;
      includes(other: ISelectionId, ignoreHighlight?: boolean): boolean;
      getKey(): string;
      getSelector(): Selector;
      getSelectorsByColumn(): Selector;
      hasIdentity(): boolean;
  }
  ```

  - `createSelectionId` создает и возвращает экземпляр **ISelectionId**, фактически **MockISelectionId**
    ```typescript
    function createSelectionId(key?: string): ISelectionId;
    ```

    Пример
    ```typescript
    import { createColorPalette } from "powerbi-visuals-utils-testutils"

    let selectionId: ISelectionId = createSelectionId();
    ```
    
> [!NOTE]
> **MockISelectionId** является фиктивной реализацией **ISelectionId** и должен использоваться только с модульными тестами.

### <a name="mockiselectionidbuilder"></a>MockISelectionIdBuilder

Реализует **ISelectionIdBuilder** для проверки визуальных элементов Power BI без внешних зависимостей, таких как Power BI Framework. 

  ```typescript
  import DataViewCategoryColumn = powerbi.DataViewCategoryColumn;
  import DataViewValueColumn = powerbi.DataViewValueColumn;
  import DataViewValueColumnGroup = powerbi.DataViewValueColumnGroup;
  import DataViewValueColumns = powerbi.DataViewValueColumns;
  import ISelectionIdBuilder = powerbi.visuals.ISelectionIdBuilder;
  import ISelectionId = powerbi.visuals.ISelectionId;

  class MockISelectionIdBuilder implements ISelectionIdBuilder {
      withCategory(categoryColumn: DataViewCategoryColumn, index: number): this;
      withSeries(seriesColumn: DataViewValueColumns, valueColumn: DataViewValueColumn | DataViewValueColumnGroup): this;
      withMeasure(measureId: string): this;
      createSelectionId(): ISelectionId;
      withMatrixNode(matrixNode: DataViewMatrixNode, levels: DataViewHierarchyLevel[]): this;
      withTable(table: DataViewTable, rowIndex: number): this;
  }
  ```

  - `createSelectionIdBuilder` создает и возвращает экземпляр **ISelectionIdBuilder**, фактически **MockISelectionIdBuilder**
    ```typescript
    function createSelectionIdBuilder(): ISelectionIdBuilder;
    ```

    Пример
    ```typescript
    import { selectionIdBuilder } from "powerbi-visuals-utils-testutils";

    let selectionIdBuilder = createSelectionIdBuilder();
    ```

> [!NOTE]
> **MockISelectionIdBuilder** является фиктивной реализацией **ISelectionIdBuilder** и должен использоваться только с модульными тестами.

### <a name="mockiselectionmanager"></a>MockISelectionManager

Реализует **ISelectionManager** для проверки визуальных элементов Power BI без внешних зависимостей, таких как Power BI Framework. 

  ```typescript
  import powerbi from "powerbi-visuals-api";
  import IPromise = powerbi.IPromise;
  import ISelectionId = powerbi.visuals.ISelectionId;
  import ISelectionManager = powerbi.extensibility.ISelectionManager;

  class MockISelectionManager implements ISelectionManager {
      select(selectionId: ISelectionId | ISelectionId[], multiSelect?: boolean): IPromise<ISelectionId[]>;
      hasSelection(): boolean;
      clear(): IPromise<{}>;
      getSelectionIds(): ISelectionId[];
      containsSelection(id: ISelectionId): boolean;
      showContextMenu(selectionId: ISelectionId, position: IPoint): IPromise<{}>;
      registerOnSelectCallback(callback: (ids: ISelectionId[]) => void): void;
      simutateSelection(selections: ISelectionId[]): void;
  }
  ```

  - `createSelectionManager` создает и возвращает экземпляр **ISelectionManager**, фактически **MockISelectionManager**
    ```typescript
    function createSelectionManager(): ISelectionManager
    ```

    Пример
    ```typescript
    import { createSelectionManager } from "powerbi-visuals-utils-testutils";

    let selectionManager: ISelectionManager = createSelectionManager();
    ```

> [!NOTE]
> **MockISelectionManager** является фиктивной реализацией **ISelectionManager** и должен использоваться только с модульными тестами.

### <a name="mockilocale"></a>MockILocale

  Задает языковой стандарт и изменяет его при необходимости в процессе модульного тестирования.
  ```typescript
  class MockILocale {
      constructor(locales?: Object): void; // Default locales are en-US and ru-RU 
      locale(key: string): void;// setter property
      locale(): string; // getter property
  }
  ```
  - `createLocale` создает и возвращает экземпляр **MockILocale**
    ```typescript
    funciton createLocale(locales?: Object): MockILocale;
    ```

### <a name="mockitooltipservice"></a><a id="mockitooltipservice"></a> MockITooltipService
Имитирует `TooltipService` и вызывает его при необходимости во время процесса модульного тестирования.
  ```typescript
  class MockITooltipService implements ITooltipService {
      constructor(isEnabled: boolean = true);
      enabled(): boolean;
      show(options: TooltipShowOptions): void;
      move(options: TooltipMoveOptions): void;
      hide(options: TooltipHideOptions): void;
  }
  ```
  - `createTooltipService` создает и возвращает экземпляр **MockITooltipService**
    ```typescript
    function createTooltipService(isEnabled?: boolean): ITooltipService;
    ```

### <a name="mockiallowinteractions"></a>MockIAllowInteractions

```typescript
export class MockIAllowInteractions {
    constructor(public isEnabled?: boolean); // false by default
}
```
  - `createAllowInteractions` создает и возвращает экземпляр **MockIAllowInteractions**
    ```typescript
    function createAllowInteractions(isEnabled?: boolean): MockIAllowInteractions;
    ```

### <a name="mockilocalizationmanager"></a><a id="mockilocalizationmanager"></a> MockILocalizationManager
Предоставляет базовые возможности **LocalizationManager**, которые необходимы для модульного тестирования.
```typescript
class MockILocalizationManager implements ILocalizationManager {
    constructor(displayNames: {[key: string]: string});
    getDisplayName(key: string): string; // returns default or setted displayNames for localized elements
}
```
  - `createLocalizationManager` создает и возвращает экземпляр **ILocalizationManager**, фактически **MockILocalizationManager**
    ```typescript
    function createLocalizationManager(displayNames?: any): ILocalizationManager;
    ```

    Пример
    ```typescript
    import { createLocalizationManager } from "powerbi-visuals-utils-testutils";
    let localizationManagerMock: ILocalizationManager = createLocalizationManager();
    ```

### <a name="mockitelemetryservice"></a>MockITelemetryService
Имитирует использование **TelemetryService**.
```typescript
class MockITelemetryService implements ITelemetryService {
    instanceId: string;
    trace(veType: powerbi.VisualEventType, payload?: string) {
    }
}
```
  Создание `MockITelemetryService`
    ```typescript
    function createTelemetryService(): ITelemetryService;
    ```
### <a name="mockiauthenticationservice"></a>MockIAuthenticationService
Имитирует работу **AuthenticationService**, предоставляя фиктивный маркер AAD.
```typescript
class MockIAuthenticationService implements IAuthenticationService  {
    constructor(token: string);
    getAADToken(visualId?: string): powerbi.IPromise<string>
}
```
  - `createAuthenticationService` создает и возвращает экземпляр **IAuthenticationService**, фактически **MockIAuthenticationService**.
    ```typescript
    function createAuthenticationService(token?: string): IAuthenticationService;
    ```

### <a name="mockistorageservice"></a>MockIStorageService
Позволяет использовать **ILocalVisualStorageService** с тем же поведением, что и **LocalStorage**.
```typescript
class MockIStorageService implements ILocalVisualStorageService {
  get(key: string): IPromise<string>;
  set(key: string, data: string): IPromise<number>;
  remove(key: string): void;
}
```
  - `createStorageService` создает и возвращает экземпляр **ILocalVisualStorageService**, фактически **MockIStorageService**.
    ```typescript
    function createStorageService(): ILocalVisualStorageService;
    ```

### <a name="mockieventservice"></a>MockIEventService
```typescript
import powerbi from "powerbi-visuals-api";
import IVisualEventService = powerbi.extensibility.IVisualEventService;
import VisualUpdateOptions = powerbi.extensibility.VisualUpdateOptions;

class MockIEventService implements IVisualEventService {
      renderingStarted(options: VisualUpdateOptions): void;
      renderingFinished(options: VisualUpdateOptions): void;
      renderingFailed(options: VisualUpdateOptions, reason?: string): void;
}
```
  - `createEventService` создает и возвращает экземпляр **IVisualEventService**, фактически **MockIEventService**.
    ```typescript
    function createEventService(): IVisualEventService;
    ```

## <a name="utils"></a>Служебные программы

Служебные программы содержат вспомогательные методы для модульного тестирования визуальных элементов Power BI, включая вспомогательные элементы, связанные с цветами, числами и событиями.

- `renderTimeout` возвращает время ожидания.
  ```typescript
  function renderTimeout(fn: Function, timeout: number = DefaultWaitForRender): number
  ```

- `testDom` помогает задать тестовый стенд в модульных тестах.
  ```typescript
  function testDom(height: number | string, width: number | string): JQuery
  ```
  Пример
  ```typescript
  import { testDom }  from "powerbi-visuals-utils-testutils";
  describe("testDom", () => {
      it("should return an element", () => {
          let element: JQuery = testDom(500, 500);
          expect(element.get(0)).toBeDefined();
      });
  });
  ```

### <a name="color-related-helper-methods"></a>Вспомогательные методы, связанные с цветом

- `getSolidColorStructuralObject`
  ```typescript
  function getSolidColorStructuralObject(color: string): any
  ```
  Возвращает следующую структуру:

  ```json
  { solid: { color: color } }
  ```

- `assertColorsMatch` сравнивает объекты **RgbColor**, проанализированные из входных строк.
  ```typescript
  function assertColorsMatch(actual: string, expected: string, invert: boolean = false): boolean
  ```

- `parseColorString` выполняет анализ цвета из входной строки и возвращает его в указанном интерфейсе **RgbColor**.
  ```typescript
  function parseColorString(color: string): RgbColor
  ```

### <a name="number-related-helper-methods"></a>Вспомогательные методы, связанные с числами

- `getRandomNumbers` создает случайное число, используя минимальное и максимальное значение. Для изменения результата можно указать `exceptionList` и предоставить функцию.
  ```typescript
  function getRandomNumber(
      min: number,
      max: number,
      exceptionList?: number[],
      changeResult: (value: any) => number = x => x): number
  ```

- `getRandomNumbers` предоставляет массив случайных чисел, созданных методом `getRandomNumber` с указанными минимальными и максимальными значениями.
  ```typescript
  function getRandomNumbers(count: number, min: number = 0, max: number = 1): number[]
  ```

### <a name="event-related-helper-methods"></a>Вспомогательные методы, связанные с событием
Следующие методы написаны для имитации событий веб-страницы в модульных тестах.

- `clickElement` имитирует щелчок на указанном элементе.
  ```typescript
  function clickElement(element: JQuery, ctrlKey: boolean = false): void
  ```

- `createTouch` возвращает объект **Touch**, помогающий имитировать событие касания.
  ```typescript
  function createTouch(x: number, y: number, element: JQuery, id: number = 0): Touch
  ```

- `createTouchesList` возвращает список имитированных событий **Touch**.
  ```typescript
  function createTouchesList(touches: Touch[]): TouchList
  ```

- `createContextMenuEvent` возвращает **MouseEvent**.
  ```typescript
  function createContextMenuEvent(x: number, y: number): MouseEvent
  ```

- `createMouseEvent` создает и возвращает объект **MouseEvent**.
  ```typescript
  function createMouseEvent(
      mouseEventType: MouseEventType,
      eventType: ClickEventType,
      x: number,
      y: number,
      button: number = 0): MouseEvent
  ```

- `createTouchEndEvent`
  ```typescript
  function createTouchEndEvent(touchList?: TouchList): UIEvent
  ```

- `createTouchMoveEvent`
  ```typescript
  function createTouchMoveEvent(touchList?: TouchList): UIEvent
  ```

- `createTouchStartEvent`
  ```typescript
  function createTouchStartEvent(touchList?: TouchList): UIEvent
  ```

### <a name="d3-event-related-helper-methods"></a>Вспомогательные методы, связанные с событием D3

Для имитации событий D3 в модульных тестах используются указанные ниже методы.

- `flushAllD3Transitions` принудительно завершает все переходы D3.

  ```typescript
  function flushAllD3Transitions()
  ```
  
  > [!NOTE]
  > Обычно переходы с нулевой задержкой выполняются после мгновенной задержки (< 10 мс), но это может привести к кратковременному мерцанию при отображении страницы в браузере дважды. Один раз в конце первого цикла обработки событий, а затем сразу же во время первого обратного вызова таймера.
  >
  > Эти мерцания более заметны в IE и с большим количеством веб-представлений. Они не рекомендуются для iOS.
  > 
  > При очистке очереди таймера в конце первого цикла событий можно немедленно запустить любые переходы с нулевой задержкой и избежать мерцания.

Также включены следующие методы.
```typescript
function d3Click(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3MouseUp(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3MouseDown(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3MouseOver(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3MouseMove(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3MouseOut(element: JQuery, x: number, y: number, eventType?: ClickEventType, button?: number): void
function d3KeyEvent(element: JQuery, typeArg: string, keyArg: string, keyCode: number): void
function d3TouchStart(element: JQuery, touchList?: TouchList): void
function d3TouchMove(element: JQuery, touchList?: TouchList): void
function d3TouchEnd(element: JQuery, touchList?: TouchList): void
function d3ContextMenu(element: JQuery, x: number, y: number): void
```

### <a name="helper-interfaces"></a>Вспомогательные интерфейсы
Во вспомогательной функции используются следующие интерфейсы и перечисления.

```typescript
interface RgbColor {
    R: number;
    G: number;
    B: number;
    A?: number; 
}

enum ClickEventType {
    Default = 0,
    CtrlKey = 1,
    AltKey = 2,
    ShiftKey = 4,
    MetaKey = 8,
}

enum MouseEventType {
    click,
    mousedown,
    mouseup,
    mouseover,
    mousemove,
    mouseout,
}
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о написании модульных тестов для визуальных элементов Power BI на основе веб-пакетов и модульном тесте с `karma` и `jasmine` см. в статье [Учебник. Добавление модульных тестов для проектов визуальных элементов Power BI](./unit-tests-introduction.md).
