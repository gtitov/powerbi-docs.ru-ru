---
title: Активация меток конфиденциальности в Power BI
description: Сведения об активации меток конфиденциальности в Power BI
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-eim
ms.topic: how-to
ms.date: 12/09/2020
LocalizationGroup: Data from files
ms.openlocfilehash: 1732c1b6b8b748c4f3a820b31c4e4fe050a66fcd
ms.sourcegitcommit: b472236df99b490db30f0168bd7284ae6e6095fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/16/2020
ms.locfileid: "97600330"
---
# <a name="enable-sensitivity-labels-in-power-bi"></a>Активация меток конфиденциальности в Power BI

Чтобы использовать [метки конфиденциальности Microsoft Information Protection](/microsoft-365/compliance/sensitivity-labels) в Power BI, их необходимо активировать в клиенте. В этой статье описаны действия, выполняемые администраторами Power BI. Общие сведения о метках конфиденциальности в Power BI см. в статье [Метки конфиденциальности в Power BI](service-security-sensitivity-label-overview.md). Сведения о применении меток конфиденциальности в Power BI см. в статье [Применение меток конфиденциальности данных в Power BI.](./service-security-apply-data-sensitivity-labels.md) 

Активация меток конфиденциальности дает следующие возможности.

* Определенные пользователи и группы безопасности в организации могут классифицировать метки конфиденциальности и [применять их](./service-security-apply-data-sensitivity-labels.md) к содержимому Power BI. В службе Power BI это их отчеты, панели мониторинга, а также наборы и потоки данных. В Power BI Desktop это PBIX-файлы.
* В службе эти метки смогут видеть все члены организации. В версии Desktop метки будут отображаться только для тех членов организации, для которых они опубликованы.

Для активации меток конфиденциальности требуется лицензия Azure Information Protection. Дополнительные сведения см. в разделе [Лицензирование и требования](#licensing-and-requirements).

>[!NOTE]
>В течение первых 48 часов после включения пользователями предварительной версии функции Information Protection **могут возникнуть проблемы с PBIX-файлами, к которым применены метки конфиденциальности (например, с публикацией PBIX-файлов в службе или скачиванием их из службы)** . Такие проблемы ожидаемы и будут автоматически устранены в течение 48 часов.

## <a name="licensing-and-requirements"></a>Лицензирование и требования

* Для применения и просмотра меток конфиденциальности Microsoft Information Protection в Power BI требуется лицензия Azure Information Protection Premium P1 или Premium P2. Средство Azure Information Protection можно приобрести как отдельно, так и в составе одного из наборов лицензирования Майкрософт. Дополнительные сведения см. в статье [Цены на Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

    >[!NOTE]
    > Если в организации используются метки конфиденциальности Azure Information Protection, их необходимо перенести на платформу унифицированных меток Microsoft Information Protection, чтобы их можно было использовать в Power BI. [Узнайте больше о переносе меток конфиденциальности.](/azure/information-protection/configure-policy-migrate-labels)

* Чтобы применять метки к содержимому и файлам Power BI, в дополнение к указанным выше лицензиям Azure Information Protection пользователям потребуется лицензия Power BI Pro.

* Приложения Office имеют отдельные [требования к лицензированию для просмотра и применения меток конфиденциальности]( https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels#subscription-and-licensing-requirements-for-sensitivity-labels ).

* Перед включением меток конфиденциальности для арендатора убедитесь, что метки конфиденциальности определены и опубликованы для соответствующих пользователей и групп. Дополнительные сведения см. в статье [Создание и настройка меток конфиденциальности и соответствующих политик](/microsoft-365/compliance/create-sensitivity-labels).

* Для использования меток конфиденциальности в версии Desktop требуется выпуск за декабрь 2020 года или более поздняя версия.

    >[!NOTE]
    > При попытке открыть защищенный PBIX-файл с помощью версии Desktop, более ранней, чем за декабрь 2020 года, произойдет сбой, и вам будет предложено обновить версию Desktop.

## <a name="enable-sensitivity-labels"></a>Активация меток конфиденциальности

Чтобы использовать метки конфиденциальности в службе и версии Desktop, необходимо активировать эти метки в клиенте. В этом разделе описывается, как включить их в параметрах клиента. Дополнительные сведения, касающиеся версии Desktop, см. в разделе [Отключение меток конфиденциальности в версии Desktop в организации](#disable-sensitivity-labels-in-desktop-across-your-org). 

Чтобы активировать метки конфиденциальности, перейдите на **портал администрирования** Power BI, откройте панель **Параметры клиента** и найдите раздел **Information Protection**.

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

## <a name="disable-sensitivity-labels-in-desktop-across-your-org"></a>Отключение меток конфиденциальности в версии Desktop в организации

Для организаций, которые хотят, чтобы PBIX-файлы **не** поддерживали применение меток конфиденциальности, администратор Power BI может создать групповую политику, запрещающую пользователям классифицировать и защищать PBIX-файлы в Power BI или открывать файлы, к которым уже применена защита. Чтобы создать такую политику, выполните следующие действия.

1. Откройте [редактор реестра](https://support.microsoft.com/windows/how-to-open-registry-editor-in-windows-10-deab38e6-91d6-e0aa-4b7c-8878d9e07b11).

1. Найдите раздел **HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Microsoft Power BI Desktop**.

1. Найдите параметр valueName **EnableInformationProtection** и задайте для него значение **false**.

Дополнительные сведения и рекомендации, касающиеся ограничений на использование меток конфиденциальности в Power BI Desktop, см. в [обзоре меток конфиденциальности](./service-security-sensitivity-label-overview.md#limitations).

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