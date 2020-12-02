---
title: 'Служба сторонних разработчиков: соединитель Google Analytics'
description: 'Служба сторонних разработчиков: Соединитель Google Analytics для Power BI Desktop'
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 05/08/2019
LocalizationGroup: Connect to data
ms.openlocfilehash: 383f69bd371e4b0f635ff2b64c7fae0523c360e4
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96392273"
---
# <a name="use-the-google-analytics-connector-for-power-bi-desktop"></a>Используйте соединитель Google Analytics для Power BI Desktop
> [!NOTE]
> Пакет содержимого и соединитель Google Analytics в Power BI Desktop основаны на API-интерфейсе Core Reporting для Google Analytics. поэтому его функции и доступность могут измениться в дальнейшем.

Подключиться к данным Google Analytics можно при помощи соединителя **Google Analytics**. Чтобы подключиться, выполните следующие действия.

1. В **Power BI Desktop** выберите **Получить данные** на вкладке ленты **Главная**.
2. В окне **Получение данных** в списке категорий в области слева выберите **Веб-службы**.
3. В списке в области справа выберите **Google Analytics** .
4. В нижней части окна выберите **Подключить**.  
   ![Снимок экрана: вкладка "Главная"с лентой "Получение данных" с выбранной службой Google Analytics и кнопкой "Подключить"](media/service-google-analytics-connector/tps_googleanalytics_1.png)

Откроется диалоговое окно, в котором сообщается, что соединитель является сторонней службой, и предупреждается о возможности изменения функций и доступности с течением времени, а также содержатся другие уточнения.  
![Снимок экрана: диалоговое окно подключения с предупреждением о том, что соединитель использует службу стороннего производителя](media/service-google-analytics-connector/tps_googleanalytics_2.png)

После нажатия кнопки **Продолжить** вам будет предложено войти в службу Google Analytics.  
![Снимок экрана: запрос Google Analytics,указывающий на то, что вам нужно войти в систему для подключения](media/service-google-analytics-connector/tps_googleanalytics_3.png)

При вводе учетных данных вам будет предложено выбрать доступ к Power BI в автономном режиме. Таким образом **Power BI Desktop** используется для доступа к данным Google Analytics.  

После принятия предложения в **Power BI Desktop** будет отображено уведомление о том, что вход выполнен.  
![Снимок экрана: запрос Google Analytics,указывающий на то, что вы вошли в систему](media/service-google-analytics-connector/tps_googleanalytics_5.png)

Выберите **Подключить**, после чего данные Google Analytics будут подключены к **Power BI Desktop** и загружены.  
![Снимок экрана: диалоговое окно "Загрузка", в котором указывается, что данные Google Analytics подключены и загружаются](media/service-google-analytics-connector/tps_googleanalytics_6.png)

## <a name="changes-to-the-api"></a>Изменения API-интерфейса
Несмотря на попытки выпуска обновлений в соответствии с любыми изменениями, API-интерфейс может измениться так, что изменения повлияют на результаты формируемых запросов. В некоторых случаях поддержка определенных запросов может отсутствовать. В связи с этой зависимостью мы не гарантируем наличие и правильность результатов запросов при использовании этого соединителя.

Дополнительные сведения об изменениях API-интерфейса Google Analytics см. в [журнале изменений](https://developers.google.com/analytics/devguides/changelog).

