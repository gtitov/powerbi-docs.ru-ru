---
title: Включение функции "Синхронизация срезов"для визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается добавление функции синхронизации срезов в визуальные элементы Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 06/18/2019
ms.openlocfilehash: bd69e05bba3e9449f9fb6f07bd9625dfb1ea0c08
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97885295"
---
# <a name="sync-slicers-in-power-bi-visuals"></a>Синхронизация срезов для визуальных элементов Power BI

Чтобы реализовать поддержку функции [Синхронизация срезов](../../visuals/power-bi-visualization-slicers.md), ваш настраиваемый визуальный элемент среза должен использовать API версии 1.13.0 или более поздней.

Кроме того, необходимо включить соответствующий параметр в файле *capabilities.json*, как показано в следующем коде:

```json
{
    ...
    "supportsHighlight": true,
    "suppressDefaultTitle": true,
    "supportsSynchronizingFilterState": true,
    "sorting": {
        "default": {}
    }
}
```

После обновления файла *capabilities.json* при выборе настраиваемого визуального элемента среза будет отображаться область параметров **Синхронизация срезов**.

> [!NOTE]
> Функция синхронизации срезов поддерживает не более одного поля. Если срез содержит несколько полей (**Категория** или **Мера**), эта функция будет отключена.

![Область "Синхронизация срезов"](media/enable-sync-slicers/sync-slicers-panel.png)

В области **Синхронизация срезов** можно узнать, что параметры видимости и фильтрации срезов могут применяться к нескольким страницам отчета.