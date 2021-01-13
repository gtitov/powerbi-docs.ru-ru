---
title: Приостановка и запуск емкости Power BI Embedded на портале Azure для решения встроенной бизнес-аналитики Power BI
description: В этой статье рассматривается приостановка и запуск емкости Power BI в Microsoft Azure при использовании решения встроенной бизнес-аналитики Power BI.
author: KesemSharabi
ms.author: kesharab
services: power-bi-embedded
editor: ''
tags: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.date: 09/28/2017
ms.openlocfilehash: 0868d63f83f42bcfa9f394e782ffab56746e23cc
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887346"
---
# <a name="pause-and-start-your-power-bi-embedded-capacity-in-the-azure-portal"></a>Приостановка и запуск емкости Power BI Embedded на портале Azure

В этой статье рассматривается приостановка и запуск емкости Power BI Embedded в Microsoft Azure. Предполагается, что вы создали емкость Power BI Embedded. Если нет, см. раздел [Создание емкости Power BI Embedded на портале Azure](azure-pbie-create-capacity.md).

Если у вас нет подписки Azure, перед началом работы [создайте бесплатную учетную запись](https://azure.microsoft.com/free/).

## <a name="pause-your-capacity"></a>Приостановка емкости

Если вы приостановите емкость, вы не будете получать за нее счета. Приостановка емкости — это удобная возможность, если вам не нужно использовать емкость какое-то время. Следуйте инструкциям ниже, чтобы приостановить емкость.

> [!NOTE]
> При приостановке емкости содержимое может быть недоступно в Power BI. Обязательно отмените назначение рабочих областей в емкости перед ее приостановкой, чтобы избежать прерывания.

1. Войдите на [портал Azure](https://portal.azure.com/).

2. Выберите **Все службы** > **Power BI Embedded**, чтобы просмотреть доступные емкости.

    ![Все службы на портале Azure](media/azure-pbie-pause-start/azure-portal-more-services.png)

3. Выберите емкость, которую нужно приостановить.

    ![Список емкостей Power BI Embedded на портале Azure](media/azure-pbie-pause-start/azure-portal-capacity-list.png)

4. Выберите **Пауза** в сведениях о емкости.

    ![Приостановка емкости](media/azure-pbie-pause-start/azure-portal-pause-capacity.png)

5. Щелкните **Да**, чтобы подтвердить приостановку емкости.

    ![Подтверждение приостановки](media/azure-pbie-pause-start/azure-portal-confirm-pause.png)

## <a name="start-your-capacity"></a>Запуск емкости

Возобновите использование емкости, запустив ее. При запуске емкости также возобновляется выставление счетов.

1. Войдите на [портал Azure](https://portal.azure.com/).

2. Выберите **Все службы** > **Power BI Embedded**, чтобы просмотреть доступные емкости.

    ![Все службы на портале Azure](media/azure-pbie-pause-start/azure-portal-more-services.png)

3. Выберите емкость, которую нужно запустить.

    ![Список емкостей Power BI Embedded на портале Azure](media/azure-pbie-pause-start/azure-portal-capacity-list.png)

4. Выберите **Запуск** в сведениях о емкости.

    ![Запуск емкости](media/azure-pbie-pause-start/azure-portal-start-capacity.png)

5. Щелкните **Да**, чтобы подтвердить запуск емкости.

    ![Подтверждение запуска](media/azure-pbie-pause-start/azure-portal-confirm-start.png)

Если для этой емкости назначено содержимое, оно будет доступно после запуска.

## <a name="next-steps"></a>Дальнейшие действия

Если вы хотите увеличить или уменьшить масштаб емкости, см. раздел [Масштабирование емкости Power BI Embedded](azure-pbie-scale-capacity.md).

Чтобы начать внедрение содержимого Power BI в приложение, см. раздел [Как внедрять панели мониторинга, отчеты и плитки Power BI](https://powerbi.microsoft.com/documentation/powerbi-developer-embedding-content/).

У вас имеются и другие вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)