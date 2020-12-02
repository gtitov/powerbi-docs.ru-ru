---
title: Экспорт отчета с разбивкой на страницы для каждой строки в таблице Excel Online или в списке SharePoint
description: В этой статье описано, как автоматизировать экспорт отчета с разбивкой на страницы для каждой строки в таблице Excel Online или в списке SharePoint Online с помощью Power Automate.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 11/17/2020
LocalizationGroup: Get started
ms.openlocfilehash: 74d61d40c4447f2649f5cce5fbcdcba68cd31afe
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96408005"
---
# <a name="export-a-paginated-report-for-each-row-in-an-excel-online-table-or-sharepoint-list"></a>Экспорт отчета с разбивкой на страницы для каждой строки в таблице Excel Online или в списке SharePoint

С помощью [Power Automate](/power-automate/getting-started) можно автоматизировать экспорт и распространение отчетов Power BI с разбивкой на страницы в разнообразные поддерживаемые форматы и сценарии. В этой статье используется шаблон Power Automate для автоматизации настройки повторяющихся операций экспорта одного или нескольких отчетов с разбивкой на страницы. Вы экспортируете их в нужном формате для каждой строки в таблице Excel Online или в списке SharePoint Online. Экспортированный отчет с разбивкой на страницы можно распространить в OneDrive для бизнеса или на сайт SharePoint Online или отправить по электронной почте с помощью Office 365 Outlook.

:::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-overview.png" alt-text="Экспорт отчета с разбивкой на страницы с помощью таблицы Excel Online.":::

Каждая строка в таблице Excel Online или в списке SharePoint Online может представлять одного пользователя для получения отчета с разбивкой на страницы в зависимости от подписки. Или наоборот, каждая строка может представлять уникальный отчет с разбивкой на страницы, который вы хотите распространить. Для таблицы или списка требуется столбец, указывающий, как распространить отчет, будь то OneDrive, SharePoint Online или Outlook. Поток Power Automate использует этот столбец в операторе switch.

Ищете другие шаблоны Power Automate для отчетов Power BI с разбивкой на страницы? Ознакомьтесь со статьей [Экспорт отчетов Power BI с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md).

## <a name="prerequisites"></a>Предварительные требования  

Для продолжения убедитесь, что у вас есть:

