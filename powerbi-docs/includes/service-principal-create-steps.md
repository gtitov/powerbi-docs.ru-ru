---
title: Создание приложения субъекта-службы
description: Создание приложения субъекта-службы
services: powerbi
author: KesemSharabi
ms.author: kesharab
ms.topic: include
ms.date: 10/15/2020
ms.custom: include file
ms.openlocfilehash: 0f6c74ddc5a7decc8c1a6444568de44d3adbbc68
ms.sourcegitcommit: 8561902ef0ad63b0881187a22f25d1aa1ec3bcbc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2020
ms.locfileid: "92210845"
---
## <a name="step-2---create-an-azure-ad-security-group"></a>Шаг 2. Создание группы безопасности Azure AD

У субъекта-службы нет доступа к любому содержимому и API-интерфейсам Power BI. Чтобы предоставить субъекту-службе доступ, создайте группу безопасности в Azure AD и добавьте созданный субъект-службу в эту группу безопасности.

Существует два способа создания группы безопасности Azure AD.
* Вручную (в Azure)
* Регистрация с помощью PowerShell

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
>:::image type="content" source="../developer/embedded/media/embed-service-principal/admin-portal.png" alt-text="Снимок экрана: страница &quot;Параметры разработчика&quot; в области параметров администратора на портале Power BI.":::

## <a name="step-4---add-the-service-principal-to-your-workspace"></a>Шаг 4. Добавление субъект-службы в рабочую область

Чтобы включить артефакты доступа к приложению Azure AD, такие как отчеты, панели мониторинга и наборы данных в службу Power BI, добавьте сущность субъекта-службы в качестве участника или администратора в рабочую область.

>[!NOTE]
>В этом разделе содержатся инструкции для пользовательского интерфейса. Вы также можете добавить субъект-службу в рабочую область, используя команду [Groups — add group user API](/rest/api/power-bi/groups/addgroupuser) (Группы — добавление API-интерфейса пользователя группы).

1. Перейдите к рабочей области, для которой требуется включить доступ, а затем в меню **Еще** выберите команду **Доступ к рабочей области**.

    :::image type="content" source="../developer/embedded/media/embed-service-principal/workspace-access.png" alt-text="Снимок экрана: кнопка &quot;Доступ к рабочей области&quot; в меню &quot;Еще&quot; в рабочей области Power BI.":::

2. Добавьте субъект-службу как **Администратор** или **Участник** в эту рабочую область.

    :::image type="content" source="../developer/embedded/media/embed-service-principal/add-service-principal-in-the-UI.png" alt-text="Снимок экрана: добавление участника или администратора в область доступа на портале Power BI.":::