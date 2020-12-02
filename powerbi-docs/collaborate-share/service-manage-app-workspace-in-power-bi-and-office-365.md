---
title: Управление рабочей областью в Power BI и Microsoft 365
description: Рабочие области в Power BI обеспечивают широкие возможности для совместной работы на основе групп Microsoft 365. Вы можете управлять рабочими областями в Power BI и в Microsoft 365.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: lukasz
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 03/02/2020
LocalizationGroup: Share your work
ms.openlocfilehash: bd1a5b0aaf694f41fdbfe4764e77c1138a57b082
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96407039"
---
# <a name="manage-your-workspace-in-power-bi-and-microsoft-365"></a>Управление рабочей областью в Power BI и Microsoft 365

Автор или администратор [рабочей области в Power BI](service-create-distribute-apps.md) или в Microsoft 365 может управлять некоторыми аспектами рабочей области в Power BI. Управление другими аспектами осуществляется в Microsoft 365.

> [!NOTE]
> В новом интерфейсе рабочей области изменятся отношения между рабочими областями Power BI и группами Microsoft 365. Группа Microsoft 365 не будет создаваться автоматически каждый раз, когда вы создаете новую рабочую область. Узнайте о [создании новых рабочих областей](service-create-the-new-workspaces.md).

В **Power BI** можно выполнять следующие задачи:

* Добавлять или удалять участников рабочей области, включая присвоение участнику рабочей области прав администратора.
* Изменить имя рабочей области.
* Удалить рабочую область (в результате также удалится группа Microsoft 365).

В **Microsoft 365** можно:

* добавлять или удалять участников рабочей области, включая присвоение участнику прав владельца;
* менять название группы, ее изображение, описание и другие параметры;
* просматривать адрес электронной почты группы;
* удалять группу.

Лицензия [Power BI Pro](../fundamentals/service-features-license-type.md) необходима для администратора или участника рабочей области. Вашим пользователям приложения также требуется лицензия Power BI Pro, если только рабочая область не хранится емкости Power BI Premium. Дополнительные сведения см. в статье [Что такое Power BI Premium?](../admin/service-premium-what-is.md)

## <a name="edit-your-workspace-in-power-bi"></a>Изменение рабочей области в Power BI

1. В службе Power BI щелкните стрелку рядом с элементом **Рабочие области**, выберите **Дополнительные параметры** (…) рядом с именем рабочей области, а затем — **Изменение этой рабочей области**.

   ![Снимок экрана: главная страница Power BI с выбранным элементом "Рабочие области" и выбранным пунктом для изменения в меню "Дополнительные параметры".](media/service-manage-app-workspace-in-power-bi-and-office-365/power-bi-app-ellipsis.png)

   > [!NOTE]
   > Элемент **Изменение этой рабочей области** отображается только для администраторов рабочих областей.

1. Здесь можно переименовать или удалить рабочую область, а также добавить или удалить членов.

   ![Диалоговое окно "Изменение рабочей области"](media/service-manage-app-workspace-in-power-bi-and-office-365/power-bi-app-edit-workspace.png)

1. Выберите **Сохранить** или **Отменить**.

## <a name="edit-power-bi-workspace-properties-in-microsoft-365"></a>Изменение свойств рабочей области Power BI в Microsoft 365

Вы также можете изменять различные аспекты рабочей области непосредственно в Outlook для Microsoft 365.

### <a name="edit-the-members-of-the-workspace-group"></a>Изменение членов группы рабочей области

1. В службе Power BI щелкните стрелку рядом с элементом **Рабочие области** и выберите **Дополнительные параметры** (…) рядом с именем рабочей области, а затем — **Члены**.

   ![Снимок экрана: главная страница Power BI с выбранным элементом "Рабочие области" и выбранным пунктом "Члены" в меню "Дополнительные параметры".](media/service-manage-app-workspace-in-power-bi-and-office-365/power-bi-app-ellipsis-members.png)

   Откроется представление Outlook для группы Microsoft 365 для рабочей области. Возможно, вам потребуется войти в свою корпоративную учетную запись.

1. Чтобы сделать пользователя **членом** или **владельцем**, выберите роль рядом с его именем. Выберите **X**, чтобы удалить пользователя из группы.

   ![Изменение группы в Microsoft 365](media/service-manage-app-workspace-in-power-bi-and-office-365/pbi_managegroupo365.png)

### <a name="add-an-image-and-set-other-workspace-properties"></a>Добавление изображения и задание других свойств рабочей области

При распространении приложения из рабочей области изображение, которое вы добавляете, является изображением вашего приложения. Ознакомьтесь с разделом [Добавление изображения в рабочую область Microsoft 365](service-create-workspaces.md#add-an-image-to-your-microsoft-365-workspace-optional) статьи **Создание рабочих областей**.

1. В представлении Outlook для Microsoft 365 своей рабочей области откройте вкладку **О программе** и выберите **Изменить**.

    ![Значок "Изменить группу"](media/service-manage-app-workspace-in-power-bi-and-office-365/pbi_editgroupo365.png)
1. Вы можете изменить имя, описание и язык для уведомлений, связанных с группой. Кроме того, здесь можно добавить изображение и задать другие свойства.

   ![Диалоговое окно "Изменить группу"](media/service-manage-app-workspace-in-power-bi-and-office-365/pbi_editgrpo365dialog.png)

1. Выберите **Сохранить** или **Отменить**.

## <a name="next-steps"></a>Дальнейшие действия

* [Публикация приложения в Power BI](service-create-distribute-apps.md)

* Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
