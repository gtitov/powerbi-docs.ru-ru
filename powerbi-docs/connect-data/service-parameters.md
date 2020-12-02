---
title: Изменение настроек параметров в службе Power BI
description: Параметры запроса создаются в Power BI Desktop, однако их можно просматривать и изменять в службе Power BI.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 08/04/2020
LocalizationGroup: Create reports
ms.openlocfilehash: 29468ea50625b1d354bd431f77c5e89edf5a889d
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96402094"
---
# <a name="edit-parameter-settings-in-the-power-bi-service"></a>Изменение настроек параметров в службе Power BI
Авторы отчетов добавляют параметры запросов в отчеты в Power BI Desktop. Параметры позволяют создавать части отчетов в зависимости от *значений* одного или нескольких параметров. Например, автор отчета может создать параметр, который ограничивает данные одной страной или регионом, или параметр, который определяет число допустимых форматов для таких полей, как поле даты, времени и текста.

![Вкладка "Главная" с пунктом "Управление параметрами" в Desktop](media/service-parameters/power-bi-manage-parameters.png)

## <a name="review-and-edit-parameters-in-power-bi-service"></a>Просмотр и изменение параметров в службе Power BI

Автор отчета определяет параметры в Power BI Desktop. Когда вы [публикуете этот отчет в службе Power BI](../create-reports/desktop-upload-desktop-files.md), настройки параметров и выбранные варианты переносятся вместе с ним. Вы можете просматривать и изменять параметры в службе Power BI, но не создавать их.

1. В службе Power BI щелкните значок шестеренки ![значок шестеренки](media/service-parameters/power-bi-cog.png), чтобы открыть окно **Параметры**.

2. Выберите вкладку **Наборы данных** и выделите набор данных в списке. 
    
    ![Окно "Параметры" с выбранной вкладкой "Наборы данных"](media/service-parameters/power-bi-select-dataset2.png)

3. Разверните узел **Параметры**.  Если выбранный набор данных не содержит параметров, вы увидите сообщение со ссылкой для получения дополнительных сведений о параметрах запроса. Если набор данных имеет параметры, развернув заголовок **Параметры**, вы увидите их. 

    ![Окно "Параметры" с развернутым разделом параметров](media/service-parameters/power-bi-settings.png)

    Просмотрите настройки параметров и при необходимости внесите изменения. Неактивные поля недоступны для редактирования. 


## <a name="next-steps"></a>Дальнейшие действия
Ситуативный способ добавления простых параметров путем [изменения URL-адреса](../collaborate-share/service-url-filters.md).
