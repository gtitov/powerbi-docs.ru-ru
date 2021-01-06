---
title: Подключение к базе данных Impala в Power BI Desktop
description: Простое и удобное подключение к базе данных Impala в Power BI Desktop и ее использование
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: how-to
ms.date: 01/04/2021
LocalizationGroup: Connect to data
ms.openlocfilehash: a9d817dc3e34cae2f496136fe19353ba5b993c8a
ms.sourcegitcommit: 932f6856849c39e34229dc9a49fb9379c56a888a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97926413"
---
# <a name="connect-to-an-impala-database-in-power-bi-desktop"></a>Подключение к базе данных Impala в Power BI Desktop
В Power BI Desktop вы можете подключиться к базе данных **Impala** и использовать ее так же, как и любой другой источник данных в Power BI Desktop.

## <a name="connect-to-an-impala-database"></a>Подключение к базе данных Impala
Для подключения к базе данных **Impala**, сделайте следующее: 

1. В **Power BI Desktop** на вкладке ленты **Главная** выберите {5}Получить данные{6}. 

2. В области слева выберите категорию **База данных**. Отобразится **Impala**.

    ![Получить данные](media/desktop-connect-impala/connect_impala_2.png)

3. В появившемся окне **Impala** введите или вставьте в поле имя сервера Impala. Нажмите кнопку **ОК**. Вы можете **импортировать** данные непосредственно в Power BI или использовать **DirectQuery**. См. дополнительные сведения об [использовании DirectQuery](desktop-use-directquery.md).

    ![Окно Impala](media/desktop-connect-impala/connect_impala_3a.png)

4. При появлении запроса введите учетные данные или подключитесь анонимно. Соединитель Impala поддерживает анонимную проверку подлинности, обычную проверку подлинности (имя пользователя и пароль) и проверку подлинности Windows.

    ![Соединитель Impala](media/desktop-connect-impala/connect_impala_4.png)

    > [!NOTE]
    > Когда будут указаны имя пользователя и пароль для определенного сервера **Impala**, Power BI Desktop запомнит эти учетные данные для последующих попыток подключения. Эти учетные данные можно изменить, последовательно выбрав элементы **Файл > Параметры и настройки > Параметры источника данных**.


5. После подключения появится окно **Навигатор**, которое отображает данные, доступные на сервере. Выберите нужные элементы для импорта и использования в **Power BI Desktop**.

    ![Окно "Навигатор"](media/desktop-connect-impala/connect_impala_5.png)

## <a name="considerations-and-limitations"></a>Рекомендации и ограничения
Существуют определенные ограничения и рекомендации, которые следует учитывать при работе с соединителем **Impala**.

* Соединитель Impala поддерживается в локальном шлюзе данных с помощью любого из трех механизмов проверки подлинности.

## <a name="next-steps"></a>Дальнейшие действия
Power BI Desktop поддерживает возможность подключения к разным источникам данных. Дополнительные сведения об источниках данных см. в следующих статьях:

* [Что такое Power BI Desktop?](../fundamentals/desktop-what-is-desktop.md)
* [Источники данных в Power BI Desktop](desktop-data-sources.md)
* [Формирование и объединение данных в Power BI Desktop](desktop-shape-and-combine-data.md)
* [Подключение к данным Excel в Power BI Desktop](desktop-connect-excel.md)   
* [Ввод данных непосредственно в Power BI Desktop](desktop-enter-data-directly-into-desktop.md)   
