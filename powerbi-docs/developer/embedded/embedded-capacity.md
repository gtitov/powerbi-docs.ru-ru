---
title: Емкость и номера SKU в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Сведения о емкости и номерах SKU в аналитике Power BI Embedded. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 05/17/2020
ms.openlocfilehash: 7ff6ada14128a6231b84adf83d90b3871e1c7537
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888818"
---
# <a name="capacity-and-skus-in-power-bi-embedded-analytics"></a>Емкость и номера SKU в аналитике Power BI Embedded

При переносе в рабочую среду для аналитики Power BI Embedded требуется емкость (ценовая категория *A*, *EM* или *P*) для публикации внедренного содержимого Power BI.

Емкость — это выделенный набор ресурсов, зарезервированных для монопольного использования. Она позволяет публиковать панели мониторинга, отчеты и наборы данных для пользователей без необходимости приобретать лицензии для них. Она также обеспечивает предсказуемую и согласованную производительность для содержимого.

>[!NOTE]
>Для публикации требуется одна учетная запись Power BI Pro.

## <a name="what-is-embedded-analytics"></a>Что такое встроенная аналитика?

Встроенная аналитика Power BI включает в себя два решения:
* *Power BI Embedded* — предложение Azure;
* внедрение Power BI в рамках *Power BI Premium* — предложение Office.

### <a name="power-bi-embedded"></a>Power BI Embedded

Служба Power BI Embedded предназначена для независимых поставщиков программного обеспечения и разработчиков, которые хотят внедрить визуальные элементы в свои приложения.

Приложения, в которых используется Power BI Embedded, позволяют пользователям потреблять содержимое, хранящееся в емкости Power BI Embedded.

### <a name="power-bi-premium"></a>Power BI Premium

[Power BI Premium](../../admin/service-premium-what-is.md) — это комплексное решение бизнес-аналитики для предприятий, которое обеспечивает единое представление данных организации, сведений о партнерах, клиентах и поставщиках.

Power BI Premium — это продукт SaaS, позволяющий пользователям работать с содержимым через мобильные приложения, приложения собственной разработки или портал Power BI (службу Power BI). Это позволяет использовать Power BI Premium как во внутренних приложениях, так и во внешних приложениях для клиентов.

## <a name="capacity-and-skus"></a>Емкость и номера SKU

Каждая емкость предоставляет ряд номеров SKU, каждый из которых обеспечивает особый уровень вычислительных ресурсов и памяти. Требуемый тип SKU зависит от типа решения, которое нужно развернуть.

Сведения о рабочих нагрузках, поддерживаемых на каждом уровне, см. в статье [Настройка рабочих нагрузок в емкости Premium](../../admin/service-admin-premium-workloads.md).

