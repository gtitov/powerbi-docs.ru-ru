---
title: Взаимодействие визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, как проверить, допускается ли взаимодействие визуальных элементов в Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 06/18/2019
ms.openlocfilehash: a5b46e901b5e8cabc00d48e4ef307b2ae98de2b6
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888519"
---
# <a name="visual-interactions-in-power-bi-visuals"></a>Взаимодействие визуальных элементов в Power BI

Визуальные элементы могут запрашивать значение флага `allowInteractions`, которое указывает, должен ли визуальный элемент допускать взаимодействие с визуальными элементами. Например, визуальные элементы допускают взаимодействие во время просмотра или редактирования отчета и не допускают его при просмотре на панели мониторинга. К таким видам взаимодействия относятся *щелчок*, *сдвиг*, *масштабирование*, *выделение* и другие. 

> [!NOTE]
> Независимо от настройки флага, необходимо включить всплывающие подсказки во всех сценариях.

Флаг `allowInteractions` передается в виде логического значения во время инициализации визуального элемента в качестве члена интерфейса IVisualHost.

В любом сценарии Power BI, требующем отсутствия взаимодействия визуальных элементов (например, для плиток панели мониторинга), для флага `allowInteractions` будет установлено значение `false`. В противном случае (например, для отчета), флагу `allowInteractions` присваивается значение `true`.

Дополнительные сведения см. в [репозитории визуальных элементов SampleBarChart](https://github.com/Microsoft/PowerBI-visuals-sampleBarChart/commit/59a47935d8f5272ce145fe804193599ddb7e2001).

```typescript
   ...
   let allowInteractions = options.host.allowInteractions;
   bars.on('click', function(d) {
       if (allowInteractions) {
           selectionManager.select(d.selectionId);
           ...
       }
   });
```
