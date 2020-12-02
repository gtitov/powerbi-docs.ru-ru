---
title: 'DAX: Использование SELECTEDVALUE вместо VALUES'
description: Рекомендации по использованию функций SELECTEDVALUE.
author: peter-myers
ms.author: v-pemyer
ms.reviewer: asaxton
ms.service: powerbi
ms.subservice: powerbi
ms.topic: conceptual
ms.date: 11/20/2019
ms.openlocfilehash: 1925333b935209484855dff444542a20040a0f6a
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96394228"
---
# <a name="dax-use-selectedvalue-instead-of-values"></a>DAX: Использование SELECTEDVALUE вместо VALUES

Специалисту по моделированию данных иногда может потребоваться написать выражение DAX, которое проверяет, фильтруется ли столбец по определенному значению.

В более ранних версиях DAX это можно было безопасно реализовать с помощью шаблона, состоящего из трех функций DAX: [IF](/dax/if-function-dax), [HASONEVALUE](/dax/hasonevalue-function-dax) и [VALUES](/dax/values-function-dax). Примером может служить представленное ниже определение меры. Оно вычисляет сумму налога с продаж, но только для продаж клиентам в Австралии.

```dax
Australian Sales Tax =
IF(
    HASONEVALUE(Customer[Country-Region]),
    IF(
        VALUES(Customer[Country-Region]) = "Australia",
        [Sales] * 0.10
    )
)
```

В этом примере функция HASONEVALUE возвращает значение TRUE только тогда, когда столбец **Country-Region** (Страна или регион) фильтруется по одному значению. Если значение равно TRUE, функция VALUES сравнивается с литеральным текстом "Australia" (Австралия). Когда функция VALUES возвращает значение TRUE, мера **Sales** (Продажи) умножается на 0,10 (то есть 10 %). Если функция HASONEVALUE возвращает значение FALSE по той причине, что столбец фильтруется более чем по одному значению, первая функция IF возвращает пустое значение.

Использование функции HASONEVALUE является мерой предосторожности. Оно необходимо по той причине, что столбец **Country-Region** может фильтроваться по нескольким значениям. В этом случае функция VALUES возвращает таблицу с несколькими строками. Сравнение таблицы из нескольких строк со скалярным значением вызывает ошибку.

## <a name="recommendation"></a>Рекомендация

Мы рекомендуем использовать функцию [SELECTEDVALUE](/dax/selectedvalue-function). Она позволяет достичь того же результата, что и описанный в этой статье шаблон, но более эффективно и элегантно.

Перепишем определение меры из примера, используя функцию SELECTEDVALUE.

```dax
Australian Sales Tax =
IF(
    SELECTEDVALUE(Customer[Country-Region]) = "Australia",
    [Sales] * 0.10
)
```

> [!TIP]
> В функцию SELECTEDVALUE можно передать _альтернативное результирующее_ значение. Оно возвращается, если к столбцу не применен ни один фильтр или применено несколько фильтров.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения по этим вопросам см. в следующих ресурсах.

- [Руководство по выражениям анализа данных (DAX)](/dax/)
- Схема обучения: [Использование DAX в Power BI Desktop](/learn/paths/dax-power-bi/)
- У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
- У вас есть предложения? [Идеи по улучшению Power BI](https://ideas.powerbi.com)