Дополнительные сведения о планировании и тестировании ресурсов:
* [Планирование ресурсов](embedded-capacity-planning.md)
* [Методы тестирования](../../admin/service-premium-capacity-optimize.md#testing-approaches)

### <a name="power-bi-embedded-skus"></a>Номера SKU Power BI Embedded

Power BI Embedded поставляется с номером SKU [*A*.](../../admin/service-admin-premium-purchase.md#purchase-a-skus-for-testing-and-other-scenarios)

### <a name="power-bi-premium-skus"></a>Номера SKU Power BI Premium

Для Power BI Premium предлагаются два номера SKU: *P* и *EM*.
* [Сведения о различиях между номерами SKU *P* и *EM*](../../admin/service-premium-what-is.md#subscriptions-and-licensing)
* [Купить номер SKU Premium](../../admin/service-admin-premium-purchase.md)

### <a name="which-sku-should-i-use"></a>Какой номер SKU выбрать?

В таблице ниже приводится сводка возможностей с указанием требуемой мощности и подходящей ценовой категории.

В этой таблице пользовательским приложением считается веб-приложение на основе встроенной аналитики. Внедрение в пользовательское веб-приложение (с помощью REST API или пакетов SDK для JavaScript или .NET) позволяет разработчику управлять пользовательским интерфейсом и настраивать его. Эта возможность недоступна при использовании других вариантов внедрения, таких как служба Power BI и Power BI Mobile.

| Сценарий | Azure   | Office          |
|----------|---------|-----------------|
|          | (Ценовая категория A) | (Ценовые категории P и EM) |
|[Внедрение для клиентов](embed-sample-for-customers.md)</br>(данные принадлежат приложению)     |✔        |✔        |
|[Внедрение для организации](embed-sample-for-your-organization.md)</br>(данные принадлежат пользователю)     |✖        |✔         |
|Приложения Microsoft 365</br>(ранее назывались приложениями Office 365)<ul><li>[Внедрение в Teams](../../collaborate-share/service-embed-report-microsoft-teams.md)</li><li>[Внедрение в SharePoint](../../collaborate-share/service-embed-report-spo.md)</li></ul>     |✖        |✔        |
|[Безопасное внедрение по URL-адресу](../../collaborate-share/service-embed-secure.md)</br>(внедрение из службы Power BI)     |✖        |✔        |

>[!NOTE]
>* Для публикации содержимого в рабочей области приложения Power BI требуется [лицензия Power BI Pro](../../admin/service-admin-purchasing-power-bi-pro.md).
>* Только **ценовая категория P** позволяет пользователям Power BI бесплатного уровня использовать приложения и общее содержимое Power BI в службе Power BI.

### <a name="capacity-considerations"></a>Рекомендации по емкости

В таблице ниже приводятся особенности оплаты и использования для каждой емкости.

</br>
<table>
<tbody>
<tr>
<td></td>
<td style="text-align: center;"><p><strong>Что такое Power BI Embedded в Azure?</strong></p></td>
<td style="text-align: center;" colspan="2"><p><strong>Power BI Premium</strong></p></td>
</tr>
<tr>
<td><p><strong>ПРЕДЛОЖЕНИЕ</strong></p></td>
<td style="text-align: center"><p>Azure</p></td>
<td style="text-align: center" colspan="2"><p>Office</p></td>
</tr>
<tr>
<td><p><strong>SKU</strong></p></td>
<td style="text-align: center"><p>А</p></td>
<td style="text-align: center"><p>EM</p></td>
<td style="text-align: center"><p>P</p></td>
</tr>
<tr>
<td><p><strong>Выставление счетов</strong></td>
<td style="text-align: center">Каждый час</td>
<td style="text-align: center">Ежемесячно</td>
<td style="text-align: center">Ежемесячно</td>
</tr>
<tr>
<td><p><strong>Обязательство</strong></td>
<td style="text-align: center">Нет</td>
<td style="text-align: center">Ежегодно</td>
<td style="text-align: center">Ежемесячно или ежегодно</td>
</tr>
<tr>
<td valign="top"><p><strong>Использование</strong></td>
<td style="text-align: center">Ресурсы Azure можно:<li><a href="azure-pbie-scale-capacity.md">масштабировать по вертикали;</a></li><li><a href="azure-pbie-pause-start.md">приостанавливать и возобновлять.</a>
</td></li>
<td style="text-align: center">Внедрение в приложения, в том числе</br> приложения Майкрософт</td>
<td style="text-align: center">Внедрение в приложения и</br> службу Power BI</td>
</tr>
</tbody>
</table>

### <a name="sku-memory-and-computing-power"></a>Память и вычислительные ресурсы SKU

В следующей таблице описаны ресурсы и ограничения для каждого SKU.

| Узлы емкости | Число виртуальных ядер | Серверные виртуальные ядра | ОЗУ (ГБ) | Интерфейсные виртуальные ядра | Подключения DirectQuery и активные подключения (в секунду) | Параллелизм обновления модели |
| --- | --- | --- | --- | --- | --- | --- |
| EM1/A1 | 1 | 0,5 | 2.5 | 0,5 | 3,75 % | 1 |
| EM2/A2 | 2 | 1 | 5 | 1 | 7,5 % | 2 |
| EM3/A3 | 4 | 2 | 10 | 2 | 15 | 3 |
| P1/A4 | 8 | 4 | 25 | 4 | 30 | 6 |
| P2/A5 | 16 | 8 | 50 | 8 | 60 | 12 |
| P3/A6 | 32 | 16 | 100 | 16 | 120 | 24 |
| P4 | 64 | 32 | 200 | 32 | 240 | 48 |
| P5 | 128 | 64 | 400 | 64 | 480 | 96 |
| | | | | | | |

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
>[Внедрение для клиентов](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Внедрение для организации](embed-sample-for-your-organization.md)

> [!div class="nextstepaction"]
> [Внедрение из приложений](embed-from-apps.md)