---
title: Создание отчета на базе списка SharePoint
description: В этом учебнике показано, как преобразовать данные списка SharePoint в отчет Power BI.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 01/10/2020
LocalizationGroup: Visualizations
ms.openlocfilehash: 5347405c13f71fa0932c48eb218618b28a9f03c8
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96404532"
---
# <a name="create-a-report-on-a-sharepoint-list"></a>Создание отчета на базе списка SharePoint

Многие команды специалистов и организации используют для хранения данных списки в SharePoint Online, обеспечивающие простоту настройки и возможность легкого обновления пользователями.  Иногда чтобы быстро получить представление о данных, пользователю гораздо проще взглянуть на диаграмму, а не на сам список. В этом учебнике мы покажем, как преобразовать данные списка SharePoint в отчет Power BI.

Посмотрите это пятиминутное учебное видео или прокрутите страницу вниз, чтобы получить пошаговые инструкции.

<iframe width="400" height="450" src="https://www.youtube.com/embed/OZO3x2NF8Ak" frameborder="0" allowfullscreen></iframe>

## <a name="part-1-connect-to-your-sharepoint-list"></a>Часть 1. Подключение к списку SharePoint

1. Если у вас еще нет Power BI Desktop, скачайте и установите это приложений [отсюда](https://powerbi.microsoft.com/desktop/).
2. Откройте Power BI Desktop и в ленте на вкладке "Главная" выберите **Получить данные** > **Дополнительно**.
3. Выберите **Веб-службы**, а затем выберите **Список SharePoint Online**.  

    <img src="media/desktop-sharepoint-online-list/desktop-sharepoint-online-list-getdata.png" alt="Screenshot shows the Get Data dialog box with Online Services selected." width="350"/>

4. Нажмите кнопку **Подключиться**.
4. Найдите адрес (также называемый URL-адресом) сайта SharePoint Online, содержащего ваш список.  На странице SharePoint Online обычно можно получить адрес сайта, выбрав **Главная** в области навигации или нажав на значок для сайта вверху и скопировав адрес из адресной строки веб-браузера.

   Посмотрите видео по этому шагу:
   <iframe width="400" height="300" src="https://www.youtube.com/embed/OZO3x2NF8Ak?start=48&end=90" frameborder="0" allowfullscreen></iframe>

5. В Power BI Desktop вставьте адрес в поле **URL-адрес сайта** в открытом диалоговом окне.

6. Возможно, появится экран доступа к SharePoint, как показано на рисунке ниже.  Если вы не видите его, перейдите к шагу 10.  Если экран отображается, выберите **Учетная запись Майкрософт** в левой части страницы.

    <img src="media/desktop-sharepoint-online-list/desktop-sharepoint-online-list-auth1.png" alt="choose Microsoft account" width="500"/>

7. Выберите **Войти** и введите имя пользователя и пароль, которые вы используете для входа в Microsoft 365.

    <img src="media/desktop-sharepoint-online-list/desktop-sharepoint-online-list-auth2.png" alt="sign in" width="500"/>

8. Выполнив вход, выберите **Подключиться**.

9. В левой части навигатора установите флажок рядом со списком SharePoint, к которому необходимо подключиться.

    <img src="media/desktop-sharepoint-online-list/desktop-sharepoint-online-list-select-list.png" alt="Screenshot shows the Navigator page with BudgetRequests selected." width="450"/>

10. Выберите **Загрузить**.  Power BI загрузит данные списка в новый отчет.

## <a name="part-2-create-a-report"></a>Часть 2. Создание отчета

1. В левой части экрана щелкните значок **Данные** и проверьте, что данные вашего списка SharePoint загружены.

2. Убедитесь, что для числовых столбцов списка в **области "Поля"** справа отображается значок суммы (буква "сигма").  Если он отсутствует, щелкните заголовок столбца в представлении таблицы, перейдите на вкладку **Моделирование** и измените **Тип данных** на **Десятичное число** или **Целое число** в зависимости от данных.  При появлении запроса на подтверждение изменений выберите **Да**.  Если ваши числа имеют особый формат (например, валюта), можно также задать его в поле **Формат**.

   Посмотрите видео по этому шагу:
   <iframe width="400" height="300" src="https://www.youtube.com/embed/OZO3x2NF8Ak?start=147&end=204" frameborder="0" allowfullscreen></iframe>

3. Щелкните значок **Отчет** слева.
4. Выберите столбцы, которые необходимо визуализировать, установив флажки для этих столбцов в области **Поля** справа.

   Посмотрите видео по этому шагу:
   <iframe width="400" height="300" src="https://www.youtube.com/embed/OZO3x2NF8Ak?start=215&end=252" frameborder="0" allowfullscreen></iframe>

5. При необходимости измените тип визуального элемента.
6. Вы можете создать в одном отчете множество визуализаций. Для этого отмените выбор существующего визуального элемента и установите флажки для других столбцов в области **Поля**.
7. Нажмите **Сохранить**, чтобы сохранить отчет.
