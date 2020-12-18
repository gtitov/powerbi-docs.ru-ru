---
title: Сохранение отчета с разбивкой на страницы в локальной папке с помощью Power Automate
description: В этой статье приводится шаблон для настройки регулярного экспорта отчета с разбивкой на страницы в нужном формате в файловую систему.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 12/08/2020
LocalizationGroup: Get started
ms.openlocfilehash: a30f0df972c375af4fb284ce3bba5372870d6efb
ms.sourcegitcommit: bbf7e9341a4e1cc96c969e24318c8605440282a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97098812"
---
# <a name="save-a-power-bi-paginated-report-to-a-local-folder--with-power-automate"></a>Сохранение отчета Power BI с разбивкой на страницы в локальной папке с помощью Power Automate

С помощью [Power Automate](/power-automate/getting-started) можно автоматизировать экспорт и распространение отчетов Power BI с разбивкой на страницы в разнообразные поддерживаемые форматы и сценарии. В этой статье приводится шаблон для настройки регулярного экспорта отчета с разбивкой на страницы в нужном формате в файловую систему. Ознакомьтесь с предварительными требованиями, если вы впервые используете действие "Экспорт в файл для отчетов с разбивкой на страницы" в потоке Power Automate.

:::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-overview.png" alt-text="Настройка регулярного экспорта отчета с разбивкой на страницы.":::

Ищете другие шаблоны Power Automate для отчетов Power BI с разбивкой на страницы? Ознакомьтесь со статьей [Экспорт отчетов Power BI с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md).

## <a name="prerequisites"></a>Предварительные требования  

Для продолжения убедитесь, что у вас есть:

- По крайней мере одна рабочая область в клиенте Power BI, поддерживаемая зарезервированной емкостью. Это может быть любой из номеров SKU A4/P1–A6/P3. Узнайте подробнее о [зарезервированных емкостях для отчетов с разбивкой на страницы в Power BI Premium](../admin/service-premium-what-is.md#paginated-reports).
- Доступ к стандартным соединителям в Power Automate, которые входят в состав любой подписки Office 365.

## <a name="save-a-power-bi-paginated-report-to-a-local-folder"></a>Сохранение отчета Power BI с разбивкой на страницы в локальной папке

1. Выберите шаблон **Сохранение отчета Power BI с разбивкой на страницы в локальной файловой системе**. Убедитесь, что вы вошли в Power BI и подключились к локальной файловой системе. Выберите **Continue** (Продолжить). 

    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-save-report-local-file-1.png" alt-text="Сохранение отчета Power BI с разбивкой на страницы в локальной файловой системе.":::

2. Возможно, для подключения к файловой системе потребуется выбрать **Добавить новое подключение**. 
1. Введите значение в поле **Имя подключения**, путь к нужной **корневой папке** и выполните аутентификацию, введя значения в поля **Имя пользователя** и **Пароль**. Выберите **шлюз** из раскрывающегося списка, если вы используете локальный шлюз данных.

    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-set-file-system-2.png" alt-text="Ввод имени подключения и корневой папки.":::
 
3. Чтобы задать частоту **повторения** для потока, выберите параметр в раскрывающемся списке **Частота** и введите требуемое значение для параметра **Интервал**.  

    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-recurrence-frequency-3.png" alt-text="Настройка частоты повторения для потока.":::

4. При необходимости выберите **Показать расширенные параметры**. Задайте дополнительные параметры **повторения**, такие как **Часовой пояс**, **Время начала**, **В эти дни**, **В эти часы** и **В эти минуты**. 
 
    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-recurrence-advanced-4.png" alt-text="Настройка расширенных параметров для повторения.":::

5. В поле **Рабочая область** выберите рабочую область с зарезервированной емкостью, в которой находится отчет. В поле **Отчет** выберите отчет с разбивкой на страницы, который необходимо экспортировать в рабочую область. В поле **Формат экспорта** выберите нужный формат экспорта. При необходимости можно указать параметры для отчета с разбивкой на страницы. Подробные описания параметров см. в [справочнике по соединителю для REST API Power BI](/connectors/powerbi/#export-to-file-for-paginated-reports).  
 
    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-select-workspace-report-5.png" alt-text="Выбор рабочей области и отчета.":::

6. В диалоговом окне **Создание файла** в поле **Путь к папке** выберите папку, в которую нужно экспортировать отчет с разбивкой на страницы.
 
    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-create-file-6.png" alt-text="Выбор папки, в которую нужно экспортировать отчет с разбивкой на страницы":::

7. Power Automate автоматически создает **имя файла** и **содержимое файла**. Вы можете изменить **имя файла**, но оставьте без изменений динамически создаваемое значение в поле **Содержимое файла**.
8. Когда все будет готово, выберите **Следующий шаг** или **Сохранить**. Power Automate создаст и проанализирует поток.
9. Если Power Automate найдет ошибки, выберите **Изменить поток**, чтобы исправить их. В противном случае нажмите стрелку назад, чтобы просмотреть сведения о потоке и запустить новый поток.
10. При запуске потока Power Automate экспортирует отчет с разбивкой на страницы в указанном формате в выбранную папку в файловой системе.

    :::image type="content" source="media/service-automate-paginated-local-file/paginated-local-file-exported-10.png" alt-text="Power Automate экспортирует отчет с разбивкой на страницы в указанном формате.":::

## <a name="next-steps"></a>Следующие шаги

- [Экспорт отчетов с разбивкой на страницы с помощью Power Automate](service-automate-paginated-integration.md)
- [Начало работы с Power Automate](/power-automate/getting-started/)
- Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)

