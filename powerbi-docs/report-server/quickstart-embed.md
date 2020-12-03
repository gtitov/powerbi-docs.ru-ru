---
title: По внедрению отчета решения "Сервер отчетов Power BI" с помощью iFrame в SharePoint Server
description: Эта статья описывает внедрение отчета Сервера отчетов Power BI с помощью iFrame в SharePoint Server.
author: maggiesMSFT
ms.author: maggies
ms.date: 07/28/2020
ms.topic: conceptual
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.custom: mvc
ms.openlocfilehash: 698f12f4bf5266373be8393d2add45d70979ab41
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96418447"
---
# <a name="embed-a-power-bi-report-server-report-using-an-iframe-in-sharepoint-server"></a>По внедрению отчета решения "Сервер отчетов Power BI" с помощью iFrame в SharePoint Server

В этой статье вы узнаете, как внедрить отчет Сервера отчетов Power BI с помощью iFrame на страницу SharePoint. Если вы используете SharePoint Online, Сервер отчетов Power BI должен быть общедоступным. В SharePoint Online веб-часть Power BI, которая работает со службой Power BI, несовместима с Сервером отчетов Power BI.  

![Пример iFrame](media/quickstart-embed/quickstart_embed_01.png)

## <a name="prerequisites"></a>Предварительные требования
* Установленный и настроенный [Сервер отчетов Power BI](https://powerbi.microsoft.com/report-server/).
* Установленное [приложение Power BI Desktop, оптимизированное для Сервера отчетов Power BI](install-powerbi-desktop.md).
* Установленная и настроенная [среда SharePoint 2013, 2016 или 2019](/sharepoint/install/install).
* Internet Explorer 11 поддерживается, только если для режима документа установлен режим IE11 (Microsoft Edge) или при использовании SharePoint Online. Вы можете использовать другие поддерживаемые браузеры в локальной среде SharePoint и в SharePoint Online.

## <a name="create-the-power-bi-report-url"></a>Создание URL-адреса отчета Power BI

1. Скачайте пример из GitHub: [демонстрация блога](https://github.com/Microsoft/powerbi-desktop-samples). Выберите **Clone or download** (Клонировать или скачать) и затем **Скачать ZIP-файл**.

    ![Скачивание примера PBIX-файла](media/quickstart-embed/quickstart_embed_14.png)

2. Распакуйте файл и откройте пример PBIX-файла в Power BI Desktop, оптимизированном для Сервера отчетов Power BI.

    ![Средство сервера отчетов для Power BI Desktop](media/quickstart-embed/quickstart_embed_02.png)

3. Сохраните отчет в решении **Сервер отчетов Power BI**. 

    ![Сохранение в решении "Сервер отчетов Power BI"](media/quickstart-embed/quickstart_embed_03.png)

4. Просмотрите отчет на веб-портале Сервера отчетов Power BI.

    ![Веб-портал](media/quickstart-embed/quickstart_embed_04.png)

### <a name="capture-the-url-parameter"></a>Запись параметра URL-адреса

Получив URL-адрес, вы можете создать iFrame для размещения отчета на веб-странице SharePoint. Для любого URL-адреса отчета Сервера отчетов Power BI добавьте следующий параметр строки запроса, чтобы внедрить отчет в iFrame SharePoint: `?rs:embed=true`.

   Например:
    ``` 
    https://myserver/reports/powerbi/Sales?rs:embed=true
    ```
## <a name="embed-the-report-in-a-sharepoint-iframe"></a>Внедрение отчета в iFrame SharePoint

1. Перейдите к странице **Содержимое сайта** в SharePoint.

    ![Страница "Содержимое сайта"](media/quickstart-embed/quickstart_embed_05.png)

2. Выберите страницу, на которую нужно добавить отчет.

    ![Приложение страницы "Содержимое сайта"](media/quickstart-embed/quickstart_embed_06.png)

3. Выберите значок шестеренки в верхней правой части страницы и элемент **Изменить страницу**.

    ![Параметр "Изменить страницу"](media/quickstart-embed/quickstart_embed_07.png)

4. Выберите **Добавить веб-часть**.

5. В разделе **Категории** выберите **Среда и контент**. В разделе **Части** выберите **Редактор содержимого** и щелкните **Добавить**.

    ![Выбор веб-части редактора содержимого](media/quickstart-embed/quickstart_embed_09.png)

6. Выберите **Click here to add new content** (Щелкните здесь, чтобы добавить новое содержимое).

7. В верхнем меню выберите **Форматирование текста** и затем **Изменить источник**.

     ![Править источник](media/quickstart-embed/quickstart_embed_11.png)

8. В окне **Изменить источник** вставьте код для iFrame в поле **Источник HTML** и нажмите кнопку **ОК**.

    ![Код iFrame](media/quickstart-embed/quickstart_embed_12.png)

     Например:
     ```html
     <iframe width="800" height="600" src="https://myserver/reports/powerbi/Sales?rs:embed=true" frameborder="0" allowFullScreen="true"></iframe>
     ```

9. В верхнем меню выберите **Страница** и затем **Остановить изменение**.

    ![Остановить изменение](media/quickstart-embed/quickstart_embed_13.png)

    Отчет отображается на странице.

    ![Пример iFrame](media/quickstart-embed/quickstart_embed_01.png)

## <a name="next-steps"></a>Дальнейшие действия

- [Создание отчета Power BI для Сервера отчетов Power BI](quickstart-create-powerbi-report.md).  
- [Создание отчета с разбивкой на страницы для Сервера отчетов Power BI](quickstart-create-paginated-report.md).  

Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI](https://community.powerbi.com/).