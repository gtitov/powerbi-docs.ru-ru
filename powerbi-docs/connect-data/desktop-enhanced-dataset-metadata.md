---
title: Использование расширенных метаданных набора данных в Power BI Desktop
description: В этой статье описывается, как использовать расширенные метаданные набора данных в Power BI.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: conceptual
ms.date: 09/22/2020
LocalizationGroup: Connect to data
ms.openlocfilehash: 2c5e465026f1ba7564bda18ad3b005b024a663a7
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96404992"
---
# <a name="using-enhanced-dataset-metadata"></a>Использование расширенных метаданных набора данных

Когда Power BI Desktop создает отчеты, он также создает метаданные набора данных в соответствующих файлах PBIX и PBIT. Ранее метаданные хранились в формате, характерном для Power BI Desktop. В нем использовались выражения M и источники данных в кодировке Base-64, а также предположения о том, как были сохранены метаданные.

С выпуском функции **расширенных метаданных набора данных** многие из этих ограничений исключаются. PBIX-файлы автоматически обновляются до расширенных метаданных при открытии файла. При включенной функции **расширенных метаданных набора данных** метаданные, созданные Power BI Desktop, используют формат, аналогичный тому, который используется для табличных моделей Analysis Services, основанных на [табличной модели объектов](/analysis-services/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo).


Функция **расширенных метаданных набора данных** является стратегической и базовой, поскольку в будущем функциональные возможности Power BI будут создаваться на основе метаданных. Некоторые дополнительные возможности, в которых могут использоваться преимущества расширенных метаданных набора данных, включают [чтение и запись XMLA](/power-platform-release-plan/2019wave2/business-intelligence/xmla-readwrite) для управления наборами данных Power BI, а также миграцию рабочих нагрузок Analysis Services в Power BI для использования преимуществ функций следующего поколения.


## <a name="next-steps"></a>Дальнейшие действия

Power BI Desktop предоставляет широкие возможности. Дополнительные сведения об этих возможностях см. в следующих ресурсах.

* [Что такое Power BI Desktop?](../fundamentals/desktop-what-is-desktop.md)
* [Новые возможности Power BI Desktop](../fundamentals/desktop-latest-update.md)
* [Об использовании Редактора запросов в Power BI Desktop](../transform-model/desktop-query-overview.md)
* [Типы данных в Power BI Desktop](desktop-data-types.md)
* [Формирование и объединение данных в Power BI Desktop](desktop-shape-and-combine-data.md)
* [Общие задачи с запросами в Power BI Desktop](../transform-model/desktop-common-query-tasks.md)