- По крайней мере одна рабочая область в клиенте Power BI, поддерживаемая зарезервированной емкостью. Это может быть любой из номеров SKU A4/P1–A6/P3. Узнайте подробнее о [зарезервированных емкостях в Power BI Premium](../admin/service-premium-what-is.md).
- Доступ к стандартным соединителям в Power Automate, которые входят в состав любой подписки Office 365.
- Если вы используете таблицу Excel Online, ее необходимо отформатировать в виде таблицы в Excel. Дополнительные сведения см. в разделе [Создание таблицы](https://support.microsoft.com/office/create-a-table-in-excel-bf0ce08b-d012-42ec-8ecf-a2259c9faf3f).

## <a name="export-a-paginated-report-for-each-row-in-a-table-or-list"></a>Экспорт отчета с разбивкой на страницы для каждой строки в таблице или списке

> [!NOTE]
> Ниже представлен порядок настройки потока с помощью шаблона **Экспорт отчета с разбивкой на страницы для каждой строки в таблице Excel Online**. Можно выполнить эти же действия, чтобы создать поток с помощью шаблона **Экспорт отчета с разбивкой на страницы для каждой строки в списке SharePoint**. Вместо таблицы Excel Online в списке SharePoint Online будут содержаться сведения о том, как экспортировать отчет с разбивкой на страницы.  

1. Войдите в Power Automate ([flow.microsoft.com](https://flow.microsoft.com/)). 
1. Выберите **Шаблоны** и найдите  **отчеты с разбивкой на страницы**. 

    :::image type="content" source="media/service-automate-paginated-integration/power-bi-paginate-automate.png" alt-text="Снимок экрана: шаблоны Power Automate для отчетов Power BI с разбивкой на страницы.":::

1. Выберите **Экспорт отчета Power BI с разбивкой на страницы для каждой строки в таблице Excel Online** или **Экспорт отчета Power BI с разбивкой на страницы для элементов в шаблоне SharePoint Online**. Убедитесь, что вы вошли в Excel Online, Power BI, OneDrive для бизнеса, SharePoint Online и Office 365 Outlook. Выберите **Continue** (Продолжить).  

   :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-excel-online-1.png" alt-text="Экспорт отчета Power BI с разбивкой на страницы для каждой строки в таблице Excel Online.":::

1. Чтобы задать **периодичность** для последовательности, выберите параметр в разделе **Частота** и введите требуемое значение для параметра **Интервал**.

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-recurrence-2.png" alt-text="Выбор периодичности для потока.":::

1. (Необязательно) Выберите **Показать дополнительные параметры**, чтобы задать дополнительные параметры **периодичности**, включая **Часовой пояс**, **Время начала**, **В эти дни**, **В эти часы** и **В эти минуты**.

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-advanced-recurrence-3.png" alt-text="(Необязательно) Выбор дополнительных параметров периодичности.":::

1. В поле **Расположение** выберите OneDrive для бизнеса или сайт SharePoint Online, где сохранена таблица Excel Online или список SharePoint Online. Затем выберите **Библиотека документов** из раскрывающегося списка.

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-location-4.png" alt-text="Выбор расположения таблицы Excel Online.":::

1. Выберите файл Excel Online или список SharePoint Online в поле **Файл**. Выберите имя таблицы или списка в раскрывающемся списке в поле **Таблица**. 
 
    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-file-table-5.png" alt-text="Выбор файла Excel Online и имени таблицы.":::

    > [!TIP]
    > Сведения о форматировании данных в виде таблицы в Excel см. в разделе [Создание таблицы](https://support.microsoft.com/office/create-a-table-in-excel-bf0ce08b-d012-42ec-8ecf-a2259c9faf3f). 

1. Инициализируйте переменную, которая будет использоваться для имени файла. Можно сохранить или изменить значения по умолчанию в полях **Имя** и **Значение**, однако следует оставить для параметра **Тип** значение **Строка**.  

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-name-type-6.png" alt-text="Ввод имени и значения и сохранения типа равным &quot;Строка&quot;.":::

1. В разделе **Применяется к каждому** в поле **Выберите выходные данные предыдущего шага** по умолчанию выбрано **значение**. Этот параметр выполняет итерацию действий, содержащихся в разделе **Применяется к каждому** для каждой строки в таблице Excel Online или в списке SharePoint Online.  

1. В поле **Рабочая область** выберите рабочую область с выделенной емкостью. В поле **Отчет** выберите отчет с разбивкой на страницы в выбранной рабочей области, которую необходимо экспортировать. Если выбрать **Введите пользовательское значение** из раскрывающегося списка, можно задать для параметров **Рабочая область** и **Отчет**, чтобы они были равны столбцу в таблице Excel Online или в списке SharePoint Online. Эти столбцы должны содержать идентификаторы рабочих областей и идентификаторы отчетов соответственно.  

1. Выберите **Формат экспорта** из раскрывающегося списка или установите его равным столбцу в таблице Excel Online, содержащему нужные форматы экспорта. Например, PDF, DOCX или PPTX. При необходимости можно указать параметры для отчета с разбивкой на страницы. Подробные описания параметров см. в [справочнике по соединителю для REST API Power BI](/connectors/powerbi/#export-to-file-for-paginated-reports).

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-export-format-9.png" alt-text="Заполнение полей экспорта в файл для отчетов с разбивкой на страницы.":::

1. В поле **Значение** введите имя отчета с разбивкой на страницы после его экспорта. Обязательно введите расширение файла. Его можно задать статически, например в формате PDF, DOCX или PPTX, либо динамически, выбрав в таблице Excel столбец, соответствующий нужному формату экспорта. 

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-output-value-10.png" alt-text="Выбор имени отчета и расширения файла.":::

1. В действии **Переключить** в поле **На** укажите столбец в таблице Excel Online, соответствующий нужному методу доставки: **OneDrive**, **SharePoint** или **Электронная почта**. 

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-switch-11.png" alt-text="Заполнение поля &quot;На&quot; в действии &quot;Переключить&quot; путем указания столбца в таблице Excel Online.":::

1. В полях **Случай**, **Случай 2** и **Случай 3** введите значения, представленные в столбце таблицы Excel Online, выбранном на предыдущем шаге.  

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-case-1-2-3-12.png" alt-text="Ввод значений в поля &quot;Случай&quot;, &quot;Случай 2&quot; и &quot;Случай 3&quot;.":::

1. Если требуется сохранить разбивку на страницы в OneDrive, выберите **путь к папке** , где ее следует сохранить.  

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-case-onedrive-13.png" alt-text="В случае сохранения в OneDrive.":::

1. В случае сохранения отчета с разбивкой на страницы в SharePoint Online введите **адрес сайта** и **путь к папке**, где его следует сохранить. 

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-case-sharepoint-14.png" alt-text="В случае сохранения отчета с разбивкой на страницы в SharePoint Online.":::

1. Если отчет с разбивкой на страницы отправляется в виде сообщения электронной почты через Outlook, заполните поля **Кому**, **Тема** и **Текст сообщения**. Эти поля могут содержать статическое содержимое или динамическое содержимое из списка в таблице Excel Online или SharePoint Online. Power Automate автоматически подключает отчет с разбивкой на страницы к этому сообщению электронной почты.  

    :::image type="content" source="media/service-automate-paginated-excel-sharepoint-list/excel-template-case-email-15.png" alt-text="В случае если отчет с разбивкой на страницы отправляется как сообщение электронной почты через Outlook.":::

1. Когда все будет готово, выберите  **Следующий шаг** или **Сохранить**. Power Automate создает и оценивает последовательность, а также позволяет определить, обнаруживаются ли ошибки. 

1. При возникновении ошибок выберите  **Изменить поток** , чтобы устранить их. В противном случае нажмите стрелку **Назад**, чтобы просмотреть сведения о потоке и запустить новый поток. 


## <a name="next-steps"></a>Следующие шаги

- [Экспорт отчетов с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md)
- [Начало работы с Power Automate](/power-automate/getting-started/)
- Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)

