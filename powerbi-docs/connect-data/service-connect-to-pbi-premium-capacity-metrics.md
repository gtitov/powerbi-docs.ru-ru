---
title: Подключение к Power BI Premium Capacity Metrics
description: Сведения о том, как установить приложение-шаблон Power BI Premium Capacity Metrics и подключиться к данным
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-template-apps
ms.topic: how-to
ms.date: 05/18/2020
LocalizationGroup: Connect to services
ms.openlocfilehash: f7bb6cdd3279ac15b2952d5e20b9c36a66a0c518
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96410604"
---
# <a name="connect-to-power-bi-premium-capacity-metrics"></a>Подключение к Power BI Premium Capacity Metrics

Отслеживание емкостей очень важно для принятия обоснованных решений в отношении оптимального использования ресурсов емкости Premium. Приложение Power BI Premium Capacity Metrics предоставляет наиболее полные сведения об эффективности использования емкостей.

![Отчет о приложении Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-report.png)

В этой статье рассказывается, как установить приложение и подключиться к источникам данных. Сведения о содержимом отчета и его использовании см. в разделе [Мониторинг емкостей Premium в приложении](../admin/service-admin-premium-monitor-capacity.md), а также в [записи блога о приложении Premium Capacity Metrics](https://powerbi.microsoft.com/blog/premium-capacity-metrics-app-new-health-center-with-kpis-to-explore-relevant-metrics-and-steps-to-mitigate-issues/).

После установки приложения и подключения к источникам данных можно настроить отчет в соответствии с вашими потребностями. Затем им можно поделиться с коллегами в организации.

> [!NOTE]
> Для установки приложений-шаблонов требуются определенные [разрешения](./service-template-apps-install-distribute.md#prerequisites). Обратитесь к администратору Power BI, если вы обнаружите, что у вас нет необходимых разрешений.

## <a name="install-the-app"></a>Установка приложения

1. Щелкните следующую ссылку, чтобы перейти к приложению: [Приложение-шаблон Power BI Premium Capacity Metrics](https://app.powerbi.com/groups/me/getapps/services/pbi_pcmm.capacity-metrics-dxt)

1. На странице приложения в AppSource нажмите кнопку [**Получить**](https://app.powerbi.com/groups/me/getapps/services/pbi_pcmm.capacity-metrics-dxt).

    [![Приложение Power BI Premium Capacity Metrics в AppSource](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-appsource-get-it-now.png)](https://app.powerbi.com/groups/me/getapps/services/pbi_pcmm.capacity-metrics-dxt)

1. Нажмите кнопку **Установить**. 

    ![Установка приложения Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metric-select-install.png)

    > [!NOTE]
    > Если приложение было установлено ранее, появится запрос на [перезапись этой установки](./service-template-apps-install-distribute.md#update-a-template-app) или установку в новой рабочей области.

    После установки приложения оно появится на странице "Приложения".

   ![Приложение Power BI Premium Capacity Metrics на странице "Приложения"](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-apps-page-icon.png)

## <a name="connect-to-data-sources"></a>подключение к источникам данных.

1. Чтобы открыть приложение, щелкните его значок на странице "Приложения".

1. На экране-заставке нажмите кнопку **Исследовать**.

   ![Экран-заставка шаблона приложения](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-splash-screen.png)

   Приложение откроется с образцом данных.

1. Щелкните ссылку **Подключите свои данные** в баннере в верхней части страницы.

   ![Ссылка "Подключите свои данные" в приложении Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-connect-data.png)

1. В появившемся диалоговом окне задайте смещение от UTC, то есть разницу в часах между временем в формате UTC и временем в вашем расположении. Нажмите кнопку **Next** (Далее).
  
   ![Диалоговое окно задания смещения от UTC в приложении Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-setutc-dialog.png)
   **Примечание. Для указания половины часа следует использовать десятичные числа (например, 5,5, 2,5 и т. д.).**

1. В следующем появившемся диалоговом окне не требуется выполнять никаких действий. Просто выберите **Войти**.

   ![Диалоговое окно проверки подлинности в приложении Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-authentication-dialog.png)

1. На экране входа Майкрософт войдите в Power BI.

   ![Экран входа Майкрософт](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-microsoft-login.png)

   После входа отчет подключится к источникам данных и заполнится актуальными данными. В течение этого времени вращается индикатор активности.

   ![Ход обновления приложения Power BI Premium Capacity Metrics](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-refresh-monitor.png)

   Данные отчета будут автоматически обновляться раз в день, если только вы не отключили это во время входа в систему. Также можно [настроить собственное расписание обновления](./refresh-scheduled-refresh.md), чтобы в отчете всегда отражались актуальные данные.

## <a name="customize-and-share"></a>Настройка и общий доступ

Чтобы приступить к настройке приложения, щелкните значок карандаша в правом верхнем углу.

 ![Значок "Изменить"](media/service-connect-to-pbi-premium-capacity-metrics/service-pbi-premium-capacity-metrics-app-customize.png)

Подробные сведения см. в статье [Настройка приложения и общий доступ к нему](./service-template-apps-install-distribute.md#customize-and-share-the-app).

## <a name="next-steps"></a>Дальнейшие действия
* [Мониторинг емкостей Premium в приложении](../admin/service-admin-premium-monitor-capacity.md)
* [Запись блога о приложении Premium Capacity Metrics](https://powerbi.microsoft.com/blog/premium-capacity-metrics-app-new-health-center-with-kpis-to-explore-relevant-metrics-and-steps-to-mitigate-issues/)
* [Что такое приложения-шаблоны Power BI?](./service-template-apps-overview.md)
* [Установка и распространение приложений-шаблонов в организации](./service-template-apps-install-distribute.md)
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)