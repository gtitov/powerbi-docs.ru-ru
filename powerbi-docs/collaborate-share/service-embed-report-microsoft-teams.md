---
title: Внедрение отчетов Power BI в Microsoft Teams
description: Можно с легкостью внедрять интерактивные отчеты Power BI в каналы и чаты Microsoft Teams. .
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
featuredvideoid: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: conceptual
LocalizationGroup: Share your work
ms.date: 09/21/2020
ms.openlocfilehash: 36973d52f94b806db860b739a84f0c94b2a8945d
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96411869"
---
# <a name="embed-power-bi-content-in-microsoft-teams"></a>Внедрение содержимого Power BI в Microsoft Teams

Можно с легкостью внедрять интерактивные отчеты Power BI в каналы и чаты Microsoft Teams. 

## <a name="requirements"></a>Требования

Чтобы использовать вкладку **Power BI** в Microsoft Teams, необходимо обеспечить следующее:

- В Microsoft Teams должна быть вкладка **Power BI**.
- Чтобы добавить отчет в Microsoft Teams на вкладке **Power BI**, необходимо иметь по крайней мере роль "Читатель" в рабочей области, в которой размещается отчет. Сведения о различных ролях см. в разделе [Роли в новых рабочих областях](service-new-workspaces.md#roles-in-the-new-workspaces).
- Чтобы просмотреть отчет на вкладке **Power BI** в Microsoft Teams, пользователи должны иметь разрешение на просмотр отчета.
- Пользователи должны быть пользователями Microsoft Teams с доступом к каналам и чатам.

Ознакомьтесь со статьей [Совместная работа в Microsoft Teams с использованием Power BI](service-embed-report-microsoft-teams.md), чтобы получить базовое понимание того, как Power BI и Microsoft Teams работают вместе, включая прочие требования.

## <a name="embed-a-report-in-microsoft-teams"></a>Внедрение отчета в Microsoft Teams

Чтобы внедрить отчет в канал или чат Microsoft Teams, выполните указанные ниже действия.

1. Откройте канал или чат в Microsoft Teams и щелкните значок **+** .

    ![Снимок экрана: добавление вкладки в канал или чат.](media/service-embed-report-microsoft-teams/service-embed-report-microsoft-teams-add.png)

1. Выберите вкладку **Power BI**.

    ![Снимок экрана: список вкладок Microsoft Teams с вкладкой Power BI.](media/service-embed-report-microsoft-teams/service-embed-report-microsoft-teams-tab.png)

1. Выберите необходимый отчет среди доступных в рабочей области или приложении Power BI.

    ![Снимок экрана: параметры вкладки Power BI для Microsoft Teams.](media/service-embed-report-microsoft-teams/service-embed-report-microsoft-teams-tab-settings.png)

1. Имя вкладки обновляется автоматически в соответствии с именем отчета, но его можно изменить.

1. Щелкните **Сохранить**.

### <a name="reports-you-can-embed-on-the-power-bi-tab"></a>Отчеты, которые можно внедрить на вкладке Power BI

На вкладке **Power BI** можно внедрять отчеты следующих типов:

- интерактивные отчеты и отчеты с разбивкой на страницы;
- отчеты из раздела **Моя рабочая область**, нового интерфейса рабочих областей и классических рабочих областей;
- отчеты из приложений Power BI.

## <a name="start-a-conversation"></a>Начало общения

При добавлении вкладки отчета Power BI в Microsoft Teams в этой службе автоматически создается беседа для обсуждения отчета.

- В правом верхнем углу выберите значок **Показать беседу во вкладке**.

    ![Снимок экрана: значок "Показать беседу во вкладке".](media/service-embed-report-microsoft-teams/power-bi-teams-conversation-icon.png)

    Первый комментарий является ссылкой на отчет. Каждый в этом канале Microsoft Teams может просматривать и обсуждать отчет в беседе.

    ![Снимок экрана: беседа во вкладке.](media/service-embed-report-microsoft-teams/power-bi-teams-conversation-tab.png)

## <a name="known-issues-and-limitations"></a>Известные проблемы и ограничения

- В Microsoft Teams при экспорте данных из визуального элемента в отчет Power BI он автоматически сохраняется в вашу папку "Загрузки". Это файл Excel с именем "data (*n*).xlsx" где *n* — число операций экспорта данных в одну папку.
- Панели мониторинга Power BI невозможно внедрить на вкладку **Power BI** для Microsoft Teams.
- [Фильтры URL-адресов](service-url-filters.md) не поддерживаются на вкладке **Power BI** для Microsoft Teams.
- В национальных облаках новая вкладка **Power BI** недоступна. Может быть доступна прежняя версия, которая не поддерживает новые возможности рабочих областей и отчеты в приложениях Power BI.
- После сохранения вкладки ее имя невозможно изменить в параметрах вкладки. Чтобы изменить его, используйте команду **Переименовать**.
- Другие проблемы см. в разделе [Известные проблемы и ограничения](service-collaborate-microsoft-teams.md#known-issues-and-limitations) статьи "Совместная работа в Microsoft Teams".

## <a name="next-steps"></a>Дальнейшие действия

- [Совместная работа в Microsoft Teams с использованием Power BI](service-collaborate-microsoft-teams.md)

Остались вопросы? [Попробуйте задать вопрос в Сообществе Power BI](https://community.powerbi.com/).
