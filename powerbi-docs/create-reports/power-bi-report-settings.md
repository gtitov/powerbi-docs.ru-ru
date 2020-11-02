---
title: Изменение параметров для отчетов Power BI
description: Изменение параметров для отчетов в службе Power BI
author: maggiesMSFT
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: how-to
ms.date: 10/14/2020
ms.author: maggies
LocalizationGroup: Reports
ms.openlocfilehash: dd87501a6865b9ea450e3154ee2ac56e0710a067
ms.sourcegitcommit: fddba666c6ea90d525a1c3188bbd3c4a03410cdc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2020
ms.locfileid: "92463088"
---
# <a name="change-settings-for-power-bi-reports"></a>Изменение параметров для отчетов Power BI

[!INCLUDE [applies-to](../includes/applies-to.md)] [!INCLUDE [yes-desktop](../includes/yes-desktop.md)] [!INCLUDE [yes-service](../includes/yes-service.md)]

С помощью параметров отчета в Power BI Desktop и службе Power BI можно управлять тем, как читатели взаимодействуют с отчетом. Например, вы можете разрешить им сохранять фильтры для отчета, персонализировать визуальные элементы в отчете или отображать страницы отчета как вкладки в нижней части отчета, а не сбоку.

:::image type="content" source="media/power-bi-report-settings/service-report-settings-pane.png" alt-text="Снимок экрана: панель параметров отчета в службе Power BI.":::

В первую очередь рекомендуем ознакомиться со следующими статьями:

- [Создание отчета в службе Power BI путем импорта набора данных](service-report-create-new.md), чтобы понять процесс создания отчета.
- [Отчеты в Power BI](../consumer/end-user-reports.md), чтобы понять опыт читателя отчетов.

 Приступим к работе!

## <a name="prerequisites"></a>Предварительные требования

- Сведения о создании отчетов с помощью Power BI Desktop см. в статье [Представление отчетов в Power BI Desktop](desktop-report-view.md).
- [Регистрация в службе Power BI](../fundamentals/service-self-service-signup-for-power-bi.md). 
- Вам необходимо иметь разрешение на правки для отчета в службе Power BI. Дополнительные сведения о разрешении см. в разделе [Роли в новых рабочих областях](../collaborate-share/service-new-workspaces.md#roles-in-the-new-workspaces).
- Если у вас еще нет отчета в службе Power BI, можно [установить пример пакета содержимого](sample-datasets.md#install-built-in-content-packs), содержащий панель мониторинга, отчет и набор данных.

## <a name="open-the-settings-pane-in-power-bi-desktop"></a>Откройте панель "Параметры" в Power BI Desktop

1. Выберите **Файл** > **Параметры и настройки** > **Параметры** .
1. В разделе **Текущий файл** выберите **Параметры отчета** .

    :::image type="content" source="media/power-bi-report-settings/desktop-report-settings-pane.png" alt-text="Снимок экрана: панель параметров отчета в службе Power BI.":::

    В оставшейся части этой статьи описываются определенные параметры отчета.

## <a name="open-the-settings-pane-in-the-power-bi-service"></a>Откройте панель "Параметры" в службе Power BI

1. В режиме чтения отчета выберите **Файл** > **Параметры** .

    :::image type="content" source="media/power-bi-report-settings/service-report-file-settings.png" alt-text="Снимок экрана: панель параметров отчета в службе Power BI.":::

1. В области **Параметры** отображается несколько переключателей, которые можно задать для этого отчета. В оставшейся части этой статьи описываются некоторые из них.

## <a name="set-featured-content"></a>Добавление содержимого в подборку

Вы можете рекомендовать панели мониторинга, отчеты и приложения, чтобы они отображались в разделе "Подборка" на главной странице Power BI ваших коллег. Дополнительные сведения см. в статье [Как добавить содержимое в подборку](../collaborate-share/service-featured-content.md).

## <a name="set-the-pages-pane"></a>Задание области страниц

В настоящее время параметр области страниц можно изменить только в службе Power BI. Если перевести переключатель **Область страниц** в положение "Вкл.", в режиме чтения вкладки страниц отчета будут отображаться в нижней части, а не сбоку. В режиме правки вкладки страницы отчета уже расположены в нижней части отчета.

:::image type="content" source="media/power-bi-report-settings/report-settings-pages-pane.png" alt-text="Снимок экрана: панель параметров отчета в службе Power BI.":::

## <a name="control-filters"></a>Фильтры элементов управления

На панели **параметров** отчета есть три параметра для управления взаимодействием читателя с фильтрами в отчете. Следующие ссылки ведут в статью [Разработка фильтров в отчетах Power BI](power-bi-report-filter.md) с подробными сведениями о каждом параметре.

- **Постоянные фильтры** позволяют читателям [сохранять фильтры в отчете](power-bi-report-filter.md#allow-saving-filters).
- **Возможности фильтрации** имеют еще два параметра:
    
    Разрешить читателям отчета [изменять типы фильтров](power-bi-report-filter.md#restrict-changes-to-filter-type).

    Включить [поиск в области фильтров](power-bi-report-filter.md#filters-pane-search).

## <a name="export-data"></a>Экспорт данных

По умолчанию [читатели отчета могут экспортировать сводные или базовые данные](../consumer/end-user-export.md) из визуальных элементов в отчете. С помощью функции **Экспорт данных** вы можете разрешить экспортировать только сводные данные или запретить экспортировать данные из отчета.

## <a name="personalize-visuals"></a>Персонализация визуальных элементов

Разрешить читателям изменять и персонализировать визуальные элементы в отчете. Узнайте больше о том, как [разрешить читателям отчета персонализировать визуальные элементы](power-bi-personalize-visuals.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Добавление содержимого в подборку на главных страницах других пользователей](../collaborate-share/service-featured-content.md)
* [Разрешение читателям отчета персонализировать визуальные элементы в отчете](power-bi-personalize-visuals.md)
* Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
