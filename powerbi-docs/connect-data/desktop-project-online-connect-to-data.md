---
title: 'Project Online: подключение к данным через Power BI Desktop'
description: 'Project Online: подключение к данным через Power BI Desktop'
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 04/01/2020
LocalizationGroup: Connect to data
ms.openlocfilehash: b6078a2122a77682af328f9935b23da0d0d0d945
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96404946"
---
# <a name="connect-to-project-online-data-through-power-bi-desktop"></a>Подключение к данным Project Online через Power BI Desktop
К данным в Project Online можно подключиться с помощью Power BI Desktop.

## <a name="step-1-download-power-bi-desktop"></a>Шаг 1. Скачивание Power BI Desktop
1. [Скачайте Power BI Desktop](https://go.microsoft.com/fwlink/?LinkID=521662) и запустите программу установки, чтобы установить **Power BI Desktop** на свой компьютер.

## <a name="step-2-connect-to-project-online-with-odata"></a>Шаг 2. Подключение к Project Online с помощью OData
1. Откройте **Power BI Desktop**.
2. На *экране приветствия* выберите **Получить данные**.
3. Выберите **канал OData** и щелкните **Подключить**.
4. Введите адрес для канала OData в поле URL-адреса и нажмите кнопку ОК.
   
   Если адрес сайта вашего веб-приложения Project имеет формат *https://\<tenantname\>.sharepoint.com/sites/pwa*, адрес канала OData должен быть в формате *https://\<tenantname\>.sharepoint.com/sites/pwa/\_api/Projectdata*.
   
   В нашем примере используется

    `https://contoso.sharepoint.com/sites/pwa/default.aspx`

5. Power BI Desktop предложит вам пройти проверку подлинности рабочей или учебной учетной записи. Выберите учетную запись организации и введите свои учетные данные.
   
   ![Снимок экрана: Power BI Desktop с запросом учетных данных для подключения](media/desktop-project-online-connect-to-data/image.png)

Учетная запись, используемая для подключения к каналу OData, должна иметь на сайте Project Web App уровень доступа не ниже Portfolio Viewer (Просмотр портфеля проектов). 

Здесь можно выбрать таблицы, к которым нужно подключиться, и создать запрос.  Хотите узнать, как приступить к работе?  В следующей записи блога показано, как создавать диаграммы сгорания задач на основе данных Project Online.  В записи блога для подключения к Project Online используется Power Query, но то же самое относится и к Power BI Desktop.

[Создание диаграмм сгорания задач для Project с помощью Power Pivot и Power Query](https://blogs.office.com/2014/03/24/creating-burndown-charts-for-project-using-power-pivot-and-power-query/)

