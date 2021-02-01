---
title: Что можно сделать с помощью API Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Что можно сделать с помощью API Power BI? Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: overview
ms.date: 03/25/2019
ms.openlocfilehash: 8fac168bf4e2d1cb7b386a1e22da99f39b579da8
ms.sourcegitcommit: 84f0e7f31e62cae3bea2dcf2d62c2f023cc2d404
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781562"
---
# <a name="what-can-developers-do-with-the-power-bi-api"></a>Какие возможности API Power BI предоставляет разработчикам?

Интерфейс REST API для Power BI позволяет создавать приложения, которые интегрируются с отчетами, панелями мониторинга и плитками Power BI.

С помощью REST API для Power BI можно управлять объектами Power BI, такими как отчеты, наборы данных и рабочие области.

Ниже перечислено несколько задач, которые можно выполнить с помощью API-интерфейсов Power BI.

| **Интересующие темы** | **Справочные материалы** |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Внедрение отчетов, панелей мониторинга и плиток для пользователей Power BI и других программ. | [Как внедрять панели мониторинга, отчеты и плитки Power BI](../embedded/embed-sample-for-customers.md) |
| Выполняйте задачи управления объектами Power BI. | [Справочник по REST API Power BI](/rest/api/power-bi/) |
| Расширение существующего рабочего бизнес-процесса для принудительной отправки ключевых данных в панель мониторинга Power BI. | [Принудительная отправка данных на панель мониторинга](walkthrough-push-data.md) |
| Аутентификация в Power BI. | [Аутентификация в Power BI](../embedded/get-azuread-access-token.md) |

> [!NOTE]
> В интерфейсах API Power BI рабочие области по-прежнему называются группами. Если упоминаются группы, это означает, что вы работаете с рабочими областями.

## <a name="api-developer-tools"></a>Инструменты API для разработчика

| Инструменты | Описание |
|---------|-------------|
| [Инструмент "Тестовая площадка"](https://microsoft.github.io/PowerBI-JavaScript/demo) | Воспользуйтесь полным примером работы с интерфейсами API клиента для аналитики Power BI Embedded. Этот инструмент также позволит быстро познакомиться с разными примерами Power BI Embedded. |
| [Интерфейсы API клиента для аналитики Power BI Embedded](/javascript/api/overview/powerbi/) | Дополнительные сведения об интерфейсах API клиента для аналитики Power BI. |
| [Postman](https://www.getpostman.com/) | Выполнение запросов, тестирование, отладка, мониторинг, запуск автоматических тестов и многое другое. |

## <a name="push-data-into-power-bi"></a>Принудительная отправка данных в Power BI

Вы можете использовать API Power BI для [принудительной отправки данных в набор](walkthrough-push-data.md). Этот компонент позволяет добавлять строки в таблицу в наборе данных. После этого новые данные отображаются на плитках панели мониторинга и в визуальных элементах отчета.

![Принудительная отправка данных](media/overview-of-power-bi-rest-api/powerbi-push-data.png)

## <a name="github-repositories"></a>Репозитории GitHub

* [Примеры для разработчиков Power BI](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Пакет SDK для .NET](https://github.com/Microsoft/PowerBI-CSharp)
* [Интерфейсы API клиента для аналитики Power BI Embedded](/javascript/api/overview/powerbi/)

## <a name="next-steps"></a>Дальнейшие действия

* [Принудительная отправка данных в панель мониторинга Power BI](walkthrough-push-data.md)
* [Разработка визуального элемента "Круговая карточка" в Power BI](../visuals/develop-circle-card.md)
* [Справочник по REST API Power BI](rest-api-reference.md)
* [REST API в Power BI](/rest/api/power-bi/)

У вас имеются и другие вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)