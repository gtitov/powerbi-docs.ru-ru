---
title: API локального хранилища в визуальных элементах Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается получение доступа к локальному хранилищу браузера с использованием API визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 01/21/2019
ms.openlocfilehash: abec68c5622d3dcd96746148ed7a6da4f06c8ec0
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888197"
---
# <a name="local-storage-api"></a>API локального хранилища

С помощью API локального хранилища пользовательский визуальный элемент может отправлять узлу запросы на сохранение или загрузку данных из хранилища устройства. Этот API реализует изоляцию, обеспечивая раздельный доступ к хранилищу для разных типов визуальных элементов.

## <a name="sample"></a>Образец

Пользовательский визуальный элемент должен увеличивать значение счетчика каждый раз при вызове метода обновления, но при этом такое значение должно сохраняться и не должно сбрасываться при каждом запуске визуального элемента:

```typescript
export class Visual implements IVisual {
        // ...
        private updateCountName: string = 'updateCount';
        private updateCount: number;
        private storage: ILocalVisualStorageService;
        // ...

        constructor(options: VisualConstructorOptions) {
            // ...
            this.storage = options.host.storageService;
            // ...

            this.storage.get(this.updateCountName).then(count =>
            {
                this.updateCount = +count;
            })
            .catch(() =>
            {
                this.updateCount = 0;
                this.storage.set(this.updateCountName, this.updateCount.toString());
            });
            // ...
        }

        public update(options: VisualUpdateOptions) {
            // ...
            this.updateCount++;
            this.storage.set(this.updateCountName, this.updateCount.toString());
            // ...
        }
}
```

## <a name="known-limitations-and-issues"></a>Известные ограничения и проблемы

По умолчанию API локального хранилища для визуальных элементов Power BI не активирован. Если вы хотите активировать его для визуального элемента Power BI, направьте запрос в службу поддержки визуальных элементов Power BI (`pbicvsupport@microsoft.com`).  
**Имейте в виду, что визуальный элемент должен быть доступен в [AppSource](https://appsource.microsoft.com/en-us/marketplace/apps?product=power-bi-visuals) и [сертифицирован](https://powerbi.microsoft.com/en-us/documentation/powerbi-custom-visuals-certified/).**
