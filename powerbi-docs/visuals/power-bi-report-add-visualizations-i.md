---
title: Часть 1. Добавление визуализаций в отчет Power BI
description: Часть 1. Добавление визуализаций в отчет Power BI
author: msftrien
ms.reviewer: mihart
featuredvideoid: ''
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: how-to
ms.date: 05/06/2020
ms.author: rien
LocalizationGroup: Visualizations
ms.openlocfilehash: 3a2002c9f17428c84704d68f621cf18443252557
ms.sourcegitcommit: 5ccab484cf3532ae3a16acd5fc954b7947bd543a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "93411896"
---
# <a name="add-visuals-to-a-power-bi-report-part-1"></a>Добавление визуальных элементов в отчет Power BI (часть 1)

[!INCLUDE[consumer-appliesto-nyyn](../includes/consumer-appliesto-nyyn.md)]    

[!INCLUDE [power-bi-visuals-desktop-banner](../includes/power-bi-visuals-desktop-banner.md)]

В этой статье содержатся краткие вводные сведения о создании визуализации в отчете. Эта информация относится к службе Power BI и к Power BI Desktop. Дополнительные сведения см. в [части 2](power-bi-report-add-visualizations-ii.md) этой серии.

## <a name="prerequisites"></a>Предварительные требования

В этом руководстве используется [PBIX-файл "Продажи и маркетинг"](https://download.microsoft.com/download/9/7/6/9767913A-29DB-40CF-8944-9AC2BC940C53/Sales%20and%20Marketing%20Sample%20PBIX.pbix).

1. В верхнем левом разделе меню Power BI Desktop выберите пункты **Файл** > **Открыть**.
   
2. Найдите свою копию **PBIX-файла "Продажи и маркетинг"** .

1. Откройте PBIX-файл **Продажи и маркетинг** в представлении отчета ![Снимок экрана: значок представления отчета](media/power-bi-visualization-kpi/power-bi-report-view.png).

1. Выбрать ![Снимок экрана: желтая вкладка,](media/power-bi-visualization-kpi/power-bi-yellow-tab.png) чтобы создать новую страницу.

> [!NOTE]
> Для предоставления общего доступа к отчету Power BI и вам, и коллеге необходимо иметь отдельные лицензии Power BI Pro или сохранить отчет в емкости Премиум. См. статью [Фильтрация и совместное использование отчета Power BI](../collaborate-share/service-share-reports.md).

## <a name="add-visualizations-to-the-report"></a>Добавление визуализаций к отчету

1. Создайте визуализацию, выбрав поле на панели **Поля** .

    Начните с числового поля, например **Sales** > **TotalSales** (Продажи - Общие продажи). Power BI создаст гистограмму с одним столбцом.

    ![Снимок экрана: гистограмма с одним столбцом.](media/power-bi-report-add-visualizations-i/power-bi-column-chart.png)

    Начните с поля категории, например **Имя** или **Продукт**. Создайте в Power BI таблицу и добавьте поле в область **Значения**.

    ![Снимок экрана таблицы с четырьмя категориями](media/power-bi-report-add-visualizations-i/power-bi-product.png)

    Кроме того, можно начать с поля для географических данных, такого как **Геообъект** > **Город**. Создание визуализации карты при помощи Power BI и Карт Bing.

    ![Снимок экрана: визуализация карты.](media/power-bi-report-add-visualizations-i/power-bi-maps.png)

## <a name="change-the-type-of-visualization"></a>Изменение типа визуализации

 Создайте визуализацию и измените ее тип. 
 
 1. Выберите **Продукт** > **Категория** , а затем **Продукт** > **Число продуктов** , чтобы добавить эти поля в раздел **Значения**.

    ![Снимок экрана: панель "Поля" с вызванным разделом "Значения".](media/power-bi-report-add-visualizations-i/power-bi-create-visual.png)

1. Измените визуализацию на гистограмму, выбрав значок **Гистограмма с накоплением**.

   ![Снимок экрана: панель "Визуализации" после нажатия значка "Гистограмма с накоплением".](media/power-bi-report-add-visualizations-i/power-bi-convert.png)

1. Чтобы изменить способ сортировки визуального элемента, выберите **Дополнительные действия** (...).  Используйте параметры сортировки, чтобы изменить направление сортировки (по возрастанию или по убыванию) и столбец, используемый для сортировки ( **Сортировать по** ).

   ![Снимок экрана с раскрывающимся списком "Другие действия".](media/power-bi-report-add-visualizations-i/power-bi-sort.png)
  
## <a name="next-steps"></a>Дальнейшие действия

 Дальнейшие действия

* [Часть 2. Добавление визуализаций в отчет Power BI](power-bi-report-add-visualizations-ii.md)

* [Взаимодействовать с визуализациями](../consumer/end-user-reading-view.md) в отчете.
