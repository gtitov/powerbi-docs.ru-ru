---
title: Использование прокси-службы веб-приложения и федеративных служб Active Directory — сервер отчетов Power BI
description: Узнайте, как использовать прокси-службы веб-приложения (WAP) и службы федерации Active Directory(AD FS) для подключения к серверу отчетов Power BI и SQL Server Reporting Services (SSRS) 2016 и более поздних версий.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 02/03/2021
ms.openlocfilehash: 73c7e0b2256d4a45fb9f433a887827e772a32257
ms.sourcegitcommit: c33e53e1fab1f29872297524a7b4f5af6c806798
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/04/2021
ms.locfileid: "99533080"
---
# <a name="use-web-application-proxy-and-active-directory-federated-services---power-bi-report-server"></a>Использование прокси-службы веб-приложения и федеративных служб Active Directory — сервер отчетов Power BI

В этой статье описывается, как использовать прокси-службы веб-приложения (WAP) и службы федерации Active Directory (AD FS) для подключения к серверу отчетов Power BI и SQL Server Reporting Services (SSRS) 2016 и более поздних версий. Благодаря этой интеграции пользователи, которые находятся вне корпоративной сети, могут получать доступ к своим отчетам на сервере отчетов Power BI и в службах Reporting Services со своих клиентских браузеров и использовать предварительную проверку подлинности AD FS. Для мобильных приложений Power BI также необходимо [настроить OAuth для подключения к серверу отчетов Power BI и службам SSRS](../consumer/mobile/mobile-oauth-ssrs.md).

## <a name="prerequisites"></a>Предварительные требования

### <a name="domain-name-services-dns-configuration"></a>Конфигурация служб доменных имен (DNS)

- Определите общедоступный URL-адрес, к которому будет подключаться пользователь. Он может выглядеть, как в следующем примере: `https://reports.contosolab.com`.
- Настройте запись DNS для имени узла, например `reports.contosolab.com`, чтобы указать общедоступный IP-адрес сервера прокси-служб веб-приложения (WAP).
- Настройте общедоступную запись DNS для сервера AD FS. Например, вы можете настроить для сервера AD FS следующий URL-адрес: `https://adfs.contosolab.com`.
- Настройте запись DNS, чтобы она указывала на общедоступный IP-адрес сервера прокси-служб веб-приложения (WAP), например `adfs.contosolab.com`. Он публикуется как часть приложения WAP.

### <a name="certificates"></a>Сертификаты

Необходимо настроить сертификаты как для приложения WAP, так и для сервера AD FS. Оба сертификата должны быть частью действительного центра сертификации, который распознают ваши компьютеры.

## <a name="1-configure-the-report-server"></a>1. Настройка сервера отчетов

Следует убедиться в наличии допустимого имени субъекта-службы (SPN). Действующее имя субъекта-службы обеспечивает правильную проверку подлинности Kerberos и включает сервер отчетов для согласования проверки подлинности.

### <a name="service-principal-name-spn"></a>Имя субъекта-службы (SPN)

Имя субъекта-службы — это уникальный идентификатор для службы, которая использует проверку подлинности Kerberos. Убедитесь, что вы указали правильное имя субъекта-службы HTTP для сервера отчетов.

Руководство по настройке правильного имени субъекта-службы (SPN) для сервера отчетов см. в статье о [регистрации имени субъекта-службы (SPN) для сервера отчетов](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server).

### <a name="enabling-negotiate-authentication"></a>Включение проверки подлинности с согласованием

Чтобы включить сервер отчетов для использования проверки подлинности Kerberos, необходимо указать RSWindowsNegotiate в качестве типа проверки подлинности на сервере отчетов. Его можно настроить в файле rsreportserver.config file.

```
<AuthenticationTypes>

    <RSWindowsNegotiate />

    <RSWindowsNTLM />

</AuthenticationTypes>
```

Дополнительные сведения см. в статьях об [изменении файла конфигурации Reporting Services ](/sql/reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config) и [настройке проверки подлинности Windows на сервере отчетов](/sql/reporting-services/security/configure-windows-authentication-on-the-report-server).

