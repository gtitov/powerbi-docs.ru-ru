---
title: Добавление гиперссылок (URL-адресов) в таблицу или матрицу
description: Из этого раздела вы узнаете, как добавлять гиперссылки (URL-адреса) в таблицу. Power BI Desktop можно использовать для добавления гиперссылок (URL-адресов) в набор данных. Затем с помощью Power BI Desktop или службы Power BI вы сможете добавить созданные гиперссылки в таблицы и матрицы отчета.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: pbi-reports-dashboards
ms.topic: how-to
ms.date: 10/15/2020
LocalizationGroup: Visualizations
ms.openlocfilehash: c60c5824f20edd6d596d23fed56f8cdfaa19a01a
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96418056"
---
# <a name="add-hyperlinks-urls-to-a-table-or-matrix"></a>Добавление гиперссылок (URL-адресов) в таблицу или матрицу
Из этого раздела вы узнаете, как добавлять гиперссылки (URL-адреса) в таблицу. Power BI Desktop можно использовать для добавления гиперссылок (URL-адресов) в набор данных. Созданные гиперссылки можно добавить в таблицы и матрицы отчета для Power BI Desktop или службы Power BI. Затем URL-адрес или значок ссылки можно отобразить или отформатировать другой столбец как текст ссылки.

![Таблицы с гиперссылками](media/power-bi-hyperlinks-in-tables/power-bi-url-link-text.png)

Вы можете также создать гиперссылки в [текстовых полях в отчетах](service-add-hyperlink-to-text-box.md) в службе Power BI и Power BI Desktop. В службе Power BI гиперссылки можно добавлять к [элементам на панели мониторинга](service-dashboard-edit-tile.md) и [текстовым полям панелей мониторинга](service-dashboard-add-widget.md). 


## <a name="format-a-url-as-a-hyperlink-in-power-bi-desktop"></a>Форматирование URL-адреса в виде гиперссылки в Power BI Desktop

