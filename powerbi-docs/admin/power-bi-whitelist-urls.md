---
title: Добавление URL-адресов Power BI в список разрешенных
description: В этой статье перечислены URL-адреса конечных точек и порты, которые нужно добавить в список разрешенных адресов для подключения к Power BI.
author: kfollis
ms.author: kfollis
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 06/25/2020
ms.custom: seodec18
ms.openlocfilehash: 1495400a59d8250f407a5f7415a550871501e4e3
ms.sourcegitcommit: cb6e0202de27f29dd622e47b305c15f952c5769b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2020
ms.locfileid: "96577516"
---
# <a name="add-power-bi-urls-to-your-allow-list"></a>Добавление URL-адресов Power BI в свой список разрешенных адресов
[//]: # "suparnap, miwehnia, natham — это контакты людей, которые работают с этим списком"

Службе Power BI требуется подключение к Интернету. Конечные точки, перечисленные в таблицах этой статьи, должны быть доступны для клиентов, использующих службу Power BI.

Для использования службы Power BI необходимо обеспечить подключение к конечным точкам, помеченным как **обязательные**, в таблицах ниже и всем конечным точкам, помеченным как **обязательные** на связанных сайтах. Если ссылка на внешний сайт указывает на конкретный раздел, вам потребуется проверить только конечные точки в этом разделе.

Можно также добавить конечные точки, отмеченные как **необязательные**, чтобы разрешить работу со списками для конкретной функциональности.

Для работы службы Power BI для указанных конечных точек требуется открыть только TCP-порт 443.

Подстановочные знаки (*) представляют все уровни в корневом домене. Когда информация недоступна, используется "н/д". Столбец **Назначения** содержит имена доменов и ссылки на внешние веб-сайты, которые содержат дополнительные сведения о конечной точке.

>[!Important]
>Сведения в приведенных ниже таблицах неприменимы к Power BI для Германии, Power BI для Китая (21Vianet) или Power BI для государственных организаций США. Дополнительные сведения о взаимодействии между облачными службами см. в статье [Подключение государственных и глобальных облачных служб Azure](service-govus-overview.md#connect-government-and-global-azure-cloud-services).

## <a name="authentication"></a>Аутентификация

Работа Power BI зависит от необходимых конечных точек в разделах идентификации и проверки подлинности Microsoft 365. Для использования Power BI необходимо подключиться к конечным точкам в связанном веб-сайте ниже.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется:** проверка подлинности и идентификация | См. документацию [по URL-адресам для Office Online и общим URL-адресам Microsoft 365](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online)  | Недоступно |

## <a name="general-site-usage"></a>Общее использование сайта

Для общего использования Power BI необходимо подключиться к конечным точкам в таблице и связанных веб-сайтах ниже.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется:** cерверные API | api.powerbi.com; | TCP 443 |
| 2 | **Требуется:** cерверные API | *.analysis.windows.net | TCP 443 |
| 3 | **Требуется:** cерверные API | *.pbidedicated.windows.net | TCP 443 |
| 4 | **Требуется:** Сеть доставки содержимого (CDN) | content.powerapps.com | TCP 443 |
| 5 | **Требуется:** Интеграция Microsoft 365 | См. документацию [по URL-адресам для Office Online и общим URL-адресам Microsoft 365](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) | Недоступно |
| 6 | **Требуется:** Портал | *.powerbi.com | TCP 443 |
| 7 | **Требуется:** телеметрия службы | dc.services.visualstudio.com | TCP 443 |
| 8 | **Необязательно**. информационные сообщения | dynmsg.modpim.com | TCP 443 |
| 9 | **Необязательно**. опросы сервера политики сети | nps.onyx.azure.net | TCP 443 |
| | | |

## <a name="administration"></a>Администрирование

Для выполнения функций администрирования в Power BI необходимо обеспечить подключение к конечным точкам в связанных сайтах ниже.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется** для управления пользователями и просмотра журналов аудита | См. документацию [по URL-адресам для Office Online и общим URL-адресам Microsoft 365](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) | Недоступно |
| | | |

## <a name="getting-data"></a>Получение данных

Чтобы получать данные из конкретных источников данных, таких как OneDrive, потребуется подключаться к конечным точкам в таблице ниже. Для определенных источников данных, используемых в организации, может потребоваться доступ к дополнительным интернет-доменам и URL-адресам.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется:** AppSource (внутренние или внешние приложения в Power BI) | appsource.microsoft.com <br> *.s-microsoft.com  | TCP 443 |
| 2 | **Необязательно**. вход и получение данных для пакетов содержимого | Зависит от используемых пакетов содержимого | Зависит от используемых пакетов содержимого |
| 3 | **Необязательно**. импорт файлов из OneDrive — персональный | См. раздел [Требуемые URL-адреса и порты для сайта OneDrive](/onedrive/required-urls-and-ports). | Недоступно |
| 4 | **Необязательно**. Power BI в 60-секундном учебном видео | *.doubleclick.net <br> *.ggpht.com <br> *.google.com <br> *.googlevideo.com <br> *.youtube.com <br> *.ytimg.com <br> fonts.gstatic.com | TCP 443 |
| 5 | **Необязательно**. источники данных потоковой передачи PubNub | См. [документацию PubNub](https://support.pubnub.com/hc/en-us/categories/360004336832-PubNub-101). | Недоступно |
| | | |

## <a name="dashboard-and-report-integration"></a>Интеграция панели мониторинга и отчетов

Поддержка панелей мониторингов и отчетов в Power BI зависит от определенных конечных точек. Для этого необходимо подключиться к конечным точкам в таблице и связанных веб-сайтах ниже.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется:** интеграция с Excel | См. документацию [по URL-адресам для Office Online и общим URL-адресам Microsoft 365](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) | Недоступно |
| | | |

## <a name="power-bi-visuals"></a>Визуальные элементы Power BI

Возможность просмотра визуализаций в Power BI и доступа к ним зависит от определенных конечных точек. Для этого необходимо подключиться к конечным точкам в таблице и связанных веб-сайтах ниже.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Требуется:** импорт пользовательского визуального элемента из интерфейса Marketplace или из файла | *.azureedge.net <br> *.blob.core.windows.net <br> *.osi.office.net <br> *.msecnd.net <br> store.office.com <br> web.vortex.data.microsoft.com <br> store-images.s-microsoft.com | TCP 443 |
| 2 | **Необязательно**. Карты Bing | bing.com <br> platform.bing.com <br> *.virtualearth.net | TCP 443 |
| 3 | **Необязательно**. PowerApps. | См. раздел [Необходимые службы](/powerapps/maker/canvas-apps/limits-and-config#required-services) на сайте требований к системе PowerApps. | Недоступно |
| 4 | **Необязательно**. Visio | См. документацию [по URL-адресам для Office Online и общим URL-адресам Microsoft 365](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online), а также по [SharePoint Online и OneDrive для бизнеса](/office365/enterprise/urls-and-ip-address-ranges#sharepoint-online-and-onedrive-for-business) | Недоступно |
| | | |

## <a name="related-external-sites"></a>Связанные внешние сайты

Ссылки Power BI на другие связанные сайты. На этих сайтах размещена документация, информация о службе поддержки, запросы новых функций и многое другое. Доступ к этим сайтам не повлияет на функциональные возможности Power BI, поэтому добавлять их в список разрешений необязательно.

| Строка | Цель | Назначение(я) | Порты |
| --- | --- | --- | --- |
| 1 | **Необязательно**. веб-сайт сообщества | community.powerbi.com <br> oxcrx34285.i.lithium.com | TCP 443 |
| 2 | **Необязательно**. Сайт документации | docs.microsoft.com <br> img-prod-cms-rt-microsoft-com.akamaized.net <br> statics-uhf-eas.akamaized.net <br> cdnssl.clicktale.net <br> ing-district.clicktale.net | TCP 443 |
| 3 | **Необязательно**. веб-сайт с материалами для скачивания (для Power BI Desktop и т. д.) | download.microsoft.com | TCP 443 |
| 4 | **Необязательно**. внешние перенаправления | aka.ms <br> сайт go.microsoft.com; | TCP 443 |
| 5 | **Необязательно:** веб-сайт обратной связи| ideas.powerbi.com <br> powerbi.uservoice.com | TCP 443 |
| 6 | **Необязательно**. веб-сайт Power BI — целевая страница, ссылки на дополнительные сведения, веб-сайт службы поддержки, ссылки на материалы для скачивания, демонстрационные материалы партнеров и т. д. | powerbi.microsoft.com | TCP 443 |
| 7 | **Необязательно**. Центр по разработке для Power BI | dev.powerbi.com | TCP 443 |
| 8 | **Необязательно**. веб-сайт службы поддержки | support.powerbi.com <br> s3.amazonaws.com <br> *.olark.com <br> logx.optimizely.com <br> mscom.demdex.net <br> tags.tiqcdn.com | TCP 443 |
| | | |
