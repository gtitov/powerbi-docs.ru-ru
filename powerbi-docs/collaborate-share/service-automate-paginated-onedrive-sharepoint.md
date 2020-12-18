---
title: Сохранение отчета с разбивкой на страницы в OneDrive для бизнеса или SharePoint Online
description: В этой статье описано, как автоматизировать сохранение отчета Power BI с разбивкой на страницы в OneDrive для бизнеса или в папке SharePoint Online с помощью Power Automate.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 11/17/2020
LocalizationGroup: Get started
ms.openlocfilehash: 6aaad48fb3e97aa6c1b4fc51834ee593a49a8192
ms.sourcegitcommit: bbf7e9341a4e1cc96c969e24318c8605440282a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97097738"
---
# <a name="save-a-paginated-report-to-onedrive-for-business-or-sharepoint-online"></a>Сохранение отчета с разбивкой на страницы в OneDrive для бизнеса или SharePoint Online

С помощью [Power Automate](/power-automate/getting-started) можно автоматизировать экспорт и распространение отчетов Power BI с разбивкой на страницы в разнообразные поддерживаемые форматы и сценарии. В этой статье описано, как автоматизировать сохранение отчета Power BI с разбивкой на страницы в OneDrive для бизнеса или в папке SharePoint Online с помощью Power Automate.


:::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/paginated-onedrive-flow.png" alt-text="Снимок экрана: поток Power Automate для сохранения отчета с разбивкой на страницы в OneDrive или SharePoint Online":::

Ищете другие шаблоны Power Automate для отчетов Power BI с разбивкой на страницы? Ознакомьтесь со статьей [Экспорт отчетов Power BI с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md). 

## <a name="prerequisites"></a>Предварительные требования  

Для продолжения убедитесь, что у вас есть:

- По крайней мере одна рабочая область в клиенте Power BI, поддерживаемая зарезервированной емкостью. Это может быть любой из номеров SKU A4/P1–A6/P3. Узнайте подробнее о [зарезервированных емкостях для отчетов с разбивкой на страницы в Power BI Premium](../admin/service-premium-what-is.md#paginated-reports)
- Доступ к стандартным соединителям в Power Automate, которые входят в состав любой подписки Office 365.

## <a name="save-a-paginated-report-to-onedrive-for-business-or-a-sharepoint-online-folder"></a>Сохранение отчета с разбивкой на страницы в OneDrive для бизнеса или в папке SharePoint Online 

С помощью любого из этих шаблонов можно настроить повторяющиеся экспорты отчета с разбивкой на страницы в нужном формате в OneDrive для бизнеса или в папку SharePoint Online. Ознакомьтесь с предварительными условиями, если вы впервые используете действие "Экспорт в файл для отчетов с разбивкой на страницы" в потоке Power Automate. 

> [!NOTE]
> Ниже представлен порядок настройки потока с помощью шаблона **Сохранение отчета с разбивкой на страницы в OneDrive для бизнеса**. Выполните те же действия, чтобы создать поток с помощью шаблона **Сохранение отчета с разбивкой на страницы в папке SharePoint Online**. При выборе места экспорта отчета с разбивкой на страницы выберите папку SharePoint Online вместо папки OneDrive для бизнеса. 

1. Войдите в Power Automate ([flow.microsoft.com](https://flow.microsoft.com/)). 
1. Выберите **Шаблоны** и найдите  **отчеты с разбивкой на страницы**. 

    :::image type="content" source="media/service-automate-paginated-integration/power-bi-paginate-automate.png" alt-text="Снимок экрана: шаблоны Power Automate для отчетов Power BI с разбивкой на страницы.":::

1. Выберите **Сохранить отчет Power BI с разбивкой на страницы в OneDrive для бизнеса** или **Сохранить отчет Power BI с разбивкой на страницы в папке SharePoint Online**. Убедитесь, что вы вошли в Power BI и OneDrive для бизнеса или SharePoint Online.

    :::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/onedrive-template-step1.png" alt-text="Снимок экрана: выбор шаблона Power BI и OneDrive для бизнеса.":::
1. Выберите **Continue** (Продолжить).  


1. Чтобы задать **периодичность** для последовательности, выберите параметр в разделе **Частота** и введите требуемое значение для параметра **Интервал**.

    :::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/onedrive-template-2-recurrence.png" alt-text="Выбор периодичности для потока.":::

1. (Необязательно) Выберите **Показать дополнительные параметры**, чтобы задать дополнительные параметры **периодичности**, включая **Часовой пояс**, **Время начала**, **В эти дни**, **В эти часы** и **В эти минуты**.  

    :::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/onedrive-template-3-advanced-recurrence.png" alt-text="Дополнительные параметры настройки периодичности.":::

1. В поле **Рабочая область** выберите рабочую область с зарезервированной емкостью. В поле **Отчет** выберите отчет с разбивкой на страницы в выбранной рабочей области, которую необходимо экспортировать. В поле **Формат экспорта** выберите нужный формат экспорта. При необходимости можно указать параметры для отчета с разбивкой на страницы. Подробные описания параметров см. в [справочнике по соединителю для REST API Power BI](/connectors/powerbi/#export-to-file-for-paginated-reports).  

    :::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/onedrive-template-4-export-format.png" alt-text="Выбор отчета с разбивкой на страницы, рабочей области и формата экспорта.":::

1. В поле **Путь к папке** выберите папку OneDrive для бизнеса или папку SharePoint Online, в которую необходимо экспортировать отчет с разбивкой на страницы.

    :::image type="content" source="media/service-automate-paginated-onedrive-sharepoint/onedrive-template-5-create-file.png" alt-text="Выбор назначения и создание файла.":::

1. Power Automate автоматически создает **имя файла** и **содержимое файла**. Вы можете изменить имя файла, однако оставьте без изменений динамически создаваемое значение **содержимого файла**. 

1. Когда все будет готово, выберите  **Следующий шаг** или **Сохранить**. Power Automate создает и оценивает последовательность, а также позволяет определить, обнаруживаются ли ошибки. 

1. При возникновении ошибок выберите  **Изменить поток** , чтобы устранить их. В противном случае нажмите стрелку **Назад**, чтобы просмотреть сведения о потоке и запустить новый поток. 

    При запуске потока Power Automate экспортирует отчет с разбивкой на страницы в указанном формате в OneDrive для бизнеса или SharePoint Online.  

## <a name="next-steps"></a>Следующие шаги

- [Экспорт отчетов с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md)
- [Начало работы с Power Automate](/power-automate/getting-started/)
- Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
