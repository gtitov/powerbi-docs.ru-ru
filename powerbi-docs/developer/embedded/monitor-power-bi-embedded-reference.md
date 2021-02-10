---
title: Справочник по данным мониторинга Power BI Embedded
description: Важные справочные материалы, которые пригодятся вам, если вы выполняете мониторинг Power BI Embedded.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.custom: subject-monitoring
ms.date: 01/14/2021
ms.openlocfilehash: 9c07e75736b3ccdb33bf76f79656a8982cddb6d8
ms.sourcegitcommit: f17acb16018752c234db6bff1f51f5130be12c58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99617026"
---
# <a name="monitoring-power-bi-embedded-data-reference"></a>Справочник по данным мониторинга Power BI Embedded

Дополнительные сведения о сборе и анализе данных мониторинга для Power BI Embedded см. в статье [Мониторинг Power BI Embedded](monitor-power-bi-embedded.md).

## <a name="metrics"></a>Метрики

В этом разделе перечислены все метрики платформы, автоматически собираемые для Power BI Embedded.  

|Тип метрики | Поставщик ресурсов/пространство имен типа<br/> и связь с отдельными метриками |
|-------|-----|
| Производительность | [Microsoft.PowerBIDedicated/capacities](/azure/azure-monitor/platform/metrics-supported#microsoftpowerbidedicatedcapacities) |

### <a name="capacities"></a>Производительность

Поставщик ресурсов и тип: [Microsoft.PowerBIDedicated/capacities](/azure/azure-monitor/platform/metrics-supported#microsoftpowerbidedicatedcapacities)

| Имя | Метрика | Unit | Описание |
|:---|:-------|:-----|:------------|
|Память (1-го поколения) |memory_metric               |Байты        |Память. Диапазон 0–3 ГБ для A1, 0–5 ГБ для A2, 0–10 ГБ для A3, 0–25 ГБ для A4, 0–50 ГБ для A5 и 0–100 ГБ для A6. Поддерживается только для ресурсов Power BI Embedded 1-го поколения. |
|Пробуксовка памяти (наборы данных) (1-го поколения) |memory_thrashing_metric     |Процент      |Среднее значение пробуксовки памяти. Поддерживается только для ресурсов Power BI Embedded 1-го поколения. |
|Высокий уровень использования QPU (1-го поколения) |qpu_high_utilization_metric |Count        |Высокий уровень использования QPU за последнюю минуту, 1 для высокого уровня использования QPU, в противном случае 0. Поддерживается только для ресурсов Power BI Embedded 1-го поколения. |
|Длительность запроса (наборы данных) (1-го поколения) |QueryDuration               |Миллисекунды |Длительность запроса DAX за последний интервал. Поддерживается только для ресурсов Power BI Embedded 1-го поколения. |
|Длина очереди заданий пула запросов (наборы данных) (1-го поколения) |QueryPoolJobQueueLength     |Count        |Число заданий в очереди пула потоков запросов. Поддерживается только для ресурсов Power BI Embedded 1-го поколения. |

## <a name="metric-dimensions"></a>Измерения метрик

Дополнительные сведения об измерениях метрик см. в разделе [Многомерные метрики](/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

В Power BI Embedded нет метрик, содержащих измерения.

## <a name="resource-logs"></a>Журналы ресурсов

В этом разделе перечислены типы журналов ресурсов, которые можно собирать для Power BI Embedded.

Для справки можно просмотреть список [всех типов категорий журналов ресурсов, поддерживаемых Azure Monitor](/azure/azure-monitor/platform/resource-logs-schema).

В этом разделе перечислены все типы категорий журналов ресурсов, собираемых для Power BI Embedded.  

|Тип журнала ресурсов | Поставщик ресурсов/пространство имен типа<br/> и связь с отдельными метриками |
|-------|-----|
| Производительность | [Microsoft.PowerBIDedicated/capacities](/azure/azure-monitor/platform/resource-logs-categories#microsoftpowerbidedicatedcapacities) |

## <a name="azure-monitor-logs-tables"></a>Таблицы журналов Azure Monitor

Этот раздел относится ко всем таблицам Kusto журналов Azure Monitor, относящимся к Power BI Embedded и доступным для запросов Log Analytics.

|Тип ресурса | Примечания |
|-------|-----|
| [Что такое Power BI Embedded в Azure?](/azure/azure-monitor/reference/tables/tables-resourcetype#power-bi-embedded) |См. список таблиц ниже |

### <a name="power-bi-embedded"></a>Power BI Embedded

| Таблица |  Описание |
|:---------|:-------------|------------------|
| [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity) | Записи из журнала действий Azure, которые позволяют получить представление о любых событиях уровня подписки или группы управления, произошедших в Azure.    |                             |                                                   | 
| [AzureDiagnostics](/azure/azure-monitor/reference/tables/azurediagnostics)   | Хранит журналы ресурсов для служб Azure, которые используют режим Диагностики Azure. В журналах ресурсов описывается внутренняя операция ресурсов Azure. |
| [AzureMetrics](/azure/azure-monitor/reference/tables/azuremetrics)   | Данные метрик, создаваемые службами Azure, которые измеряют их работоспособность и производительность. |

Справочные сведения обо всех журналах Azure Monitor и таблицах Log Analytics см. в статье [Справочник по таблицам журналов Azure Monitor по типам ресурсов](/azure/azure-monitor/reference/tables/tables-resourcetype).

## <a name="activity-log"></a>Журнал действий

Можно выбрать категорию **Engine** и (или) **AllMetrics**.

### <a name="engine"></a>Подсистема

Категория обработчика указывает ресурсу регистрировать события, перечисленные ниже. Для каждого события существуют определенные свойства.

|     Название мероприятия     |     Описание события     |
|----------------------------|----------------------------------------------------------------------------------|
|    Audit Login    |    Запись всех новых событий подключения к подсистеме с момента запуска трассировки.    |
|    Session Initialize    |    Запись всех событий инициализации сеанса с момента запуска трассировки.    |
|    Vertipaq Query Begin    |    Запись всех событий начала запроса VertiPaq SE с момента запуска трассировки.    |
|    Query Begin    |    Запись всех событий начала запроса с момента запуска трассировки.    |
|    Query End    |    Запись всех событий окончания запроса с момента запуска трассировки.    |
|    Vertipaq Query End    |    Запись всех событий окончания запроса VertiPaq SE с момента запуска трассировки.    |
|    Audit Logout    |    Запись всех событий отключения от модуля с момента запуска трассировки.    |
|    Ошибка    |    Запись всех событий ошибок в модуле с момента запуска трассировки.    |

#### <a name="event-example"></a>Пример события

В таблице ниже показан пример события.

| Имя свойства | Пример Vertipaq Query End | Описание свойства |
|---|---|---|
| EventClass | XM_SEQUERY_END | EventClass используется для классификации событий по категориям. |
| EventSubclass | 0 | EventSubclass предоставляет дополнительные сведения о каждом классе событий (например, 0: VertiPaq Scan). |
| RootActivityId | ff217fd2-611d-43c0-9c12-19e202a94f70 | Идентификатор корневой операции. |
| CurrentTime | 2018-04-06T18:30:11.9137358Z | Время начала события, если доступно. |
| StartTime | 2018-04-06T18:30:11.9137358Z | Время начала события, если доступно. |
| JobID | 0 | Идентификатор выполняемого задания. |
| ObjectID | 464 | Идентификатор объекта |
| ObjectType | 802012 | ObjectType |
| EndTime | 2018-04-06T18:30:11.9137358Z | Время окончания события. |
| Duration | 0 | Время (в миллисекундах), затраченное событием. |
| SessionType | User | Тип сеанса (какая сущность вызвала операцию). |
| ProgressTotal | 0 | Общий ход выполнения. |
| IntegerData | 0 | Целочисленные данные. |
| Severity | 0 | Уровень серьезности исключения. |
| Успешное завершение | 1 | 1 = успех. 0 = ошибка (например, 1 означает успешную проверку наличия разрешений, а 0 означает ошибку при этой проверке). |
| Ошибка | 0 | Номер ошибки определенного события. |
| ConnectionID | 3 | Уникальный идентификатор подключения. |
| DatasetID | 5eaa550e-06ac-4adf-aba9-dbf0e8fd1527 | Идентификатор набора данных, в котором выполняется инструкция пользователя. |
| SessionID | 3D063F66-A111-48EE-B960-141DEBDA8951 | Идентификатор GUID сеанса. |
| SPID | 180 | Идентификатор серверного процесса. Однозначно идентифицирует сеанс пользователя. Прямо соответствует идентификатору GUID сеанса, используемому XML/A. |
| ClientProcessID | null | Идентификатор процесса клиентского приложения. |
| ApplicationName | null | Имя клиентского приложения, установившего подключение к серверу. |
| CapacityName | pbi641fb41260f84aa2b778a85891ae2d97 | Имя ресурса емкости Power BI Embedded. |

### <a name="allmetrics"></a>AllMetrics

Если выбрать параметр **AllMetrics**, будут регистрироваться данные по всем метрикам, которые можно использовать с ресурсом Power BI Embedded.

В следующей таблице перечислены операции, связанные с Power BI Embedded, которые можно создавать в журнале действий.

## <a name="schemas"></a>Схемы

Power BI Embedded использует **выделенную схему Power BI**.

## <a name="next-steps"></a>Дальнейшие действия

>[!div class="nextstepaction"]
>[Мониторинг Azure Power BI Embedded](monitor-power-bi-embedded.md)

>[!div class="nextstepaction"]
>[Ведение журналов диагностики ресурсов Azure](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

>[!div class="nextstepaction"]
>[Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/Set-AzureRmDiagnosticSetting)
