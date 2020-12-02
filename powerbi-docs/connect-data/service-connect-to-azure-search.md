---
title: Подключение к службе "Поиск Azure" с помощью Power BI
description: Поиск Azure для Power BI
author: davidiseminger
ms.author: davidi
ms.reviewer: maggiesMSFT
ms.service: powerbi
ms.subservice: powerbi-template-apps
ms.topic: conceptual
ms.date: 08/29/2019
LocalizationGroup: Connect to services
ms.openlocfilehash: 5c2c5d3b6382fdb85125a71829d62624dab31e83
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96403382"
---
# <a name="connect-to-azure-search-with-power-bi"></a>Подключение к службе "Поиск Azure" с помощью Power BI
Аналитика трафика службы поиска Azure позволяет отслеживать трафик и получать по нему подробные сведения в службе поиска Azure. Пакет содержимого службы поиска Azure для Power BI предоставляет подробные сведения по данным службы поиска, включая поиск, индексацию, статистику служб и задержки за последние 30 дней. Дополнительные сведения см. в [записи блога Azure](https://azure.microsoft.com/blog/analyzing-your-azure-search-traffic/).

[!INCLUDE [include-short-name](../includes/service-deprecate-content-packs.md)]

Подключите [пакет содержимого службы поиска Azure](https://app.powerbi.com/getdata/services/azure-search) для Power BI.

## <a name="how-to-connect"></a>Способы подключения
1. В нижней части области навигации выберите **Получить данные**.
   
   ![Снимок экрана: элемент "Получить данные" в Power BI Desktop с кнопкой на панели навигатора](media/service-connect-to-azure-search/pbi_getdata.png) 
2. В поле **Службы** выберите **Получить**.
   
   ![Снимок экрана: диалоговое окно "Службы" с кнопкой "Получить"](media/service-connect-to-azure-search/pbi_getservices.png) 
3. Выберите **Поиск Azure** \> **Получить**.
   
   ![Снимок экрана: диалоговое окно "Службы Azure" со ссылкой "Получить"](media/service-connect-to-azure-search/azuresearch.png)
4. Укажите имя учетной записи хранилища таблиц, в которой хранится анализ службы поиска Azure.
   
   ![Снимок экрана: диалоговое окно "Подключение к службе поиска Azure" с полем имени учетной записи хранения Azure](media/service-connect-to-azure-search/params.png)
5. Выберите **Ключ** в качестве механизма проверки подлинности и укажите ключ учетной записи хранения. Щелкните **Войти** , чтобы начать процесс загрузки.
   
   ![Снимок экрана: диалоговое окно "Подключение к службе поиска Azure" с указанием ключа в поле метода проверки подлинности](media/service-connect-to-azure-search/creds.png)
6. После завершения загрузки на панели навигации появятся новая панель мониторинга, отчет и модель. Выберите панель мониторинга, чтобы просмотреть импортированные данные.
   
    ![Снимок экрана: область навигации с панелью мониторинга, отчетом и моделью](media/service-connect-to-azure-search/dashboard2.png)

**Дальнейшие действия**

* Попробуйте [задать вопрос в поле "Вопросы и ответы"](../consumer/end-user-q-and-a.md) в верхней части информационной панели.
* [Измените плитки](../create-reports/service-dashboard-edit-tile.md) на информационной панели.
* [Выберите плитку](../consumer/end-user-tiles.md), чтобы открыть соответствующий отчет.
* Хотя набор данных будет обновляться ежедневно по расписанию, вы можете изменить график обновлений или попытаться выполнять обновления по запросу с помощью кнопки **Обновить сейчас**

## <a name="system-requirements"></a>Требования к системе
Для пакета содержимого службы поиска Azure требуется включить аналитику трафика службы поиска Azure в учетной записи.

## <a name="troubleshooting"></a>Устранение неполадок
Убедитесь, что имя учетной записи хранения правильно указано вместе с полным ключом доступа. Имя учетной записи хранения должно соответствовать учетной записи, настроенной в аналитике трафика службы поиска Azure.

## <a name="next-steps"></a>Дальнейшие действия
[Что такое Power BI?](../fundamentals/power-bi-overview.md)

[Основные понятия для разработчиков в службе Power BI](../fundamentals/service-basic-concepts.md)
