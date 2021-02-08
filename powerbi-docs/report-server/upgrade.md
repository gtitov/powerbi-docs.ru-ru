---
title: Обновить сервер отчетов Power BI
description: Узнайте, как обновлять сервер отчетов Power BI.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 68494784e3c5b21c0c3e15bd5a3a816fd07e5f8b
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99043558"
---
# <a name="upgrade-power-bi-report-server"></a>Обновить сервер отчетов Power BI

Узнайте, как обновлять сервер отчетов Power BI.

 **Скачать** ![Значок скачивания](media/upgrade/download.png "Значок скачивания")

Чтобы скачать Сервер отчетов Power BI и приложение Power BI Desktop для Сервера отчетов Power BI, перейдите на страницу [Локальная работа с отчетами с использованием сервера Power BI Report Server](https://powerbi.microsoft.com/report-server/).

## <a name="before-you-begin"></a>Перед началом

Перед обновлением сервера отчетов советуем выполнить следующие шаги, чтобы создать его резервную копию.

### <a name="backing-up-the-encryption-keys"></a>Архивация ключей шифрования

При настройке установки сервера отчетов в первый раз выполните резервное копирование ключей шифрования. Кроме того, выполняйте резервное копирование ключей при каждом изменении удостоверения учетных записей службы или переименовании компьютера. Дополнительные сведения см. в разделе [Резервное копирование и восстановление ключей шифрования служб Reporting Services](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

### <a name="backing-up-the-report-server-databases"></a>Архивация баз данных сервера отчетов

Так как сервер отчетов является сервером без отслеживания состояния, все данные приложений хранятся в базах данных **reportserver** и **reportservertempdb**, выполняющихся на экземпляре ядра СУБД SQL Server. Вы можете создать резервные копии баз данных **reportserver** и **reportservertempdb** с помощью одного из поддерживаемых методов архивации баз данных SQL Server. Эти рекомендации относятся к базам данных сервера отчетов:

* Используйте полную модель восстановления для создания резервной копии базы данных **reportserver**.
* Используйте простую модель восстановления для создания резервной копии базы данных **reportservertempdb**.
* Можно использовать разные расписания для резервного копирования каждой базы данных. Единственная причина создания резервной копии базы данных **reportservertempdb** состоит в том, чтобы избежать ее повторного создания в случае сбоя оборудования. В случае сбоя оборудования нет необходимости восстанавливать данные в базе данных **reportservertempdb**, однако необходима структура таблицы. При утере базы данных **reportservertempdb** единственный способ вернуть ее — это повторно создать базу данных сервера отчетов. При повторном создании базы данных **reportservertempdb** важно, чтобы она имела то же имя, что и первичная база данных сервера отчетов.

Дополнительные сведения об архивации и восстановлении реляционных баз данных SQL Server см. в [этой статье](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).

### <a name="backing-up-the-configuration-files"></a>Архивация файлов конфигурации

Сервер отчетов Power BI использует файлы конфигурации для хранения настроек приложений. Архивируйте эти файлы при первой настройке сервера, а также после развертывания каких-либо пользовательских модулей. Необходимо создать резервные копии следующих файлов:

* config.json
* RSHostingService.exe.config;
* RSReportServer.config
* Rssvrpolicy.config
* Reportingservicesservice.exe.config;
* Web.config для приложений ASP.NET сервера отчетов;
* Machine.config для ASP.NET.

## <a name="upgrade-the-report-server"></a>Обновление сервера отчетов

Само по себе обновление сервера отчетов Power BI выполняется очень легко. Нужно выполнить лишь несколько действий по установке файлов.

1. Найдите папку с файлом PowerBIReportServer.exe и запустите установщик.

2. Щелкните **Обновить сервер отчетов Power BI**.

    ![Обновление Сервера отчетов Power BI](media/upgrade/reportserver-upgrade1.png "Обновить сервер отчетов Power BI")

3. Прочтите и примите условия лицензионного соглашения, а затем щелкните **Обновить**.

    ![Лицензионное соглашение](media/upgrade/reportserver-upgrade-eula.png "Лицензионное соглашение")

4. После успешного обновления щелкните **Настроить сервер отчетов**, чтобы запустить диспетчер конфигурации служб Reporting Services, или щелкните **Закрыть**, чтобы выйти из установщика.

    ![Конфигурация обновления](media/upgrade/reportserver-upgrade-configure.png)

## <a name="enable-microsoft-update-security-fixes-for-power-bi-report-server"></a>Включение исправлений безопасности Центра обновления Майкрософт для Сервера отчетов Power BI

Сервер отчетов Power BI получает исправления безопасности с помощью Центра обновления Майкрософт. Чтобы получить их, вручную предоставьте согласие на получение обновлений из Центра обновления Майкрософт.

1.  Откройте Центр обновления Windows в параметрах **Обновление и безопасность** на компьютере, который вы хотите использовать для получения обновлений.
2.  Выберите **Дополнительные параметры**.
3.  Установите флажок **При обновлении Windows предоставить обновления для других продуктов Майкрософт**.

## <a name="upgrade-power-bi-desktop"></a>Обновление Power BI Desktop

После обновления сервера отчетов необходимо, чтобы все авторы отчетов Power BI обновились до версии Power BI Desktop для Сервера отчетов Power BI, соответствующей версии сервера.

## <a name="next-steps"></a>Дальнейшие действия

* [Обзор функций администратора](admin-handbook-overview.md)  
* [Установка Power BI Desktop для Сервера отчетов Power BI](install-powerbi-desktop.md)  
* [Verify a Reporting Services installation](/sql/reporting-services/install-windows/verify-a-reporting-services-installation) (Проверка установки служб Reporting Services)  
* [Configure the Report Server Service Account (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager) (Настройка учетной записи службы сервера отчетов (System Center Configuration Manager))  
* [Configure Report Server URLs (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager) (Настройка URL-адресов сервера отчетов (System Center Configuration Manager))  
* [Configure a Report Server Database Connection (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager) (Настройка подключения к базе данных сервера отчетов (System Center Configuration Manager))  
* [SSRS Encryption Keys — Initialize a Report Server](/sql/reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server) (Ключи шифрования SSRS — инициализация сервера отчетов)  
* [Configure SSL Connections on a Native Mode Report Server](/sql/reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server) (Настройка подключений SSL на сервере отчетов в основном режиме)  
* [Configure Windows Service Accounts and Permissions](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) (Настройка учетных записей и разрешений службы Windows)  
* [Поддержка браузера для сервера отчетов Power BI](browser-support.md)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)