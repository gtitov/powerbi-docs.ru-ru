---
title: Пометка полей штрихкодов в Power BI Desktop для обеспечения фильтрации по штрихкодам в мобильных приложениях
description: Когда вы помечаете поле штрихкода в модели Power BI Desktop пользователи мобильных приложений могут сканировать штрихкоды для получения отфильтрованных данных на своих телефонах и планшетах с iOS и Android.
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: pbi-transform-model
ms.topic: how-to
ms.date: 01/20/2021
LocalizationGroup: Model your data
ms.openlocfilehash: 4674347d3acd6520d7d156a7d1634a13df611afe
ms.sourcegitcommit: f7330dabb9cd8bce90bb2efec3e3273a11578f10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "99494421"
---
# <a name="tag-barcode-fields-in-power-bi-desktop-to-enable-barcode-scan-filtering-in-the-mobile-apps"></a>Пометка полей штрихкодов в Power BI Desktop для обеспечения фильтрации по штрихкодам в мобильных приложениях

В Power BI Desktop можно [задавать категории данных](desktop-data-categorization.md) в столбцах, чтобы приложение Power BI Desktop понимало, как интерпретировать соответствующие значения в визуальных элементах отчета. Столбцу также можно присвоить категорию **Штрихкод**. Затем, когда кто-нибудь в вашей организации [сканирует штрихкод](../consumer/mobile/mobile-apps-scan-barcode-iphone.md) на изделии с помощью мобильного приложения Power BI на телефоне или планшете с iOS или Android, он видит все отчеты с этим штрихкодом. При открытии отчета в нем автоматически отфильтровываются данные, связанные с этим штрихкодом.

## <a name="categorize-barcode-data"></a>Классификация данных по штрихкодам

Предположим, у вас есть отчет, содержащий штрихкоды. 

1. В Power BI Desktop перейдите в представление данных.
2. Выберите столбец, содержащий данные штрихкода. Список [поддерживаемых форматов штрихкодов](#supported-barcode-formats) приведен ниже.
3. На вкладке **Средства работы со столбцами** выберите **Категория данных** > **Штрихкод**.
   
    ![Список категорий данных](media/desktop-mobile-barcodes/power-bi-desktop-barcode.png)

    >[!WARNING]
    >Не следует классифицировать более одного столбца во всех таблицах данных отчета как **Штрихкод**. Мобильные приложения поддерживают фильтрацию по штрихкоду только для отчетов, во всех таблицах которых имеется только один столбец штрихкода. Если в отчете несколько таких столбцов, фильтрации не произойдет.

4. В представлении отчета добавьте поле штрихкода в визуальные элементы, которые должны фильтроваться по штрихкоду.
5. Сохраните отчет и опубликуйте его в службе Power BI.

Теперь, когда вы откроете сканер в приложении Power BI для телефонов и планшетов с iOS или Android и отсканируете штрихкод, вы увидите этот отчет в списке отчетов со штрихкодами. При открытии отчета его визуальные элементы будут отфильтрованы по штрихкоду изделия, который вы отсканировали.

## <a name="supported-barcode-formats"></a>Поддерживаемые форматы штрихкодов
Ниже перечислены форматы штрихкодов, которые распознает приложение Power BI, если они помечены в отчете соответствующим образом. 

* UPCECode 
* Code39Code  
* A39Mod43Code 
* EAN13Code 
* EAN8Code  
* 93Code  
* 128Code 
* PDF417Code 
* Interleaved2of5Code 
* ITF14Code 

## <a name="next-steps"></a>Дальнейшие действия
* [Сканирование штрихкода из приложения Power BI на телефоне или планшете с iOS или Android](../consumer/mobile/mobile-apps-scan-barcode-iphone.md)
* [Проблемы при сканировании штрихкодов](../consumer/mobile/mobile-apps-scan-barcode-iphone.md#issues-with-scanning-a-barcode)
* [Категоризация данных в Power BI Desktop](desktop-data-categorization.md)  
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
