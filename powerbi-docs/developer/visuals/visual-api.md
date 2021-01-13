---
title: API IVisual в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается использование API IVisual для визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 03/19/2020
ms.openlocfilehash: 7b81ecfa1b97b202b6c1ff306cf858f2ea00acde
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888542"
---
# <a name="visual-api"></a>API визуальных элементов
Все визуальные элементы начинаются с класса, реализующего интерфейс `IVisual`. Классу можно присвоить любое имя, если существует только один класс, реализующий интерфейс `IVisual`.

> [!NOTE]
> Имя визуального класса должно соответствовать значению, определенному в файле *pbiviz.json*.

Ознакомьтесь с примером класса визуального элемента с указанными ниже методами, которые необходимо реализовать:

* `constructor` — стандартный конструктор для инициализации состояния визуального элемента.
* `update` необходим для обновления данных визуального элемента.
* `enumerateObjectInstances` необходим, чтобы вернуть объекты для заполнения панели свойств (параметры форматирования), позволяющей выполнить необходимые изменения.
* `destroy` — стандартный деструктор для очистки.

```typescript
class MyVisual implements IVisual {
    
    constructor(options: VisualConstructorOptions) {
        //one time setup code goes here (called once)
    }
    
    public update(options: VisualUpdateOptions): void {
        //code to update your visual goes here (called on all view or data changes)
    }

    public enumerateObjectInstances(options: EnumerateVisualObjectInstancesOptions): VisualObjectInstanceEnumeration {
        //returns objects to populate the property pane (called for each object defined in capabilities)
    }
    
    public destroy(): void {
        //one time cleanup code goes here (called once)
    }
}
```

## <a name="constructor"></a>constructor

Конструктор класса визуальных элементов вызывается при создании экземпляра визуального элемента. Его можно использовать для любых операций настройки, необходимых для визуального элемента.

```typescript
constructor(options: VisualConstructorOptions)
```

**VisualConstructorOptions**

* `element: HTMLElement` — ссылка на элемент DOM, который будет содержать визуальный элемент.
* `host: IVisualHost` — коллекция свойств и служб, которые можно использовать для взаимодействия с узлом визуального элемента (Power BI).

   `IVisualHost` содержит следующие службы:

   ```typescript
   export interface IVisualHost extends extensibility.IVisualHost {
       createSelectionIdBuilder: () => visuals.ISelectionIdBuilder;
       : () => ISelectionManager;
       colorPalette: ISandboxExtendedColorPalette;
       persistProperties: (changes: VisualObjectInstancesToPersist) => void;
       applyJsonFilter: (filter: IFilter[] | IFilter, objectName: string, propertyName: string, action: FilterAction) => void;
       tooltipService: ITooltipService;
       telemetry: ITelemetryService;
       authenticationService: IAuthenticationService;
       locale: string;
       allowInteractions: boolean;
       launchUrl: (url: string) => void;
       fetchMoreData: () => boolean;
       instanceId: string;
       refreshHostData: () => void;
       createLocalizationManager: () => ILocalizationManager;
       storageService: ILocalVisualStorageService;
       eventService: IVisualEventService;
       switchFocusModeState: (on: boolean) => void;
   }
   ```
   * `createSelectionIdBuilder`: создает и сохраняет метаданные для выбираемых элементов в визуальном элементе.
   * `createSelectionManager`: создает мост связи, используемый для уведомления узла визуального элемента об изменениях в состоянии выбора (см. сведения на [этой странице](./selection-api.md)).
   * `createLocalizationManager`: создает диспетчер для помощи с [локализацией](./localization.md).
   * `allowInteractions: boolean` — логический флажок, указывающий, должен ли визуальный элемент быть интерактивным.
   * `applyJsonFilter`: применяет определенные типы фильтров (см. страницу об [API фильтров](./filter-api.md)).
   * `persistProperties`: позволяет пользователям сохранять свойства вместе с определением визуального элемента, чтобы они были доступны при следующей перезагрузке.
   * `eventService`: возвращает [службу событий](./event-service.md) для поддержки событий **преобразователя**.
   * `storageService`: возвращает службу для помощи при использовании [локального хранилища](./local-storage.md) в визуальном элементе.
   * `authenticationService`: создает службу для помощи при проверке подлинности пользователя.
   * `tooltipService`: возвращает [службу подсказки](./add-tooltips.md) для помощи при использовании подсказок в визуальном элементе.
   * `launchUrl`: помогает при [открытии URL-адреса](./launch-url.md) в следующей вкладке.
   * `locale`: возвращает строку языкового стандарта (см. сведения на [этой странице](./localization.md)).
   * `instanceId`: возвращает строку для определения текущего экземпляра визуального элемента.
   * `colorPalette`: возвращает colorPalette для применения цветов к данным.
   * `fetchMoreData`: поддерживает использование большего количества данных, чем при стандартном ограничении (1000 строк).
   * `switchFocusModeState`: помогает при изменении состояния режима фокусировки.

## <a name="update"></a>обновить

Все визуальные элементы должны реализовывать общедоступный метод обновления, который вызывается при изменении в среде данных или узла.

```typescript
public update(options: VisualUpdateOptions): void
```

**VisualUpdateOptions**

* `viewport: IViewport` — размеры окна просмотра, в котором визуальный элемент должен быть преобразован.
* `dataViews: DataView[]` — объект dataview, который содержит все данные, необходимые для преобразования визуального элемента (визуальный элемент обычно использует категориальное свойство в DataView).
* `type: VisualUpdateType` — флажки для обозначения типов данного обновления (**Данные** | **Изменить размер** | **ViewMode** | **Стиль** | **ResizeEnd**).
* `viewMode: ViewMode` — флажки для обозначения режима просмотра визуального элемента (**Просмотр** | **Изменить** | **InFocusEdit**).
* `editMode: EditMode` — флажок для обозначения режима редактирования визуального элемента (**По умолчанию** | **Расширенный**) (если визуальный элемент поддерживает **AdvancedEditMode**, он должен преобразовывать свои расширенные элементы управления пользовательского интерфейса для просмотра, только если для **editMode** задано значение **Расширенный**; см. страницу со сведениями об [AdvancedEditMode](./advanced-edit-mode.md)).
* `operationKind?: VisualDataChangeOperationKind` — флажок для обозначения типа изменения данных (**Создать** | **Добавить**).
* `jsonFilters?: IFilter[]` — коллекция примененных фильтров JSON.
* `isInFocus?: boolean` — флажок, указывающий, находится ли визуальный элемент в режиме фокусировки.
    
## <a name="enumerateobjectinstances-optional"></a>enumerateObjectInstances `optional`

Этот метод вызывается для каждого объекта, указанного в возможностях. Используя эти параметры (в настоящее время только имя), вы возвращаете `VisualObjectInstanceEnumeration` с информацией о том, как отобразить это свойство.

```typescript
enumerateObjectInstances(options:EnumerateVisualObjectInstancesOptions):VisualObjectInstanceEnumeration
```

**EnumerateVisualObjectInstancesOptions**

* `objectName: string` — имя объекта.

## <a name="destroy-optional"></a>destroy `optional`

Функция destroy вызывается при выгрузке визуального элемента и может использоваться для задач очистки, таких как удаление прослушивателей событий.

``` typescript
public destroy(): void
```

> [!Note]
> Power BI обычно не вызывает `destroy`, так как быстрее удалить весь IFrame, содержащий визуальный элемент.
