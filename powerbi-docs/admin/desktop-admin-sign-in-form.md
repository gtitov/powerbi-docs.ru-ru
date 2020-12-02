---
title: Как администраторы могут управлять формами для входа в Power BI Desktop
description: Узнайте, как управлять начальной формой для входа, отображаемой при открытии Power BI Desktop.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: how-to
ms.date: 04/15/2019
ms.openlocfilehash: 633d71326009881b22b7b7d235316b4ebe5c132f
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96386888"
---
# <a name="administrators-manage-the-power-bi-desktop-sign-in-form"></a>Администраторы Управление формой для входа в Power BI Desktop
При первом запуске Power BI Desktop отображается форма для входа. Вы можете заполнить эту форму или войти в Power BI, чтобы продолжить. Администраторы управляют этой формой с помощью раздела реестра. 

![Снимок экрана: начальная форма для входа в Power BI Desktop](media/desktop-admin-sign-in-form/sign-in-form.png)

Администраторы могут отключить форму для входа, используя указанный ниже раздел реестра. Ее также можно отключить для всей организации с помощью глобальных политик.

```
Key: HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Microsoft Power BI Desktop
valueName: ShowLeadGenDialog
```
Вы также можете воспользоваться следующим разделом. Такой способ подошел некоторым клиентам с учетом их конфигураций.

```
Key: HKEY_CURRENT_USER\SOFTWARE\Microsoft\Microsoft Power BI Desktop
valueName: ShowLeadGenDialog
```

Задайте значение 0, чтобы отключить диалоговое окно.




Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)

