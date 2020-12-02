---
title: Текстовые поля и фигуры в отчетах Power BI
description: Вы можете добавлять и создавать текстовые поля и фигуры в отчетах с помощью службы Microsoft Power BI.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
featuredvideoid: _3q6VEBhGew
ms.service: powerbi
ms.subservice: pbi-reports-dashboards
ms.topic: how-to
ms.date: 05/29/2019
LocalizationGroup: Visualizations
ms.openlocfilehash: 90c7489ad047be47a2a1f9ac9e814a9da5724f32
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96393561"
---
# <a name="add-text-boxes-and-shapes-to-power-bi-reports"></a>Добавление текстовых полей и фигур в отчеты Power BI
Вы можете добавлять текстовые поля и фигуры в отчеты с помощью службы Power BI и Power BI Desktop. В обоих случаях требуются разрешения на изменение отчета. Если доступ к отчету в службе Power BI вам предоставил другой пользователь, у вас не будет прав на редактирование. 

Посмотрите видео о том, как с помощью Power BI Desktop [добавить статические изображения в отчет](/learn/modules/visuals-in-power-bi/12-formatting). Затем сделайте это самостоятельно, но уже в службе Power BI, следуя приведенным ниже инструкциям.
> 
> <iframe width="560" height="315" src="https://www.youtube.com/embed/_3q6VEBhGew" frameborder="0" allowfullscreen></iframe>
> 

## <a name="add-a-text-box-to-a-report"></a>Добавление текстового поля в отчет
1. Откройте отчет в режиме редактирования.

2. Поместите курсор в любое пустое место холста отчетов и выберите **Текстовое поле** в верхнем меню.
   
   ![Выбор текстового поля](media/power-bi-reports-add-text-and-shapes/pbi_textbox.png)
3. Введите текст в текстовое поле и по желанию выберите шрифт, цвет и выравнивание текста. 
   
   ![Ввод текста](media/power-bi-reports-add-text-and-shapes/pbi_textbox2new.png)
4. Чтобы изменить расположение текстового поля, выберите серую область вверху и перетащите поле. Чтобы изменить размер текстового поля, выберите и перетащите один из маркеров. 
   
   ![Позиционирование текстового поля](media/power-bi-reports-add-text-and-shapes/textboxsmaller.gif)

5. Выбрав текстовое поле, добавьте параметры форматирования на панели **Визуализации**. В этом примере мы отформатировали фон и границы. Можно также создать точный размер и положение для текстового поля.  

   ![Форматирование текстового поля](media/power-bi-reports-add-text-and-shapes/power-bi-borders.png)

6. Чтобы закрыть текстовое поле, выберите любое пустое место на холсте отчета. 

7. Нажмите значок закрепления,  ![Значок булавки](media/power-bi-reports-add-text-and-shapes/pbi_pintile.png) для закрепления текстового поля на панели мониторинга. 

## <a name="add-a-shape-to-a-report"></a>Добавление фигуры в отчет
1. Поместите курсор в любом месте холста отчета и выберите **Фигуры**.
   
   ![Выбор фигур](media/power-bi-reports-add-text-and-shapes/power-bi-shapes.png)
2. В раскрывающемся списке выберите фигуру, чтобы добавить ее на холст отчета. В этом примере добавьте стрелку, чтобы направить внимание на пузырек с наибольшим суммарным отклонением продаж. 
   
   В области **Формат фигуры** настройте фигуру. В этом примере мы создали красную стрелку с темной красной границей, повернутую на 90 градусов.
   
   ![Настройка фигуры](media/power-bi-reports-add-text-and-shapes/power-bi-arrrow.png)
3. Чтобы изменить расположение фигуры, выберите серую область вверху и перетащите фигуру. Чтобы изменить размер фигуры, выберите и перетащите один из маркеров. Как и для текстового поля, для фигуры можно также создать точный размер и положение.

   > [!NOTE]
   > Фигуры невозможно закрепить на панели мониторинга, только если это не один из визуальных элементов на [закрепляемой динамической странице](service-dashboard-pin-live-tile-from-report.md). 
   > 
   > 

## <a name="next-steps"></a>Дальнейшие действия

Рекомендуем также ознакомиться со следующими материалами:

* [Добавление гиперссылки в текстовое поле](service-add-hyperlink-to-text-box.md)
* [Основные понятия для разработчиков в службе Power BI](../fundamentals/service-basic-concepts.md)
* [Советы по улучшению анализа с помощью фигур, изображений и значков в отчетах Power BI](../guidance/report-tips-shapes-images-icons.md)
* У вас имеются и другие вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
