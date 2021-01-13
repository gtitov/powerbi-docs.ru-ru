---
title: Режим расширенного редактирования для визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается настройка расширенных элементов управления пользовательского интерфейса для визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 06/18/2019
ms.openlocfilehash: 02f02f23d3dfd7ec514e17d1bab17be715e9cd7d
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97889140"
---
# <a name="advanced-edit-mode-in-power-bi-visuals"></a>Режим расширенного редактирования для визуальных элементов Power BI

Если вы хотите использовать расширенные элементы управления пользовательского интерфейса для визуального элемента Power BI, примените режим расширенного редактирования. В режиме редактирования отчета нажмите кнопку **Изменить**, чтобы перейти в режим редактирования **Расширенный**. Визуальный элемент может использовать флаг `EditMode`, чтобы определить, нужно ли отображать такой элемент управления пользовательского интерфейса.

По умолчанию визуальный элемент не поддерживает режим расширенного редактирования. Если требуется другое поведение, вы можете явно задать его в файле *capabilities.json* визуального элемента с помощью свойства `advancedEditModeSupport`.

Допустимые значения:

- `0` — NotSupported

- `1` — SupportedNoAction

- `2` — SupportedInFocus

## <a name="enter-advanced-edit-mode"></a>Вход в режим расширенного редактирования

Кнопка **Изменить** отображается в следующих случаях:

* Свойству `advancedEditModeSupport` в файле *capabilities.json* присвоено значение `SupportedNoAction` или `SupportedInFocus`.

* Визуальный элемент открыт в режиме редактирования отчета.

Если свойство `advancedEditModeSupport` в файле *capabilities.json* отсутствует или имеет значение `NotSupported`, кнопка **Изменить** не отображается.

![Вход в режим редактирования](media/advanced-edit-mode/edit-mode.png)

Если нажать кнопку **Изменить**, визуальный элемент получает вызов update(), в котором элементу EditMode присвоено значение `Advanced`. В зависимости от заданного в файле *capabilities.json* значения выполняются следующие действия:

* `SupportedNoAction` —  не требуется никаких дальнейших действий со стороны узла.
* `SupportedInFocus` —  узел развертывает визуальный элемент в режим фокусировки.

## <a name="exit-advanced-edit-mode"></a>Выход из режима расширенного редактирования

Кнопка **Назад к отчету** отображается в следующих случаях:

* Свойству `advancedEditModeSupport` в файле *capabilities.json* присвоено значение `SupportedInFocus`.
