---
title: Просмотр локальных отчетов и ключевых показателей эффективности в мобильных приложениях Power BI
description: Мобильные приложения Power BI обеспечивают динамический мобильный доступ с поддержкой сенсорного ввода к локальным бизнес-данным в службах SQL Server Reporting Services и на сервере отчетов Power BI.
author: paulinbar
ms.author: painbar
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-mobile
ms.topic: how-to
ms.date: 12/05/2019
ms.openlocfilehash: 18ad1be61202ddf189da064a833fddf6d793a2ba
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96413410"
---
# <a name="view-on-premises-report-server-reports-and-kpis-in-the-power-bi-mobile-apps"></a>Просмотр локальных отчетов на сервере отчетов и ключевых показателей эффективности в мобильных приложениях Power BI

Мобильные приложения Power BI обеспечивают динамический мобильный доступ с поддержкой сенсорного ввода к локальным бизнес-данным на сервере отчетов Power BI и в службах SQL Server 2016 Reporting Services (SSRS).

Область применения:

| ![iPhone](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/iphone-logo-50-px.png) | ![iPad](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/ipad-logo-50-px.png) | ![Телефон Android](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/android-phone-logo-50-px.png) | ![Планшет Android](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/android-tablet-logo-50-px.png) |
|:--- |:--- |:--- |:--- |
| iPhones |iPad |Телефоны под управлением Android |Планшеты Android |


![Домашняя страница сервера отчетов в мобильных приложениях](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-ipad-pbi-report-server-home.png)

## <a name="first-things-first"></a>Начните с главного
**Мобильные приложения расположены не там, где создается содержимое Power BI, а там, где вы просматриваете его.**

* Вы и ваши коллеги можете [создавать отчеты Power BI с помощью Power BI Desktop, а затем публиковать их на веб-портале сервера отчетов Power BI](../../report-server/quickstart-create-powerbi-report.md). 
* Создавайте [ключевые показатели эффективности непосредственно на веб-портале](/sql/reporting-services/working-with-kpis-in-reporting-services), включайте их в папки и добавляйте в избранное для быстрого поиска. 
* [Создайте мобильные отчеты Reporting Services](/sql/reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher) при помощи издателя мобильных отчетов для SQL Server 2016 Enterprise Edition и опубликуйте их на [веб-портале служб Reporting Services](/sql/reporting-services/web-portal-ssrs-native-mode).  

Затем в мобильных приложениях Power BI можно подключиться к пяти серверам отчетов, чтобы отобразить в папках или списке избранных элементов отчеты Power BI и ключевые показатели эффективности. 

## <a name="explore-samples-in-the-mobile-apps-without-a-server-connection"></a>Изучение примеров в мобильных приложениях без подключения к серверу
Ознакомиться с ключевыми показателями эффективности и функциями мобильных отчетов Reporting Services можно даже без доступа к веб-порталу служб Reporting Services. 

1. Коснитесь изображения профиля в левом верхнем углу, а затем элемента **Настройки** на появившейся панели учетных записей.

2. На открывшейся странице настроек выберите **Примеры для Reporting Services**, а затем просмотрите и изучите примеры ключевых показателей эффективности и мобильных отчетов.
   
   ![Примеры для Reporting Services](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-iphone-ssrs-samples.png)

## <a name="connect-to-an-on-premises-report-server"></a>Подключение к локальному серверу отчетов
Вы можете просматривать локальные отчеты Power BI, мобильные отчеты Reporting Services и ключевые показатели эффективности в мобильных приложениях Power BI. 

1. Откройте приложение Power BI на своем мобильном устройстве.
2. Если вы еще не вошли в Power BI, выберите **Сервер отчетов**.
   
   ![Вход на сервер отчетов](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-connect-to-rs-login.png)
   
   Если вы уже вошли в приложение Power BI, коснитесь изображения профиля в левом верхнем углу, а затем элемента **Настройки** на появившейся панели учетных записей.
3. На открывшейся странице настроек выберите **Подключение к серверу**.
   
    ![Подключение к серверу](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-android-server-sign-in.png)

    Мобильному приложению необходимо обеспечить доступ к серверу. Это можно сделать несколькими способами:
     * Проще всего использовать ту же сеть или VPN.
     * Можно использовать прокси веб-приложения для подключения вне организации. См. дополнительные сведения о [подключении к Reporting Services с помощью OAuth](mobile-oauth-ssrs.md).
     * Откройте подключение (порт) в брандмауэре.

