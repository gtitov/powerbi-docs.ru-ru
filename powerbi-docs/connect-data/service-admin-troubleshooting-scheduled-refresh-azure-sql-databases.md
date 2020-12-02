---
title: Устранение неполадок с запланированным обновлением для баз данных SQL Azure
description: Устранение неполадок с запланированным обновлением для баз данных SQL Azure в Power BI
author: davidiseminger
ms.author: davidi
ms.reviewer: kayu
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: troubleshooting
ms.date: 09/04/2019
ms.custom: seodec18
LocalizationGroup: Troubleshooting
ms.openlocfilehash: a9f69c8177766352d768d86903f15977ae0d8d1c
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96410742"
---
# <a name="troubleshooting-scheduled-refresh-for-azure-sql-databases-in-power-bi"></a>Устранение неполадок с запланированным обновлением для баз данных SQL Azure в Power BI

Дополнительные сведения об обновлении см. в статьях [Обновление данных в Power BI](refresh-data.md) и [Настройка запланированного обновления](refresh-scheduled-refresh.md).

Если при настройке запланированного обновления базы данных SQL Azure во время редактирования учетных данных возникает ошибка с кодом 400, попробуйте выполнить следующие действия, чтобы настроить соответствующее правило брандмауэра:

1. Войдите на [портал Azure](https://portal.azure.com).

1. Перейдите в базу данных SQL Azure, для которой выполняется настройка обновления.

1. В верхней части колонки **Обзор** выберите **Настройка брандмауэра для сервера**.

1. Убедитесь, что в колонке **Параметры брандмауэра** для параметра **Разрешить доступ к службам Azure** задано значение **ВКЛ**.

    ![Разрешенные службы Azure](media/service-admin-troubleshooting-scheduled-refresh-azure-sql-databases/azurerefresh.png)  

У вас имеются и другие вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
