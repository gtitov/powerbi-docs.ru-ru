---
title: Подключение к LinkedIn Sales Navigator в Power BI Desktop
description: Простое и удобное подключение к данным из LinkedIn и их использование с помощью приложения Power BI Desktop
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 01/04/2021
LocalizationGroup: Connect to data
ms.openlocfilehash: 6121e2050fdb4d9c94732508dc96c8719598fec3
ms.sourcegitcommit: 932f6856849c39e34229dc9a49fb9379c56a888a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97926984"
---
# <a name="connect-to-linkedin-sales-navigator-in-power-bi-desktop"></a>Подключение к LinkedIn Sales Navigator в Power BI Desktop

В **Power BI Desktop** можно подключиться к **LinkedIn Sales Navigator**, чтобы находить и создавать связи так же, как любой другой источник данных в Power BI Desktop, а также создавать готовые отчеты о ходе выполнения.

![Вкладка "LinkedIn Sales Navigator Usage" (Использование LinkedIn Sales Navigator)](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-01.png)


Чтобы подключиться к данным LinkedIn с помощью **LinkedIn Sales Navigator**, необходимо иметь план LinkedIn Sales Navigator Enterprise, а также быть администратором или пользователем отчетности с контрактом Sales Navigator.

В следующем видео представлен краткий обзор и учебник по использованию приложения шаблона **LinkedIn Sales Navigator**, которое подробно описано [далее в этой статье](#using-the-linkedin-sales-navigator-template-app). 

> [!VIDEO https://www.youtube.com/embed/ZqhmaiORLw0]

## <a name="connect-to-linkedin-sales-navigator"></a>Подключение к LinkedIn Sales Navigator

Чтобы подключиться к данным **LinkedIn Sales Navigator**, выберите **Get Data** (Получить данные) на ленте **Home** (Главная) в Power BI Desktop. Выберите **Online Services** (Веб-службы) среди категорий слева, а затем прокрутите экран до **LinkedIn Sales Navigator (Beta)** .

![Получение данных в Power BI Desktop](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-02.png)

Вам будет предложено подключиться к сторонним соединителям, которые все еще разрабатываются. 

![Предупреждение о службе сторонних производителей](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-03.png)

Нажав кнопку **Continue** (Далее), укажите нужные данные.

![Запрос о предоставляемой информации](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-04.png)


В появившемся окне **LinkedIn Sales Navigator** в первом раскрывающемся списке выберите данные, которые требуется вернуть: *All contacts* (Все контакты) или *Selected contacts* (Выбранные контакты). Затем можно указать начальную и окончательную даты, чтобы ограничить количество получаемых данных определенным временным окном.

После того, как данные предоставлены, Power BI Desktop подключается к данным, связанным с контрактом LinkedIn Sales Navigator. Используйте тот же адрес электронной почты, который используется для входа в LinkedIn Sales Navigator на веб-сайте. 

![Вход в LinkedIn](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-05.png)

При успешном подключении вам будет предложено выбрать данные из контракта LinkedIn Sales Navigator в окне **Navigator**.

![Выбор данных с помощью Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-09.png)

Вы можете создавать любые отчеты с данными из LinkedIn Sales Navigator. Чтобы упростить эту задачу, также можно использовать загружаемый PBIX-файл LinkedIn Sales Navigator с уже предоставленными демонстрационными данными, чтобы вы могли ознакомиться с данными и отчетами без необходимости начинать с нуля.

PBIX-файл можно загрузить по следующему адресу:
* [PBIX-файл для LinkedIn Sales Navigator](service-template-apps-samples.md)

Помимо PBIX-файла, в LinkedIn Sales Navigator также имеется шаблонное приложение, которое можно загрузить и использовать. Подробно шаблонное приложение описывается в следующем разделе.


## <a name="using-the-linkedin-sales-navigator-template-app"></a>Использование шаблонного приложения LinkedIn Sales Navigator

Чтобы упростить использование **LinkedIn Sales Navigator**, можно использовать [шаблонное приложение](service-template-apps-overview.md), которое автоматически создает готовый отчет из данных LinkedIn Sales Navigator.

![Шаблонное приложение для LinkedIn Sales Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-10.png)

После загрузки приложения можно выбрать, следует ли подключаться к данным или изучать приложение с помощью демонстрационных данных. После изучения образца данных вы всегда можете вернуться и подключиться к собственным данным LinkedIn Sales Navigator. 

![Подключение к данным для LinkedIn Sales Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-11.png)



Вы можете получить шаблонное приложение **LinkedIn Sales Navigator** по следующей ссылке:
* [Шаблонное приложение LinkedIn Sales Navigator](https://appsource.microsoft.com/en-us/product/power-bi/pbi-contentpacks.linkedin_navigator)

Шаблонное приложение содержит четыре вкладки для анализа и совместного использования информации:

* Использование
* Поиск
* InMail
* SSI

На вкладке **Usage** (Использование) отображаются общие данные LinkedIn Sales Navigator.

![На вкладке Usage (Использование) в LinkedIn Sales Navigator отображаются общие данные LinkedIn Sales Navigator.](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-12.png)

Вкладка **Search** (Поиск) позволяет углубленно анализировать результаты поиска:

![Вкладка Search (Поиск) в LinkedIn Sales Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-13.png)

На вкладке **InMail** предоставлены аналитические сведения об использовании сообщений InMail, в том числе о количестве отправленных сообщений InMail, количестве принятых и другие полезные сведения:

![Вкладка InMail в LinkedIn Sales Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-14.png)

На вкладке **SSI** содержатся дополнительные сведения об индексе социального сбыта (SSI):

![Вкладка SSI в LinkedIn Sales Navigator](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-15.png)

Чтобы перейти от образца данных к собственным данным, выберите команду **edit app** (Изменить приложение) в правом верхнем углу (значок карандаша), а затем на появившемся экране выберите команду **Connect your data** (Подключить свои данные).

![Подключение собственных данных](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-16.png)

Здесь можно подключить собственные данные, выбрав количество дней для загрузки данных. Данные можно загрузить не более чем за 365 дней. Вам потребуется выполнить вход, используя тот же адрес электронной почты, который используется для входа в LinkedIn Sales Navigator через веб-сайт. 

![Вход](media/desktop-connect-linkedin-sales-navigator/linkedin-sales-navigator-17.png)

Затем шаблонное приложение обновляет данные в приложении вашими данными. Кроме этого, вы можете настроить обновление по расписанию, чтобы в приложение с указанной частотой обновления попадали текущие данные. 

После обновления данных можно увидеть, как приложение заполняется вашими собственными данными.

## <a name="getting-help"></a>Получение справки

Если при подключении к данным возникают проблемы, вы можете обратиться в службу поддержки LinkedIn Sales Navigator по адресу https://www.linkedin.com/help/sales-navigator. 

## <a name="next-steps"></a>Дальнейшие действия
В Power BI Desktop можно подключаться к данным самых разных видов. Дополнительные сведения об источниках данных см. в перечисленных ниже статьях.

* [Что такое Power BI Desktop?](../fundamentals/desktop-what-is-desktop.md)
* [Источники данных в Power BI Desktop](desktop-data-sources.md)
* [Формирование и объединение данных с Power BI Desktop](desktop-shape-and-combine-data.md)
* [Подключение к данным Excel в Power BI Desktop](desktop-connect-excel.md)   
* [Ввод данных непосредственно в Power BI Desktop](desktop-enter-data-directly-into-desktop.md)   
