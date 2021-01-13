---
title: Примеры визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье представлены примеры визуальных элементов Power BI, в том числе срезы, более 20 типов диаграмм, WebGL, визуальные элементы и скрипты R. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 03/17/2019
ms.openlocfilehash: 3da805a10a8b43dc7b1f1750583a79494557d519
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888496"
---
# <a name="samples-of-power-bi-visuals"></a>Примеры визуальных элементов Power BI

Вы можете скачать, использовать и изменить эти визуальные элементы Power BI на сайте GitHub. В этих примерах показано, как обрабатываются распространенные ситуации при разработке с помощью Power BI.

## <a name="slicers"></a>Срезы

Срез сужает часть данных, отображаемую в других визуализациях в отчете. Срезы — это один из нескольких способов фильтрации данных в Power BI.

| <img src="media/samples/chiclet-slicer.png" alt="Screenshot shows Chiclet Slicer." width="200">  | <img src="media/samples/timeline-slicer.png" alt="Screenshot shows Timeline slicer." width="200"> | <img src="media/samples/sample-slicer.png" alt="Screenshot shows Slicer sample." width="200">|
| ------------- | ------------- | -------------|
| [Срез Chiclet](https://github.com/Microsoft/powerbi-visuals-chicletslicer/)  </br>Кнопки с изображениями и текстом, которые служат фильтром на холсте в других визуальных элементах | [Timeline slicer](https://github.com/Microsoft/powerbi-visuals-timeline/) </br>Графический селектор диапазонов дат, с помощью которого выполняется фильтрация по датам. | [Пример среза](https://github.com/Microsoft/powerbi-visuals-sampleslicer/) </br>Демонстрирует использование API расширенной фильтрации.

## <a name="charts"></a>Диаграммы

Используйте преимущества нашей коллекции, в том числе линейчатых диаграмм, круговых диаграмм, облака слов и др.

| <img src="media/samples/aster-plot.png" alt="Screenshot shows Aster Plot." width="200">  | <img src="media/samples/bullet-chart.png" alt="Screenshot shows Bullet chart." width="200"> | <img src="media/samples/Chord.png" alt="Screenshot shows Chord." width="200">|
| ------------- | ------------- | -------------|
| [Круговая диаграмма с индивидуальным радиусом срезов](https://github.com/Microsoft/powerbi-visuals-asterplot/)  </br>Изгиб на стандартной кольцевой диаграмме, где второе значение используется для указания угла поворота | [Диаграмма-шкала](https://github.com/Microsoft/powerbi-visuals-bulletchart/) </br>Линейчатая диаграмма с дополнительными визуальными элементами, предоставляющими контекст для отслеживания целей | [Хордовая диаграмма](https://github.com/Microsoft/powerbi-visuals-chord/) </br>Графический метод отображения взаимосвязей данных в матрице
| <img src="media/samples/dot-plot.png" alt="Screenshot shows Dot plot." width="200"> | <img src="media/samples/dual-kpi.png" alt="Screenshot shows Dual K P I." width="200">| <img src="media/samples/enhanced-scatter.png" alt="Screenshot shows Enhanced Scatter." width="200"> 
| [Точечная диаграмма](https://github.com/Microsoft/powerbi-visuals-dotplot/) </br>Показывает распределение частот в виде удобной диаграммы. | [Dual KPI](https://github.com/Microsoft/powerbi-visuals-dualkpi/) </br>Эффективная визуализация двух мер с течением времени, отображающая их тенденцию на объединенной временной шкале | [Расширенная точечная диаграмма](https://github.com/Microsoft/powerbi-visuals-enhancedscatter/) </br>Улучшения на имеющейся точечной диаграмме
| <img src="media/samples/forcegraph.png" alt="Screenshot shows Force Graph." width="200">| <img src="media/samples/gantt.png" alt="Screenshot shows Gantt." width="200">| <img src="media/samples/table-heatmap.png" alt="Screenshot shows Table Heatmap." width="200">
| [Force Graph](https://github.com/Microsoft/powerbi-visuals-forcegraph/) </br>Принудительно структурированная диаграмма с изогнутыми траекториями. Полезна для отображения связей между сущностями | [Диаграмма Ганта](https://github.com/Microsoft/powerbi-visuals-gantt/) </br>Линейчатая диаграмма, которая иллюстрирует временную шкалу или расписание проекта вместе с ресурсами | [Диаграмма "Тепловая карта"](https://github.com/Microsoft/powerbi-visuals-heatmap/) </br>Простое и интуитивно понятное сравнение данных в таблице с использованием цветов
| <img src="media/samples/histogram-chart.png" alt="Screenshot shows Histogram chart." width="200"> | <img src="media/samples/linedot-chart.png" alt="Screenshot shows LineDot chart." width="200"> | <img src="media/samples/mekko-chart.png" alt="Screenshot shows Mekko chart." width="200"> 
| [Гистограмма](https://github.com/Microsoft/powerbi-visuals-histogram/) </br>Визуализация распределения данных за непрерывный интервал или определенный период времени | [Линейно-точечная диаграмма](https://github.com/Microsoft/powerbi-visuals-linedotchart/) </br>График с анимированными точками, который помогает привлечь внимание аудитории к данным | [Диаграмма Mekko](https://github.com/Microsoft/powerbi-visuals-mekkochart/) </br>Сочетание нормированной гистограммы и нормированной линейчатой диаграммы в одном представлении
| <img src="media/samples/multikpi.png"alt="Screenshot shows Multi K P I." width="200"> | <img src="media/samples/powerkpi.png"alt="Screenshot shows Power K P I." width="200"> | <img src="media/samples/powerkpi-matrix.png"alt="Screenshot shows Power K P I Matrix." width="200"> 
| [Несколько КПЭ](https://github.com/microsoft/PowerBI-visuals-MultiKPI/) </br> Эффективная визуализация с несколькими КПЭ, содержащая ключевой показатель КПЭ и несколько спарклайнов для поддержки данных | [Ключевой показатель эффективности производительности](https://github.com/microsoft/PowerBI-visuals-PowerKPI/) </br>Эффективный индикатор КПЭ с многострочным графиком и метками для текущей даты, значения и расхождений. | [Матрица КПЭ производительности](https://github.com/microsoft/PowerBI-visuals-PowerKPIMatrix/) </br>Мониторинг сбалансированных систем показателей и неограниченного количества метрик и ключевых показателей эффективности в форме компактного, удобного для чтения списка
| <img src="media/samples/pulse-chart.png" alt="Screenshot shows Pulse chart." width="200">| <img src="media/samples/radar-chart.png" alt="Screenshot shows Radar chart." width="200"> | <img src="media/samples/sankey-chart.png" alt="Screenshot shows Sankey chart." width="200"> 
| [Диаграмма "Пульс"](https://github.com/Microsoft/powerbi-visuals-pulsechart/) </br>Этот график с примечаниями в виде ключевых событий идеально подходит для описания ситуаций с использованием данных| [Лепестковая диаграмма](https://github.com/Microsoft/powerbi-visuals-radarchart/) </br>Диаграмма с несколькими мерами, нанесенными на ось категорий для сравнения атрибутов | [Диаграмма Sankey](https://github.com/Microsoft/powerbi-visuals-sankey/) </br>Диаграмма потока, в которой ширина ряда пропорциональна объему потока
| <img src="media/samples/stream-graph.png" alt="Screenshot shows Stream graph." width="200"> | <img src="media/samples/sunburst.png" alt="Screenshot shows Sunburst chart." width="200">| <img src="media/samples/tornado.png" alt="Screenshot shows Tornado chart." width="200">
| [График потока](https://github.com/Microsoft/powerbi-visuals-streamgraph/) </br>Диаграмма с областями и накоплением с плавной интерполяцией, которая часто используется для отображения значений за период времени | [Диаграмма "солнечные лучи"](https://github.com/Microsoft/powerbi-visuals-sunburst/) </br>Многоуровневая кольцевая диаграмма для визуализации иерархических данных| [Диаграмма-торнадо](https://github.com/Microsoft/powerbi-visuals-tornado/) </br>Сравнение относительной важности переменных между двумя группами
 | <img src="media/samples/word-cloud.png" alt="Screenshot shows Word Cloud." width="200">
 | [Облако Word](https://github.com/Microsoft/powerbi-visuals-wordcloud/) </br>Интересный визуальный элемент, показывающий частоту использования слов в тексте

## <a name="webgl"></a>WebGL

WebGL позволяет веб-содержимому использовать API на основе OpenGL ES 2.0 для двумерной и трехмерной отрисовки на холсте HTML.

| <img src="media/samples/globe-map.png" alt="Screenshot shows Globe Map." width="250">|
| ------------- |
| [Схема земного шара](https://github.com/Microsoft/powerbi-visuals-globemap/) </br>График расположений на интерактивной трехмерной карте

## <a name="r-visuals"></a>Визуальные элементы R

В этих примерах показано, как использовать аналитические и визуальные возможности визуальных элементов и скриптов на основе R.

| <img src="media/samples/association-rules.png" alt="Screenshot shows Association rules." width="200">| <img src="media/samples/clustering.png" alt="Screenshot shows Clustering." width="200">| <img src="media/samples/clustering-with-outliers.png" alt="Screenshot shows Clustering with outliers." width="200">|
|------------- |------------- |------------- |------------- |
| [Правила взаимосвязей](https://github.com/Microsoft/powerbi-visuals-assorules/) </br>Обнаружение связей между на первый взгляд несвязанными данными с помощью операторов if-then | [Кластеризация](https://github.com/Microsoft/powerbi-visuals-clustering-kmeans/) </br>Поиск групп сходства в данных с помощью алгоритма K-средних | [Кластеризация с использованием выбросов](https://github.com/microsoft/PowerBI-visuals-dbscan/) </br>Поиск групп сходства и выбросов в данных
| <img src="media/samples/correlation-plot.png" alt="Screenshot shows Correlation plot." width="200"> | <img src="media/samples/decision-tree-chart.png" alt="Screenshot shows Decision tree chart." width="200"> | <img src="media/samples/forecasting-tbats.png" alt="Screenshot shows Forecasting T B A T S." width="200"> 
| [Диаграмма корреляции](https://github.com/Microsoft/powerbi-visuals-corrplot/) </br>Выделение наиболее коррелированных переменных в таблице данных | [Схема дерева решений](https://github.com/Microsoft/powerbi-visuals-decision-tree/) </br>Схематическая диаграмма в виде дерева для определения статистической вероятности с использованием рекурсивного секционирования | [Диаграмма прогнозирования TBATS](https://github.com/Microsoft/powerbi-visuals-forcasting-tbats/) </br>Прогнозирование временных рядов с несколькими сезонностями с использованием модели TBATS
| <img src="media/samples/forecasting-with-ARIMA.png" alt="Screenshot shows Forecasting with ARIMA." width="200"> | <img src="media/samples/funnel-plot.png" alt="Screenshot shows Funnel plot." width="200"> | <img src="media/samples/outliers-detection.png" alt="Screenshot shows Outliers detection." width="200"> 
| [Прогнозирование с помощью ARIMA](https://github.com/Microsoft/powerbi-visuals-forcastingarima/) </br>Прогнозирование будущих значений на основе исторических данных с использованием авторегрессионного интегрированного скользящего среднего (ARIMA) | [Воронкообразная диаграмма](https://github.com/Microsoft/powerbi-visuals-funnel/) </br>Поиск выбросов в данных с помощью воронкообразного графика | [Обнаружение выбросов](https://github.com/Microsoft/powerbi-visuals-outliers-det/) </br>Поиск выбросов в данных с помощью наиболее подходящего метода и графика
| <img src="media/samples/spline-chart.png" alt="Screenshot shows Spline chart." width="200"> | <img src="media/samples/time-series-decomposition-chart.png" alt="Screenshot shows Time Series decomposition chart." width="200"> | <img src="media/samples/time-series-forecasting-chart.png" alt="Screenshot shows Time series forecasting chart." width="200">
| [Сплайн-диаграмма](https://github.com/Microsoft/powerbi-visuals-spline/) </br>Визуализация и понимание искаженных данных | [Диаграмма декомпозиции временных рядов](https://github.com/Microsoft/powerbi-visuals-timeseriesdecomposition/) </br>Общие сведения о компонентах временных рядов с использованием "сезонных и трендовых декомпозиций с помощью Loess" | [Диаграмма прогнозирования временных рядов](https://github.com/Microsoft/powerbi-visuals-forcasting-exp/) </br>Использование модели экспоненциального сглаживания для прогнозирования будущих значений на основе ранее отслеживаемых значений

## <a name="next-steps"></a>Дальнейшие действия

Попробуйте создать визуализации Power BI, выполнив инструкции, приведенные в руководстве [Разработка визуализации "Круговая карточка" в Power BI](develop-circle-card.md).
