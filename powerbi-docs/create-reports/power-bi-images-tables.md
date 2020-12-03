---
title: Отображение изображений в таблице или матрице в отчете
description: В Power BI Desktop создается столбец с гиперссылками на изображения. Затем в Power BI Desktop или Службе Power BI вы добавляете эти гиперссылки в таблицу, матрицу, срез или многострочную карту отчета, чтобы отобразить изображение.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.service: powerbi
ms.subservice: pbi-reports-dashboards
ms.topic: how-to
ms.date: 09/11/2019
LocalizationGroup: Visualizations
ms.openlocfilehash: 4ba0042804d366ddfd80935c48246cadeadf3614
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96417964"
---
# <a name="display-images-in-a-table-matrix-or-slicer-in-a-report"></a>Отображение изображений в таблице, матрице или срезе в отчете

Изображения улучшают наглядность отчета. Статические изображения подходят для выполнения некоторых задач. Но иногда требуются изображения, связанные с данными в отчете. В этом разделе объясняется, как добавлять изображения в таблицу, матрицу, срез или многострочную карту. 

![Изображения в таблице](media/power-bi-images-tables/power-bi-url-images-table.png)

## <a name="add-images-to-your-report"></a>Добавление изображений в отчет

1. Создайте столбец с URL-адресами изображений. Требования к изображениям изложены в разделе [Примечания](#considerations) далее в этой статье.

1. Выберите этот столбец. На ленте **Моделирование** для параметра **Категория данных** выберите **URL-адрес изображения**.

    ![Определение URL-адреса изображения в качестве категории данных](media/power-bi-images-tables/power-bi-set-url-image.png)

1. Добавьте столбец в таблицу, матрицу, срез или многострочную карту.

    ![Срез с изображениями](media/power-bi-images-tables/power-bi-url-images-slicer.png)

## <a name="considerations"></a>Ограничения

- Поддерживается добавление изображений в таких форматах: BMP, JPG, JPEG, GIF PNG и SVG.
- URL-адрес должен поддерживать анонимный доступ и не быть адресом сайта, на который необходимо выполнять вход (например, сайта SharePoint). Но если изображения размещаются в SharePoint или OneDrive, вы можете получить код внедрения, который указывает непосредственно на эти изображения. 


## <a name="next-steps"></a>Дальнейшие действия

[Форматирование и макет страницы](/learn/modules/visuals-in-power-bi/12-formatting)

[Основные понятия для разработчиков в службе Power BI](../fundamentals/service-basic-concepts.md)

У вас имеются и другие вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
