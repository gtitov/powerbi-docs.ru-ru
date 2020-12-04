---
title: Устранение неполадок запланированного обновления в решении "Сервер отчетов Power BI"
description: Ресурсы для устранения неполадок запланированного обновления в решении "Сервер отчетов Power BI".
author: maggiesMSFT
ms.author: maggies
ms.reviewer: kayu
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: troubleshooting
ms.date: 11/01/2017
ms.openlocfilehash: 8cb8bf4e6d67f01f7bbdc4370d8a60691dba5a63
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96418286"
---
# <a name="troubleshoot-scheduled-refresh-in-power-bi-report-server"></a>Устранение неполадок запланированного обновления в решении "Сервер отчетов Power BI"
Ресурсы для устранения неполадок запланированного обновления в решении "Сервер отчетов Power BI".

При обнаружении проблем в эту статью будет добавляться новая информация.

## <a name="common-issues"></a>Распространенные проблемы
Ниже описаны самые распространенные проблемы, с которыми вы можете столкнуться при попытке запланировать обновление отчета. 

### <a name="driver-related-problems"></a>Проблемы с драйвером
Для подключения к различным источникам данных могут потребоваться драйверы сторонних производителей. Их нужно установить не только на компьютере, на котором вы работаете с Power BI Desktop, но и на сервере отчетов.

Драйвер может быть 32-разрядной и 64-разрядной версии. Устанавливайте 64-разрядную версию драйвера, поскольку используется 64-разрядная версия решения "Сервер отчетов Power BI".

Инструкциями по установке и настройке драйверов сторонних поставщиков можно получить у производителя.

### <a name="memory-pressure"></a>Нехватка памяти
Если для обработки и отображения отчетов требуется значительная емкость, может возникнуть нехватка памяти. При планировании обновлений отчетов может использоваться значительный объем памяти на компьютере. Особенно это касается больших отчетов. Нехватка памяти может привести к ошибкам при создании отчетов, а также к сбою на самом сервере отчетов.

При систематической нехватке памяти проверьте развертывание сервера отчетов, чтобы распределить нагрузку на ресурсы. Также нужно определить, используется ли сервер отчетов для обновления данных с параметром `IsDataModelRefreshService` в файле rsreportserver.config. С помощью этого параметра можно назначить один сервер (или несколько серверов) сервером переднего плана для обработки в отчетов по запросу, а другой набор серверов можно использовать только для запланированного обновления.

Сведения о мониторинге экземпляра Analysis Services см. в статье [Наблюдение за экземпляром служб Analysis Services](/sql/analysis-services/instances/monitor-an-analysis-services-instance).

Сведения о параметрах памяти служб Analysis Services см. в статье [Свойства памяти](/sql/analysis-services/server-properties/memory-properties).

### <a name="kerberos-configuration"></a>Конфигурация Kerberos
Чтобы подключиться к источнику данных с помощью учетных данных Windows, может потребоваться настроить ограниченное делегирование Kerberos. Дополнительные сведения о настройке ограниченного делегирования Kerberos см. в статье [Настройка Kerberos для использования отчетов Power BI](configure-kerberos-powerbi-reports.md).

## <a name="known-issues"></a>Известные проблемы
По мере доступности здесь будут отображаться сведения об известных проблемах.

## <a name="configuration-settings"></a>Параметры конфигурации
С помощью этих параметров можно изменить запланированное обновление. Настройки, заданные в SQL Server Management Studio (SSMS), применяются ко всем серверам отчетов в развертывании. Параметры, заданные в файле rsreportserver.config, применяются к конкретному серверу.

**Параметры в SSMS**

| Параметр | Описание |
| --- | --- |
| MaxFileSizeMb |Максимальный размер файла для передаваемых отчетов. Значение по умолчанию — 1000 МБ (1 ГБ). Максимальное значение — 2000 МБ (2 ГБ). |
| ModelCleanupCycleMinutes |Определяет, как часто модель проверяется, чтобы вытеснить ее из памяти. Значение по умолчанию — 15 минут. |
| ModelExpirationMinutes |Определяет время до истечения срока действия модели с учетом ее последнего использования и вытеснения. Значение по умолчанию — 60 минут. |
| ScheduleRefreshTimeoutMinutes |Определяет, сколько может длиться обновление данных в определенном режиме. Значение по умолчанию — 120 минут. Верхнее ограничение отсутствует. |

**Параметры в файле rsreportserver.config**

```xml
<Configuration>
    <Service>
        <PollingInterval>10</PollingInterval>
        <IsDataModelRefreshService>false</IsDataModelRefreshService>
        <MaxQueueThreads>0</MaxQueueThreads>
    </Service>
</Configuration>
```