## <a name="2-configure-active-directory-federation-services-ad-fs"></a>2. Настройка служб федерации Active Directory (AD FS)

Вам необходимо настроить AD FS на сервере Windows 2016 в вашей среде. Для этой настройки, в диспетчере серверов в разделе "Управление" выберите "Добавить роли и компоненты". Дополнительные сведения см. в документации [служб федерации Active Directory](/windows-server/identity/active-directory-federation-services).

На сервере AD FS с помощью приложения управления AD FS выполните следующие действия.

1. Щелкните правой кнопкой мыши **Отношения доверия с проверяющей стороной** > **Добавить отношение доверия проверяющей стороны**.

    ![Добавление отношения доверия проверяющей стороны](media/connect-adfs-wap-report-server/report-server-adfs-add-relying-party-trust.png)

2. Выполните действия, описанные в мастере **добавления отношения доверия проверяющей стороны**.

    Выберите параметр **Не поддерживающие утверждения**, чтобы использовать встроенную систему безопасности Windows в качестве механизма проверки подлинности.

    ![Добро пожаловать в мастер добавления отношений доверия проверяющей стороны](media/connect-adfs-wap-report-server/report-server-adfs-add-relying-party-trust-welcome.png)

    Введите нужное имя в поле **Укажите отображаемое имя** и выберите команду **Далее**.
    Добавьте идентификатор отношения доверия проверяющей стороны: `<ADFS\_URL>/adfs/services/trust`

    Например: `https://adfs.contosolab.com/adfs/services/trust`

    ![Сервер отчетов](media/connect-adfs-wap-report-server/report-server-adfs-configure-identifiers.png)

    Выберите **политику управления доступом**, которая соответствует требованиям вашей организации, а затем нажмите кнопку **Далее**.

    ![Выбор управления доступом](media/connect-adfs-wap-report-server/report-server-adfs-choose-access-control.png)
    
    Нажмите кнопку **Далее**, а затем выберите команду **Завершить**, чтобы завершить работу мастера **добавления отношений доверия проверяющей стороны**.

    По завершении настройки свойства отношений доверия проверяющей стороны должны выглядеть следующим образом.

    ![Отношения доверия с проверяющей стороной](media/connect-adfs-wap-report-server/report-server-adfs-relying-party-trusts.png)

## <a name="3-configure-web-application-proxy-wap"></a>3. Настройка прокси-службы веб-приложения (WAP)

