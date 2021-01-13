---
title: Масштабирование емкости Power BI Embedded для решения встроенной бизнес-аналитики Power BI
description: В этой статье рассматривается масштабирование емкости Power BI в Microsoft Azure для решения встроенной бизнес-аналитики Power BI.
author: KesemSharabi
ms.author: kesharab
services: power-bi-embedded
editor: ''
tags: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.date: 01/31/2019
ms.openlocfilehash: 19dfff03e2ec17c2b969a80c9fe0d2087c189184
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887323"
---
# <a name="scale-your-power-bi-embedded-capacity-in-the-azure-portal"></a>Масштабирование емкости Power BI Embedded на портале Azure

В этой статье рассматривается масштабирование емкости Power BI Embedded в Microsoft Azure. Масштабирование позволяет увеличить или уменьшить размер доступной емкости.

Предполагается, что вы создали емкость Power BI Embedded. Если нет, см. раздел [Создание емкости Power BI Embedded на портале Azure](azure-pbie-create-capacity.md).

> [!NOTE]
> Операция масштабирования может занять около минуты. В это время емкость будет недоступна. Внедренное содержимое может не загрузиться.

## <a name="scale-a-capacity"></a>Масштабирование емкости

1. Войдите на [портал Azure](https://portal.azure.com/).

2. Выберите **Все службы** > **Power BI Embedded**, чтобы просмотреть доступные емкости.

    ![Все службы на портале Azure](media/azure-pbie-scale-capacity/azure-portal-more-services.png)

3. Выберите емкость, которую нужно масштабировать.

    ![Список емкостей Power BI Embedded на портале Azure](media/azure-pbie-scale-capacity/azure-portal-capacity-list.png)

4. Выберите **Ценовая категория** в разделе **Масштаб** в емкости.

    ![Параметр ценовой категории в разделе масштаба](media/azure-pbie-scale-capacity/azure-portal-scale-pricing-tier.png)

    Текущая ценовая категория выделена синим цветом.

    ![Текущая ценовая категория выделена синим цветом](media/azure-pbie-scale-capacity/azure-portal-current-tier.png)

5. Чтобы увеличить или уменьшить масштаб, выберите новую ценовую категорию. При выборе новой ценовой категории этот вариант будет выделен пунктирной синей линией. Выберите **Выбрать** для перехода на новую категорию.

    ![Выбор новой категории](media/azure-pbie-scale-capacity/azure-portal-select-new-tier.png)

    Масштабирование емкости может занять одну-две минуты.

6. Подтвердите категорию, просмотрев вкладку общих сведений. Указана текущая ценовая категория.

    ![Подтверждение текущей категории](media/azure-pbie-scale-capacity/azure-portal-confirm-tier.png)

## <a name="next-steps"></a>Дальнейшие действия

Сведения о том, как приостановить или запустить емкость, см. в разделе [Приостановка и запуск емкости Power BI Embedded на портале Azure](azure-pbie-pause-start.md).

Чтобы начать внедрение содержимого Power BI в приложение, см. раздел [Как внедрять панели мониторинга, отчеты и плитки Power BI](https://powerbi.microsoft.com/documentation/powerbi-developer-embedding-content/).

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