## <a name="tools-for-troubleshooting"></a>Инструменты для устранения неполадок
### <a name="logs-relevant-for-scheduled-refresh-of-power-bi-reports"></a>Журналы, которые касаются запланированного обновления отчетов Power BI
Файлы журналов RSPowerBI_ logs содержат сведения о запланированном обновлении. Они находятся в папке LogFiles в расположении, где установлен сервер отчетов. 

```
C:\Program Files\Microsoft Power BI Report Server\PBIRS\LogFiles\RSPowerBI_*.log
```

**Условие ошибки**

```
2017-10-20 02:00:09.5188|ERROR|744|Error Processing Data Model Refresh: SessionId: e960c25e-ddd4-4763-aa78-0e5dceb53472, Status: Error Model can not be refreshed because not all the data sources are embedded, Exception Microsoft.PowerBI.ReportServer.AsServer.InvalidDataSourceException: Model can not be refreshed because not all the data sources are embedde
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.AnalysisServicesDataRefresh.CanModelRefresh(IEnumerable`1 dataSources)
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<>c__DisplayClass7.<ExecuteActionWithLogging>b__5()
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<ExecuteFuncWithLogging>d__1`1.MoveNext()
```

**_Успешное обновление_* _

```
2017-10-25 15:23:41.9370|INFO|6|Handling event with data: TimeEntered: 10/25/2017 8:23:41 PM, Type: Event, SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, EventType: DataModelRefresh
2017-10-25 15:23:41.9370|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Data Refresh.
2017-10-25 15:23:41.9370|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Retrieving PBIX AsDatabaseInfo.
2017-10-25 15:23:42.7134|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Verifying all the data sources are embedded.
2017-10-25 15:23:42.7134|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Verifying connection strings are valid.
2017-10-25 15:23:42.7134|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Streaming model to Analysis Server.
2017-10-25 15:23:42.7603|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Refreshing the model.
2017-10-25 15:23:51.5258|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Removing credentials from the model.
2017-10-25 15:23:51.6508|INFO|6|Processing Data Model Refresh: SessionId: 46d398db-0b1f-49d8-b7bd-c5461c07ec7a, Status: Starting Saving model to the catalog.
```

_ *Неправильные учетные данные**

```
2017-10-20 08:22:01.5595|INFO|302|Processing Data Model Refresh: SessionId: 22cd9ec3-b21a-4eb1-81ae-15fac8d379ea, Status: Starting Refreshing the model.
2017-10-20 08:22:02.3758|ERROR|302|Error Processing Data Model Refresh: SessionId: 22cd9ec3-b21a-4eb1-81ae-15fac8d379ea, Status: Error Failed to refresh the model, Exception Microsoft.AnalysisServices.OperationException: Failed to save modifications to the server. Error returned: 'The credentials provided for the SQL source are invalid. (Source at rosecatalog;reportserver.). The exception was raised by the IDbCommand interface.
'.
   at Microsoft.AnalysisServices.Tabular.Model.SaveChanges(SaveOptions saveOptions)
   at Microsoft.PowerBI.ReportServer.AsServer.TOMWrapper.RefreshModel(Database database)
   at Microsoft.PowerBI.ReportServer.AsServer.AnalysisServicesServer.RefreshDatabase(String databaseName, IEnumerable`1 dataSources)
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.AnalysisServicesDataRefresh.RefreshDatabase(AsDatabaseInfo asDatabaseInfo)
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<>c__DisplayClass7.<ExecuteActionWithLogging>b__5()
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<ExecuteFuncWithLogging>d__1`1.MoveNext()
2017-10-20 08:22:02.4588|ERROR|302|Error Processing Data Model Refresh: SessionId: 22cd9ec3-b21a-4eb1-81ae-15fac8d379ea, Status: Error Failed Data Refresh, Exception Microsoft.AnalysisServices.OperationException: Failed to save modifications to the server. Error returned: 'The credentials provided for the SQL source are invalid. (Source at rosecatalog;reportserver.). The exception was raised by the IDbCommand interface.
'.
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.ExecuteActionWithLogging(Action methodToExecute, String description, String localizedDescription, String messageInFailure, RefreshInfo refreshInfo, DataAccessors dataAccessors, ReportEventType operation, Int64 size, Boolean isDataRetrieval, Boolean showInExecutionLog)
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.AnalysisServicesDataRefresh.RefreshData(RefreshInfo refreshInfo)
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<>c__DisplayClass7.<ExecuteActionWithLogging>b__5()
   at Microsoft.PowerBI.ReportServer.WebHost.EventHandler.DataRefreshScope.<ExecuteFuncWithLogging>d__1`1.MoveNext()
