---
title: Советы и рекомендации по формулировке вопросов в функции "Вопросы и ответы"
description: Советы и рекомендации по формулировке вопросов в функции "Вопросы и ответы" в Power BI
author: mihart
ms.author: mihart
ms.reviewer: Mohammad.ali
ms.service: powerbi
ms.subservice: pbi-explore
ms.topic: how-to
ms.date: 09/23/2020
LocalizationGroup: Ask questions of your data
ms.openlocfilehash: 7757c883daee390b8cdcc93e0d6b9f8376d53f62
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96389835"
---
# <a name="tips-for-asking-questions-in-power-bi-qa"></a>Советы по запросам в функцию "Вопросы и ответы" в Power BI

[!INCLUDE[consumer-appliesto-yyny](../includes/consumer-appliesto-yyny.md)]

## <a name="words-and-terminology-that-qa-recognizes"></a>Слова и термины, распознаваемые функцией "Вопросы и ответы"
Список ключевых слов на этой странице не являетсяс исчерпывающим.  Чтобы понять, распознает ли Power BI то или иное ключевое слово, попробуйте ввести его в поле вопроса.  Если слово или термин затенены, значит Power BI не распознает его.

В приведенном ниже списке используется настоящее время, однако в большинстве случаев распознаются все временные формы. Например, слово is включает все его формы: **are**, **was**, **were**, **will be**, **have**, **has**, **had**, **will have**, **has got**, **do**, **does**, **did**.  А слово sort включает формы **sorted** и **sorting**.  Power BI также распознает и использует формы слов в единственном и множественном числах. 

> [!NOTE]
> Компонент "Вопросы и ответы" также доступен в [приложении Microsoft Power BI для iOS на устройствах iPad, iPhone и iPod Touch](mobile/mobile-apps-ios-qna.md).
>  


|Категория  |Ключевые слова  |
|---------|---------|---------|
|**Статистические функции**     | total, sum, amount, number, quantity, count, average, most, least, fewest, largest, smallest, highest, biggest, maximum, max, greatest, lowest, littlest, minimum, min          |
|     |         |         
**Артикли**     |  a, an, the              |
|     |         |         
|**Пустые значения и логические выражения**     |   blank, empty, null, префиксы non и non-, empty string, empty text, true, t, false, f          |
|     |         |         |
|**Сравнения**     |   vs, versus, compared to, compared with            |
|     |         |         |
|**Союзы**     |  and, or, each of, with, versus, &, and, but, nor, along with, in addition to       |         
|          |         |
|**Сокращения**     |  Компонент "Вопросы и ответы" распознает практически все сокращения, смело экспериментируйте с ними.  Вот лишь несколько примеров: didn’t, haven’t, he’d, he’s, isn’t, it’s, she’ll, they’d, weren’t, who’s, won’t, wouldn’t.          |
|        |         |
|**Даты**     |       Power BI распознает большинство терминов, связанных с датами (day, week, month, year, quarter, decade и т. д.), а также даты, записанные в самых разных форматах (см. ниже). Power BI также распознает следующие ключевые слова: MonthName, Days 1-31, decade. Примеры: January 3rd of 1995, January 3rd 1995, jan 03 1995, 3 Jan 1995, the 3rd of January, January 1995, 1995 January, 1995-01, 01/1995, названия месяцев.         |
|        |         |
|**Относительные даты**     |   today, right now, current time, yesterday, tomorrow, the current, next, the coming, last, previous, ago, before now, sooner than, after, later than, from, at, on, from now, after now, in the future, past, last, previous, within, in, over, N days ago, N days from now, next, once, twice.|
|    |  Пример: count of orders in the past 6 days (количество заказов за последние 6 дней).  |            |
|        |         |
|**Равенство (диапазоны)**     |   in, equal to, =, after, is more than, in, between, before  |
|  |Примеры: Order year is before 2012 (год заказа до 2012)? Price equals between 10 and 20 (цена в диапазоне от 10 до 20)? Is the age of John greater than 40 (возраст Джона больше 40)? Total sales in 200-300 (общий объем продаж в диапазоне 200-300)?              |
|        |         |
|**Равенство (значение)**     |   is, equal, equal to, in, of, for, within, is in, is on |
|   | Примеры: Какие продукты зеленые? Order date equals 2012 (год заказа равен 2012). Is the age of John 40 (возраст Джона 40)? Total sales that is not equal to 200 (общий объем продаж не равен 200)? Order date of 1/1/2016 (дата заказа 01.01.2016). 10 in price (10 в значении цены)? Green for color (зеленый цвет)? 10 in price (10 в значении цены)?              |
|        |         |
|**Имена**     |       Если столбец в наборе данных содержит слово name (Имя), как например EmployeeName, функция "Вопросы и ответы" определяет, что значения в этом столбце являются именами. Вы можете задавать по ним такие вопросы, как "which employees are named robert" (каких сотрудников зовут Роберт).          |
|        |         |
**Местоимения**  | he, him, himself, his, she, herself, her, hers, it, itself, its, they, their, them, themselves, theirs, this, these, that, those
|**Команды запросов**     |    sorted, sort by, direction, group, group by, by, show, list, display, give me, name, just, only, arrange, rank, compare, to, with, against, alphabetically, ascending, descending, order             |
|        |         |
|**Диапазон**     |      greater, more, larger, above, over, >, less, smaller, fewer, below, under, <, at least, no less than, >=, at most, no more than, <=, in, between, in the range of, from, later, earlier, sooner, after, on, at, later than, after, since, starting with, starting from, ending with           |
|        |         |
**Время**  |am, pm, o'clock, noon, midnight, hour, minute, second, hh:mm:ss  |
|  |  Примеры: 10 pm, 10:35 pm, 10:35:15 pm, 10 o clock, noon, midnight, hour, minute, second.  |
|  |  |
|**N значений по порядку**     |     (порядок и ранжирование): top, bottom, highest, lowest, first, last, next, earliest, newest, oldest, latest, most recent, next            |
|        |         |
|**Типы визуальных элементов**     |  Все типы визуальных элементов, поддерживаемые Power BI.  Если соответствующий параметр есть в области "Визуализации", его можно использовать в вопросе.  Исключением из этого правила являются [пользовательские визуальные элементы Power BI](../developer/visuals/power-bi-custom-visuals.md), которые вы добавили в область визуализации вручную.  |
|  |  Пример: show districts by month and sales total as bar chart (показать районы по месяцам и общие продажи как линейчатую диаграмму)               |
|        |         |
|**Вопросы (отношения и качества)**  | when, where, which, who, whom, how many, how much, how many times, how often, how frequently, amount, number, quantity, how long, what                |

