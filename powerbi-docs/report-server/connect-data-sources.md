---
title: Источники данных для отчетов с разбивкой на страницы в решении "Сервер отчетов Power BI"
description: Сведения о том, к каким источникам данных могут подключаться отчеты с разбивкой на страницы (RDL) в решении "Сервер отчетов Power BI".
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: conceptual
ms.date: 06/26/2020
ms.openlocfilehash: 4559995baa7d3e0b5796ca6076687c26c4a0854d
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96415388"
---
# <a name="paginated-report-data-sources--in-power-bi-report-server"></a>Источники данных для отчетов с разбивкой на страницы в решении "Сервер отчетов Power BI"
Отчеты Reporting Services с разбивкой на страницы в решении "Сервер отчетов Power BI" поддерживают те же источники данных, которые используются в SQL Server Reporting Services. См. дополнительные сведения об [источниках данных, поддерживаемых службами Reporting Services](/sql/reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs).

## <a name="connect-to-oracle-data-sources-with-useinstalleduiculture"></a>Подключение к источникам данных Oracle с помощью UseInstalledUICulture

Для подключения к источникам данных Oracle Сервер отчетов Power BI использует поставщик данных Oracle для .NET (ODP.NET), который не зависит от NLS.

По умолчанию для загрузки ODP.NET сервер отчетов использует язык и региональные параметры пользовательского интерфейса первого клиента.  В результате до перезапуска службы все последующие подключения с сервера отчетов к Oracle будут использовать первоначальные язык и региональные параметры пользовательского интерфейса.  Такой подход может вызвать проблемы при преобразовании отчета для просмотра из-за несовпадений в форматировании языка и региональных параметров пользовательского интерфейса.

Чтобы обеспечить лучшую работу в Сервере отчетов Power BI, мы предоставили параметр конфигурации с именем UseInstalledUICulture. Если для UseInstalledUICulture задано значение true, сервер отчетов всегда будет загружать ODP.NET, используя язык и региональные параметры пользовательского интерфейса сервера, а не первого клиента.
Этот параметр доступен в Сервере отчетов Power BI, начиная с выпуска службы за март 2020 г.

Чтобы включить эту функцию, измените запись расширения ORACLE в файле rsreportserver.config, как показано ниже.
```xml
<Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions">
    <Configuration>
        <UseInstalledUICulture>true</UseInstalledUICulture>
    </Configuration>
</Extension>
```

## <a name="next-steps"></a>Дальнейшие действия
Подключившись к источнику данных, [создайте отчет с разбивкой на страницы](quickstart-create-paginated-report.md).  


Остались вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)