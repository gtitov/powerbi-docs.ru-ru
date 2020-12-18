---
title: Экспорт отчетов с разбивкой на страницы с помощью Power Automate
description: Сведения о том, как создавать потоки Power Automate для экспорта отчетов Power BI с разбивкой на страницы.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 12/14/2020
LocalizationGroup: Get started
ms.openlocfilehash: 5c69abe925751e8b065f262e151bfee65c487238
ms.sourcegitcommit: 46cf62d9bb33ac7b7eae7910fbba6756f626c65f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2020
ms.locfileid: "97492065"
---
# <a name="export-power-bi-paginated-reports-with-power-automate"></a>Экспорт отчетов с разбивкой на страницы с помощью Power Automate

С помощью [Power Automate](/power-automate/getting-started) можно автоматизировать экспорт и распространение отчетов Power BI с разбивкой на страницы в разнообразные поддерживаемые форматы и сценарии. В этой статье вы узнаете, какие шаблоны следует использовать для создания собственных потоков для экспорта отчетов с разбивкой на страницы.  

## <a name="prerequisites"></a>Предварительные требования  

Для продолжения убедитесь, что у вас есть:

- По крайней мере одна рабочая область в клиенте Power BI, поддерживаемая зарезервированной емкостью. Это может быть любой из номеров SKU A4/P1–A6/P3. Узнайте подробнее о [зарезервированных емкостях в Power BI Premium](../admin/service-premium-what-is.md).
- Доступ к стандартным соединителям в Power Automate, которые входят в состав любой подписки Office 365.

## <a name="create-a-flow-from-a-template"></a>Создание потока из шаблона 

1. Войдите в Power Automate ([flow.microsoft.com](https://flow.microsoft.com/)). 
1. Выберите **Шаблоны** и найдите  **отчеты с разбивкой на страницы**. 

    :::image type="content" source="media/service-automate-paginated-integration/power-bi-paginate-automate.png" alt-text="Снимок экрана: шаблоны Power Automate для отчетов Power BI с разбивкой на страницы.":::

## <a name="select-a-template"></a>Выберите шаблон 

Выберите шаблон из списка, чтобы начать работу с пошаговым руководством.  

- [Сохранение отчета с разбивкой на страницы в OneDrive для бизнеса или в папке SharePoint Online.](service-automate-paginated-onedrive-sharepoint.md)  
- [Экспорт отчета Power BI с разбивкой на страницы для элементов в списке SharePoint Online или для каждой строки в таблице Excel Online.](service-automate-paginated-excel-sharepoint-list.md)
- [Сохранение отчета Power BI с разбивкой на страницы в локальной системной папке](service-automate-paginated-local-file.md).

## <a name="next-steps"></a>Следующие шаги

- [API Power BI для экспорта отчетов с разбивкой на страницы](../developer/embedded/export-paginated-report.md)
- [Начало работы с Power Automate](/power-automate/getting-started/)
- Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