## <a name="qa-helps-you-phrase-the-question"></a>Функция "Вопросы и ответы" помогает сформулировать вопрос
Функция "Вопросы и ответы" делает все возможное, чтобы правильно распознать заданный вопрос и ответить на него. Для этого применяется несколько способов. Во всех формулировках действие можно принимать полностью, частично или не принимать совсем. При вводе вопроса функция "Вопросы и ответы":

* Автоматически заканчивает слова и вопросы. При этом применяются различные стратегии, включая автозавершение узнаваемых слов, хранимые вопросы и учет ранее заданных вопросов, на которые был предоставлен действительный ответ. Если вариантов для автозавершения несколько, они предоставляются в виде раскрывающегося списка.
* исправляет орфографические ошибки;
* Обеспечивает предварительный просмотр ответов в форме визуализации. Визуализация обновляется по мере ввода и изменения вопроса (до нажатия клавиши ВВОД).
* При повторном наведении указателя мыши на поле вопроса предлагает замены терминов из подключенных наборов данных.
* изменяет формулировку вопроса в зависимости от того, какие данные входят в соответствующий набор. Функция "Вопросы и ответы" заменяет введенные слова на синонимы из подключенных наборов данных. Измененная формулировка позволяет оценить, правильно ли служба "Вопросы и ответы"поняла ваш вопрос. 
* добавляет двойное подчеркивание в слова, которые он не понимает.
* добавляет одинарное подчеркивание в слова, которые он понимает.
* позволяет связаться с отчетом или владельцем панели мониторинга, если термин не найден или ваш вопрос не имеет результатов.

## <a name="dont-stop-now"></a>Не останавливайтесь
Продолжайте диалог даже после того, как получите ответы на заданные вопросы. Воспользуйтесь интерактивными функциями визуализации и функции "Вопросы и ответы", чтобы получить больше полезных сведений.

## <a name="next-steps"></a>Дальнейшие действия
Назад к статье [Вопросы и ответы в Power BI](end-user-q-and-a.md)  

[Power BI — основные понятия](end-user-basic-concepts.md)  

Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)

