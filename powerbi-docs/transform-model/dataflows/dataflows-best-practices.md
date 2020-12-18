---
title: Рекомендации по потокам данных
description: Коллекция рекомендаций и инструкций по потокам данных
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: pbi-dataflows
ms.topic: how-to
ms.date: 12/10/2020
LocalizationGroup: Data from files
ms.openlocfilehash: 116458c094159cbeeadaf2e955744759e4648220
ms.sourcegitcommit: bbf7e9341a4e1cc96c969e24318c8605440282a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97097968"
---
# <a name="dataflows-best-practices"></a>Рекомендации по потокам данных

**Потоки данных** представляют собой корпоративное решение для подготовки данных, обеспечивая экосистему данных, готовых к потреблению, повторному использованию и интеграции. В этой статье приведен список рекомендаций, а также ссылки на статьи и другие сведения, которые помогут понять и полноценно использовать потоки данных.

## <a name="dataflows-across-the-power-platform"></a>Потоки данных в Power Platform

Потоки данных можно использовать в различных технологиях Power Platform, таких как Power Query, Microsoft Dynamics 365, а также в других предложения Майкрософт. Дополнительные сведения о том, как потоки данных могут работать в Power Platform, см. в разделе, посвященном [использованию потоков данных в продуктах Майкрософт](https://docs.microsoft.com/power-query/dataflows/overview-dataflows-across-power-platform-dynamics-365).


## <a name="dataflows-best-practices-table-and-links"></a>Рекомендации по потокам данных (таблица и ссылки)

В следующей таблице приводятся ссылки на статьи, в которых описаны рекомендации по созданию потоков данных и работе с ними. Ссылки включают сведения о разработке бизнес-логики, разработке сложных потоков данных, повторном использовании потоков данных и о том, как добиться корпоративного масштабирования с помощью потоков данных.


|**Раздел**  |**Тема**  |**Ссылка на статью или содержимое**  |
|---------|---------|---------|
|Power Query     | Советы и рекомендации по максимально эффективной первичной обработке данных        |[Рекомендации по работе с Power Query](https://docs.microsoft.com/power-query/best-practices)        |
|Использование вычисляемых сущностей     |Использование вычисляемых сущностей в потоке данных дает преимущества в производительности         |[Сценарии с вычисляемыми сущностями](https://docs.microsoft.com/power-query/dataflows/computed-entities-scenarios)         |
|Разработка сложных потоков данных     |Шаблоны для разработки крупномасштабных и производительных потоков данных         |[Сложные потоки данных](https://docs.microsoft.com/power-query/dataflows/best-practices-developing-complex-dataflows)         |
|Повторное использование потоков данных     |Шаблоны, рекомендации и варианты использования         |[Повторное использование потоков данных](https://docs.microsoft.com/power-query/dataflows/best-practices-reusing-dataflows)         |
|Крупномасштабные реализации     |Крупномасштабное использование и рекомендации по дополнению корпоративной архитектуры         |[Хранение данных с помощью потоков данных](https://docs.microsoft.com/power-query/dataflows/best-practices-for-data-warehouse-using-dataflows)         |
|Использование расширенных вычислений     |Потенциальное повышение производительности потока данных до 25 раз         |[Расширенное ядро вычислений](dataflows-premium-workload-configuration.md#using-the-compute-engine-to-improve-performance)         |
|Оптимизация параметров рабочей нагрузки     |Получите максимальную производительность инфраструктуры потоков данных с помощью возможностей для повышения производительности         |[Конфигурация рабочей нагрузки потоков данных](dataflows-premium-workload-configuration.md)         |
|Соединение и развертывание таблиц     |Создание высокопроизводительных соединений         |[Оптимизация операций по развертыванию таблиц](https://docs.microsoft.com/power-query/optimize-expanding-table-columns)         |
|Рекомендации по свертыванию запросов     |Ускорение преобразований с использованием исходной системы         |[Свертывание запроса](https://docs.microsoft.com/power-query/power-query-folding)         |
|Использование профилирования данных     |Общие сведения о качестве, распределении и профиле столбцов         |[Средства профилирования данных](https://docs.microsoft.com/power-query/data-profiling-tools)         |
|Реализация обработки ошибок     |Разработка надежных потоков данных, устойчивых к ошибкам обновления, с рекомендациями         |[Шаблоны для распространенных ошибок](https://docs.microsoft.com/power-query/dealing-with-errors)  </br> [Обработка сложных ошибок](https://docs.microsoft.com/power-query/error-handling)      |
|Использование представления схемы      |Улучшение процесса разработки при работе с широкой таблицей и выполнении операций на уровне схемы         |[Представление схемы](https://docs.microsoft.com/power-query/schema-view)         |
|Связанные сущности      |Повторное использование преобразований и ссылки на них         |[Связанные сущности](https://docs.microsoft.com/power-query/dataflows/linked-entities)         |
|Добавочное обновление      |Загрузка последних или измененных данных в сравнении с полной перезагрузкой         |[Добавочное обновление](https://docs.microsoft.com/power-query/dataflows/incremental-refresh)         |
|||


        
## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о потоках данных и Power BI вы можете получить в следующих статьях.

* [Вводные сведения о потоках данных и самостоятельной подготовке данных](dataflows-introduction-self-service.md)
* [Создание потока данных](dataflows-create.md)
* [Настройка и использование потока данных](dataflows-configure-consume.md)
* [Функции потоков данных уровня "Премиум"](dataflows-premium-features.md)
* [Настройка хранилища потоков данных для использования Azure Data Lake 2-го поколения](dataflows-azure-data-lake-storage-integration.md)
* [ИИ с потоками данных](dataflows-machine-learning-integration.md)
* [Рекомендации и ограничения, касающиеся потоков данных](dataflows-features-limitations.md)