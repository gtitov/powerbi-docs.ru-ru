---
title: Исходящий трафик Power BI и Azure
description: Узнайте, как взимается плата за исходящий трафик Azure и Power BI в зависимости от расположения клиента и Power BI Premium
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 01/19/2021
LocalizationGroup: Data from databases
ms.openlocfilehash: ec47968294e0fd905d1733bdb30ae1840069aed7
ms.sourcegitcommit: 96080432af4c8e3fe46c23274478ccffa0970efb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "98597475"
---
# <a name="power-bi-and-azure-egress"></a>Исходящий трафик Power BI и Azure

Исходящий трафик центров обработки данных Azure может повлечь расходы, связанные с платой за пропускную способность. При использовании Power BI с источниками данных Azure платы за исходящий трафик Azure можно избежать, сделав так, чтобы ваш клиент Power BI находился в том же регионе, что и источники данных Azure.

Когда клиент Power BI развертывается в одном регионе Azure с развертываемыми источниками данных, плата за исходящий трафик для планового обновления и взаимодействия DirectQuery не взимается. 

## <a name="determining-where-your-power-bi-tenant-is-located"></a>Как определить, где расположен ваш клиент Power BI

Чтобы узнать, где расположен ваш клиент Power BI, см. статью [Где расположен мой клиент Power BI](../admin/service-admin-where-is-my-tenant-located.md).

Для клиентов Power BI Premium с несколькими регионами: если ваш клиент Power BI не в оптимальном расположении относительно некоторых источников данных в Azure, можно развернуть Power BI Premium с поддержкой нескольких регионов в нужном регионе Azure и использовать преимущества расположения вашего клиента Power BI и источников данных Azure в одном регионе Azure.

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о Power BI Premium и размещении в различных регионах см. на следующих ресурсах:

* [Сведения о ценах на пропускную способность Azure](https://azure.microsoft.com/pricing/details/bandwidth/)
* [Что такое Microsoft Power BI Premium?](../admin/service-premium-what-is.md)
* [Как купить Power BI Premium](../admin/service-admin-premium-purchase.md)
* [Поддержка нескольких регионов Power BI Premium (предварительная версия)](../admin/service-admin-premium-multi-geo.md)
* [Где расположен мой клиент Power BI?](../admin/service-admin-where-is-my-tenant-located.md)
* [Вопросы и ответы по Power BI Premium](../admin/service-premium-faq.md)
