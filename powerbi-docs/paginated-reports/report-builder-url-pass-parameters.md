---
title: Передача параметра отчета в URL-адресе для отчета с разбивкой на страницы в Power BI (построитель отчетов Power BI)
description: Здесь приводятся сведения о передаче параметров отчета в отчет путем их включения в URL-адрес отчета с разбивкой на страницы.
author: maggiesMSFT
ms.author: maggies
ms.service: powerbi
ms.subservice: report-builder
ms.topic: how-to
ms.reviewer: cfinlan
ms.custom: ''
ms.date: 05/01/2020
ms.openlocfilehash: ac3cd10ec4c356da92aca6983292ff57b16f58b3
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96415595"
---
# <a name="pass-a-report-parameter-in-a-url-for-a-paginated-report-in-power-bi"></a>Передача параметра отчета в URL-адресе для отчета с разбивкой на страницы в Power BI 

[!INCLUDE [applies-to](../includes/applies-to.md)] [!INCLUDE [yes-service](../includes/yes-service.md)] [!INCLUDE [yes-paginated](../includes/yes-paginated.md)] [!INCLUDE [yes-premium](../includes/yes-premium.md)] [!INCLUDE [no-desktop](../includes/no-desktop.md)] 

Вы можете передать параметры отчета в отчет, включив их в URL-адрес отчета с разбивкой на страницы. Все параметры запроса могут иметь соответствующие параметры отчета. Таким образом, параметр запроса передается в отчет путем передачи соответствующего параметра отчета. Чтобы служба Power BI смогла распознать имя параметра в URL-адресе, к имени необходимо добавить префикс `rp:`. 

Параметры отчета зависят от регистра. В них используются следующие специальные символы. 

- Пробел в части параметра URL-адреса заменяется знаком "плюс" (+).  Пример: 

    ```rp:Holiday=Christmas+Day```

- Точка с запятой в любой части строки заменяется символами `%3A`.

Браузер должен автоматически выполнить необходимую кодировку URL-адреса. Кодировать символы вручную не требуется. 

Чтобы задать параметр отчета в URL-адресе, используйте следующий синтаксис: 

```
rp:parameter=value
```

Например, чтобы указать два параметра ("Salesperson" и "State"), определенных в отчете в области "Моя рабочая область", используйте следующий URL-адрес: 

```
https://app.powerbi.com/groups/me/rdlreports/xxxxxxx-abc7-40f0-b456-febzf9cdda4d?rp:Salesperson=Tie+Bear&rp:State=Utah 
```

Чтобы указать те же два параметра, которые определены в отчете в приложении, используйте следующий URL-адрес: 

```
https://app.powerbi.com/groups/me/apps/xxxxxxx-c4c4-4217-afd9-3920a0d1e2b0/rdlreports/b1d5e659-639e-41d0-b733-05d2bca9853c?rp:Salesperson=Tiggee&rp:State=Utah 
```

Чтобы задать параметру значение NULL, используйте следующий синтаксис: 

```
parameter:isnull=true
```

Пример:

```
rp:SalesOrderNumber:isnull=true
```

Чтобы передать логическое значение, используйте 0 для параметра false и 1 для параметра true. Чтобы передать число с плавающей точкой, включите десятичный разделитель языкового стандарта сервера.

> [!NOTE]
> Если отчет содержит параметр отчета со значением по умолчанию, а свойству **Prompt** задано значение **false**, (то есть свойство **Prompt User** не задано в диспетчере отчетов), вы не можете передать значение для этого параметра отчета в URL-адресе. В этом случае администраторы могут запрещать пользователям добавлять или изменять значения определенных параметров отчета.
> 
> Power BI не поддерживает строку запроса длиной более 2000 символов.  Это значение может быть превышено, если для просмотра отчета с разбиением на страницы используются параметры URL-адреса.  Это особенно верно, если используются параметры с несколькими значениями.

## <a name="additional-examples"></a>Дополнительные примеры 

Следующий пример URL-адреса содержит многозначный параметр "Salesperson". Формат многозначного параметра необходим, чтобы повторять имя параметра для каждого значения. 

```
https://app.powerbi.com/groups/me/rdlreports/xxxxxxx-abc7-40f0-b456-febzf9cdda4d?rp:Salesperson=Tie+Bear&rp:Salesperson=Mickey 
```

В приведенном ниже примере URL-адреса передается один параметр SellStartDate со значением "7/1/2005" для сервера отчетов в основном режиме.

```
https://app.powerbi.com/groups/me/rdlreports/xxxxxxx-abc7-40f0-b456-febzf9cdda4d?rp:SellStartDate=7/1/2005
```

## <a name="next-steps"></a>Дальнейшие действия

- [Параметры URL-адреса в отчетах с разбивкой на страницы в Power BI](report-builder-url-parameters.md)
- [Сведения об отчетах с разбивкой на страницы в Power BI Premium](paginated-reports-report-builder-power-bi.md)
