---
title: Работа с маленькими диаграммами в Power BI (предварительная версия)
description: В этой статье показано, как взаимодействовать с маленькими диаграммами.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: mihart
ms.service: powerbi
ms.subservice: pbi-visuals
ms.topic: how-to
ms.date: 02/05/2021
LocalizationGroup: Visualizations
ms.openlocfilehash: 6d700d4a4bb7453f7630c76c5a3f265ee022e02a
ms.sourcegitcommit: f17acb16018752c234db6bff1f51f5130be12c58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99628247"
---
# <a name="interact-with-small-multiples-in-power-bi-preview"></a>Работа с маленькими диаграммами в Power BI (предварительная версия)

[!INCLUDE [applies-to](../includes/applies-to.md)] [!INCLUDE [yes-desktop](../includes/yes-desktop.md)] [!INCLUDE [yes-service](../includes/yes-service.md)]

Маленькие диаграммы создаются путем разделения визуального элемента на несколько его версий. В этой статье показано, как максимально эффективно взаимодействовать с ними.

:::image type="content" source="media/power-bi-visualization-small-multiples/small-mulitple-sales-category-region.png" alt-text="Снимок экрана: маленькие диаграммы для категории и региона.":::

Хотите создать маленькие диаграммы? См. статью [Создание маленьких диаграмм в Power BI (предварительная версия)](power-bi-visualization-small-multiples.md).

## <a name="scroll-in-a-small-multiple"></a>Прокрутка в маленькой диаграмме

Маленькие диаграммы могут содержать дополнительные отдельные диаграммы, которые помещаются в сетку. При этом вы можете выполнить прокрутку вниз, чтобы просмотреть остальные категории.

Для оси X с несколькими категориями также отображается полоса прокрутки в каждой копии такой оси. При прокрутке по оси все копии перемещаются одновременно. Если вы используете колесо прокрутки, удерживайте клавишу SHIFT для прокрутки осей категорий.

## <a name="select-data-to-cross-highlight"></a>Выбор данных для перекрестного выделения

Вы можете выбрать разные наборы данных, выбрав различные части визуального элемента.

### <a name="select-data-points"></a>Выбор точек данных

Наведите указатель мыши на точку данных на одной из маленьких диаграмм, чтобы отобразить всплывающую подсказку в этой диаграмме. Вы также увидите направляющую на оси X для графиков. Выберите эту точку данных, чтобы выполнить перекрестное выделение для других визуальных элементов по значениям на осях и по категории маленькой диаграммы, а также чтобы затемнить отображение других маленьких диаграмм.

:::image type="content" source="media/power-bi-visualization-small-multiples/small-multiple-select-data-point.png" alt-text="Выбор точки данных в маленькой диаграмме.":::

### <a name="select-a-categorical-axis-value"></a>Выбор значения по оси категорий

Выберите метку категории, чтобы выполнить перекрестное выделение других визуальных элементов по такому значению оси.

:::image type="content" source="media/power-bi-visualization-small-multiples/small-multiple-select-category-axis.png" alt-text="Выбор оси категорий в маленькой диаграмме.":::

### <a name="select-a-title"></a>Выбор заголовка

Выберите заголовок маленькой диаграммы, чтобы выполнить перекрестное выделение других визуальных элементов по категории в таком подзаголовке.

:::image type="content" source="media/power-bi-visualization-small-multiples/small-multiple-select-title.png" alt-text="Выбор заголовка в маленькой диаграмме.":::

### <a name="legend"></a>Условные обозначения

Выберите категорию условных обозначений, чтобы выполнить перекрестное выделение других визуальных элементов и других маленьких диаграмм.

:::image type="content" source="media/power-bi-visualization-small-multiples/small-multiple-select-legend.png" alt-text="Выбор элемента в условных значениях в маленькой диаграмме.":::


## <a name="sort"></a>Сортировка

Новые функции сортировки позволяют одновременно отсортировать несколько аспектов визуального элемента. Выполните сортировку по категории, а также по оси в каждой маленькой диаграмме. 

:::image type="content" source="media/power-bi-visualization-small-multiples/small-multiple-sort.png" alt-text="Сортировка маленьких диаграмм.":::

## <a name="next-steps"></a>Дальнейшие действия

[Создание маленьких диаграмм в Power BI (предварительная версия)](power-bi-visualization-small-multiples.md)
