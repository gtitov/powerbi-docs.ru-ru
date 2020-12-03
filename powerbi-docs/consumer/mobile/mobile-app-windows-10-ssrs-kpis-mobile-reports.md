---
title: Просмотр локальных отчетов и КПЭ в приложении Power BI для Windows
description: Мобильное приложение Power BI для Windows 10 обеспечивает доступ в режиме реального времени к важнейшей бизнес-информации с сенсорного экрана.
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-mobile
ms.topic: how-to
ms.date: 05/19/2020
ms.openlocfilehash: eb6b86b2810609c0ad795190afc91c40677f5e70
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96413318"
---
# <a name="view-on-premises-reports-and-kpis-in-the-power-bi-windows-app"></a>Просмотр локальных отчетов и КПЭ в приложении Power BI для Windows
Приложение Power BI для Windows 10 обеспечивает доступ в режиме реального времени к важнейшей бизнес-информации в Reporting Services SQL Server 2016. 

![Мобильные отчеты Reporting Services](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report.png)

## <a name="first-things-first"></a>Начните с главного
Вы можете [создавать мобильные отчеты Reporting Services](/sql/reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher) при помощи издателя мобильных отчетов для SQL Server 2016 Enterprise Edition и публиковать их на [веб-портале служб Reporting Services](/sql/reporting-services/web-portal-ssrs-native-mode). Создавайте ключевые показатели эффективности прямо на веб-портале. Объединяйте их в папки и добавляйте в избранное, чтобы легко находить. 

В приложении Power BI для Windows 10 КПЭ, мобильные отчеты и отчеты Power BI отображаются в папках или в списке избранного. 

> [!NOTE]
> Ваше устройство должно работать под управлением Windows 10. Лучше всего приложение работает на устройствах, где доступно не менее 1 ГБ ОЗУ и 8 ГБ внутренней памяти.

>[!NOTE]
>Поддержка мобильного приложения Power BI для **телефонов под управлением Windows 10 Mobile** будет прекращена 16 марта 2021 г. [Дополнительные сведения](/legal/powerbi/powerbi-mobile/power-bi-mobile-app-end-of-support-for-windows-phones)

## <a name="explore-samples-without-a-sql-server-2016-reporting-services-server"></a>Изучение примеров без сервера SQL Server 2016 Reporting Services
Ознакомиться с функциями мобильных отчетов Reporting Services можно даже в отсутствие доступа к веб-порталу Reporting Services.

1. Откройте приложение Power BI на устройстве Windows 10.
2. Коснитесь кнопки глобальной навигации ![Кнопка глобальной навигации](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/powerbi_windows10_options_icon.png) в левом верхнем углу.
3. Коснитесь значка **Параметры**![Значок "Параметры"](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-settings-icon.png), щелкните правой кнопкой мыши или нажмите и удерживайте элемент **Подключение к серверу**, а затем выберите команду **Просмотреть примеры**.
   
   ![Просмотр примеров SSRS](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-win10-connect-ssrs-samples.png)
4. Откройте папку отчетов по розничным продажам или отчетов по сбыту и изучите ключевые показатели эффективности и мобильные отчеты.
   
   ![Примеры ключевых показателей эффективности и мобильных отчетов](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-win10-ssrs-sample-kpis.png)

Просмотрите примеры и изучите ключевые показатели эффективности и мобильные отчеты.

## <a name="connect-to-a-reporting-services-report-server"></a>Подключение к серверу отчетов Reporting Services
1. В нижней части области навигации выберите **Параметры** ![Значок параметров](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-settings-icon.png).
2. Выберите **Подключение к серверу**.
3. Введите адрес сервера, имя пользователя и пароль. Используйте следующий формат для адреса сервера:
   
     `https://<servername>/reports` ИЛИ `https://<servername>/reports`
   
   > [!NOTE]
   > В начале строки подключения укажите префикс **http** или **https**.
   > 
   > 
   
    По желанию коснитесь пункта **Дополнительный параметр**, чтобы присвоить имя серверу.
4. Коснитесь значка галочки для подключения. 
   
   Новый сервер появится в области навигации.
   
   ![Сервер в области навигации](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report-server.png)
   
   >[!TIP]
   >С помощью кнопки глобальной навигации ![Кнопка глобальной навигации](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/powerbi_windows10_options_icon.png) вы можете в любой момент переключиться между мобильными отчетами Reporting Services и панелями мониторинга в службе Power BI. 
   > 

   >[!NOTE]
   >Серверы отчетов, настроенные с использованием настраиваемых портов, не поддерживаются и недоступны из приложения Power BI для Windows. 

## <a name="view-reporting-services-kpis-and-mobile-reports-in-the-power-bi-app"></a>Просмотр ключевых показателей эффективности и мобильных отчетов Reporting Services в приложении Power BI
Отчеты Power BI (предварительная версия), КПЭ и мобильные отчеты Reporting Services отображаются в тех же папках, в которых они расположены на веб-портале служб Reporting Services.

![Папки отчетов](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report-folders.png)

* Выберите ключевой показатель эффективности, чтобы просмотреть его в режиме фокуса.
  
    ![Ключевой показатель эффективности в режиме фокусировки](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report-kpis.png)
* Выберите мобильный отчет, чтобы открыть его в приложении Power BI, где с ним можно взаимодействовать.
  
    ![Мобильный отчет Reporting Services](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report.png)

## <a name="view-your-favorite-kpis-and-reports"></a>Просмотр избранных ключевых показателей эффективности и отчетов
На веб-портале Reporting Services КПЭ, мобильные отчеты и отчеты Power BI можно отметить как избранные и удобно просматривать на устройстве с Windows 10 в одной папке вместе с избранными панелями мониторинга и отчетами Power BI.

* Выберите **Избранное**.
  
   ![Значок "Избранное"](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-ssrs-mobile-report-favorite-menu.png)
  
   Все, чтобы вы добавили в избранное на веб-портале, отобразиться на этой странице.
  
Дополнительные сведения об избранном в мобильных приложениях Power BI см. [здесь](mobile-apps-favorites.md).

## <a name="remove-a-connection-to-a-report-server"></a>Удаление подключения к серверу отчетов
В приложении для iPhone в каждый момент времени может быть установлено подключение только к одному серверу отчетов. Чтобы подключиться к другому серверу, необходимо разорвать соединение с текущим.

1. В нижней части области навигации выберите **Параметры** ![Значок параметров](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-settings-icon.png).
2. Нажмите и удерживайте имя сервера, с которым хотите разорвать соединение.
3. Коснитесь пункта **Удалить сервер**.
   
    ![Удалить сервер](media/mobile-app-windows-10-ssrs-kpis-mobile-reports/power-bi-windows-10-ssrs-remove-server-menu.png)

## <a name="create-reporting-services-mobile-reports-and-kpis"></a>Создание мобильных отчетов и ключевых показателей эффективности Reporting Services
Ключевые показателей эффективности и мобильные отчеты Reporting Services не создаются в приложении Power BI. Для их создания используются приложение SQL Server Mobile Report Publisher и веб-портал служб SQL Server 2016 Reporting Services.

* Вы можете [создавать собственные мобильные отчеты](/sql/reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher) и публиковать их на веб-портале Reporting Services.
* Создание [ключевых показателей эффективности на веб-портале Reporting Services](/sql/reporting-services/working-with-kpis-in-reporting-services)

## <a name="next-steps"></a>Дальнейшие действия
* [Начало работы с мобильным приложением Power BI для Windows 10](mobile-windows-10-phone-app-get-started.md)  
* [Что такое Power BI?](../../fundamentals/power-bi-overview.md)  
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)