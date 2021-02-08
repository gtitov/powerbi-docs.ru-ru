---
title: Создание отчета Power BI для Сервера отчетов Power BI
description: Узнайте, как создать отчет Power BI для сервера отчетов Power BI за несколько простых шагов.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 07/24/2020
ms.openlocfilehash: e3c4d97ba6d5ba43e05feecca6a1f0d0c27c89aa
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99043810"
---
# <a name="create-a-power-bi-report-for-power-bi-report-server"></a>Создание отчета Power BI для Сервера отчетов Power BI
Отчеты Power BI можно хранить и администрировать локально на веб-портале Сервера отчетов Power BI так же, как и в облачной службе Power BI (https://powerbi.com). Вы можете создавать и редактировать отчеты в приложении Power BI Desktop, а затем публиковать их на веб-портале. Затем можно сообщить читателям в вашей организации о том, что эти отчеты можно просматривать в браузере или мобильном приложении Power BI на мобильных устройствах.

![Отчет Power BI на веб-портале](media/quickstart-create-powerbi-report/report-server-powerbi-report.png)

Ниже описаны четыре шага, с помощью которых можно приступить к работе.

## <a name="step-1-install-power-bi-desktop-for-power-bi-report-server"></a>Шаг 1. Установка Power BI Desktop для Сервера отчетов Power BI

Если вы уже создавали отчеты Power BI в приложении Power BI Desktop, то вы практически готовы создавать отчеты Power BI для сервера отчетов Power BI. Рекомендуется установить версию Power BI Desktop для Сервера отчетов Power BI, так как это обеспечит постоянную синхронизацию сервера с приложением. Обе версии Power BI Desktop можно установить на одном компьютере.

1. На веб-портале сервера отчетов последовательно выберите **Загрузка** > **Power BI Desktop**.

    ![Скачивание Power BI Desktop из веб-портала](media/install-powerbi-desktop/report-server-download-web-portal.png)

    Либо перейдите на домашнюю страницу [Сервера отчетов Power BI](https://powerbi.microsoft.com/report-server/) и выберите **Расширенные параметры загрузки**.

2. На странице Центра загрузки нажмите кнопку **Скачать**.

3. В зависимости от компьютера выберите файл:

    - **PBIDesktopRS.msi** (32-разрядная версия);

    - **PBIDesktopRS_x64.msi** (64-разрядная версия).

4. Скачав установщик, запустите мастер установки Power BI Desktop.

2. На завершающем этапе процесса установки выберите параметр **Start Power BI Desktop now** (Запустить Power BI Desktop).
   
    После автоматического запуска приложения вы будете готовы к работе. Если в строке заголовка отображается **Power BI Desktop (январь 2021 г.)** , вы установили правильную версию.

    ![Power BI Desktop (январь 2021 г.)](media/install-powerbi-desktop/power-bi-report-server-desktop.png)

3. Если вы не знакомы с Power BI Desktop, просмотрите видеоролики на экране приветствия.
   
    ![Начальный экран Power BI Desktop](media/quickstart-create-powerbi-report/report-server-powerbi-desktop-start.png)

## <a name="step-2-select-a-data-source"></a>Шаг 2. Выбор источника данных
Вы можете подключаться к разным типам источников данных. Узнайте больше о [подключении к источникам данных](connect-data-sources.md).

1. На экране приветствия выберите **Get Data** (Получить данные).
   
    На вкладке **Home** (Главная) выберите пункт **Get Data** (Получить данные).
2. Выберите источник данных (в этом примере **Analysis Services**).
   
    ![Выбор источника данных](media/quickstart-create-powerbi-report/power-bi-report-server-get-data-ssas.png)
3. Заполните поле **Server** (Сервер) и при необходимости поле **Database** (База данных). Убедитесь, что установлен флажок **Connect live** (Подключение в реальном времени) и нажмите кнопку **ОK**.
   
    ![Имя сервера](media/quickstart-create-powerbi-report/report-server-ssas-server-name.png)
4. Выберите сервер отчетов, на котором вы будете хранить отчеты.
   
    ![Выбор сервера отчетов](media/quickstart-create-powerbi-report/report-server-select-server.png)

## <a name="step-3-design-your-report"></a>Шаг 3. Создание отчета
Здесь начинается самое интересное: нужно создать визуальные элементы, иллюстрирующие ваши данные.

Например, можно создать воронкообразную диаграмму на основе значений, отображающих годовой доход пользователей и групп.

![Создание отчета](media/quickstart-create-powerbi-report/report-server-create-funnel.png)

1. В разделе **Visualizations** (Визуализации) выберите элемент **Funnel chart** (Воронкообразная диаграмма).
2. Перетащите поле для подсчета в область **Values** (Значения). Если это не числовое поле, Power BI Desktop автоматически установит для него значение *Count of* (Количество).
3. Перетащите поле в группу в область **Group** (Группа).

См. дополнительные сведения о [создании отчетов Power BI](../create-reports/desktop-report-view.md).

## <a name="step-4-save-your-report-to-the-report-server"></a>Шаг 4. Сохранение отчета на сервере отчетов
Когда отчет будет готов, вы сможете сохранить его на сервере отчетов Power BI, который вы выбрали на шаге 2.

1. В меню **Файл** выберите пункт **Сохранить как** > **Сервер отчетов Power BI**.
   
    ![Сохранение на сервере отчетов](media/quickstart-create-powerbi-report/report-server-save-as-powerbi-report-server.png)
2. Теперь вы можете просмотреть отчет на веб-портале.
   
    ![Просмотр отчета в веб-портале](media/quickstart-create-powerbi-report/report-server-powerbi-report.png)
    
> [!NOTE]
> Если вы захотите изменить отчет в будущем, на рабочем столе всегда будут представлены данные, кэшированные на момент создания отчета.  Чтобы работать с актуальными данными при редактировании отчета, необходимо обновить данные в приложении Power BI Desktop.

## <a name="next-steps"></a>Дальнейшие действия
### <a name="power-bi-desktop"></a>Power BI Desktop
Существует много отличных ресурсов для создания отчетов в Power BI Desktop. Советуем начать с этих материалов:

* [Начало работы с Power BI Desktop](../fundamentals/desktop-getting-started.md)
* Интерактивное обучение [Изучение Power BI Desktop](/learn/modules/get-data-power-bi/2-getting-started-power-bi-desktop)

### <a name="power-bi-report-server"></a>Cервере отчетов Power BI
* [Установка Power BI Desktop для Сервера отчетов Power BI](install-powerbi-desktop.md)  
* [Что такое Сервер отчетов Power BI?](get-started.md)  

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
