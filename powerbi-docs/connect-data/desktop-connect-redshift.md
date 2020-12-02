---
title: Подключение к базе данных Amazon Redshift в Power BI Desktop
description: Простое и удобное подключение к базе данных Amazon Redshift в Power BI Desktop и ее использование
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 05/08/2019
LocalizationGroup: Connect to data
ms.openlocfilehash: 60bf73e4500785c766a485fffc92a25bd8f2c852
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96411363"
---
# <a name="connect-to-an-amazon-redshift-database-in-power-bi-desktop"></a>Подключение к базе данных Amazon Redshift в Power BI Desktop
В **Power BI Desktop** вы можете подключиться к базе данных **Amazon Redshift** и использовать ее так же, как и любой другой источник данных в Power BI Desktop.

## <a name="connect-to-an-amazon-redshift-database"></a>Подключение к базе данных Amazon Redshift
Для подключения к базе данных **Amazon Redshift** на вкладке **Главная** на ленте в Power BI Desktop выберите **Получение данных**. Слева выберите категорию **База данных**. Отобразится пункт **Amazon Redshift**.

![Снимок экрана: диалоговое окно "Получить данные", показывающее выбор базы данных Amazon Redshift](media/desktop-connect-redshift/connect_redshift_3.png)

В открывшемся окне **Amazon Redshift** введите или вставьте имя сервера и базы данных **Amazon Redshift** в соответствующие поля. В качестве части поля *Сервер* пользователи могут указать порт в следующем формате: *URL-адрес_сервера:порт*.

![Снимок экрана: диалоговое окно Amazon Redshift, показывающее поля сервера и базы данных](media/desktop-connect-redshift/connect_redshift_4.png)

При появлении запроса укажите имя пользователя и пароль. Во избежание ошибок следует использовать имя сервера, которое в точности соответствует SSL-сертификату. 

![Снимок экрана: запрос учетных данных Amazon Redshift с полями "Имя пользователя" и "Пароль"](media/desktop-connect-redshift/connect_redshift_5.png)

После успешного подключения откроется окно **Навигатор**, содержащее данные, доступные на сервере. Из них вы можете выбрать один или несколько элементов для импорта и использования в **Power BI Desktop**.

![Снимок экрана: диалоговое окно "Навигатор", показывающее доступные данные на сервере](media/desktop-connect-redshift/connect_redshift_6.png)

Выбрав необходимые элементы в окне **Навигатор**, вы можете либо **загрузить**, либо **изменить** данные.

* Если вы решили **загрузить** данные, для этого вам будет предложено использовать режим *импорта* или *DirectQuery*. Для получения дополнительной информации ознакомьтесь с этой [статьей, в которой объясняется, что такое режим DirectQuery](desktop-use-directquery.md).
* Если вы решили **изменить** данные, отобразится **редактор запросов**, с помощью которого можно выполнять любые преобразования данных и применять к ним любые фильтры, многие из которых используются с основной базой данных **Amazon Redshift** (если такая возможность поддерживается).

## <a name="next-steps"></a>Дальнейшие действия
В Power BI Desktop можно подключаться к данным самых разных видов. Дополнительные сведения об источниках данных см. в перечисленных ниже статьях.

* [Что такое Power BI Desktop?](../fundamentals/desktop-what-is-desktop.md)
* [Источники данных в Power BI Desktop](desktop-data-sources.md)
* [Формирование и объединение данных в Power BI Desktop](desktop-shape-and-combine-data.md)
* [Подключение к данным Excel в Power BI Desktop](desktop-connect-excel.md)   
* [Ввод данных непосредственно в Power BI Desktop](desktop-enter-data-directly-into-desktop.md)   
