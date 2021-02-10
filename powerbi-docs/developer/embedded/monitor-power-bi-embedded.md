---
title: Мониторинг Power BI Embedded
description: Узнайте, как выполнять мониторинг Power BI Embedded.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.custom: subject-monitoring
ms.topic: how-to
ms.date: 01/14/2021
ms.openlocfilehash: 5cea43f4be9a3fee7c2fb0f99ef0acef99bb8364
ms.sourcegitcommit: f17acb16018752c234db6bff1f51f5130be12c58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99617003"
---
# <a name="monitor-power-bi-embedded"></a>Мониторинг Power BI Embedded

При наличии критически важных приложений и бизнес-процессов, использующих ресурсы Azure, необходимо отслеживать эти ресурсы на предмет их доступности, производительности и работы. В этой статье описываются данные мониторинга, создаваемые Power BI Embedded, а также способы использования функций Azure Monitor для анализа этих данных и отправки оповещений о них.

## <a name="monitor-overview"></a>Общие сведения о мониторинге

Страница **Обзор** на портале Azure для каждого экземпляра *Power BI Embedded* содержит следующие сведения:

* **Группа ресурсов** — [группа ресурсов](/azure/azure-resource-manager/management/overview#resource-groups), которой принадлежит экземпляр.
* **Состояние** — состояние экземпляра Power BI Embedded.
* **Расположение** — расположение экземпляра Power BI Embedded.
* **Имя ресурса** — имя экземпляра Power BI Embedded.
* **SKU** — номер SKU, который использует экземпляр Power BI Embedded.
* **Имя подписки** — имя подписки на экземпляр Power BI Embedded.
* **Идентификатор подписки** — идентификатор подписки на экземпляр Power BI Embedded.

## <a name="what-is-azure-monitor"></a>Общие сведения об Azure Monitor

*Power BI Embedded* создает данные мониторинга с помощью [Azure Monitor](/azure/azure-monitor/overview). Это комплексная служба мониторинга в Azure, которая предоставляет полный набор функций для мониторинга ресурсов Azure наряду с ресурсами в других облаках и локальных средах.

Начните со статьи [Мониторинг ресурсов Azure с помощью Azure Monitor](/azure/azure-monitor/insights/monitor-azure-resource), в которой описаны следующие понятия:

- Общие сведения об Azure Monitor
- затраты, связанные с мониторингом;
- данные мониторинга, собираемые в Azure;
- настройка сбора данных;
- стандартные средства Azure для анализа данных мониторинга и оповещения.

В следующих разделах, основанных на этой статье, описываются определенные данные, собираемые для Power BI Embedded, и приводятся примеры настройки сбора и анализа этих данных с помощью средств Azure.

## <a name="monitoring-data"></a>Данные мониторинга

Power BI Embedded собирает данные мониторинга тех же типов, что и другие ресурсы Azure, описанные в статье [Мониторинг ресурсов Azure с помощью Azure Monitor](/azure/azure-monitor/insights/monitor-azure-resource#monitoring-data-from-Azure-resources).

Дополнительные сведения о метриках и журналах, созданных Power BI Embedded, см. в статье [Справочник по данным мониторинга *Power BI Embedded*](monitor-power-bi-embedded-reference.md).

## <a name="collection-and-routing"></a>Сбор и маршрутизация

Метрики платформы и журнал действий собираются и сохраняются автоматически, но их можно направить в другие расположения с помощью параметра диагностики.  

Журналы ресурсов не собираются и не сохраняются, пока вы не создадите параметр диагностики и не направите их в одно или несколько расположений.

Подробный процесс создания параметров диагностики с помощью портала Azure, интерфейса командной строки или PowerShell см. в статье [Создание параметров диагностики для отправки журналов платформы и метрик в разные места назначения](/azure/azure-monitor/platform/diagnostic-settings). Создавая параметр диагностики, нужно указать, какие категории журналов должны собираться. Категории для *Power BI Embedded* перечислены в статье [Справочник по данным мониторинга Power BI Embedded](monitor-power-bi-embedded-reference.md#resource-logs).

### <a name="using-powershell-to-enable-diagnostics"></a>Включение диагностики с помощью PowerShell

Чтобы включить метрики и ведение журналов диагностики с помощью PowerShell, используйте приведенные ниже команды. Дополнительные сведения об использовании PowerShell для включения диагностики см. в статье [Создание и настройка рабочей области Log Analytics в Azure Monitor с помощью PowerShell](/azure/azure-monitor/platform/powershell-workspace-configuration).

* Выполните приведенную ниже команду, чтобы включить отправку журналов диагностики в учетную запись хранения:

    ```powershell
    Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
    ```
    Идентификатор учетной записи хранения — это идентификатор ресурса учетной записи хранения, в которую будут отправляться журналы.

* Чтобы включить потоковую передачу журналов диагностики в концентратор событий, используйте следующую команду:

    ```powershell
    Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
    ```
* Идентификатор правила служебной шины Azure — это строка в формате:

    ```powershell
    {service bus resource ID}/authorizationrules/{key name}
    ```

* Чтобы включить отправку журналов диагностики в рабочую область Log Analytics, используйте следующую команду:

    ```powershell
        Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
    ```

* Идентификатор ресурса рабочей области Log Analytics можно получить с помощью следующей команды:

    ```powershell
    (Get-AzureRmOperationalInsightsWorkspace).ResourceId
    ```

Можно объединять эти параметры, чтобы получить несколько вариантов вывода.

Собираемые метрики и журналы обсуждаются в следующих разделах.

## <a name="analyzing-metrics"></a>Анализ метрик

Вы можете анализировать метрики *Power BI Embedded* и метрики из других служб Azure с помощью обозревателя метрик, открыв раздел **Метрики** в меню **Azure Monitor**. Подробные сведения об использовании этого средства см. в статье [Начало работы с обозревателем метрик Azure](/azure/azure-monitor/platform/metrics-getting-started).

Список метрик платформы, собранных для Power BI Embedded, см. в разделе [Справочник по данным мониторинга *Power BI Embedded*](monitor-power-bi-embedded-reference.md#metrics).  

Для справки можно просмотреть список [всех метрик ресурсов, поддерживаемых Azure Monitor](/azure/azure-monitor/platform/metrics-supported).

## <a name="analyzing-logs"></a>анализ журналов;

Данные в журналах Azure Monitor хранятся в таблицах, и каждая таблица имеет собственный набор уникальных свойств.  

Все журналы ресурсов в Azure Monitor имеют те же поля, за которыми следуют поля, связанные со службой. Общая схема описана в статье [Распространенная и связанная со службой схема для журналов ресурсов Azure](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-schema#top-level-resource-logs-schema). Схему для журналов ресурсов Power BI Embedded см. в статье [Справочник по данным Power BI Embedded](monitor-power-bi-embedded-reference.md#schemas).

[Журналы действий](/azure/azure-monitor/platform/activity-log) — это средство платформы Azure, которое предоставляет представление о событиях уровня подписки. Вы можете просмотреть их независимо или направить в журналы Azure Monitor, где можно выполнять гораздо более сложные запросы с помощью Log Analytics.  

Список типов журналов ресурсов, собранных для Power BI Embedded, см. в статье [Справочник по данным мониторинга Power BI Embedded](monitor-power-bi-embedded-reference.md#resource-logs).  

Список таблиц, используемых Azure Monitor журналами и запрашиваемых Log Analytics, см. в статье [Справочник по данным мониторинга Power BI Embedded](monitor-power-bi-embedded-reference.md#azure-monitor-logs-tables).  

### <a name="sample-kusto-queries"></a>Примеры запросов Kusto

> [!IMPORTANT]
> Когда вы выберете **Журналы** в меню Power BI Embedded, откроется Log Analytics с областью запроса, для которой задан текущий ресурс Power BI Embedded. Это означает, что запросы к журналам будут содержать данные только из этого ресурса. Если необходимо выполнить запрос, включающий данные из другого ресурса Power BI Embedded или других служб Azure, выберите **Журналы** в меню **Azure Monitor**. Подробные сведения см. в статье [Область запросов журнала и временной диапазон в Azure Monitor Log Analytics](/azure/azure-monitor/log-query/scope/).

Ниже приведены примеры запросов для мониторинга Power BI Embedded.

* Это запрос, который завершается менее чем за пять минут (300 000 миллисекунд).

    ```Kusto
        search *
        | where Type == "AzureDiagnostics"
        | where ( OperationName == "QueryEnd" )
        | where toint(Duration_s) < 300000   
    ```
* Определение имен емкостей.

    ```Kusto
        search *
        | where Type == "AzureDiagnostics"
        | where ( OperationName == "QueryEnd" )
        | where toint(Duration_s) < 300000   
    ```

## <a name="alerts"></a>видны узлы

Оповещения Azure Monitor заблаговременно уведомляют вас при обнаружении важных условий в данных мониторинга. Они позволяют выявлять и устранять проблемы в системе до того, как ваши клиенты заметят их. Оповещения можно настроить для [метрик](/azure/azure-monitor/platform/alerts-metric-overview), [журналов](/azure/azure-monitor/platform/alerts-unified-log) и [журнала действий](/azure/azure-monitor/platform/activity-log-alerts).

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о ведении журналов диагностики ресурсов Azure:

>[!div class="nextstepaction"]
>[Справочник по данным мониторинга Power BI Embedded](monitor-power-bi-embedded-reference.md)

>[!div class="nextstepaction"]
>[Мониторинг ресурсов Azure с помощью Azure Monitor](/azure/azure-monitor/insights/monitor-azure-resource)
