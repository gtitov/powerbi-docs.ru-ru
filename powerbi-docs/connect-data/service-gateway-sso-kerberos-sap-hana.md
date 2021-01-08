---
title: Использование Kerberos для единого входа в SAP HANA
description: Настройка сервера SAP HANA для включения единого входа из службы Power BI
author: arthiriyer
ms.author: arthii
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: how-to
ms.date: 12/16/2020
LocalizationGroup: Gateways
ms.openlocfilehash: 3f50b174e8293d75a0077e1799cb64ff4fdcd696
ms.sourcegitcommit: 5c09d121d3205e65fb33a2eca0e60bc30e777773
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2020
ms.locfileid: "97675127"
---
# <a name="use-kerberos-for-single-sign-on-sso-to-sap-hana"></a>Использование Kerberos для единого входа в SAP HANA

> [!IMPORTANT]
> Так как [SAP больше не поддерживает OpenSSL](https://help.sap.com/viewer/b3ee5778bc2e4a089d3299b82ec762a7/2.0.05/en-US/de15ffb1bb5710148386ffdfd857482a.html), корпорация Майкрософт также прекратила поддержку этой библиотеки. Существующие подключения продолжат работать, но вы не сможете создавать новые подключения начиная с февраля 2021 г. В дальнейшем используйте библиотеку CommonCryptoLib.

В этой статье описывается, как настроить источник данных SAP HANA для включения единого входа из службы Power BI.

> [!NOTE]
> Прежде чем пытаться обновить отчет на основе SAP HANA, в котором используется единый вход Kerberos, выполните действия, описанные в этой статье, а также инструкции в статье [Настройка единого входа на основе Kerberos](service-gateway-sso-kerberos.md).

## <a name="enable-sso-for-sap-hana"></a>Включение единого входа для SAP HANA

Чтобы включить единый вход для SAP HANA, выполните следующие действия:

1. Убедитесь, что для сервера SAP HANA используется минимально допустимая версия, которая зависит от уровня платформы сервера SAP HANA:
   - [HANA 2 SPS 01 Rev 012.03](https://launchpad.support.sap.com/#/notes/2557386)
   - [HANA 2 SPS 02 Rev 22](https://launchpad.support.sap.com/#/notes/2547324)
   - [HANA 1 SP 12 Rev 122.13](https://launchpad.support.sap.com/#/notes/2528439)

2. На компьютере шлюза установите последнюю версию драйвера ODBC для SAP HANA. Минимальная версия драйвера ODBC для HANA — 2.00.020.00, выпущенная в августе 2017 г.

3. Убедитесь, что сервер SAP HANA настроен для единого входа на основе Kerberos. Дополнительные сведения о настройке единого входа для SAP HANA с помощью Kerberos см. в разделе о [едином входе с использованием Kerberos](https://help.sap.com/viewer/b3ee5778bc2e4a089d3299b82ec762a7/2.0.03/1885fad82df943c2a1974f5da0eed66d.html) руководства по безопасности SAP HANA. На этой странице приведены полезные ссылки, в частности примечание SAP 1837331 — HOWTO HANA DBSSO Kerberos/Active Directory.

Мы также рекомендуем указанные ниже дополнительные действия, которые позволят обеспечить небольшое повышение производительности.

1. В каталоге установки шлюза найдите и откройте этот файл конфигурации: Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config.

2. Найдите свойство `FullDomainResolutionEnabled` и измените его значение на `True`.

    ```xml
    <setting name=" FullDomainResolutionEnabled " serializeAs="String">
          <value>True</value>
    </setting>
    ```

Теперь [запустите отчет Power BI](service-gateway-sso-kerberos.md#run-a-power-bi-report).

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о локальном шлюзе данных и DirectQuery см. в следующих ресурсах:

* [Что такое локальный шлюз данных?](/data-integration/gateway/service-gateway-onprem)
* [Power BI и DirectQuery](desktop-directquery-about.md)
* [Источники данных, поддерживаемые DirectQuery](power-bi-data-sources.md)
* [Использование DirectQuery и SAP Business Warehouse (BW)](desktop-directquery-sap-bw.md)
* [DirectQuery и SAP HANA](desktop-directquery-sap-hana.md)
