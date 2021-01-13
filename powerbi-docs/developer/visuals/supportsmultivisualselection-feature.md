---
title: Функция supportsMultiVisualSelection в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается, как использовать функцию supportsMultiVisualSelection в визуальных элементах Power BI, а также требования к ее использованию. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: 9e6b17a4576f2354a5cbecc0c3a965a5611784ee
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887944"
---
# <a name="use-the-supportsmultivisualselection-feature"></a>Использование функции supportsMultiVisualSelection

Функция `supportsMultiVisualSelection` позволяет использовать выбор в нескольких визуальных элементах в отчете.

## <a name="example"></a>Пример

В отчете, состоящем более чем с одного визуального элемента, выберите два значения, чтобы эти значения применялись к другим визуальным элементам. Например, в [примере анализа розничной торговли](../../create-reports/sample-retail-analysis.md) выберите **Fashions Direct** в одном визуальном элементе. Нажмите клавишу "CTRL" и выберите **Jan** в другом визуальном элементе. Параметры выбора в отчете применяются к другим визуальным элементам, поддерживающим использование этой функции. Другие визуальные элементы теперь применяются в **Fashions Direct** и **Jan**.

## <a name="requirements"></a>Требования

Для этой функции требуется API версии 3.2.0 или более поздней версии.

Эту функцию нельзя применить к визуальным элементам изображения. Ее нельзя применить к некоторым расширенным визуальным элементам, таким как ключевые драйверы, дерево декомпозиции, визуальные элементы вопросов и ответов, текстовые поля и диаграммы датчиков.

## <a name="usage"></a>Использование

Чтобы использовать функцию `supportsMultiVisualSelection`, добавьте следующий код в файл `capabilities.json` визуального элемента.

```json
    {   
            ...
        "supportsMultiVisualSelection": true
            ...
    }
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о концепциях Power BI см. в статье [Визуальные элементы в Power BI](power-bi-visuals-concept.md).

Чтобы испытать разработку в Power BI, см. статью [Разработка круговой карточки в Power BI](develop-circle-card.md).
