---
title: Активация меток конфиденциальности в Power BI
description: Сведения об активации меток конфиденциальности в Power BI
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-eim
ms.topic: how-to
ms.date: 08/10/2020
LocalizationGroup: Data from files
ms.openlocfilehash: eb2afe2e7fa21bc0583185cfc8a160b20f56236c
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96412122"
---
# <a name="enable-sensitivity-labels-in-power-bi"></a>Активация меток конфиденциальности в Power BI

Чтобы использовать [метки конфиденциальности Microsoft Information Protection](/microsoft-365/compliance/sensitivity-labels) в Power BI, их необходимо активировать в клиенте. В этой статье описаны действия, выполняемые администраторами Power BI. Общие сведения о метках конфиденциальности в Power BI см. в статье [Метки конфиденциальности в Power BI](service-security-sensitivity-label-overview.md). Сведения о применении меток конфиденциальности в Power BI см. в статье [Применение меток конфиденциальности данных в Power BI.](./service-security-apply-data-sensitivity-labels.md) 

Активация меток конфиденциальности дает следующие возможности.

* Определенные пользователи и группы безопасности в организации могут классифицировать метки конфиденциальности и [применять их](./service-security-apply-data-sensitivity-labels.md) к своим панелям мониторинга, отчетам, наборам данных и потокам данных Power BI.
* Все члены организации могут просматривать эти метки.

Для активации меток конфиденциальности требуется лицензия Azure Information Protection. Дополнительные сведения см. в разделе [Лицензирование и требования](#licensing-and-requirements).

## <a name="licensing-and-requirements"></a>Лицензирование и требования

* Для применения и просмотра меток конфиденциальности Microsoft Information Protection в Power BI требуется лицензия Azure Information Protection Premium P1 или Premium P2. Средство Azure Information Protection можно приобрести как отдельно, так и в составе одного из наборов лицензирования Майкрософт. Дополнительные сведения см. в статье [Цены на Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

* Чтобы применять метки к содержимому Power BI, в дополнение к указанным выше лицензиям Azure Information Protection пользователям потребуется лицензия Power BI Pro.

* Приложения Office имеют отдельные [требования к лицензированию для просмотра и применения меток конфиденциальности]( https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels#subscription-and-licensing-requirements-for-sensitivity-labels ).

* Перед включением меток конфиденциальности для арендатора убедитесь, что метки конфиденциальности определены и опубликованы для соответствующих пользователей и групп. Дополнительные сведения см. в статье [Создание и настройка меток конфиденциальности и соответствующих политик](/microsoft-365/compliance/create-sensitivity-labels).

>[!NOTE]
> Если в организации используются метки конфиденциальности Azure Information Protection, их необходимо перенести на платформу унифицированных меток Microsoft Information Protection, чтобы их можно было использовать в Power BI. [Узнайте больше о переносе меток конфиденциальности.](/azure/information-protection/configure-policy-migrate-labels)

## <a name="enable-sensitivity-labels"></a>Активация меток конфиденциальности

Перейдите на портал **администрирования** Power BI, откройте панель **Параметры клиента** и найдите раздел **Information Protection**.

![Поиск раздела "Information Protection"](media/service-security-enable-data-sensitivity-labels/enable-data-sensitivity-labels-01.png)

В разделе **Information Protection** выполните следующие действия:
1. Откройте **Разрешить пользователям применять метки конфиденциальности к содержимому Power BI**.
1. Включите переключатель.
1. Определите, кто может применять метки конфиденциальности к ресурсам Power BI и изменять их. По умолчанию метки конфиденциальности могут применять все пользователи вашей организации. При необходимости вы можете разрешить задание меток конфиденциальности только отдельным пользователям или группам безопасности. Выбрав всю организацию или отдельные группы безопасности, вы можете исключить некоторых пользователей или конкретные группы безопасности.
   
   * Если метки конфиденциальности активированы для всей организации, как правило, исключаются группы безопасности.
   * Если метки конфиденциальности включены для отдельных пользователей или групп безопасности, исключаются обычно конкретные пользователи.  
    Такой подход позволяет запретить применять метки конфиденциальности Power BI некоторым пользователям, даже если они входят в группу с соответствующими разрешениями.

1. Нажмите кнопку **Применить**.

![Активация меток конфиденциальности](media/service-security-enable-data-sensitivity-labels/enable-data-sensitivity-labels-02.png)

> [!IMPORTANT]
> Задавать и редактировать метки конфиденциальность могут только те пользователи Power BI Pro с разрешениями на *создание* и *изменение* ресурса, которые входят в соответствующую группу безопасности, как описывается в этом разделе. Пользователи, не включенные в такую группу, не смогут задавать или редактировать метки.  

## <a name="troubleshooting"></a>Устранение неполадок

В Power BI используются метки конфиденциальности Microsoft Information Protection. Если при попытке активировать метки конфиденциальности появляется сообщение об ошибке, это может быть вызвано одной из следующих причин:

* У вас нет [лицензии](#licensing-and-requirements) Azure Information Protection.
* Метки конфиденциальности не [перенесены](#enable-sensitivity-labels) в версию Microsoft Information Protection, поддерживаемую Power BI.
* [В организации не определены](#enable-sensitivity-labels) метки конфиденциальности Microsoft Information Protection.

## <a name="considerations-and-limitations"></a>Рекомендации и ограничения

Список ограничений на использование меток конфиденциальности в Power BI см. в статье [Метки конфиденциальности в Power BI](service-security-sensitivity-label-overview.md#limitations).

## <a name="next-steps"></a>Дальнейшие действия

В этой статье была рассмотрена активация меток конфиденциальности в Power BI. В следующих статьях вы найдете дополнительные сведения о защите данных в Power BI. 

* [Общие сведения о метках конфиденциальности в Power BI](service-security-sensitivity-label-overview.md)
* [Применение меток конфиденциальности в Power BI](./service-security-apply-data-sensitivity-labels.md)
* [Использование элементов управления Microsoft Cloud App Security в Power BI](service-security-using-microsoft-cloud-app-security-controls.md)
* [Отчет о метриках защиты](service-security-data-protection-metrics-report.md)