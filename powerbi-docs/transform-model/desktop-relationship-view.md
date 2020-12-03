---
title: Представление "Модель" в Power BI Desktop
description: Представление "Модель" в Power BI Desktop
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-transform-model
ms.topic: how-to
ms.date: 01/17/2020
LocalizationGroup: Model your data
ms.openlocfilehash: b257fc5af97cb16798cc27bdbdb92c1b63a65181
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96413778"
---
# <a name="work-with-model-view-in-power-bi-desktop"></a>Работа с представлением "Модель" в Power BI Desktop

В *представлении "Модель"* показаны все таблицы, столбцы и связи в модели. Это может быть особенно удобно, если модель содержит сложные связи между большим количеством таблиц.

Чтобы просмотреть представление существующей модели, щелкните значок **Модель** в боковой части окна. Наведите курсор на строку связи для отображения используемых столбцов.

![Представление "Модель", Power BI Desktop](media/desktop-relationship-view/model-view-full-screen.png)

На рисунке видно, что таблица *Stores* имеет столбец *StoreKey*, связанный с таблицей *Sales*, которая также имеет столбец *StoreKey*. Две таблицы имеют связь *Многие к одному* (\*: 1). Стрелка в середине строки показывает направление потока контекста фильтра. Двойная стрелка означает, что для кросс-фильтрации выбрано значение *Двунаправленная*.

Дважды щелкните связь, чтобы открыть ее в диалоговом окне **Изменение связи**. Дополнительные сведения о связях см. в разделе [Создание связей и управление ими в Power BI Desktop](desktop-create-and-manage-relationships.md).
