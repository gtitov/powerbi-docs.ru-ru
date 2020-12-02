---
title: Подключение к отчету о присутствии для антикризисных коммуникаций
description: Узнайте, как получить и установить шаблон приложения "Отчет о присутствии для антикризисных коммуникаций в связи с COVID-19" и как подключиться к данным.
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-template-apps
ms.topic: how-to
ms.date: 04/06/2020
LocalizationGroup: Connect to services
ms.openlocfilehash: 7cce4f9e78fce27fedf795a4a0016593580f061a
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96403175"
---
# <a name="connect-to-the-crisis-communication-presence-report"></a>Подключение к отчету о присутствии для антикризисных коммуникаций

Это приложение Power BI представляет собой артефакт отчета или панели мониторинга в решении Microsoft Power Platform для антикризисных коммуникаций. Оно позволяет пользователям приложения для антикризисных коммуникаций отслеживать местонахождение сотрудников. В решении сочетаются возможности Power Apps, Power Automate, Teams, SharePoint и Power BI. Его можно использовать в браузере, на мобильном устройстве или в Teams.

![Отчет в приложении "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report.png)

На панели мониторинга приводятся сводные данные по системе здравоохранения, которые помогают специалистам по управлению в чрезвычайных ситуациях своевременно принимать правильные решения.

В этой статье рассказывается, как установить приложение и как подключиться к источникам данных. Дополнительные сведения о приложении для коммуникации в кризисных ситуациях см. в разделе [Настройка и изучение примера шаблона "Антикризисные коммуникации" в Power Apps](/powerapps/maker/canvas-apps/sample-crisis-communication-app).

После установки шаблона приложения и подключения к источникам данных можно настроить отчет в соответствии с вашими потребностями. Затем его можно распространить в виде приложения среди коллег в организации.

## <a name="prerequisites"></a>Предварительные требования

Перед установкой этого шаблона приложения необходимо установить и настроить [образец "Антикризисные коммуникации"](/powerapps/maker/canvas-apps/sample-crisis-communication-app). При установке этого решения создаются ссылки на источники данных, необходимые для заполнения приложения данными.

При установке образца "Антикризисные коммуникации" запишите [путь к папке со списком SharePoint "CI_Employee Status" и идентификатор этого списка](/powerapps/maker/canvas-apps/sample-crisis-communication-app#monitor-office-absences-with-power-bi).

## <a name="install-the-app"></a>Установка приложения

1. Щелкните следующую ссылку, чтобы перейти к приложению: [шаблон приложения "Отчет о присутствии для антикризисных коммуникаций"](https://appsource.microsoft.com/en-us/product/power-bi/pbi-contentpacks.crisiscomms)

1. На странице приложения в AppSource нажмите кнопку [**Получить**](https://appsource.microsoft.com/en-us/product/power-bi/pbi-contentpacks.crisiscomms).

    [![Приложение "Отчет о присутствии для антикризисных коммуникаций" в AppSource](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-appsource-get-it-now.png)](https://appsource.microsoft.com/en-us/product/power-bi/pbi-contentpacks.crisiscomms)

1. Ознакомьтесь с информацией в окне **Дополнительно** и нажмите кнопку **Продолжить**.

    ![Приложение "Отчет о присутствии для антикризисных коммуникаций", окно "Дополнительно"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-1-more-thing.png)

1. Нажмите кнопку **Установить**. 

    ![Установка приложения "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-select-install.png)

    После установки приложения оно появится на странице "Приложения".

   ![Приложение "Отчет о присутствии для антикризисных коммуникаций" на странице "Приложения"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-apps-page-icon.png)

## <a name="connect-to-data-sources"></a>подключение к источникам данных.

1. Чтобы открыть приложение, щелкните его значок на странице "Приложения".

1. На экране-заставке нажмите кнопку **Исследовать**.

   ![Экран-заставка шаблона приложения](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-splash-screen.png)

   Приложение откроется с образцом данных.

1. Щелкните ссылку **Подключите свои данные** в баннере в верхней части страницы.

   ![Ссылка "Подключите свои данные" в приложении "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-connect-data.png)

1. В диалоговом окне выполните указанные ниже действия.
   1. В поле SharePoint_Folder введите [путь к списку SharePoint "CI_Employee Status"](/powerapps/maker/canvas-apps/sample-crisis-communication-app#monitor-office-absences-with-power-bi).
   1. В поле List_ID введите идентификатор списка, полученный в параметрах списка. По завершении нажмите кнопку **Далее**.

   ![Диалоговое окно для ввода URL-адреса в приложении "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-url-dialog.png)

1. В следующем диалоговом окне выберите метод проверки подлинности **OAuth2**. Уровень конфиденциальности менять не нужно.

   Выберите **Войти**.

   ![Диалоговое окно для настройки проверки подлинности в приложении "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-authentication-dialog.png)

1. На экране входа Майкрософт войдите в Power BI.

   ![Экран входа Майкрософт](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-microsoft-login.png)

   После входа отчет подключится к источникам данных и заполнится актуальными данными. В течение этого времени вращается индикатор активности.

   ![Обновление данных в приложении "Отчет о присутствии для антикризисных коммуникаций"](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-refresh-monitor.png)

## <a name="schedule-report-refresh"></a>Планирование обновления отчета

Когда обновление данных завершится, [настройте расписание обновления](../connect-data/refresh-scheduled-refresh.md), чтобы поддерживать данные отчета в актуальном состоянии.

1. В верхней строке заголовка выберите **Power BI**.

   ![Элемент навигации Power BI](media/service-connect-to-crisis-communication-presence-report/service-crisis-communication-presence-report-app-powerbi-breadcrumb.png)

1. В области навигации слева найдите рабочую область "Панель поддержки принятия решений по неотложной медицинской помощи" в разделе **Рабочие области** и следуйте инструкциям, приведенным в статье [Настройка запланированного обновления](../connect-data/refresh-scheduled-refresh.md).

## <a name="customize-and-share"></a>Настройка и общий доступ

Подробные сведения см. в статье [Настройка приложения и общий доступ к нему](../connect-data/service-template-apps-install-distribute.md#customize-and-share-the-app). Перед публикацией или распространением приложения обязательно ознакомьтесь с [предостережениями](../create-reports/sample-covid-19-us.md#disclaimers).

## <a name="next-steps"></a>Дальнейшие действия
* [Настройка и дополнительные сведения о шаблоне "Антикризисные коммуникации" в Power Apps](/powerapps/maker/canvas-apps/sample-crisis-communication-app)
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
* [Что такое приложения-шаблоны Power BI?](../connect-data/service-template-apps-overview.md)
* [Установка и распространение приложений-шаблонов в организации](../connect-data/service-template-apps-install-distribute.md)