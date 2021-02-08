---
title: Подключение к хранилищу Snowflake Computing в Power BI Desktop
description: 'Хранилище вычислительных ресурсов Snowflake в Power BI Desktop: простое подключение и использование'
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 01/04/2021
LocalizationGroup: Connect to data
ms.openlocfilehash: 377ede2171a721a33aa0b70819ef511d721f2590
ms.sourcegitcommit: f7330dabb9cd8bce90bb2efec3e3273a11578f10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "99494450"
---
# <a name="connect-to-snowflake-in-power-bi-desktop"></a>Подключение к Snowflake в Power BI Desktop
В Power BI Desktop вы можете подключиться к хранилищу вычислительных ресурсов **Snowflake**, чтобы использовать его так же, как и любой другой источник данных в Power BI Desktop. 

## <a name="connect-to-a-snowflake-computing-warehouse"></a>Подключение к хранилищу вычислительных ресурсов Snowflake
Для подключения к хранилищу вычислительных ресурсов **Snowflake** на вкладке **Главная** на ленте в Power BI Desktop выберите **Получить данные**. В области слева выберите категорию **База данных**. Отобразится пункт **Snowflake**.

![Снимок экрана: диалоговое окно "Получить данные", показывающее выбор базы данных Snowflake](media/desktop-connect-snowflake/connect-snowflake-2b.png)

В появившемся окне **Snowflake** введите или вставьте в поле имя хранилища вычислительных ресурсов Snowflake и нажмите кнопку **ОК**. Обратите внимание, что можно **импортировать** данные непосредственно в Power BI или использовать **DirectQuery**. Вы можете ознакомиться с дополнительными сведениями об [использовании DirectQuery](desktop-use-directquery.md). Обратите внимание на то, что единый вход AAD поддерживает только DirectQuery.

![Снимок экрана: диалоговое окно Snowflake с выбранным переключателем "Импорт"](media/desktop-connect-snowflake/connect-snowflake-3.png)

При появлении запроса укажите имя пользователя и пароль.

![Снимок экрана: запрос учетных данных Snowflake с полями "Имя пользователя" и "Пароль"](media/desktop-connect-snowflake/connect-snowflake-4.png)

> [!NOTE]
> Если указаны имя пользователя и пароль для определенного сервера **Snowflake**, Power BI Desktop будет использовать те же учетные данные при последующих попытках подключения. Эти учетные данные можно изменить, последовательно выбрав элементы **Файл > Параметры и настройки > Параметры источника данных**.
> 
> 

Чтобы использовать учетную запись Майкрософт, необходимо настроить интеграцию Snowflake с AAD на стороне Snowflake. Для этого ознакомьтесь с разделом Getting Started (Начало работы) в [документации Snowflake по этой теме](https://docs.snowflake.net/manuals/user-guide/oauth-powerbi.html#power-bi-sso-to-snowflake).

![Тип проверки подлинности учетной записи Майкрософт в соединителе Snowflake.](media/desktop-connect-snowflake/connect-snowflake-6.png)


После успешного подключения откроется окно **Навигатор**, содержащее данные, доступные на сервере. Из них вы можете выбрать один или несколько элементов для импорта и использования в **Power BI Desktop**.

![Ошибка ODBC 28000, приводящая к сбою подключения.](media/desktop-connect-snowflake/connect-snowflake-5.png)

Вы можете **загрузить** выбранную таблицу, после чего таблица будет целиком перемещена в **Power BI Desktop**. Или же можно **изменить** запрос — в таком случае откроется **редактор запросов**, с помощью которого можно отфильтровать и уточнить набор нужных вам данных, а затем загрузить уточненный набор данных в **Power BI Desktop**.

## <a name="custom-roles"></a>Пользовательские роли

В настоящее время пользовательская роль в соединителе Snowflake поддерживается только для обычной проверки подлинности. Эта проблема будет устранена в ближайшем будущем.

## <a name="next-steps"></a>Дальнейшие действия
В Power BI Desktop можно подключаться к данным самых разных видов. Дополнительные сведения об источниках данных см. в перечисленных ниже статьях.

* [Что такое Power BI Desktop?](../fundamentals/desktop-what-is-desktop.md)
* [Источники данных в Power BI Desktop](desktop-data-sources.md)
* [Формирование и объединение данных в Power BI Desktop](desktop-shape-and-combine-data.md)
* [Подключение к данным Excel в Power BI Desktop](desktop-connect-excel.md)   
* [Ввод данных непосредственно в Power BI Desktop](desktop-enter-data-directly-into-desktop.md)   
