---
title: Экспорт отчета и его отправка по электронной почте с помощью Power Automate
description: В этой статье описывается, как использовать Power Automate для автоматизации экспорта и распространения отчетов Power BI в различные поддерживаемые форматы и сценарии.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 12/10/2020
LocalizationGroup: Get started
ms.openlocfilehash: 45bccbefc6e499375d33aa049ead8a6c6e47bc8c
ms.sourcegitcommit: bbf7e9341a4e1cc96c969e24318c8605440282a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97098833"
---
# <a name="export-and-email-a-power-bi-report-with-power-automate"></a>Экспорт отчета Power BI и его отправка по электронной почте с помощью Power Automate

С помощью [Power Automate](/power-automate/getting-started) можно автоматизировать экспорт и распространение отчетов Power BI в различные поддерживаемые форматы и сценарии. С помощью инструкций из этой статьи вы создадите с нуля собственный поток. Используйте действие "Экспорт в файл для отчетов Power BI", чтобы автоматически распространить отчет Power BI по электронной почте.

:::image type="content" source="media/service-automate-power-bi-report-export/automate-power-bi-report-overview.png" alt-text="Шаги по экспорту отчета и его отправке по электронной почте с помощью Power Automate.":::

## <a name="prerequisites"></a>Предварительные требования  

Для продолжения убедитесь, что у вас есть:

- По крайней мере одна рабочая область в клиенте Power BI, поддерживаемая зарезервированной емкостью. Такая емкость может иметь любой SKU из A1/EM1–A6/P3. Узнайте подробнее о [зарезервированных емкостях в Power BI Premium](../admin/service-premium-what-is.md).
- Доступ к стандартным соединителям в Power Automate, которые входят в состав любой подписки Office 365.

## <a name="create-a-flow-from-scratch"></a>Создание потока с нуля 

С помощью этой задачи вы создадите с нуля простой поток. Поток экспортирует отчет Power BI в формате PDF и прикрепляет его к сообщению электронной почты, которое отправляется еженедельно.  

1. Войдите в Power Automate (flow.microsoft.com).
2. Выберите **Создать** > **Поток по расписанию**. 

    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-scheduled-flow-2.png" alt-text="Создание потока по расписанию в Power Automate.":::

3. В окне **Создание потока по расписанию** присвойте потоку имя. 
4. В разделе **Запуск потока** выберите дату и время начала для потока, а также частоту повторения.
5. В разделе **В эти дни** выберите, по каким дням нужно запускать поток, и нажмите **Создать**.

    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-build-flow-5.png" alt-text="Настройка расписания потока в Power Automate.":::

6. На странице **Повторение** выберите **Показать расширенные параметры** и введите значения в поля **В эти часы** и **В эти минуты**, чтобы задать конкретное время для запуска потока.
 
    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-recurrence-6.png" alt-text="Настройка повторения в Power Automate.":::

7. Выберите **Новый шаг**.
8. В разделе **Выберите действие** выполните поиск по строке **Power BI** и выберите **Экспорт в файл для отчетов Power BI**.
 
    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-choose-action-8.png" alt-text="Выбор действия в Power Automate.":::

9. На странице **Экспорт в файл для отчетов Power BI** выберите **рабочую область** и **отчет** из раскрывающихся списков.
10. Выберите нужный **формат экспорта** для своего отчета Power BI.
 
    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-export-file-10.png" alt-text="Выбор формата экспорта в Power Automate.":::

11. При необходимости укажите определенные страницы для экспорта в поле **pageName для страницы — 1**. Обратите внимание, что параметр имени страницы отличается от отображаемого имени страницы. Найдите имя страницы, перейдя на страницу в службе Power BI и скопировав последнюю часть URL-адреса.
 
     :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-copy-url-11.png" alt-text="Выбор имени области в URL-адресе.":::

12. При необходимости укажите конкретную закладку, которая будет отображаться в поле **Имя закладки страницы**. Как и в случае с параметром имени страницы, параметр имени закладки можно найти в URL-адресе отчета. Вы можете указать дополнительные параметры для отчета Power BI. Подробные описания этих параметров см. в [справочнике по соединителю для REST API Power BI](/connectors/powerbi/#export-to-file-for-power-bi-reports).

    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-bookmark-url-12.png" alt-text="Выбор имени закладки в URL-адресе.":::

13. Выберите **Новый шаг**.
14. В разделе **Выберите действие** выполните поиск по строке **Outlook** и выберите **Отправка электронной почты (V2)** .
15. На странице **Отправка электронной почты (V2)** введите данные в поля **Кому**, **Тема** и **Текст** для сообщения электронной почты.
16. Выберите **Показать расширенные параметры**. В поле **Имя вложения — 1** введите имя своего вложения. Добавьте расширение файла к его имени (например, .PDF), которое соответствует нужному **формату экспорта**.
17. В поле **Содержимое вложения** выберите **Содержимое файла**, чтобы вложить экспортированный отчет Power BI.  
 
    :::image type="content" source="media/service-automate-power-bi-report-export/automate-report-send-email-17.png" alt-text="Выбор экспортированного отчета для сообщения электронной почты.":::

18. Когда все будет готово, выберите **Следующий шаг** или **Сохранить**. Power Automate создает и оценивает последовательность, а также позволяет определить, обнаруживаются ли ошибки.
1. При возникновении ошибок выберите  **Изменить поток** , чтобы устранить их. В противном случае щелкните стрелку **назад**, чтобы просмотреть сведения о потоке и запустить новый поток.
    При запуске потока Power Automate экспортирует отчет Power BI в указанном формате и по расписанию отправляет его в виде вложения по электронной почте.  

## <a name="next-steps"></a>Дальнейшие действия

- [Интеграция оповещений о данных Power BI с Power Automate](service-flow-integration.md)
- [Начало работы с Power Automate](/power-automate/getting-started/)
- Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
