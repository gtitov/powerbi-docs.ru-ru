---
title: Предварительные требования к источникам данных Power BI
description: Предварительные требования к источникам данных Power BI
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: conceptual
ms.date: 01/29/2020
LocalizationGroup: Connect to data
ms.openlocfilehash: 55e219ff5da73774adaec768b48a0aedd90c1748
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96405383"
---
# <a name="power-bi-data-source-prerequisites"></a>Предварительные требования к источникам данных Power BI
Для каждого поставщика данных Power BI поддерживает конкретную версию поставщика для объектов. Дополнительные сведения об источниках данных, доступных для Power BI, см. в разделе [Источники данных](desktop-data-sources.md). В следующей таблице описаны эти требования.

| Источник данных | Поставщик | Минимальная версия поставщика | Минимальная версия источника данных | Поддерживаемые объекты источника данных | Ссылка на скачивание |
| --- | --- | --- | --- | --- | --- |
| SQL Server |ADO.NET (встроенный в .NET Framework) |.NET Framework 3.5 (только) |SQL Server 2005 и более поздних версий |Таблицы и представления, скалярные функции, табличные функции |В составе .NET Framework 3.5 или более поздних версий |
| Доступ |Ядро СУБД Microsoft Access (ACE) |ACE 2010 с пакетом обновления 1 (SP1) |Без ограничений |Таблицы и представления |[Ссылка для загрузки](./desktop-access-database-errors.md) |
| Excel (только файлы XLS) (см. примечание 1) |Ядро СУБД Microsoft Access (ACE) |ACE 2010 с пакетом обновления 1 (SP1) |Без ограничений |Таблицы, листы |[Ссылка для загрузки](./desktop-access-database-errors.md) |
| Oracle (см. примечание 2) |ODP.NET |ODAC 11.2 Release 5 (11.2.0.3.20) |9.x и более поздних версий |Таблицы и представления |[Ссылка для загрузки](./desktop-connect-oracle-database.md) |
| | System.Data.OracleClient (встроенный в .NET Framework) |.Net Framework 3.5 |9.x и более поздних версий |Таблицы и представления |В составе .NET Framework 3.5 или более поздних версий |
| IBM DB2 |Клиент ADO.Net от IBM (часть пакета драйверов сервера данных IBM) |10.1 |9.1+ |Таблицы и представления |[Ссылка для загрузки](https://go.microsoft.com/fwlink/?linkid=274911&clcid=0x409) |
| MySQL |Соединитель .Net |6.6.5 |5.1 |Таблицы и представления, скалярные функции |[Ссылка для загрузки](https://go.microsoft.com/fwlink/?linkid=278885&clcid=0x409) |
| PostgreSQL |Поставщик NPGSQL ADO.NET (поставляется с Power BI Desktop) |4.0.10 |9.4 |Таблицы и представления |[Ссылка для загрузки](https://go.microsoft.com/fwlink/?linkid=282716&clcid=0x409) |
| Teradata |Поставщик данных .NET для Teradata |14+ |12+ |Таблицы и представления |[Ссылка для загрузки](https://go.microsoft.com/fwlink/?linkid=278886&clcid=0x409) |
| SAP Sybase SQL Anywhere |iAnywhere.Data.SQLAnywhere для .NET 3.5 |16+ |16+ |Таблицы и представления |[Ссылка для загрузки](https://go.microsoft.com/fwlink/?linkid=324846) |

>[!NOTE]
>Файлы Excel с расширением XLSX не требуют установки отдельного поставщика.

>[!NOTE]
>Поставщикам Oracle также требуется клиентское программное обеспечение Oracle (версии 8.1.7 и более поздних).
> 
>