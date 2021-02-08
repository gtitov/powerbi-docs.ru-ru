---
title: Установка Power BI Desktop для Сервера отчетов Power BI
description: Узнайте, как установить приложение Power BI Desktop для Сервера отчетов Power BI.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: how-to
ms.date: 10/16/2020
ms.openlocfilehash: 068d4a025bda878899e2d54f93bc56eaea336f3e
ms.sourcegitcommit: 7ed995eed0fd6e718748accf87bae384211cd95d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99044087"
---
# <a name="install-power-bi-desktop-for-power-bi-report-server"></a>Установка Power BI Desktop для Сервера отчетов Power BI

Чтобы создавать отчеты Power BI для сервера отчетов Power BI, скачайте и установите версию Power BI Desktop, которая оптимизирована для этого сервера. Этот выпуск отличается от выпуска Power BI Desktop, который используется в службе Power BI. Например, версия Power BI Desktop для службы Power BI включает предварительные версии функций. Эти функции не публикуются на Сервере отчетов Power BI, пока они не будут предоставлены в общий доступ. Использование этого выпуска позволяет обеспечить взаимодействие между сервером отчетов и известной версией отчетов и модели. 

Не беспокойтесь. Приложения Power BI Desktop и Power BI Desktop для Сервера отчетов Power BI можно устанавливать параллельно на одном компьютере.

## <a name="download-and-install-power-bi-desktop"></a>Загрузка и установка Power BI Desktop

Самый простой способ скачать последнюю версию приложения Power BI Desktop для Сервера отчетов Power BI — запустить его с веб-портала Сервера отчетов.

1. На веб-портале сервера отчетов последовательно выберите **Загрузка** > **Power BI Desktop**.

    ![Скачивание Power BI Desktop из веб-портала](media/install-powerbi-desktop/report-server-download-web-portal.png)

    Либо перейдите на домашнюю страницу [Сервера отчетов Power BI](https://powerbi.microsoft.com/report-server/) и выберите **Расширенные параметры загрузки**.

2. На странице центра загрузки выберите язык и нажмите кнопку **Скачать**.

3. В зависимости от компьютера выберите файл: 

    - **PBIDesktopRS.msi** (32-разрядная версия);
    - **PBIDesktopRS_x64.msi** (64-разрядная версия).

1. Скачав установщик, запустите мастер установки Power BI Desktop.

2. На завершающем этапе процесса установки выберите параметр **Запустить Power BI Desktop**.

    После автоматического запуска приложения вы будете готовы к работе.

## <a name="verify-youre-using-the-correct-version"></a>Проверка используемой версии
Проверить используемую версию Power BI Desktop нетрудно: Посмотрите на экран запуска или заголовок окна Power BI Desktop. Если в строке заголовка отображается **Power BI Desktop (январь 2021 г.)** или более поздний выпуск, вы установили правильную версию. Кроме того, цвета логотипа Power BI изменены на обратные: желтый на черном вместо черного на желтом.

![Power BI Desktop (январь 2021 г.)](media/install-powerbi-desktop/power-bi-report-server-desktop.png)

В строке заголовка версии Power BI Desktop для службы Power BI не указаны месяц и год выпуска.

## <a name="file-extension-association"></a>Сопоставление расширения файла
Предположим, что вы установили приложения Power BI Desktop и Power BI Desktop для Сервера отчетов Power BI параллельно на одном компьютере. Файлы PBIX сопоставляются с самой последней установкой Power BI Desktop. Поэтому при двойном щелчке по PBIX-файлу будет запущен последний установленный экземпляр Power BI Desktop.

Если у вас уже есть Power BI Desktop, а затем вы устанавливаете Power BI Desktop для Сервера отчетов Power BI, все PBIX-файлы будут по умолчанию открываться в Power BI Desktop для Сервера отчетов Power BI. Если необходимо, чтобы при открытии PBIX-файлов по умолчанию запускалось приложение Power BI Desktop, переустановите [Power BI Desktop из Microsoft Store](https://aka.ms/pbidesktopstore).

Всегда можно открыть ту версию Power BI Desktop, которую нужно использовать первой, а затем открыть файл в приложении Power BI Desktop.

Вот самый надежный способ всегда открывать правильную версию Power BI Desktop. Начните редактировать отчет Power BI на Сервере отчетов Power BI или создайте отчет Power BI в службе Power BI.

## <a name="considerations-and-limitations"></a>Рекомендации и ограничения

Отчеты на сервере отчетов Power BI и в службе Power BI (`https://app.powerbi.com`), а также в мобильных приложениях Power BI работают почти одинаково, но некоторые функции все же различаются.

### <a name="selecting-a-language"></a>Выбор языка

Для версии Power BI Desktop для Сервера отчетов Power BI выбор языка осуществляется при установке приложения. Вы не можете изменить сделанный выбор, однако при необходимости можно установить версию на другом языке.

### <a name="report-visuals-in-a-browser"></a>Визуальные элементы отчетов в браузере

Отчеты на сервере отчетов Power BI поддерживают почти все визуализации, в том числе визуальные элементы Power BI. Отчеты на сервере отчетов Power BI не поддерживают:

* визуальные элементы R;
* строки навигации;
* Функции предварительной версии Power BI Desktop

### <a name="reports-in-the-power-bi-mobile-apps"></a>Отчеты в мобильных приложениях Power BI

Отчеты на сервере отчетов Power BI поддерживают все функциональные возможности, доступные в [мобильных приложениях Power BI](../consumer/mobile/mobile-apps-for-mobile-devices.md), в том числе:

* [Макет отчета для мобильной версии](../create-reports/desktop-create-phone-report.md). Вы можете оптимизировать отчет для мобильных приложений Power BI. На мобильных устройствах у оптимизированных отчетов есть специальный значок ![Макет отчета для телефона](media/install-powerbi-desktop/power-bi-rs-mobile-optimized-icon.png) и макет.
  
    ![Отчет, оптимизированный для телефонов](media/install-powerbi-desktop/power-bi-rs-mobile-optimized-report.png)

В мобильных приложениях Power BI отчеты на сервере отчетов Power BI не поддерживают:

* Визуальные элементы R
* Визуальные элементы Power BI
* строки навигации;
* географическую фильтрацию и штрихкоды.

### <a name="custom-security"></a>Настраиваемая безопасность

Приложение Power BI Desktop для Сервера отчетов Power BI не поддерживает настраиваемую безопасность. Если в сервере отчетов Power BI включен настраиваемый модуль безопасности, вы не сможете сохранить отчет Power BI из приложения Power BI Desktop (оптимизированного для сервера отчетов Power BI) на экземпляре сервера отчетов Power BI. Необходимо вместо этого сохранить PBIX-файл отчета из Power BI Desktop и отправить его на сайт портала сервера отчетов Power BI.

### <a name="saving-reports-to-a-power-bi-report-server-in-a-different-domain"></a>Сохранение отчетов на сервере отчетов Power BI в другом домене

При сохранении отчета Power BI на сервере отчетов Power BI используются учетные данные Windows. Сохранение напрямую на сервере отчетов в другом домене с учетными данными Windows не поддерживается. Чтобы просмотреть сервер отчетов и вручную отправить файл с компьютера, можно использовать веб-браузер.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда приложение Power BI Desktop установлено, можно приступить к созданию отчетов Power BI.

[Создание отчета Power BI для Сервера отчетов Power BI](quickstart-create-powerbi-report.md)  
[Что такое Сервер отчетов Power BI?](get-started.md)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)