Вы можете отформатировать URL-адреса в виде гиперссылок, используя Power BI Desktop, но не службу Power BI. Кроме того, вы можете [форматировать гиперссылки в Excel Power Pivot](#create-a-table-or-matrix-hyperlink-in-excel-power-pivot) перед импортом книги в Power BI.

1. Если гиперссылка еще не существует как поле в наборе данных, добавьте ее как [пользовательский столбец](../transform-model/desktop-common-query-tasks.md) с помощью приложения Power BI Desktop.

    > [!NOTE]
    > В режиме DirectQuery нельзя создать столбец.  Но если данные уже содержат URL-адреса, то их можно превратить в гиперссылки.

2. Выберите столбец в представлении данных или отчета. 

3. На вкладке **Моделирование** выберите **Категория данных** > **URL веб-узла**.
   
    ![Раскрывающийся список категорий данных](media/power-bi-hyperlinks-in-tables/power-bi-format-web-url.png)

    > [!NOTE]
    > URL-адреса должны начинаться с определенных префиксов. Полный список см. в разделе [Рекомендации и устранение неполадок](#considerations-and-troubleshooting) в этой статье.

## <a name="create-a-table-or-matrix-with-a-hyperlink"></a>Создание таблицы или матрицы с гиперссылкой

1. После [форматирования гиперссылки в виде URL-адреса](#format-a-url-as-a-hyperlink-in-power-bi-desktop) перейдите в представление отчетов.
2. Создайте таблицу или матрицу с полем, классифицированным как URL веб-узла. Гиперссылки отображаются синим цветом и подчеркиванием.

    ![Синие и подчеркнутые ссылки](media/power-bi-hyperlinks-in-tables/power-bi-url-blue-underline.png)


## <a name="display-a-hyperlink-icon-instead-of-a-url"></a>Отображение значка гиперссылки вместо URL-адреса

Вместо длинного URL-адреса в таблице можно отобразить значок гиперссылки ![Значок гиперссылки](media/power-bi-hyperlinks-in-tables/power-bi-hyperlink-icon.png) . 

> [!NOTE]
> Значки в матрице невозможно отобразить.
   
1. Для начала [создайте таблицу с гиперссылкой](#create-a-table-or-matrix-with-a-hyperlink).

2. Выберите таблицу, чтобы сделать ее активной.

    Щелкните значок **Форматирование**, ![значок с изображением валика](media/power-bi-hyperlinks-in-tables/power-bi-paintroller.png), чтобы открыть вкладку "Форматирование".

    Разверните узел **Значения**, найдите **значок URL-адреса** и установите для него значение **Вкл.**

    ![Включение значка URL-адреса](media/power-bi-hyperlinks-in-tables/power-bi-url-icon-on.png)

1. (Необязательно) [Опубликуйте отчет](desktop-upload-desktop-files.md) из Power BI Desktop в службу Power BI. Гиперссылки также работают при открытии отчета в службе Power BI.

## <a name="format-link-text-as-a-hyperlink"></a>Форматирование текста ссылки в виде гиперссылки

Можно также отформатировать другое поле в таблице как гиперссылку, не имея столбец для URL-адреса. В этом случае столбец не форматируется как URL веб-узла.

> [!NOTE]
> В матрице другое поле нельзя форматировать как гиперссылку.

1. Если поле с гиперссылкой еще не существует в наборе данных, добавьте ее как [пользовательский столбец](../transform-model/desktop-common-query-tasks.md) с помощью приложения Power BI Desktop. Опять же, в режиме DirectQuery нельзя создать столбец.  Но если данные уже содержат URL-адреса, то их можно превратить в гиперссылки.

2. В представлении данных или отчета выберите столбец, содержащий URL-адрес. 

3. На вкладке **Моделирование** выберите пункт **Категория данных**. Убедитесь, что столбец отформатирован как **Без категории**.

2. В представлении отчетов создайте таблицу или матрицу со столбцом URL-адреса и столбцом, который будет отформатирован как текст ссылки.

3. Щелкните значок **Форматирование**, ![значок с изображением валика](media/power-bi-hyperlinks-in-tables/power-bi-paintroller.png), чтобы открыть вкладку "Форматирование".

4. Разверните **Условное форматирование**, убедившись в том, что имя в поле является столбцом, который нужно использовать в качестве текста ссылки. Найдите **URL-адрес в Интернете** и задайте его как **Вкл**.

    ![Условного форматирования URL веб-узла](media/power-bi-hyperlinks-in-tables/power-bi-format-conditional-web-url.png)

    > [!NOTE]
    > Если **URL-адрес в Интернете** не отображается, убедитесь, что столбец, содержащий гиперссылки, *не* отформатирован как **URL-адрес в Интернете** в раскрывающемся списке **Категория данных**.

5. В диалоговом окне **URL веб-узла** выберите поле, содержащее URL-адрес в окне **На основе поля** > **ОК**.

    ![Диалоговое окно "URL веб-узла"](media/power-bi-hyperlinks-in-tables/power-bi-format-web-url-dialog.png)

    Теперь текст в этом столбце форматируется как ссылка.

    ![Текст, отформатированный как гиперссылка](media/power-bi-hyperlinks-in-tables/power-bi-url-link-text.png)

1. (Необязательно) [Опубликуйте отчет](desktop-upload-desktop-files.md) из Power BI Desktop в службу Power BI. Гиперссылки также работают при открытии отчета в службе Power BI.

## <a name="create-a-table-or-matrix-hyperlink-in-excel-power-pivot"></a>Создание гиперссылки в таблице или матрице в Excel Power Pivot

Другим способом добавления гиперссылок в таблицы и матрицы Power BI является создание гиперссылок в наборе данных перед подключением к набору данных и его импортом из Power BI. В этом примере используется книга Excel.

1. Откройте книгу в Excel.
2. Перейдите на вкладку **PowerPivot**, а затем выберите **Управление**.
   
   ![Открытие PowerPivot в Excel](media/power-bi-hyperlinks-in-tables/createhyperlinkinpowerpivot2.png)
1. В открывшемся окне Power Pivot выберите вкладку **Дополнительно**.
   
   ![Вкладка "Дополнительно" в PowerPivot"](media/power-bi-hyperlinks-in-tables/createhyperlinkinpowerpivot3.png)
4. Поместите курсор в столбец, содержащий URL-адреса, которые вы хотите преобразовать в гиперссылки в таблицах Power BI.
   
   > [!NOTE]
   > URL-адреса должны начинаться с определенных префиксов. Полный список см. в разделе [Рекомендации и устранение неполадок](#considerations-and-troubleshooting).
   > 
   
5. В группе **Свойства отчетов** щелкните раскрывающийся список **Категория данных** и выберите **URL-адрес веб-сайта**. 
   
   ![Раскрывающийся список категорий данных в Excel](media/power-bi-hyperlinks-in-tables/createhyperlinksnew.png)

6. В службе Power BI или Power BI Desktop подключитесь к этой книге или импортируйте ее.
7. Создайте визуализацию таблицы, содержащую поле URL-адреса.
   
   ![Создание таблицы в Power BI с полем URL-адреса](media/power-bi-hyperlinks-in-tables/hyperlinksintables.gif)

## <a name="considerations-and-troubleshooting"></a>Рекомендации и устранение неполадок

Значение URL-адреса может начинаться со следующих последовательностей:
- http
- HTTP
- mailto
- ftp
- news
- telnet

Вопрос. Можно ли использовать настраиваемый URL-адрес в качестве гиперссылки в таблице или матрице?    
Ответ. Нет. Можно использовать значок ссылки. Если вам нужен настраиваемый текст для гиперссылок и ваш список URL-адресов короткий, попробуйте использовать текстовое поле.


## <a name="next-steps"></a>Дальнейшие действия
[Визуализации в отчетах Power BI](../visuals/power-bi-report-visualizations.md)

[Основные понятия для разработчиков в службе Power BI](../fundamentals/service-basic-concepts.md)

Остались вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
