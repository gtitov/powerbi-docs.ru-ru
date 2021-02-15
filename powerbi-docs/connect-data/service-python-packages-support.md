---
title: Узнайте, какие пакеты Python поддерживаются
description: Поддерживаемые и неподдерживаемые пакеты Python в Power BI
author: otarb
ms.author: otarb
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.topic: conceptual
ms.date: 06/26/2020
LocalizationGroup: Connect to data
ms.openlocfilehash: d3a30098b793ccb75cbae6c271ab1685b3176a10
ms.sourcegitcommit: f17acb16018752c234db6bff1f51f5130be12c58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99616971"
---
# <a name="create-visuals-by-using-python-packages-in-the-power-bi-service"></a>Создание визуальных элементов с помощью пакетов Python в службе Power BI
Вы можете использовать эффективный [язык программирования Python](https://www.python.org/) для создания визуальных элементов в службе Power BI. В службе Power BI поддерживается множество пакетов Python, и многие из них поддерживаются постоянно.

В следующих разделах приводятся поддерживаемые и неподдерживаемые пакеты Python в Power BI. 

## <a name="request-support-for-a-new-python-package"></a>Запрос поддержки для нового пакета Python
Пакеты, поддерживаемые Python для использования в **службе Power BI**, перечислены в разделе **Поддерживаемые пакеты**. Чтобы запросить поддержку для пакета Python, который отсутствует в списке, опубликуйте запрос на сайте [Power BI Ideas](https://ideas.powerbi.com).

## <a name="requirements-and-limitations-of-python-packages"></a>Требования и ограничения для пакетов Python
Для пакетов Python существуют определенные требования и ограничения.

* Текущая среда выполнения Python: Python 3.7.7.
* Служба Power BI преимущественно поддерживает пакеты Python с лицензиями на свободное ПО и ПО с открытым исходным кодом, включая GPL-2, GPL-3, MIT+ и т. д.
* Служба Power BI поддерживает пакеты, опубликованные в PyPI. Служба не поддерживает закрытые или пользовательские пакеты Python. Пользователям рекомендуется сделать свои закрытые пакеты доступными в PyPI, прежде чем запрашивать доступность пакета в службе Power BI.
* Для визуальных элементов Python в **Power BI Desktop** можно установить любой пакет, в том числе пользовательские пакеты Python.
* Из соображений конфиденциальности и безопасности пакеты Python, которые передают запросы клиент-сервера в службу через Интернет, не поддерживаются. Возможность подключения для таких попыток заблокирована.
* При утверждении нового пакета Python для включения используется дерево зависимостей. При этом некоторые необходимые для установки службы зависимости не поддерживаются.

## <a name="python-packages-that-are-supported-in-power-bi"></a>Поддерживаемые пакеты Python в Power BI
В таблице ниже приведены пакеты, которые **поддерживаются** в службе Power BI.


|        Пакет        |   Версия   |                                   Ссылка                                   |
|-----------------------|-------------|--------------------------------------------------------------------------|
|matplotlib|3.2.1|https://pypi.org/project/matplotlib|
|numpy|1.18.4|https://pypi.org/project/numpy|
|pandas|1.0.1|https://pypi.org/project/pandas|
|scikit-learn|0.23.0|https://pypi.org/project/scikit-learn|
|scipy|1.4.1|https://pypi.org/project/scipy|
|seaborn|0.10.1|https://pypi.org/project/seaborn|
|statsmodels|0.11.1|https://pypi.org/project/statsmodels|
|XGBoost|1.1.0|https://pypi.org/project/xgboost|

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о Python в Power BI см. в следующих статьях:

* [Создание визуальных элементов Power BI с помощью Python](desktop-python-visuals.md)
* [Выполнение сценариев Python в Power BI Desktop](desktop-python-scripts.md)
* [Использование языка Python в редакторе запросов](desktop-python-in-query-editor.md)
