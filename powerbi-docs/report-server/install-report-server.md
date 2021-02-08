---
title: Установка сервера отчетов Power BI
description: Узнайте, как установить сервер отчетов Power BI.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 01/16/2020
ms.openlocfilehash: 3347bb18306497781ab5915225db8c3e071cfa3f
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99044110"
---
# <a name="install-power-bi-report-server"></a>Установка сервера отчетов Power BI

Узнайте, как установить сервер отчетов Power BI.

## <a name="download-power-bi-report-server"></a>Скачивание сервера отчетов Power BI

На странице [Локальная работа с отчетами с использованием Сервера отчетов Power BI](https://powerbi.microsoft.com/report-server/) выберите **Download free trial** (Скачать бесплатную пробную версию).

При запуске файла PowerBIReportServer.exe вы можете выбрать бесплатную пробную версию или ввести ключ продукта. Чтобы получить дополнительные сведения, продолжите чтение.

## <a name="before-you-install"></a>Подготовка к установке

Прежде чем устанавливать Сервер отчетов Power BI, рекомендуем ознакомиться с [требованиями к оборудованию и программному обеспечению для установки Сервера отчетов Power BI](system-requirements.md).

 > [!IMPORTANT]
 > Сервер отчетов Power BI можно установить в среде, имеющей контроллер домена только для чтения (RODC), но для правильной работы ему необходим доступ к контроллеру домена для чтения и записи. Если Сервер отчетов Power BI имеет доступ только к RODC, при попытке администрирования службы могут возникнуть ошибки.

### <a name="power-bi-report-server-product-key"></a>Ключ продукта сервера отчетов Power BI

Ключ продукта для Сервера отчетов Power BI можно получить из двух различных источников:

- Power BI Premium
- SQL Server Enterprise Software Assurance (SA)

Чтобы получить дополнительные сведения, продолжите чтение.

#### <a name="power-bi-premium"></a>Power BI Premium

Если вы приобрели Power BI Premium, то сможете получить ключ продукта для Сервера отчетов Power BI на вкладке **Параметры Premium** портала администрирования Power BI. Портал администрирования доступен только глобальным администраторам или пользователям, которым назначена роль "Администратор службы Power BI".

![Параметры Premium](../report-server/media/install-report-server/pbirs-product-key.png "Ключ Сервера отчетов Power BI в параметрах версии Premium")

Выберите **Ключ сервера отчетов Power BI**, и появится диалоговое окно с вашим ключом продукта. Вы можете скопировать его и использовать при установке.

![Ключ продукта](../report-server/media/install-report-server/pbirs-product-key-dialog.png "Ключ продукта сервера отчетов Power BI")

#### <a name="sql-server-enterprise-software-assurance-sa"></a>SQL Server Enterprise Software Assurance (SA)

Если вы заключили соглашение SQL Server Enterprise SA, то можете получить ключ продукта на веб-сайте [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/).

## <a name="install-your-report-server"></a>Установка сервера отчетов

Сама по себе установка Сервера отчетов Power BI выполняется очень легко. Чтобы установить его, нужно выполнить совсем немного действий.

Для установки вам не требуется ядро СУБД SQL Server. После установки нужно будет настроить службы отчетов Reporting Services.

1. Найдите папку с файлом PowerBIReportServer.exe и запустите установщик.

2. Выберите **Install Power BI Report Server** (Установить сервер отчетов Power BI).

    ![Установка сервера отчетов Power BI](media/install-report-server/pbireportserver-install.png)
3. Выберите выпуск, который нужно установить, и нажмите кнопку **Далее**.

    ![Выбор выпуска](media/install-report-server/pbireportserver-choose-edition.png)

    Выберите выпуск Evaluation или Developer.

    ![Выпуск 2](media/install-report-server/pbireportserver-choose-edition2.png)

    В противном случае введите ключ продукта для сервера, полученный из службы Power BI или на сайте Volume License Service Center. Дополнительные сведения о получении ключа продукта см. в разделе [Подготовка к установке](#before-you-install) выше.
4. Прочтите и примите условия лицензионного соглашения, а затем нажмите кнопку **Далее**.

    ![Условия лицензионного соглашения](media/install-report-server/pbireportserver-eula.png)
5. Для хранения базы данных сервера отчетов требуется ядро СУБД. Нажмите кнопку **Далее**, чтобы установить только сервер отчетов.

    ![Установка только файлов](media/install-report-server/pbireportserver-install-files-only.png)
6. Укажите расположение установки для сервера отчетов. Нажмите кнопку **Установить**, чтобы продолжить.

    ![Указание пути установки](media/install-report-server/pbireportserver-install-file-path.png)

    Путь по умолчанию: C:\Program Files\Microsoft Power BI Report Server.

7. После успешной установки нажмите кнопку **Настроить сервер отчетов**, чтобы запустить диспетчер конфигурации служб Reporting Services.

    ![Настройка сервера отчетов](media/install-report-server/pbireportserver-configure.png)

## <a name="configure-your-report-server"></a>Настройка сервера отчетов

Если нажать кнопку **Настроить сервер отчетов** в программе установки, откроется диспетчер конфигурации служб Reporting Services. Дополнительные сведения см. в статье о [диспетчере конфигурации служб Reporting Services](/sql/reporting-services/install-windows/reporting-services-configuration-manager-native-mode).

Для завершения начальной настройки Reporting Services необходимо [создать базу данных сервера отчетов](/sql/reporting-services/install-windows/ssrs-report-server-create-a-report-server-database). Для выполнения этого шага требуется сервер базы данных SQL Server.

### <a name="creating-a-database-on-a-different-server"></a>Создание базы данных на другом сервере

Если для создания базы данных сервера отчетов вы используете сервер базы данных на другом компьютере, необходимо изменить учетную запись службы для сервера отчетов на учетные данные, принимаемые сервером базы данных. 

По умолчанию сервер отчетов использует учетную запись виртуальной службы. При попытке создать базу данных на другом сервере может появиться следующая ошибка на этапе применения прав на подключение.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Чтобы устранить ее, измените учетную запись службы на учетную запись сетевой службы или учетную запись домена. Если изменить учетную запись службы на учетную запись сетевой службы, будут применены права в контексте учетной записи компьютера сервера отчетов.

![Настройка учетной записи службы сервера отчетов](media/install-report-server/pbireportserver-configure-account.png)

Дополнительные сведения см. в разделе [Настройка учетной записи службы сервера отчетов](/sql/reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager).

## <a name="windows-service"></a>Служба Windows

Служба Windows создается в процессе установки. Она отображается как **сервер отчетов Power BI**. Имя службы — **PowerBIReportServer**.

![Служба Windows сервера отчетов](media/install-report-server/pbireportserver-windows-service.png)

![Свойства службы Windows сервера отчетов](media/install-report-server/pbireportserver-windows-service2.png)

## <a name="default-url-reservations"></a>Резервирование URL-адресов по умолчанию

Резервирование URL-адреса состоит из префикса, имени узла, порта и виртуального каталога.

| Часть | Описание |
| --- | --- |
| Префикс |Префикс по умолчанию — HTTP. Если сертификат SSL уже установлен, программа установки попытается создать резервирование URL-адресов с префиксом HTTPS. |
| Имя узла |Имя узла по умолчанию является строгим подстановочным знаком (+). Он указывает, что сервер отчетов принимает все HTTP-запросы в заданном порте для любого имени узла, который соответствует компьютеру, включая `https://<computername>/reportserver`, `https://localhost/reportserver` или `https://<IPAddress>/reportserver.` |
| Порт |Порт по умолчанию — 80. Если используется порт, отличный от порта 80, необходимо явно добавить его в URL-адрес при открытии веб-портала в окне браузера. |
| Виртуальный каталог |По умолчанию виртуальные каталоги создаются в формате ReportServer для веб-службы сервера отчетов и Reports — для веб-портала. Для веб-службы сервера отчетов виртуальный каталог по умолчанию — **reportserver**. Для веб-портала виртуальный каталог по умолчанию — **reports**. |

Пример полной строки URL-адреса может выглядеть следующим образом:

* `https://+:80/reportserver` — предоставляет доступ к серверу отчетов;
* `https://+:80/reports`, предоставляет доступ к веб-порталу.

## <a name="firewall"></a>Брандмауэр

Если при доступе к серверу отчетов с удаленного компьютера используется брандмауэр, необходимо корректно настроить правила брандмауэра.

Откройте TCP-порт, настроенный для URL веб-службы и URL веб-портала. По умолчанию для них используется TCP-порт 80.

## <a name="additional-configuration"></a>Дополнительная настройка

* Чтобы настроить интеграцию со службой Power BI и иметь возможность закреплять элементы отчета на панели мониторинга Power BI, см. статью об [интеграции со службой Power BI](/sql/reporting-services/install-windows/power-bi-report-server-integration-configuration-manager).
* Чтобы настроить электронную почту для обработки подписок, см. статьи о [параметрах электронной почты](/sql/reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager) и [доставке электронной почты на сервере отчетов](/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).
* Чтобы настроить веб-портал и иметь возможность открывать его на компьютере отчетов для просмотра отчетов и управления ими, см. статьи о [настройке брандмауэра для доступа к серверу отчетов](/sql/reporting-services/report-server/configure-a-firewall-for-report-server-access) и [настройке сервера отчетов для удаленного администрирования](/sql/reporting-services/report-server/configure-a-report-server-for-remote-administration).
* Дополнительные сведения о настройке системных свойств сервера отчетов в SQL Server Management Studio см. в статье [Свойства сервера (страница "Дополнительно") — службы Reporting Services](/sql/reporting-services/tools/server-properties-advanced-page-reporting-services). Если не указано иное, параметры применяются как к Серверу отчетов Power BI, так и к SQL Server Reporting Services.

## <a name="next-steps"></a>Дальнейшие действия

[Обзор функций администратора](admin-handbook-overview.md)  
[Как найти ключ продукта сервера отчетов](find-product-key.md)  
[Установка Power BI Desktop для Сервера отчетов Power BI](install-powerbi-desktop.md)  
[Verify a Reporting Services installation](/sql/reporting-services/install-windows/verify-a-reporting-services-installation) (Проверка установки служб Reporting Services)  
[Configure the Report Server Service Account (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager) (Настройка учетной записи службы сервера отчетов (System Center Configuration Manager))  
[Configure Report Server URLs (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager) (Настройка URL-адресов сервера отчетов (System Center Configuration Manager))  
[Configure a Report Server Database Connection (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager) (Настройка подключения к базе данных сервера отчетов (System Center Configuration Manager))  
[SSRS Encryption Keys — Initialize a Report Server](/sql/reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server) (Ключи шифрования SSRS — инициализация сервера отчетов)  
[Configure SSL Connections on a Native Mode Report Server](/sql/reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server) (Настройка подключений SSL на сервере отчетов в основном режиме)  
[Configure Windows Service Accounts and Permissions](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) (Настройка учетных записей и разрешений службы Windows)  
[Поддержка браузера для сервера отчетов Power BI](browser-support.md)

У вас имеются и другие вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)