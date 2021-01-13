---
title: Ограничения REST API Power BI в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: REST API Power BI имеет следующие ограничения. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 06/08/2018
ms.openlocfilehash: 1196917f0223ccde012d203d75c4e96fbc3b9dcf
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97887668"
---
# <a name="power-bi-rest-api-limitations"></a>Ограничения REST API Power BI  
  
**Операции POST со строками**
  
* Максимум 75 столбцов
* Максимум 75 таблиц
* Максимум 10 000 строк на один запрос строк POST  
* 1 000 000 добавляемых строк в час на набор данных  
* Максимум 5 ожидающих запросов на операции POST со строками в наборе данных  
* 120 запросов операций POST со строками в минуту на набор данных
* Если в таблице 250 000 или более строк, 120 запросов строк POST в час на набор данных
* Максимум 200 000 сохраняемых строк для каждой таблицы в наборе данных FIFO
* Максимум 5 000 000 сохраняемых строк для каждой таблицы в наборе данных "без политики хранения"  
* 4 000 символов на значение для столбца строки в операции POST со строками
  
## <a name="see-also"></a>См. также раздел

* [Ограничения службы Azure AD](/azure/active-directory/active-directory-service-limits-restrictions)   
* [Обзор интерфейса REST API Power BI](/rest/api/power-bi/)