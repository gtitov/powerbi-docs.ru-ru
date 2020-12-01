---
title: Внедрение содержимого Power BI с помощью субъект-службы и секрета приложения
description: Сведения о том, как выполнять проверку подлинности внедренной аналитики с помощью субъекта-службы приложения Azure Active Directory и секрета приложения.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: how-to
ms.custom: ''
ms.date: 11/23/2020
ms.openlocfilehash: 17c0a4d0809aa87f50225e0c59ca3962776bd2b1
ms.sourcegitcommit: 9d033abd9c01a01bba132972497dda428d7d5c12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95514515"
---
# <a name="embed-power-bi-content-with-service-principal-and-an-application-secret"></a>Внедрение содержимого Power BI с помощью субъект-службы и секрета приложения

Субъект-служба — это метод проверки подлинности, который можно использовать, чтобы предоставить приложению Azure AD доступ к содержимому службы и API-интерфейсам Power BI.

При создании приложения Azure Active Directory (Azure AD) создается [объект субъекта-службы](/azure/active-directory/develop/app-objects-and-service-principals#service-principal-object). Объект субъекта-службы, также известный как *субъект-служба*, позволяет Azure AD проверить подлинность приложения. После проверки подлинности приложение может получить доступ к ресурсам клиента Azure AD.

Для проверки подлинности субъект-служба использует *идентификатор приложения* приложения Azure AD и один из этих идентификаторов:

* Сертификат
* Секрет приложения

В этой статье описывается проверка подлинности субъекта-службы с помощью *идентификатора приложения* и *секрета приложения*.

>[!NOTE]
>Azure AD рекомендует защищать серверные службы с помощью сертификатов, а не секретных ключей.
>* [Дополнительные сведения о получении маркеров доступа из Azure AD с помощью секретных ключей или сертификатов](/azure/architecture/multitenant-identity/client-assertion).
>* Чтобы защитить решение с помощью сертификата, следуйте инструкциям в этой статье, а затем выполните действия, описанные в разделе [Внедрение содержимого Power BI с помощью субъекта-службы и сертификата](embed-service-principal-certificate.md).

## <a name="method"></a>Метод

Чтобы использовать субъект-службу и идентификатор приложения со встроенной аналитикой, выполните следующие действия.

1. Создайте [приложение Azure AD](/azure/active-directory/manage-apps/what-is-application-management).

    1. Создайте секрет приложения Azure AD.
    
    2. Получите *Идентификатор приложения* и *Секрет приложения*.

    >[!NOTE]
    >Эти действия описаны в **шаге 1**. Дополнительные сведения о создании приложения Azure AD см. в статье [Создание приложения Azure AD](/azure/active-directory/develop/howto-create-service-principal-portal).

2. Создайте группу безопасности Azure AD.

3. Включите параметры администрирования службы Power BI.

4. Добавьте субъект-службу в рабочую область.

5. Внедрите свое содержимое.

> [!IMPORTANT]
> После активации субъекта-службы для использования с Power BI разрешения приложения в Active Directory перестают действовать. В дальнейшем управление разрешениями приложения осуществляется на портале администрирования Power BI.

## <a name="step-1---create-an-azure-ad-app"></a>Шаг 1. Создание приложения Azure AD

Создайте приложение Azure AD одним из методов, перечисленных ниже.

* [Создание приложения на портале Microsoft Azure](embed-service-principal.md#creating-an-azure-ad-app-in-the-microsoft-azure-portal)

* [Создание приложения с помощью PowerShell](embed-service-principal.md#creating-an-azure-ad-app-using-powershell)

### <a name="creating-an-azure-ad-app-in-the-microsoft-azure-portal"></a>Создание приложения Azure AD на портале Microsoft Azure

1. Выполните вход в [Microsoft Azure](https://ms.portal.azure.com/#allservices).

2. В строке поиска найдите **Регистрация приложений** и щелкните ссылку **Регистрация приложений**.

    ![регистрация приложения azure](media/embed-service-principal/azure-app-registration.png)

3. Щелкните **Новая регистрация**.

    ![новая регистрация](media/embed-service-principal/new-registration.png)

4. Заполните необходимые сведения:
    * **Имя** — введите имя для своего приложения.
    * **Поддерживаемые типы учетных записей** — выберите поддерживаемые типы учетных записей.
    * (Необязательно) **URI перенаправления** — при необходимости введите универсальный код ресурса (URI).

5. Щелкните **Зарегистрировать**.

6. После регистрации на вкладке **Обзор** доступен *Идентификатор приложения*. Скопируйте и сохраните *Идентификатор приложения* для последующего использования.

    ![Снимок экрана: получение ИД приложения на вкладке "Обзор".](media/embed-service-principal/application-id.png)

7. Перейдите на вкладку **Сертификаты и секреты**.

     ![Снимок экрана: панель "Сертификаты и секреты" для приложения на портале Azure.](media/embed-service-principal/certificates-and-secrets.png)

8. Щелкните **Создать секрет клиента**.

    ![Снимок экрана: кнопка "Создать секрет клиента" на панели "Сертификаты и секреты".](media/embed-service-principal/new-client-secret.png)

9. В окне *Добавление секрета клиента* введите описание, укажите, когда должен истечь срок действия секрета клиента, и нажмите кнопку **Добавить**.

10. Скопируйте и сохраните значение *Секрет клиента*.

    ![Снимок экрана: размытое значение секрета на панели "Сертификаты и секреты".](media/embed-service-principal/client-secret-value.png)

    >[!NOTE]
    >После закрытия этого окна значение секрета клиента будет скрыто, и вы не сможете снова просмотреть или скопировать его.

### <a name="creating-an-azure-ad-app-using-powershell"></a>Создание приложения Azure AD с помощью PowerShell

В этом разделе содержится пример скрипта для создания нового приложения Azure AD с помощью [PowerShell](/powershell/azure/create-azure-service-principal-azureps).

```powershell
# The app ID - $app.appid
# The service principal object ID - $sp.objectId
# The app key - $key.value

# Sign in as a user that's allowed to create an app
Connect-AzureAD

# Create a new Azure AD web application
$app = New-AzureADApplication -DisplayName "testApp1" -Homepage "https://localhost:44322" -ReplyUrls "https://localhost:44322"

# Creates a service principal
$sp = New-AzureADServicePrincipal -AppId $app.AppId

# Get the service principal key
$key = New-AzureADServicePrincipalPasswordCredential -ObjectId $sp.ObjectId
```

## <a name="step-2---create-an-azure-ad-security-group"></a>Шаг 2. Создание группы безопасности Azure AD

У субъекта-службы нет доступа к любому содержимому и API-интерфейсам Power BI. Чтобы предоставить субъекту-службе доступ, создайте группу безопасности в Azure AD и добавьте созданный субъект-службу в эту группу безопасности.

Существует два способа создания группы безопасности Azure AD.
* [Вручную (в Azure)](embed-service-principal.md#create-a-security-group-manually)
* [PowerShell](embed-service-principal.md#create-a-security-group-using-powershell)

### <a name="create-a-security-group-manually"></a>Создание группы безопасности вручную

Чтобы создать группу безопасности Azure вручную, следуйте инструкциям в статье [Создание простой группы и добавление в нее участников с помощью Azure Active Directory](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal). 

### <a name="create-a-security-group-using-powershell"></a>Создание группы безопасности с помощью PowerShell

Ниже приведен пример скрипта для создания новой группы безопасности и добавления приложения в эту группу безопасности.

>[!NOTE]
>Если вы хотите включить доступ субъекта-службы для всей организации, пропустите этот шаг.

```powershell
# Required to sign in as admin
Connect-AzureAD

# Create an Azure AD security group
$group = New-AzureADGroup -DisplayName <Group display name> -SecurityEnabled $true -MailEnabled $false -MailNickName notSet

# Add the service principal to the group
Add-AzureADGroupMember -ObjectId $($group.ObjectId) -RefObjectId $($sp.ObjectId)
```

## <a name="step-3---enable-the-power-bi-service-admin-settings"></a>Шаг 3. Включение параметров администрирования службы Power BI

Чтобы приложение Azure AD могло получить доступ к содержимому и API-интерфейсам Power BI, администратор Power BI должен включить доступ субъекта-службы на портале администрирования Power BI.

Добавьте группу безопасности, созданную в Azure AD, в раздел отдельных групп безопасности на странице **Параметры разработчика**.

>[!IMPORTANT]
>Субъекты-службы имеют доступ ко всем параметрам клиента, для которых они включены. В зависимости от параметров администратора, это может быть определенная группа безопасности или вся организация.
>
>Чтобы ограничить доступ субъекта-службы к параметрам определенного клиента, разрешите доступ только к определенным группам безопасности. Кроме того, можно создать выделенную группу безопасности для субъектов-служб и исключить ее из параметров нужного клиента.

>[!div class="mx-imgBorder"]
>:::image type="content" source="media/embed-service-principal/admin-portal.png" alt-text="Снимок экрана: страница &quot;Параметры разработчика&quot; в области параметров администратора на портале Power BI.":::

## <a name="step-4---add-the-service-principal-to-your-workspace"></a>Шаг 4. Добавление субъект-службы в рабочую область

Чтобы включить артефакты доступа к приложению Azure AD, такие как отчеты, панели мониторинга и наборы данных в службу Power BI, добавьте сущность субъекта-службы или группу безопасности, в которую входит субъект-служба, в качестве участника или администратора в рабочую область.

>[!NOTE]
>В этом разделе содержатся инструкции для пользовательского интерфейса. Вы также можете добавить субъект-службу или группу безопасности в рабочую область, используя команду [Groups — add group user API](/rest/api/power-bi/groups/addgroupuser) (Группы — добавление API-интерфейса пользователя группы).

1. Перейдите к рабочей области, для которой требуется включить доступ, а затем в меню **Еще** выберите команду **Доступ к рабочей области**.

    :::image type="content" source="media/embed-service-principal/workspace-access.png" alt-text="Снимок экрана: кнопка &quot;Доступ к рабочей области&quot; в меню &quot;Еще&quot; в рабочей области Power BI.":::

2. В области **Доступ** в текстовом поле добавьте одно из следующего:

    * Свою **субъект-службу**. Имя субъекта-службы — это *отображаемое имя* приложения Azure AD, как оно отображается на вкладке обзора приложения Azure AD.

    * **Группу безопасности**, которая включает субъект-службу.

3. В раскрывающемся меню выберите **Член** или **Администратор**.

4. Выберите **Добавить**.

## <a name="step-5---embed-your-content"></a>Шаг 5. Внедрение содержимого

Вы можете внедрить содержимое в пример приложения или в собственное приложение.

* [Внедрение содержимого с помощью примера приложения](embed-sample-for-customers.md#embed-content-using-the-sample-application)
* [Внедрение содержимого в приложении](embed-sample-for-customers.md#embed-content-within-your-application)

После того, как содержимое будет внедрено, вы можете [переносить его в производственную среду](embed-sample-for-customers.md#move-to-production).

>[!NOTE]
>Чтобы защитить содержимое с помощью сертификата, выполните действия, описанные в разделе [Внедрение содержимого Power BI с помощью субъекта-службы и сертификата](embed-service-principal-certificate.md).

## <a name="considerations-and-limitations"></a>Рекомендации и ограничения

* Субъекты-службы работают только с [новыми рабочими областями](../../collaborate-share/service-create-the-new-workspaces.md).
* **Моя рабочая область** не поддерживается при использовании субъекта-службы.
* Для миграции в рабочую среду требуется емкость.
* С помощью субъекта-службы нельзя входить на портал Power BI.
* Для включения субъекта-службы в параметрах разработчика на портале администрирования Power BI требуются права администратора Power BI.
* [Внедренные для организации](embed-sample-for-your-organization.md) приложения не могут использовать субъект-службу.
* Управление [потоками данных](../../transform-model/dataflows/dataflows-introduction-self-service.md) не поддерживается.
* Сейчас субъект-служба не поддерживает никакие API администратора.
* При использовании субъекта-службы с источником данных [Azure Analysis Services](/azure/analysis-services/analysis-services-overview) сам субъект-служба должен иметь разрешения экземпляра Azure Analysis Services. Использовать для этой цели группу безопасности, содержащую субъект-службу, нельзя.

## <a name="next-steps"></a>Дальнейшие действия

>[!div class="nextstepaction"]
>[Регистрация приложения](register-app.md)

> [!div class="nextstepaction"]
>[Power BI Embedded для клиентов](embed-sample-for-customers.md)

>[!div class="nextstepaction"]
>[Внедрение с использованием субъекта-службы и сертификата](embed-service-principal-certificate.md)

>[!div class="nextstepaction"]
>[Объекты приложения и субъекта-службы в Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals)

>[!div class="nextstepaction"]
>[Безопасность на уровне строк с использованием локального шлюза данных с субъектом-службой](embedded-row-level-security.md#on-premises-data-gateway-with-service-principal)