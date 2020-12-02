---
title: Кольцевые диаграммы в Power BI
description: Кольцевые диаграммы в Power BI
author: mihart
ms.author: mihart
ms.reviewer: mihart
ms.service: powerbi
ms.subservice: pbi-visuals
ms.topic: how-to
ms.date: 05/05/2020
LocalizationGroup: Visualizations
ms.openlocfilehash: 3ebd618011f8c7a5fefb1187283702a85dee407c
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96386190"
---
# <a name="create-and-use-doughnut-charts-in-power-bi"></a>Создание и использование кольцевых диаграмм в Power BI

[!INCLUDE[consumer-appliesto-nyyn](../includes/consumer-appliesto-nyyn.md)]

[!INCLUDE [power-bi-visuals-desktop-banner](../includes/power-bi-visuals-desktop-banner.md)]

Кольцевая диаграмма похожа на круговую диаграмму в том, что она показывает отношение между целым и частями. Единственное отличие в том, что центр диаграммы пуст и в него можно добавить подпись или значок.

## <a name="prerequisite"></a>Необходимое условие

В этом руководстве используется пример PBIX-файла с примером [Анализ розничной торговли](https://download.microsoft.com/download/9/6/D/96DDC2FF-2568-491D-AAFA-AFDD6F763AE3/Retail%20Analysis%20Sample%20PBIX.pbix).

1. В верхнем левом разделе меню выберите **Файл** > **Открыть**.
   
2. Найдите свою копию PBIX-файла с примером **Анализ розничной торговли**.

1. Откройте PBIX-файл с примером **Анализ розничной торговли** в представлении отчета ![Снимок экрана: значок представления отчета](media/power-bi-visualization-kpi/power-bi-report-view.png).

1. Выбрать ![Снимок экрана: желтая вкладка,](media/power-bi-visualization-kpi/power-bi-yellow-tab.png) чтобы создать новую страницу.


> [!NOTE]
> Для предоставления общего доступа к отчету Power BI и вам, и коллеге необходимо иметь отдельные лицензии Power BI Pro или сохранить отчет в емкости Премиум.    

## <a name="create-a-doughnut-chart"></a>Создание кольцевой диаграммы

1. Откройте пустую страницу отчета и в области "Поля" выберите **Продажи** \> **Продажи за последний год**.  
   
3. В области "Визуализации" щелкните значок кольцевой диаграммы ![значок кольцевой диаграммы](media/power-bi-visualization-doughnut-charts/power-bi-icon.png), чтобы преобразовать линейчатую диаграмму в кольцевую. Если поля **Продажи за прошлый год** нет в области **Значения**, перетащите его туда.
     
   ![Панель визуализации с выбранным значком кольцевой диаграммы](media/power-bi-visualization-doughnut-charts/power-bi-doughnut-chart.png)

4. Выберите **Элемент** \> **Категория**, чтобы добавить его в область **условных обозначений**. 
     
    ![кольцевая диаграмма рядом с областью полей](media/power-bi-visualization-doughnut-charts/power-bi-doughnut-done.png)

5. При необходимости [настройте размер и цвет текста диаграммы](power-bi-visualization-customize-title-background-and-legend.md). 

## <a name="considerations-and-troubleshooting"></a>Рекомендации и устранение неполадок
* Сумма значений кольцевой диаграммы должна составлять 100 %.
* Слишком большое число категорий затрудняет чтение и понимание.
* Кольцевые диаграммы лучше подходят для сравнения определенной части с целым, а не отдельных частей друг с другом. 

## <a name="next-steps"></a>Дальнейшие действия
[Воронкообразные диаграммы в Power BI](power-bi-visualization-funnel-charts.md)

[Типы визуализаций в Power BI](power-bi-visualization-types-for-reports-and-q-and-a.md)