4. Укажите адрес сервера и при желании присвойте серверу понятное имя. Используйте следующий формат для адреса сервера:
   
     `https://<servername>/reports`
   
     ИЛИ
   
     `https://<servername>/reports`
   
   В начале строки подключения укажите префикс **http** или **https**.
   
    ![Диалоговое окно "Подключение к серверу"](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-ios-connect-to-server-dialog.png)
5. Введя адрес сервера и при необходимости понятное имя, выберите **Подключиться**, а затем при появлении запроса укажите свои имя пользователя и пароль.
6. Сервер появится в области "Учетные записи". В данном примере его имя — Work server.
   
   ![Сервер отчетов в области навигации](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-iphone-left-nav-report-server.png)

## <a name="connect-to-an-on-premises-report-server-in-ios-or-android"></a>Подключение к локальному серверу отчетов в iOS или Android

Если вы работаете с Power BI в мобильном приложении для iOS или Android, возможно, ИТ-администратор определил политику настройки приложения. В этом случае процедура подключения к серверу отчетов упрощается и вам требуется предоставлять меньше сведений. 

1. Появляется сообщение о том, что для мобильного приложения настроен доступ к серверу отчетов. Коснитесь элемента **Вход**.

    ![Вход на сервер отчетов](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-config-server-sign-in.png)

2.  На странице **Подключение к серверу** сведения о сервере отчетов уже заполнены. Нажмите **Подключиться**.

    ![Заполненные сведения о сервере отчетов](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-ios-remote-configure-connect-server.png)

3. Введите пароль, чтобы пройти проверку подлинности, а затем коснитесь элемента **Вход**. 

    ![Снимок экрана: поле для ввода пароля и кнопка входа.](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-config-server-address.png)

Теперь вы можете просматривать ключевые показатели эффективности и отчеты Power BI, хранящиеся на сервере отчетов, и взаимодействовать с ними.

## <a name="view-power-bi-reports-and-kpis-in-the-power-bi-app"></a>Просмотр отчетов Power BI и ключевых показателей эффективности в приложении Power BI
Отчеты Power BI, мобильные отчеты Reporting Services и ключевые показатели эффективности отображаются в тех же папках, в которых они расположены на веб-портале служб Reporting Services. 

* Коснитесь отчета Power BI ![Значок отчета Power BI](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-rs-mobile-report-icon.png). Он открывается в альбомной ориентации и доступен для работы в приложении Power BI.

    > [!NOTE]
  > Детализация углублением и обобщением в настоящий момент не включена в отчетах Power BI на сервере отчетов Power BI.
  
    ![Отчет Power BI](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-iphone-report-server-report.png)
* В Power BI Desktop владельцы отчета могут [оптимизировать отчет](../../create-reports/desktop-create-phone-report.md) для мобильных приложений Power BI. На мобильных телефонах в оптимизированных отчетах есть специальный значок ![Оптимизированный значок отчета Power BI](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-rs-mobile-optimized-icon.png) и макет.
  
    ![Отчет Power BI, оптимизированный для мобильных устройств](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-rs-mobile-optimized-report.png)
* Выберите ключевой показатель эффективности, чтобы просмотреть его в режиме фокуса.
  
    ![Ключевой показатель эффективности в режиме фокусировки](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/pbi_ipad_ssmrp_tile.png)

## <a name="view-your-favorite-kpis-and-reports"></a>Просмотр избранных ключевых показателей эффективности и отчетов
На веб-портале ключевые показатели эффективности и отчеты можно отметить как избранные. Так вы сможете просматривать эти данные на мобильном устройстве в одной папке вместе с избранными панелями мониторинга Power BI.

* На панели навигации выберите **Избранное**.
  
   !["Избранное" в области навигации](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-ipad-faves-pbi-report-server-update.png)
  
   Ваши избранные ключевые показатели эффективности и отчеты находятся на этой странице веб-портала вместе с панелями мониторинга Power BI в службе Power BI:
  
   ![Отчеты и панель мониторинга Power BI на странице "Избранное"](./media/mobile-app-ssrs-kpis-mobile-on-premises-reports/power-bi-ipad-favorites.png)

## <a name="remove-a-connection-to-a-report-server"></a>Удаление подключения к серверу отчетов
1. Откройте область учетных записей и коснитесь элемента **Настройки**.
2. Выберите имя сервера, к которому необходимо подключиться.
3. Коснитесь пункта **Удалить сервер**.

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое Power BI?](../../fundamentals/power-bi-overview.md)  
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)