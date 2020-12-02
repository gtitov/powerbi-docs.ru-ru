---
title: Локальный шлюз данных во всех подробностях
description: В этой статье подробно рассматривается локальный шлюз. В ней рассказывается, как служба использует каталог Azure Active Directory и локальный каталог Active Directory при работе с Analysis Services.
author: arthiriyer
ms.author: arthii
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: how-to
ms.date: 07/15/2019
LocalizationGroup: Gateways
ms.openlocfilehash: 0964ad3e391c8e066c31ea7bb53f67e97f254422
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96392365"
---
# <a name="on-premises-data-gateway-in-depth"></a>Локальный шлюз данных во всех подробностях

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

Мы перенесли информацию из этой статьи в несколько статей, посвященных Power BI и общим вопросам. Чтобы найти соответствующее содержимое, перейдите по ссылкам под каждым заголовком.

## <a name="how-the-gateway-works"></a>Принцип работы шлюза

См. статью [Архитектура локального шлюза данных](/data-integration/gateway/service-gateway-onprem-indepth).

## <a name="list-of-available-data-source-types"></a>Список доступных типов источников данных

См. статью [Управление источниками данных](service-gateway-data-sources.md).

## <a name="authentication-to-on-premises-data-sources"></a>Проверка подлинности в локальных источниках данных

См. статью [Проверка подлинности в локальных источниках данных](/data-integration/gateway/service-gateway-onprem-indepth#authentication-to-on-premises-data-sources).

## <a name="authentication-to-a-live-analysis-services-data-source"></a>Проверка подлинности на динамическом источнике данных Analysis Services

См. статью [Проверка подлинности на динамическом источнике данных Analysis Services](service-gateway-enterprise-manage-ssas.md#authentication-to-a-live-analysis-services-data-source).

## <a name="role-based-security"></a>Безопасность на основе ролей

См. статью [Безопасность на основе ролей](service-gateway-enterprise-manage-ssas.md#role-based-security).

## <a name="row-level-security"></a>Защита на уровне строк

См. статью [Безопасность на уровне строк](service-gateway-enterprise-manage-ssas.md#row-level-security).

## <a name="what-about-azure-active-directory"></a>Об Azure Active Directory

См. статью [Azure Active Directory](/data-integration/gateway/service-gateway-onprem-indepth#azure-active-directory).

## <a name="how-do-i-tell-what-my-upn-is"></a>Как узнать свое имя участника-пользователя?

См. статью [Как узнать свое имя участника-пользователя?](/data-integration/gateway/service-gateway-onprem-indepth#how-do-i-tell-what-my-upn-is).

## <a name="map-user-names-for-analysis-services-data-sources"></a>Сопоставление имен пользователей для источников данных Analysis Services

См. статью [Сопоставление имен пользователей для источников данных Analysis Services](service-gateway-enterprise-manage-ssas.md#map-user-names-for-analysis-services-data-sources).

## <a name="synchronize-an-on-premises-active-directory-with-azure-active-directory"></a>Синхронизация локальной Active Directory с Azure Active Directory

См. статью [Синхронизация локальной Active Directory с Azure Active Directory](/data-integration/gateway/service-gateway-onprem-indepth#synchronize-an-on-premises-active-directory-with-azure-active-directory).

## <a name="what-to-do-next"></a>Дальнейшие действия

Ознакомьтесь со статьями, посвященными источникам данных:

[Управление источниками данных](service-gateway-data-sources.md)
[Управление своим источником данных — службы Analysis Services](service-gateway-enterprise-manage-ssas.md)  
[Управление своим источником данных — SAP HANA](service-gateway-enterprise-manage-sap.md)  
[Управление своим источником данных — SQL Server](service-gateway-enterprise-manage-sql.md)  
[Управление своим источником данных — Oracle](service-gateway-onprem-manage-oracle.md)  
[Управление источником данных — импорт или запланированное обновление](service-gateway-enterprise-manage-scheduled-refresh.md)  

## <a name="where-things-can-go-wrong"></a>Где могут возникнуть проблемы

См. статьи [Устранение неполадок локального шлюза данных](/data-integration/gateway/service-gateway-tshoot) и [Устранение неполадок со шлюзами — Power BI](service-gateway-onprem-tshoot.md).

## <a name="sign-in-account"></a>Учетная запись для входа

См. статью [Учетная запись для входа](/data-integration/gateway/service-gateway-onprem-indepth#sign-in-account).

## <a name="windows-service-account"></a>Учетная запись службы Windows

См. статью [Изменение учетной записи службы локального шлюза данных](/data-integration/gateway/service-gateway-service-account).

## <a name="ports"></a>Порты

См. статью [Порты](/data-integration/gateway/service-gateway-communication#ports).

## <a name="forcing-https-communication-with-azure-service-bus"></a>Принудительная установка связи по HTTPS со служебной шиной Azure

См. статью [Принудительная установка связи по HTTPS со служебной шиной Azure](/data-integration/gateway/service-gateway-communication#force-https-communication-with-azure-service-bus).

## <a name="support-for-tls-12"></a>Поддержка протокола TLS 1.2

См. статью [TLS 1.2 для трафика шлюза](/data-integration/gateway/service-gateway-communication#tls-12-for-gateway-traffic).

## <a name="how-to-restart-the-gateway"></a>Как перезапустить шлюз

См. статью [Перезапуск шлюза](/data-integration/gateway/service-gateway-restart).

## <a name="next-steps"></a>Дальнейшие действия

См. статью [Что такое локальный шлюз данных?](service-gateway-onprem.md)

Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)