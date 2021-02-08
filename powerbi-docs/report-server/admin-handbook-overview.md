---
title: Общие сведения об администрировании Сервера отчетов Power BI
description: В этой статье описано, как администрировать Сервер отчетов Power BI — локальное расположение для хранения и администрирования ваших отчетов Power BI, мобильных отчетов и отчетов с разбивкой на страницы.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: conceptual
ms.date: 05/22/2019
ms.openlocfilehash: 9b4b7557a977c5975920e0ef414b7daf8183c062
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99044248"
---
# <a name="admin-overview-power-bi-report-server"></a>Общие сведения об администрировании Сервера отчетов Power BI
В этой статье описано, как администрировать Сервер отчетов Power BI — локальное расположение для хранения и администрирования ваших отчетов Power BI, мобильных отчетов и отчетов с разбивкой на страницы. В этом руководстве описаны концепции планирования, развертывания и администрирования Сервера отчетов Power BI и приведены ссылки на дополнительные материалы.

![Снимок экрана сервера отчетов Power BI с параметрами входа](media/admin-handbook-overview/admin-handbook.png)
 
## <a name="installing-and-migration"></a>Установка и миграция
Чтобы начать использовать Сервер отчетов Power BI, его нужно установить. Выполнение этой задачи описывается в ряде статей.

Перед началом установки, обновления или миграции на Сервер отчетов Power BI просмотрите [требования к системе](system-requirements.md) для сервера отчетов.

### <a name="installing"></a>Установка
Развертывая новый сервер отчетов Power BI, ознакомьтесь со следующими материалами. 

[Установка сервера отчетов Power BI](install-report-server.md)

### <a name="migration"></a>Миграция
Для SQL Server Reporting Services обновление на месте не поддерживается. Если у вас есть экземпляр SQL Server Reporting Services, который нужно сделать Сервером отчетов Power BI, необходимо выполнить перенос. Миграцию может потребоваться выполнить и по иным причинам. Дополнительные сведения см. в документации по миграции.

[Миграция установки сервера отчетов](migrate-report-server.md)

## <a name="configuring-your-report-server"></a>Настройка сервера отчетов
Настройка сервера отчетов предусматривает разные возможности. Будет ли использоваться SSL? Будет ли настроен почтовый сервер? Нужно ли интегрировать службу Power BI, чтобы закреплять визуализации?

Настройка преимущественно будет выполняться в диспетчере конфигурации сервера отчетов. Дополнительные сведения см. в документации по [диспетчеру настройки](/sql/reporting-services/install-windows/reporting-services-configuration-manager-native-mode).

## <a name="security"></a>Безопасность
Любая организация стремится обезопасить свои данные. Дополнительные сведения об аутентификации, авторизации, ролях и разрешениях см. в документации по [обеспечению безопасности](/sql/reporting-services/security/reporting-services-security-and-protection).

## <a name="next-steps"></a>Дальнейшие действия
[Установка сервера отчетов Power BI](install-report-server.md)  
[Поиск ключа продукта сервера отчетов](find-product-key.md)  
[Установка Power BI Desktop для Сервера отчетов Power BI](install-powerbi-desktop.md)  
[Загрузка построителя отчетов](https://www.microsoft.com/download/details.aspx?id=53613)  
[Download SQL Server Data Tools (SSDT)](/sql/ssdt/download-sql-server-data-tools-ssdt) (Скачивание SQL Server Data Tools (SSDT))

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)