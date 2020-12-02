---
title: Представление общего доступа непосредственно в Microsoft Teams из службы Power BI
description: Вы можете предоставлять доступ к панелям мониторинга Power BI и отчетам непосредственно в Microsoft Teams из службы Power BI.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
featuredvideoid: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
LocalizationGroup: Share your work
ms.date: 07/31/2020
ms.openlocfilehash: 0a6f73c14c8dd8ebb48f856f3079ec8f5922ef9e
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96411570"
---
# <a name="share-directly-to-microsoft-teams-from-the-power-bi-service"></a>Представление общего доступа непосредственно в Microsoft Teams из службы Power BI

Вы можете предоставлять доступ к панелям мониторинга, отчетам и визуальным элементам Power BI непосредственно в Microsoft Teams из службы Power BI. С помощью функции **Поделиться в Teams** можно быстро начать беседу при просмотре отчетов и панелей мониторинга в службе Power BI.

## <a name="requirements"></a>Требования

Чтобы воспользоваться функцией **Поделиться в Teams** в Power BI, убедитесь в следующем:

- Администраторы Power BI не отключили для клиента параметр **Поделиться в Teams** на портале администрирования Power BI. Этот параметр позволяет организациям скрывать кнопку **Поделиться в Teams**. Дополнительные сведения см. в статье [Портал администрирования Power BI](../admin/service-admin-portal.md#share-to-teams).

Ознакомьтесь со статьей [Совместная работа в Microsoft Teams с использованием Power BI](service-collaborate-microsoft-teams.md), чтобы получить базовое понимание того, как Power BI и Microsoft Teams работают вместе, включая прочие требования.

## <a name="share-power-bi-content-to-microsoft-teams"></a>Предоставление общего доступа к содержимому Power BI в Microsoft Teams

Выполните следующие действия, чтобы поделиться ссылками на отчеты, информационные панели и визуальные элементы в службе Power BI в каналах и чатах Microsoft Teams.

1. Выберите один из следующих вариантов:

   * Нажмите **Поделиться в Teams** на панели действий на панели мониторинга или отчета:

       ![Снимок экрана: кнопка "Поделиться в Teams" на панели действий.](media/service-share-report-teams/service-teams-share-to-teams-action-bar-button.png)
    
   * Пункт **Поделиться в Teams** в контекстном меню для визуального элемента:
    
      ![Снимок экрана: пункт "Поделиться в Teams" в контекстном меню визуального элемента.](media/service-share-report-teams/service-teams-share-to-teams-visual-context-menu.png)

1. В диалоговом окне **Предоставление общего доступа в Microsoft Teams** выберите команду или канал, куда нужно отправить ссылку. При необходимости можно ввести сообщение. Возможно, вам будет предложено сначала войти в Microsoft Teams.

    ![Снимок экрана: диалоговое окно "Предоставление общего доступа в Microsoft Teams" с информацией и сообщением.](media/service-share-report-teams/service-teams-share-to-teams-dialog.png)

1. Выберите **Поделиться**, чтобы отправить ссылку.
    
1. Ссылка будет добавлена к существующим беседам или будет инициировать создание нового чата.

    ![Снимок экрана: беседа в Microsoft Teams со ссылкой на элемент Power BI.](media/service-share-report-teams/service-teams-share-to-teams-deep-link.png)

1. Щелкните ссылку, чтобы открыть элемент в службе Power BI.

1. Если для определенного визуального элемента использовалось контекстное меню, он выделяется при открытии отчета.

    ![Снимок экрана: открытый отчет Power BI с выделенным визуальным элементом.](media/service-share-report-teams/service-teams-share-to-teams-spotlight-visual.png)


## <a name="known-issues-and-limitations"></a>Известные проблемы и ограничения

- Пользователи, у которых нет лицензии Power BI или разрешения на доступ к отчету, видят сообщение "Содержимое недоступно".
- Кнопки **Поделиться в Teams** могут не работать, если в браузере используются ограниченные параметры конфиденциальности. Воспользуйтесь параметром **Не получается? Попробуйте открыть в новом окне**, если диалоговое окно не открывается правильно.
- Для функции **Поделиться в Teams** не предусмотрен предварительный просмотр ссылок.
- Предварительный просмотр ссылок и функция **Поделиться в Teams** не дают пользователям разрешений на просмотр элемента. Разрешения следует настроить отдельно.
- Кнопка **Поделиться в Teams** недоступна в контекстных меню визуальных элементов, когда автор отчета задает в разделе **Дополнительно** значение **Выкл.** для визуального элемента.
- Другие проблемы см. в разделе [Известные проблемы и ограничения](service-collaborate-microsoft-teams.md#known-issues-and-limitations) статьи "Совместная работа в Microsoft Teams".

## <a name="next-steps"></a>Дальнейшие действия

- [Совместная работа в Microsoft Teams с использованием Power BI](service-collaborate-microsoft-teams.md)

Остались вопросы? [Попробуйте задать вопрос в Сообществе Power BI](https://community.powerbi.com/).
