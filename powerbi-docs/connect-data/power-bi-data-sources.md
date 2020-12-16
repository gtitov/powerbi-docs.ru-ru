---
title: Источники данных Power BI
description: В этой статье перечислены источники данных, поддерживаемые Power BI, включая сведения о DirectQuery и локальном шлюзе данных.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: conceptual
ms.date: 12/14/2020
ms.openlocfilehash: 67a0577c906e23fc51182120f1445814bdcd8028
ms.sourcegitcommit: 46cf62d9bb33ac7b7eae7910fbba6756f626c65f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2020
ms.locfileid: "97491835"
---
# <a name="power-bi-data-sources"></a>Источники данных Power BI

В следующей таблице указаны источники данных, поддерживаемые Power BI для наборов данных, включая сведения о DirectQuery и локальном шлюзе данных. См. сведения о [подключении к источникам данных для потоков данных Power BI](../transform-model/dataflows/dataflows-configure-consume.md).

| Источник данных | Подключение из версии Desktop | Подключение и обновление из службы | Подключение DirectQuery и активное подключение | Шлюз (поддерживается) | Шлюз (обязательно) | Потоки данных Power BI |
|---|---|---|---|---|---|---|---|
| База данных Access | Да | Да | Нет | Да <sup>1</sup> | Да | Да |
| ActiveDirectory | Да | Да | Нет | Да | Да | Да |
| Adobe Analytics | Да | Да | Нет | Нет | Нет | Нет |
| Amazon Redshift | Да | Да | Да | Да | нет | Да |
| appFigures | Да | Да | Нет | Нет | Нет | Нет |
| Кубы AtScale | Да | Да | Да | Да | Нет | Нет |
| Службы Azure Analysis Services | Да | Да | Да | Нет | Нет | Нет |
| хранилище BLOB-объектов Azure | Да | Да | Нет | Да | Нет | Да |
| Azure Cosmos DB | Да | Да | Нет | Нет | Нет | Нет |
| Управление затратами Azure | Да | Да | Нет | Нет | нет | Нет |
| Azure Data Explorer (Kusto) | Да | Да | Да | Да | Нет | Да |
| Хранилище Azure Data Lake Storage 1-го поколения | Да | Да | нет | Нет | Нет | Нет |
| Azure Data Lake Storage 2-го поколения | Да | Да | Нет | Да | Нет | Да |
| Azure Databricks | Да | Да | Да | Да | Нет | Нет |
| Azure DevOps | Да | Да | Нет | Нет | Нет | Нет |
| Azure DevOps Server | Да | Да | Нет | Да | Да | Нет |
| Azure HDInsight (HDFS) | Да | Да | Нет | нет | Нет | Нет |
| Azure HDInsight — Spark | Да | Да | Да | Нет | Нет | Да |
| База данных SQL Azure | Да | Да | Да | Да | Нет | Да |
| Хранилище данных SQL Azure | Да | Да | Да | Да | Нет | Да |
| Хранилище таблиц Azure | Да | Да | Нет | Да | Нет | Да |
| Соединитель BI | Да | Да | Да | Да | Да | Нет |
| BI360 — отчеты по бюджетам и финансам | Да | Да | Нет | нет | Нет | Нет |
| Microsoft Dataverse | Да | Да | нет | Нет | Нет | Да |
| Data.World — получение набора данных | Да | Да | Нет | Нет | Нет | Нет |
| Denodo | Да | Да | Да | Да | Да | Нет |
| Dremio | Да | Да | Да | Да | Да | нет |
| Dynamics 365 (в сети) | Да | Да | Нет | Нет | нет | Нет |
| Dynamics 365 Business Central | Да | Да | Нет | Нет | Нет | Нет |
| Dynamics 365 Business Central (локальный) | Да | Да | Нет | Нет | Нет | Нет |
| Dynamics 365 Customer Insights | Да | Да | Нет | Нет | Нет | Нет |
| Dynamics NAV | Да | Да | Нет | Нет | Нет | Нет |
| Источник данных Emigo | Да | Да | Нет | Нет | Нет | нет |
| Entersoft Business Suite | Да | Да | Нет | Нет | нет | Нет |
| Essbase | Да | Да | Да | Да | Да | Нет |
| Exasol | Да | Да | Да | Да | Да | Нет |
| Excel | Да <sup>3</sup> | Да <sup>3</sup> | Нет | Да <sup>3</sup> | Нет <sup>4</sup> | Да |
| Facebook | Да | Да | Нет | Нет | Нет | Нет |
| Файл | Да | Да | Нет | Да | Да | Да |
| Папка | Да | Да | Нет | Да | Да | Да |
| GitHub | Да | Да | Нет | Нет | Нет | Нет |
| Google Analytics | Да | Да | Нет | Нет | Нет | Нет |
| Google BigQuery | Да | Да | Да | Да | Нет | Да |
| Файл Hadoop (HDFS) | Да | Нет | Нет | Нет | Нет | Нет |
| Hive LLAP | Да | Да | Да | Да | Нет | нет |
| HDInsight Interactive Query | Да | Да | Да | Нет | Нет | Нет |
| IBM DB2 | Да | Да | Да | Да | Нет | Да |
| База данных IBM Informix | Да | Да | Нет | Да | Нет | Нет |
| IBM Netezza | Да | Да | Да | Да | Да | Нет |
| Impala | Да | Да | Да | Да | Да | Да |
| Indexima | Да | Да | Да | Да | Да | нет |
| Industrial App Store | Да | Да | Нет | Нет | нет | Нет |
| Information Grid | Да | Да | Нет | нет | Нет | Нет |
| Intersystems IRIS | Да | Да | Да | Да | Да | Нет |
| Хранилище данных Intune | Да | Да | Нет | Нет | Нет | Нет |
| Jethro ODBC | Да | Да | Да | Да | Да | Нет |
| JSON | Да | Да | Нет | Да** | Нет <sup>4</sup> | Да |
| Kyligence Enterprise | Да | Да | Да | Да | Да | Нет |
| MailChimp | Да | Да | Нет | Нет | Нет | Нет |
| Marketo | Да | Да | нет | Нет | Нет | Нет |
| MarkLogic ODBC | Да | Да | Да | Да | Да | Нет |
| Microsoft Azure Consumption Insights | Да | Да | Нет | Нет | Нет | Нет |
| Microsoft Exchange | Да | Да | Нет | Да | Нет | нет |
| Microsoft Exchange Online | Да | Да | Нет | Нет | Нет | Да |
| Безопасность Microsoft Graph | Да | Да | Нет | Да | Нет | Нет |
| Mixpanel | Да | Да | Нет | нет | Нет | Нет |
| MySQL | Да | Да | Нет | Да | Да | Да |
| OData | Да | Да <sup>7</sup> | Нет | Да | Нет | Да |
| ODBC | Да | Да | Нет | Да | Да | Да |
| OleDb | Да | Да | Нет | Да | Да | Нет |
| Oracle; | Да | Да | Да | Да | Да | Да |
| Paxata <sup>8</sup> | Да | Да | нет | Да | Нет | Нет |
| PDF | Да | Да | Нет | Да | Нет <sup>4</sup> | Да |
| Planview Enterprise One — CTM | Да | Да | Нет | Нет | Нет | Нет |
| Planview Enterprise One — PRM | Да | Да | Нет | Нет | Нет | Нет |
| Planview Projectplace | Да | Да | Нет | Нет | Нет | Нет |
| PostgreSQL | Да | Да | Да | Да | Нет | Да |
| Потоки данных Power BI | Да | Да | нет | Нет | Нет | Да |
| Наборы данных Power BI | Да | Да | Да | Нет | Нет | Нет |
| Потоки данных Power Platform | Да | Да | Нет | Нет | Нет | Да |
| Сценарий Python | Да | Да <sup>5</sup> | Нет | Да <sup>5</sup> | Да | Нет |
| QubolePresto | Да | Да | Да | Да | Да | Нет |
| Quick Base | Да | Да | Нет | Да | Да | Нет |
| QuickBooks Online | Да | Да | Нет | Нет | Нет | Нет |
| Скрипт R | Да | Да <sup>5</sup> | Нет | Да <sup>5</sup> | Нет | Нет |
| Roamler | Да | Да | Нет | Да | Нет | Нет |
| Объекты Salesforce | Да | Да | Нет | Нет | Нет | Да |
| Отчеты SalesForce | Да | Да | Нет | Нет | нет | Да |
| Сервер сообщений SAP Business Warehouse | Да | Да | Да | Да | Да | Да |
| Сервер SAP Business Warehouse | Да | Да | Да | Да | Да | Да |
| SAP HANA | Да | Да | Да | Да | Да | Да |
| Папка SharePoint | Да | Да | Нет | Да | Нет <sup>4</sup> | Да |
| SharePoint | Да | Да | Нет | Да | Нет <sup>4</sup> | Да |
| Список SharePoint Online | Да | Да | Нет | Да | нет | Да |
| Smartsheet | Да | Да | Нет | нет | Нет | Да |
| Snowflake | Да | Да | Да | Да | Нет | Да |
| Spark | Да | Да | Да | Да | Нет | Да |
| SparkPost | Да | Да | Нет | Нет | Нет | Нет |
| SQL Server | Да | Да | Да | Да | Да | Да |
| службы SQL Server Analysis Services | Да | Да | Да | Да | Да | Нет |
| Stripe | Да | Да | Нет | Нет | Нет | Нет |
| SurveyMonkey | Да | Да | Нет | Да | Нет | Нет |
| SweetIQ | Да | Да | Нет | Нет | Нет | Нет |
| Sybase | Да | Да | Нет | Да | Да | Да |
| TeamDesk | Да | Да | Нет | Да | Нет | Нет |
| Tenforce | Да | Да | Нет | Нет | Нет | Нет |
| Teradata | Да | Да | Да | Да | Да | Да |
| Text/CSV | Да | Да | Нет | Да | Нет <sup>4</sup> | Да |
| Twilio | Да | Да | Нет | Нет | Нет | Нет |
| tyGraph | Да | Да | Нет | Нет | Нет | Нет |
| Vertica | Да | Да | Да | Да | Да | Да |
| Интернет | Да | Да | Нет | Да | Да <sup>6</sup> | Да |
| Webtrends | Да | Да | Нет | Нет | Нет | Нет |
| Workforce Dimensions | Да | Да | Нет | Да | Нет | Нет |
| XML | Да | Да | Нет | Да | Нет <sup>4</sup> | Да |
| Zendesk | Да | Да | Нет | Нет | Нет | Нет |
| | | | | | | | |