Вам понадобится включить роль Windows прокси-службы веб-приложения (роль) на сервере в вашей среде. Эта роль должна быть включена на сервере Windows 2016. Дополнительные сведения см. в статье о [прокси-службе веб-приложения в Windows Server 2016](/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server) и в разделе о [публикации приложений с помощью предварительной проверки подлинности AD FS](/windows-server/remote/remote-access/web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication#BKMK_1.2).

### <a name="configure-constrained-delegation"></a>Настройка ограниченного делегирования

Чтобы перейти с проверки подлинности с помощью форм на проверку подлинности Windows, понадобится использовать ограниченное делегирование с переходом протоколов. Этот этап является частью конфигурации Kerberos. В конфигурации сервера отчетов уже определено имя субъекта-службы сервера отчетов.

Теперь необходимо настроить в Active Directory ограниченное делегирование на учетную запись компьютера сервера WAP. Если у вас нет прав на доступ Active Directory, обратитесь к администратору домена.

Чтобы настроить ограниченное делегирование, выполните следующие действия.

1. На компьютере со средствами Active Directory запустите средство **Пользователи и компьютеры Active Directory**.
2. Найдите учетную запись компьютера для сервера WAP. По умолчанию она будет находиться в контейнере **Компьютеры**.
3. Щелкните правой кнопкой мыши сервер WAP и выберите пункт **Свойства**.
4. На вкладке **Делегирование** выберите параметр **Доверять этому компьютеру при делегировании указанных служб** и **Использовать любой протокол проверки подлинности**.

    ![Доверять этому компьютеру](media/connect-adfs-wap-report-server/report-server-adfs-delegation-use-any.png)

1. Этот параметр задает ограниченное делегирование для этой учетной записи компьютера сервера WAP. Далее нужно указать службы, которые этот компьютер может делегировать.
2. Выберите **Добавить** в поле служб.

    ![Добавить доверие в AD FS](media/connect-adfs-wap-report-server/report-server-adfs-trust-add.png)

1. Выберите **Пользователи или компьютеры**.
2. Введите учетную запись службы, которую вы используете для сервера отчетов. Это та же учетная запись, которая использовалась для добавления имени субъекта-службы HTTP в предыдущем разделе [конфигурации сервера отчетов](#1-configure-the-report-server). 

3. Выберите имя субъекта-службы HTTP для сервера отчетов, а затем нажмите кнопку **ОК**.

    > [!NOTE]
    > Вы можете видеть только имя субъекта-службы NetBIOS. Фактически оно выбирает имена субъекта-службы NetBIOS и полного доменного имени, если они оба существуют.

1. При установке флажка **Развернуто** результат должен выглядеть примерно так, как показано в примере ниже.

    ![Свойства WAP](media/connect-adfs-wap-report-server/report-server-wap-properties.png)

### <a name="add-wap-application"></a>Добавление приложения WAP

1. На сервере прокси-служб веб-приложения откройте консоль **управления удаленным доступом** и выберите в области навигации пункт **Прокси веб-приложения**. 

2. В области **Задачи** выберите **Опубликовать**.

2. На странице приветствия нажмите кнопку **Далее**.

    ![Добро пожаловать в публикацию](media/connect-adfs-wap-report-server/report-server-welcome-publish-new-app-wizard.png)

3. На странице **Предварительная проверка подлинности** выберите **Active Directory Federation Services (AD FS)** (Службы федерации Active Directory (AD FS)), а затем нажмите кнопку **Далее**.

    ![Предварительная авторизация](media/connect-adfs-wap-report-server/report-server-preauthentication-new-app-wizard.png)

4. Выберите предварительную проверку подлинности **Интернет и MSOFBA**, так как будет настроен только доступ с помощью браузера к серверу отчетов, без доступа с помощью мобильных приложений.

    ![Поддерживаемые клиенты](media/connect-adfs-wap-report-server/report-server-supported-clients-publish-new-app-wizard.png)

5. Добавьте пункт **Проверяющая сторона**, созданный на сервере AD FS, как показано ниже, а затем нажмите кнопку **Далее**.

    ![Публикация проверяющей стороны](media/connect-adfs-wap-report-server/report-server-relying-party-publish-new-app-wizard.png)

6. В разделе **Внешний URL-адрес** укажите общедоступный URL-адрес, настроенный на сервере WAP. Добавьте URL-адрес, настроенный с использованием сервера отчетов (Диспетчер конфигурации сервера отчетов), как показано ниже, в разделе **URL-адрес внутреннего сервера**. Добавьте имя субъекта-службы сервера отчетов в разделе **Имя субъекта-службы внутреннего сервера**.

    ![Параметры публикации](media/connect-adfs-wap-report-server/report-server-publishing-settings-new-app-wizard.png)

7. Нажмите кнопку **Далее**, а затем — **Опубликовать**.
8. Выполните следующую команду PowerShell, чтобы проверить конфигурацию WAP.

    ```
    Get-WebApplicationProxyApplication -Name "PBIRSWAP" | FL
    ```

    ![Команда PowerShell](media/connect-adfs-wap-report-server/report-server-powershell-get-webapplication.png)

## <a name="connect-to-the-report-server-through-the-browser"></a>Подключение к серверу отчетов с помощью браузера

После этого из браузера можно получить доступ к общедоступному URL-адресу WAP, например `https://reports.contosolab.com/ReportServer` для веб-службы и `https://reports.contosolab.com/Reports` для веб-портала. После успешного прохождения проверки подлинности можно просмотреть отчеты.

![Вход в AD FS](media/connect-adfs-wap-report-server/report-server-adfs-sign-in.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Настройка OAuth для подключения к серверу отчетов Power BI и службам SSRS](../consumer/mobile/mobile-oauth-ssrs.md)
*[Что такое сервер отчетов Power BI?](get-started.md)  

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
