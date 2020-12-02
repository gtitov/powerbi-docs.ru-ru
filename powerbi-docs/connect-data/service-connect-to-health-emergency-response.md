---
title: Подключение к панели поддержки принятия решений по неотложной медицинской помощи
description: Узнайте, как получить и установить шаблон приложения "Панель поддержки принятия решений по неотложной медицинской помощи в связи с COVID-19" и как подключиться к данным.
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-template-apps
ms.topic: how-to
ms.date: 05/13/2020
LocalizationGroup: Connect to services
ms.openlocfilehash: 823c8429c95a0b4d858540b2cf1183ca1c7caac7
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96403152"
---
# <a name="connect-to-the-hospital-emergency-response-decision-support-dashboard"></a>Подключение к панели поддержки принятия решений по неотложной медицинской помощи
Шаблон приложения "Панель поддержки принятия решений по неотложной медицинской помощи" — это компонент для создания отчетов в составе [решения Microsoft Power Platform для реагирования на чрезвычайные медицинские ситуации](https://powerapps.microsoft.com/blog/emergency-response-solution-a-microsoft-power-platform-solution-for-healthcare-emergency-response/). На панели мониторинга приводятся сводные данные по системе здравоохранения, которые помогают специалистам по управлению в чрезвычайных ситуациях своевременно принимать правильные решения.

![Отчет в приложении "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-report.png)

В этой статье рассказывается, как установить приложение и как подключиться к источникам данных. Сведения об использовании отчета в этом приложении см. в [документации по панели поддержки принятия решений по неотложной медицинской помощи](/powerapps/sample-apps/emergency-response/deploy-configure#view-the-power-bi-dashboard).

После установки шаблона приложения и подключения к источникам данных можно настроить отчет в соответствии с вашими потребностями. Затем его можно распространить в виде приложения среди коллег в организации.

## <a name="prerequisites"></a>Предварительные требования

Перед установкой этого шаблона приложения необходимо установить и настроить [решение Power Platform для реагирования на чрезвычайные медицинские ситуации](/powerapps/sample-apps/emergency-response/deploy-configure). При установке этого решения создаются ссылки на источники данных, необходимые для заполнения приложения данными.

При установке решения Power Platform для реагирования на чрезвычайные медицинские ситуации запишите [URL-адрес экземпляра среды Common Data Service](/powerapps/sample-apps/emergency-response/deploy-configure#publish-the-power-bi-dashboard). Он понадобится для подключения шаблона приложения к данным.

## <a name="install-the-app"></a>Установка приложения

1. Щелкните следующую ссылку, чтобы перейти к приложению: [шаблон приложения "Панель поддержки принятия решений по неотложной медицинской помощи"](https://aka.ms/AppSource_Hospital_offer)

1. На странице приложения в AppSource нажмите кнопку [**Получить**](https://aka.ms/AppSource_Hospital_offer).

    [![Приложение "Панель поддержки принятия решений по неотложной медицинской помощи" в AppSource](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-appsource-get-it-now.png)](https://aka.ms/AppSource_Hospital_offer)

1. Ознакомьтесь с информацией в окне **Дополнительно** и нажмите кнопку **Продолжить**.

    ![Приложение "Панель поддержки принятия решений по неотложной медицинской помощи", окно "Дополнительно"](media/service-connect-to-health-emergency-response/service-health-emergency-response-1-more-thing.png)

1. Нажмите кнопку **Установить**. 

    ![Установка приложения "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-select-install.png)

    После установки приложения оно появится на странице "Приложения".

   ![Приложение "Панель поддержки принятия решений по неотложной медицинской помощи" на странице "Приложения"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-apps-page-icon.png)

## <a name="connect-to-data-sources"></a>подключение к источникам данных.

1. Чтобы открыть приложение, щелкните его значок на странице "Приложения".

1. На экране-заставке нажмите кнопку **Исследовать**.

   ![Экран-заставка шаблона приложения](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-splash-screen.png)

   Приложение откроется с образцом данных.

1. Щелкните ссылку **Подключите свои данные** в баннере в верхней части страницы.

   ![Ссылка "Подключите свои данные" в приложении "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-connect-data.png)

1. В диалоговом окне выполните указанные ниже действия.
   1. В поле названия организации введите название вашей организации, например "Системы здравоохранения Contoso". Это поле является необязательным. Это имя отображается в левом верхнем углу панели мониторинга.
   1. В поле CDS_base_solution введите [URL-адрес экземпляра среды Common Data Service](/powerapps/sample-apps/emergency-response/deploy-configure#publish-the-power-bi-dashboard). Пример: https://[myenv].crm.dynamics.com. По завершении нажмите кнопку **Далее**.

   ![Диалоговое окно для ввода URL-адреса в приложении "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-url-dialog.png)

1. В следующем диалоговом окне выберите метод проверки подлинности **OAuth2**. Уровень конфиденциальности менять не нужно.

   Выберите **Войти**.

   ![Диалоговое окно для настройки проверки подлинности в приложении "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-authentication-dialog.png)

1. На экране входа Майкрософт войдите в Power BI.

   ![Экран входа Майкрософт](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-microsoft-login.png)

   После входа отчет подключится к источникам данных и заполнится актуальными данными. В течение этого времени вращается индикатор активности.

   ![Обновление данных в приложении "Панель поддержки принятия решений по неотложной медицинской помощи"](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-refresh-monitor.png)

## <a name="schedule-report-refresh"></a>Планирование обновления отчета

Когда обновление данных завершится, [настройте расписание обновления](../connect-data/refresh-scheduled-refresh.md), чтобы поддерживать данные отчета в актуальном состоянии.

1. В верхней строке заголовка выберите **Power BI**.

   ![Элемент навигации Power BI](media/service-connect-to-health-emergency-response/service-health-emergency-response-app-powerbi-breadcrumb.png)

1. В области навигации слева найдите рабочую область "Панель поддержки принятия решений по неотложной медицинской помощи" в разделе **Рабочие области** и следуйте инструкциям, приведенным в статье [Настройка запланированного обновления](../connect-data/refresh-scheduled-refresh.md).

## <a name="customize-and-share"></a>Настройка и общий доступ

Подробные сведения см. в статье [Настройка приложения и общий доступ к нему](../connect-data/service-template-apps-install-distribute.md#customize-and-share-the-app). Перед публикацией или распространением приложения обязательно ознакомьтесь с [предостережениями](../create-reports/sample-covid-19-us.md#disclaimers).

## <a name="next-steps"></a>Дальнейшие действия
* [Сведения об отчете "Реагирование на чрезвычайные медицинские ситуации"](/powerapps/sample-apps/emergency-response/deploy-configure#view-the-power-bi-dashboard)
* [Настройка и дополнительные сведения о шаблоне "Антикризисные коммуникации" в Power Apps](/powerapps/maker/canvas-apps/sample-crisis-communication-app)
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
* [Что такое приложения-шаблоны Power BI?](../connect-data/service-template-apps-overview.md)
* [Установка и распространение приложений-шаблонов в организации](../connect-data/service-template-apps-install-distribute.md)