<sup>1</sup> Поддерживаются [поставщиком ACE OLEDB](https://www.microsoft.com/download/details.aspx?id=54920), установленным на том же компьютере, что и шлюз.

<sup>3</sup> Для файлов Файлы Excel 1997–2003 (XLS) требуется [поставщик ACE OLEDB](https://www.microsoft.com/download/details.aspx?id=54920).

<sup>4</sup> Требуется для локальной версии данной технологии.

<sup>5</sup> Поддерживается только в [персональном шлюзе](service-gateway-personal-mode.md).

<sup>6</sup> Требуется для HTML-, XLS-файлов и баз данных Access.

<sup>7</sup> Служба Power BI не поддерживает универсальный OAuth2.

<sup>8</sup> Paxata поддерживается в версии Power BI Desktop, оптимизированной для сервера отчетов Power BI. Это решение не поддерживается в отчетах Power BI, опубликованных на сервере отчетов Power BI. Список поддерживаемых источников данных см. в статье [Источники данных отчетов Power BI в решении "Сервер отчетов Power BI"](../report-server/data-sources.md).

## <a name="considerations-and-limitations"></a>Рекомендации и ограничения

- Для проверки подлинности во многих соединителях данных для Power BI Desktop требуется Internet Explorer 10 (или более поздняя версия). 
- Некоторые источники данных, доступные в Power BI Desktop, оптимизированы для сервера отчетов Power BI, но не поддерживаются для публикации на сервере отчетов Power BI. Список поддерживаемых источников данных см. в статье [Источники данных отчетов Power BI в решении "Сервер отчетов Power BI"](../report-server/data-sources.md).

## <a name="single-sign-on-sso-for-directquery-sources"></a>Единый вход для источников DirectQuery

Если включен параметр единого входа и пользователям предоставлен доступ к отчетам на основе источника данных, Power BI отправляет их учетные данные для проверки подлинности Azure AD в запросах к базовому источнику данных. Это позволяет Power BI использовать параметры безопасности, настроенные на уровне источника данных.
Параметр единого входа применяется ко всем наборам данных, в которых используется этот источник. Это не влияет на метод аутентификации, который применяется для сценариев импорта. Следующие источники данных поддерживают единый вход для подключений через DirectQuery.

- База данных SQL Azure
- Хранилище данных SQL Azure
- Impala
- SAP HANA
- SAP BW
- Сервер сообщений SAP BW
- Snowflake
- Spark
- SQL Server
- Teradata

## <a name="next-steps"></a>Дальнейшие действия

[Подключение к данным в Power BI Desktop](desktop-quickstart-connect-to-data.md)  
[Использование DirectQuery в Power BI](desktop-directquery-about.md)  
[Динамические данные служб SQL Server Analysis Services в Power BI](sql-server-analysis-services-tabular-data.md)  
[Что такое локальный шлюз данных?](service-gateway-onprem.md)  
[Источники данных отчетов Power BI в решении "Сервер отчетов Power BI"](../report-server/data-sources.md)