```

#### <a name="enabling-verbose-logging"></a>Включение записи подробных сведений в журнал
Запись подробных сведений в журнал в решении "Сервер отчетов Power BI" включается так же, как и для SQL Server Reporting Services.

1. Откройте файл `<install directory>\PBIRS\ReportServer\bin\ReportingServicesService.exe.config`.
2. В разделе `<system.diagnostics>` присвойте параметру **DefaultTraceSwitch** значение **4**.
3. В разделе `<RStrace>` присвойте параметру **Components** значение **all:4**. 

### <a name="executionlog"></a>Журнал выполнения
При отображении отчета Power BI или планировании обновления новые записи добавляются в журнал выполнения в базе данных. Эти записи доступны в представлении **ExecutionLog3** в базе данных каталога на сервере отчетов.

Записи в журнале выполнения для отчетов Power BI отличаются от записей для отчетов других типов.

* Столбцы TimeRendering всегда имеют значение 0. Отображение отчетов Power BI выполняется в браузере, а не на сервере.
* Есть два типа запросов и последующих действий с элементом:
  * **Interactive** — при каждом просмотре отчета.
    * **ASModelStream** — когда модель данных передается в Analysis Services из каталога.
    * **ConceptualSchema** — когда пользователь выбирает просмотр отчета.
    * **QueryData** — при каждом запросе данных от клиента.
  * **Refresh Cache** — при каждом выполнении запланированного обновления.
    * **ASModelStream** — при каждой передаче модели данных в Analysis Services из каталога.
    * **DataRefresh** — при каждом обновлении данных из одного или нескольких источников.
    * **SaveToCatalog** — при каждом сохранении модели данных в каталог.

## <a name="analysis-services"></a>Analysis Services
Иногда может потребоваться изменить Analysis Services из-за проблем с диагностикой или настроить ограничения памяти.

> [!IMPORTANT]
> Эти параметры сбрасываются при каждом обновлении сервера отчетов. Обязательно сохраните копию изменений и при необходимости повторно применяйте их.
> 
> 

### <a name="install-location"></a>Расположение установки
По умолчанию решение "Сервер отчетов Power BI" и службы Analysis Services находятся в этой папке:

`C:\Program Files\Microsoft Power BI Report Server\PBIRS\ASEngine`

### <a name="configuring-analysis-services-settings-msmdsrvini"></a>Настройка параметров Analysis Services (msmdsrv.ini)
В каталоге `<install directory>\PBIRS\ASEngine` есть файл *msmdsrv.ini*, который можно использовать для управления разными параметрами Analysis Services. Когда вы откроете этот файл, то увидите, что он не содержит все нужные вам параметры. 

Это связано с тем, что фактический процесс Analysis Services, который выполняется в решении "Сервер отчетов Power BI", запускается в `<install directory>\PBIRS\ASEngine\workspaces`. В этой папке содержится полный файл *msmdsrv.ini*, с которым вы привыкли работать. Очень важно не изменять файл в папке рабочих областей, так как он перезаписывается каждый раз, когда запускается процесс Analysis Services. Если нужно изменить параметр, сделайте это в файле msmdsrv.ini в каталоге `<install directory>\PBIRS\ASEngine`.

Указанные ниже параметры сбрасываются при каждом запуске процесса Analysis Services. Все изменения, внесенные в эти параметры, будут игнорироваться.

* ConfigurationSettings\PrivateProcess
* ConfigurationSettings\DataDir
* ConfigurationSettings\LogDir
* ConfigurationSettings\TempDir
* ConfigurationSettings\BackupDir
* ConfigurationSettings\AllowedBrowsingFolders
* ConfigurationSettings\CrashReportsFolder
* ConfigurationSettings\ExtensionDir
* ConfigurationSettings\Port
* ConfigurationSettings\DeploymentMode
* ConfigurationSettings\ServerLocation
* ConfigurationSettings\TMCompatabilitySKU
* ConfigurationSettings\FlightRecorder\TraceDefinitionFile

### <a name="profiling-the-local-analysis-services-process"></a>Профилирование локального процесса Analysis Services
Для локального процесса Analysis Services в целях диагностики можно выполнить трассировку SQL Profiler. Чтобы подключиться к локальному экземпляру Analysis Services, выполните описанные ниже действия.

Трассировка SQL Server Profiler включена в файл [загрузки SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms).

1. Запустите **SQL Server Profiler** от имени администратора.
2. Нажмите кнопку **Создать трассировку**.
3. В диалоговом окне **Подключение к серверу** выберите **Analysis Services** и введите имя сервера **localhost:5132**.
4. В диалоговом окне **Свойства трассировки** выберите события для записи и нажмите кнопку **Выполнить**.

## <a name="lock-pages-in-memory-windows-privilege"></a>Право доступа Windows "Блокировка страниц в памяти"
Если отчет Power BI не отображается, назначьте право доступа **блокировка страниц в памяти** для учетной записи служб, с которой работает решение "Сервер отчетов Power BI". Дополнительные сведения о настройке **блокировки страниц в памяти** см. в разделе [Права доступа Windows, назначенные учетной записи служб Analysis Services](/sql/analysis-services/instances/configure-service-accounts-analysis-services#bkmk_winpriv).

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)