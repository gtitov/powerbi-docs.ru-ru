---
title: Подключение к файлам в OneDrive для классической рабочей области
description: Узнайте о хранении файлов Excel, CSV и Power BI Desktop в хранилище OneDrive для классической рабочей области Power BI, а также о подключении к ним.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: lukasz
ms.service: powerbi
ms.subservice: pbi-collaborate-share
ms.topic: how-to
ms.date: 01/28/2021
LocalizationGroup: Share your work
ms.openlocfilehash: f6544a137b8f656e938db4516de5e8c0685394b4
ms.sourcegitcommit: fb529c4532fbbdfde7ce28e2b4b35f990e8f21d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2021
ms.locfileid: "99085823"
---
# <a name="connect-to-files-stored-in-onedrive-for-a-classic-workspace"></a>Подключение к файлам, хранящимся в OneDrive, для классической рабочей области
При [создании *классической* рабочей области в Power BI](service-create-workspaces.md) также создается группа Microsoft 365 со связанным хранилищем OneDrive для бизнеса. В этой статье объясняется, как хранить и обновлять файлы Excel, CSV и Power BI Desktop в OneDrive для бизнеса. Эти обновления будут автоматически отражаться в отчетах и на панелях мониторинга Power BI на основе этих файлов.

> [!NOTE]
> В *новом* интерфейсе рабочей области изменятся отношения между рабочими областями Power BI и группами Microsoft 365. Группа Microsoft 365 не создается автоматически при каждом создании одной из новых рабочих областей. Вы также можете [выбрать новую рабочую область для OneDrive](service-create-the-new-workspaces.md#set-a-workspace-onedrive).

Добавление файлов в классическую рабочую область состоит из двух этапов. 

1. Сначала вам необходимо [отправить файлы в хранилище OneDrive для бизнеса](#1-upload-files-to-the-onedrive-for-business-for-your-workspace) для рабочей области.
2. Затем вы [подключитесь к этим файлам из Power BI](#2-import-excel-files-as-datasets-or-as-excel-online-workbooks).

> [!NOTE]
> Рабочие области доступны только по лицензии [Power BI Pro](../fundamentals/service-features-license-type.md).
> 

## <a name="1-upload-files-to-the-onedrive-for-business-for-your-workspace"></a>1\. Отправка файлов в хранилище OneDrive для бизнеса для рабочей области
1. В службе Power BI щелкните стрелку рядом с элементом "Рабочие области" и выберите кнопку с многоточием ( **…** ) рядом с именем рабочей области. 
   
   ![Снимок экрана: рабочая область Power BI с выбранным именем рабочей области](media/service-connect-to-files-in-app-workspace-onedrive-for-business/power-bi-app-ellipsis.png)
2. Выберите **Файлы**, чтобы открыть OneDrive для бизнеса для рабочей области в Microsoft 365.
   
   > [!NOTE]
   > Если в меню рабочей области не отображается параметр **Файлы**, выберите **участников**, чтобы открыть хранилище OneDrive для бизнеса для рабочей области. Затем выберите **Файлы**. Microsoft 365 задает расположение хранилища OneDrive для файлов рабочей области группы приложения. Этот процесс может занять некоторое время.
   > 
   > 
3. Теперь вы можете отправить файлы в хранилище OneDrive для бизнеса для рабочей области. Выберите команду **Отправить** и перейдите к своим файлам.
   
   ![Снимок экрана OneDrive для бизнеса, демонстрирующий переход к отправке файла](media/service-connect-to-files-in-app-workspace-onedrive-for-business/pbi_grpfilesonedrive.png)

## <a name="2-import-excel-files-as-datasets-or-as-excel-online-workbooks"></a>2\. Импорт файлов Excel в качестве наборов данных или книг Excel Online
Теперь, когда файлы находятся в хранилище OneDrive для бизнеса вашей рабочей области, есть два варианта действий. Вы можете выбрать один из следующих вариантов. 

* [Импортировать данные из книги Excel в виде наборов данных](../connect-data/service-get-data-from-files.md), чтобы использовать эти данные для создания отчетов и панелей мониторинга. Их можно просматривать в браузере и на мобильных устройствах.
* [Подключиться к целой книге Excel в Power BI](../connect-data/service-excel-workbook-files.md) и отобразить ее так же, как в Excel Online.

### <a name="import-or-connect-to-the-files-in-your-workspace"></a>Импорт файлов в рабочей области или подключение к ним
1. В Power BI перейдите в рабочую область, чтобы ее имя отобразилось в левом верхнем углу. 
2. В нижней части области навигации выберите **Получить данные**. 
   
   ![Снимок экрана: кнопка "Получить данные" в области навигации](media/service-connect-to-files-in-app-workspace-onedrive-for-business/power-bi-app-get-data-button.png)
3. В поле **Файлы** выберите **Получить**.
   
   ![Снимок экрана: диалоговое окно "Файлы" с кнопкой "Получить"](media/service-connect-to-files-in-app-workspace-onedrive-for-business/pbi_getfiles.png)
4. Выберите **OneDrive** - *имя вашей рабочей области*.
   
    ![Снимок экрана: три плитки для выбора рабочей области — "Локальный файл", "OneDrive" и "SharePoint"](media/service-connect-to-files-in-app-workspace-onedrive-for-business/pbi_grp_one_drive_shrpt.png)
5. Щелкните нужный файл, затем — **Подключиться**.
   
    На этом этапе вы решаете, что следует делать: [импортировать данные из книги Excel](../connect-data/service-get-data-from-files.md) или [подключиться к книгам Excel целиком](../connect-data/service-excel-workbook-files.md).
6. Выберите команду **Импортировать** или **Подключиться**.
   
    ![Снимок экрана: диалоговое окно OneDrive для бизнеса с параметрами для импорта из Excel или подключения к Excel](media/service-connect-to-files-in-app-workspace-onedrive-for-business/pbi_importexceldataorwholecrop.png)
7. Если выбрать **Импортировать**, книга отобразится на вкладке **Наборы данных**. 
   
    ![Снимок экрана: рабочие области в Power BI с вкладкой "Наборы данных"](media/service-connect-to-files-in-app-workspace-onedrive-for-business/power-bi-app-excel-file-import.png)
   
    Если выбрать **Подключиться**, книга отобразится на вкладке **Книги**.
   
    ![Снимок экрана: рабочие области в Power BI с вкладкой "Книги"](media/service-connect-to-files-in-app-workspace-onedrive-for-business/power-bi-app-excel-file-connect.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Создание и распространение приложений и рабочих областей в Power BI](../collaborate-share/service-create-distribute-apps.md)
* [Импорт данных из книг Excel](../connect-data/service-get-data-from-files.md)
* [Подключение к целым книгам Excel](../connect-data/service-excel-workbook-files.md
* Появились дополнительные вопросы? [Ответы на них см. в сообществе Power BI.](https://community.powerbi.com/)
* Хотите оставить отзыв? Посетите [форум идей по улучшению Power BI](https://ideas.powerbi.com/forums/265200-power-bi).
