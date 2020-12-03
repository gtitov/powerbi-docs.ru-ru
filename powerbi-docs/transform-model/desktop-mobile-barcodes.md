---
title: Добавление тегов для поля со штрихкодом в Power BI Desktop для мобильных приложений
description: Если для поля со штрихкодом в модели Power BI Desktop добавлены теги, вы можете автоматически фильтровать данные штрихкодов в приложении Power BI на устройстве iPhone
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: pbi-transform-model
ms.topic: how-to
ms.date: 01/16/2018
LocalizationGroup: Model your data
ms.openlocfilehash: 91cf4fb4101b710ad49e49c914dbc4bcaa03682a
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96413939"
---
# <a name="tag-barcodes-in-power-bi-desktop-for-use-in-the-mobile-app"></a>Добавьте теги в Power BI Desktop для использования в мобильном приложении

В Power BI Desktop можно [задавать категории данных](desktop-data-categorization.md) в столбцах, чтобы приложение Power BI Desktop понимало, как интерпретировать соответствующие значения в визуальных элементах отчета. Столбцу также можно присвоить категорию **Штрихкод**. [Отсканировав штрихкод изделия в приложении Power BI](../consumer/mobile/mobile-apps-scan-barcode-iphone.md) на устройстве iPhone, вы сможете увидеть все отчеты, в которых есть этот штрихкод. При открытии отчета в мобильном приложении Power BI автоматически фильтрует данные в нем в соответствии с указанным штрихкодом.

1. В Power BI Desktop перейдите в представление данных.
2. Выберите столбец с данными штрихкодов. Список [поддерживаемых форматов штрихкодов](#supported-barcode-formats) приведен ниже.
3. На вкладке **Моделирование** выберите **Категория данных** > **Штрихкод**.
   
    ![Список категорий данных](media/desktop-mobile-barcodes/power-bi-desktop-barcode.png)
4. В представлении отчета добавьте это поле в визуальные элементы, которые должны фильтроваться по штрихкоду.
5. Сохраните отчет и опубликуйте его в службе Power BI.

Теперь откройте сканер в [приложении Power BI для iPhone](../consumer/mobile/mobile-iphone-app-get-started.md) и отсканируйте штрихкод, и вы увидите данный отчет в списке отчетов. При открытии отчета его визуальные элементы будут отфильтрованы по штрихкоду изделия, который вы отсканировали.

## <a name="supported-barcode-formats"></a>Поддерживаемые форматы штрихкодов
Ниже перечислены штрихкоды, которые распознает приложение Power BI, если они помечены в отчете соответствующим образом. 

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
* [Сканирование штрихкода из приложения Power BI на iPhone](../consumer/mobile/mobile-apps-scan-barcode-iphone.md)
* [Проблемы при сканировании штрихкодов на iPhone](../consumer/mobile/mobile-apps-scan-barcode-iphone.md#issues-with-scanning-a-barcode)
* [Категоризация данных в Power BI Desktop](desktop-data-categorization.md)  
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
