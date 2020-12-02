---
title: Подключение к панели мониторинга реагирования на чрезвычайные ситуации в регионе
description: Узнайте, как получить и установить приложение-шаблон "Панель поддержки принятия решений по реагированию на чрезвычайные ситуации в регионах в связи с COVID-19" и как подключиться к данным
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-template-apps
ms.topic: how-to
ms.date: 04/24/2020
LocalizationGroup: Connect to services
ms.openlocfilehash: b8cb2be15d084bba3fc2a70152165ce3b2909dab
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96410558"
---
# <a name="connect-to-the-regional-emergency-response-dashboard"></a>Подключение к панели мониторинга реагирования на чрезвычайные ситуации в регионе
Панель мониторинга реагирования на чрезвычайные ситуации в регионе — это компонент для создания отчетов в составе [решения Microsoft Power Platform для реагирования на чрезвычайные ситуации в регионе](/powerapps/sample-apps/regional-emergency-response/overview). Администраторы региональной организации могут просматривать панель мониторинга в клиенте Power BI. Это позволяет им быстро просматривать важные данные и метрики, которые помогут принимать эффективные решения.

![Отчет в приложении панели мониторинга реагирования на чрезвычайные ситуации в регионе](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-report.png)

В этой статье описывается, как установить приложение аварийного реагирования на чрезвычайные ситуации в регионе с помощью приложения-шаблона "Панель мониторинга реагирования на чрезвычайные ситуации в регионе" и подключиться к источникам данных.

Дополнительные сведения о компонентах панели мониторинга см. в разделе [Аналитические сведения](/powerapps/sample-apps/regional-emergency-response/portals-admin-reporting#get-insights).

После установки шаблона приложения и подключения к источникам данных можно настроить отчет в соответствии с вашими потребностями. Затем его можно распространить в виде приложения среди коллег в организации.

## <a name="prerequisites"></a>Предварительные требования

Перед установкой этого приложения-шаблона необходимо установить и настроить [решение для реагирования на чрезвычайные ситуации в регионе](/powerapps/sample-apps/regional-emergency-response/deploy). При установке этого решения создаются ссылки на источники данных, необходимые для заполнения приложения данными.

При установке решения для реагирования на чрезвычайные ситуации в регионе запишите [URL-адрес экземпляра среды Common Data Service](/powerapps/sample-apps/regional-emergency-response/deploy#step-5-configure-and-publish-power-bi-dashboard). Он понадобится для подключения шаблона приложения к данным.

## <a name="install-the-app"></a>Установка приложения

1. Щелкните следующую ссылку, чтобы перейти к приложению: [Приложение-шаблон "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](https://appsource.microsoft.com/product/power-bi/powerapps_cxo.regional_response)

1. На странице приложения в AppSource нажмите кнопку [**Получить**](https://appsource.microsoft.com/product/power-bi/powerapps_cxo.regional_response).

    [![Приложение "Панель мониторинга реагирования на чрезвычайные ситуации в регионе" в AppSource](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-appsource-get-it-now.png)](https://appsource.microsoft.com/product/power-bi/powerapps_cxo.regional_response)

1. Нажмите кнопку **Установить**. 

    ![Установка приложения "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-select-install.png)

    После установки приложения оно появится на странице "Приложения".

   ![Приложение "Панель мониторинга реагирования на чрезвычайные ситуации в регионе" на странице приложения](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-apps-page-icon.png)

## <a name="connect-to-data-sources"></a>подключение к источникам данных.

1. Чтобы открыть приложение, щелкните его значок на странице "Приложения".

1. На экране-заставке нажмите кнопку **Исследовать**.

   ![Экран-заставка шаблона приложения](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-splash-screen.png)

   Приложение откроется с образцом данных.

1. Щелкните ссылку **Подключите свои данные** в баннере в верхней части страницы.

   ![Ссылка "Подключите свои данные" в приложении "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-connect-data.png)

1. В появившемся диалоговом окне введите [URL-адрес экземпляра среды Common Data Service](/powerapps/sample-apps/emergency-response/deploy-configure#publish-the-power-bi-dashboard). Пример: https://[myenv].crm.dynamics.com. По завершении нажмите кнопку **Далее**.

   ![Диалоговое окно URL-адреса приложения "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-url-dialog.png)

1. В следующем диалоговом окне выберите метод проверки подлинности **OAuth2**. Уровень конфиденциальности менять не нужно.

   Выберите **Войти**.

   ![Диалоговое окно аутентификации приложения "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-authentication-dialog.png)

1. На экране входа Майкрософт войдите в Power BI.

   ![Экран входа Майкрософт](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-microsoft-login.png)

   После входа отчет подключится к источникам данных и заполнится актуальными данными. В течение этого времени вращается индикатор активности.

   ![Обновление данных в приложении "Панель мониторинга реагирования на чрезвычайные ситуации в регионе"](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-refresh-monitor.png)

## <a name="schedule-report-refresh"></a>Планирование обновления отчета

Когда обновление данных завершится, [настройте расписание обновления](../connect-data/refresh-scheduled-refresh.md), чтобы поддерживать данные отчета в актуальном состоянии.

1. В верхней строке заголовка выберите **Power BI**.

   ![Элемент навигации Power BI](media/service-connect-to-regional-emergency-response/service-regional-emergency-response-app-powerbi-breadcrumb.png)

1. В области навигации слева найдите рабочую область "Панель мониторинга реагирования на чрезвычайные ситуации в регионе" в разделе **Рабочие области** и следуйте инструкциям, приведенным в статье [Настройка запланированного обновления](../connect-data/refresh-scheduled-refresh.md).

## <a name="customize-and-share"></a>Настройка и общий доступ

Подробные сведения см. в статье [Настройка приложения и общий доступ к нему](../connect-data/service-template-apps-install-distribute.md#customize-and-share-the-app). Перед публикацией или распространением приложения обязательно ознакомьтесь с [предостережениями](/powerapps/sample-apps/regional-emergency-response/overview#disclaimer).

## <a name="next-steps"></a>Дальнейшие действия
* [Сведения о панели мониторинга реагирования на чрезвычайные ситуации в регионе](/powerapps/sample-apps/regional-emergency-response/portals-admin-reporting#get-insights)
* [Настройка и дополнительные сведения о шаблоне "Антикризисные коммуникации" в Power Apps](/powerapps/maker/canvas-apps/sample-crisis-communication-app)
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
* [Что такое приложения-шаблоны Power BI?](../connect-data/service-template-apps-overview.md)
* [Установка и распространение приложений-шаблонов в организации](../connect-data/service-template-apps-install-distribute.md)