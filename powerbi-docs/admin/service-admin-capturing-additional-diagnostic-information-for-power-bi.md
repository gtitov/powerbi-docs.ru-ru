---
title: Сбор диагностических сведений для службы поддержки
description: В этой статье показано, как вручную собирать дополнительные диагностические сведения из службы Power BI. Отправьте эти сведения в службу поддержки, чтобы помочь специалистам устранить неполадки.
author: kfollis
ms.author: kfollis
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 01/21/2021
ms.custom: seodec18
LocalizationGroup: Troubleshooting
ms.openlocfilehash: 59e434d571c5b8d10c944bc385fb4e18ed89963c
ms.sourcegitcommit: 84f0e7f31e62cae3bea2dcf2d62c2f023cc2d404
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780959"
---
# <a name="capture-diagnostic-information-from-the-power-bi-service"></a>Сбор диагностических сведений из службы Power BI

Прежде чем связаться со службой поддержки Майкрософт для получения помощи в решении проблемы, возникающей при работе со службой Power BI, можно собрать файлы, которые помогут нам решить вашу проблему. Мы рекомендуем получить трассировку браузера из сеанса браузера. Трассировка браузера — это диагностический файл, который может предоставить важные сведения о том, что происходит в службе Power BI при возникновении проблемы.

Администраторы Power BI могут использовать раздел **Справка и поддержка** в [центре администрирования Power Platform](https://admin.powerplatform.microsoft.com/), чтобы получить решения для самостоятельного устранения проблем или обратиться в службу поддержки. Диагностические файлы, собранные с помощью приведенных ниже действий, можно вложить в запрос на поддержку, чтобы помочь нам устранить неполадки. Дополнительные варианты поддержки см. в статье [Варианты поддержки Power BI Pro и Power BI Premium](service-support-options.md).

Чтобы получить сведения о трассировке браузера и других сеансах, выполните следующие действия для используемого браузера.

## <a name="collect-a-browser-trace"></a>Сбор трассировки браузера

> [!IMPORTANT]
>Войдите в [службу Power BI](https://app.powerbi.com), *прежде чем* начать сбор данных трассировки браузера независимо от используемого браузера. Этот шаг важен, так как данные трассировки не должны включать конфиденциальную информацию, связанную с выполнением входа.

#### <a name="google-chrome-or-microsoft-edge"></a>[Google Chrome или Microsoft Edge](#tab/google-chrome-or-microsoft-edge)

Google Chrome и новая версия Microsoft Edge основаны на [проекте Chromium с открытым кодом](https://www.chromium.org/Home). В следующих шагах показано, как использовать похожие средства разработчика в двух браузерах. Дополнительные сведения см. в статьях о средствах для разработчиков [Chrome](https://developers.google.com/web/tools/chrome-devtools) и [Microsoft Edge (Chromium)](/microsoft-edge/devtools-guide-chromium).

1. Выполнив вход, нажмите клавишу F12 на клавиатуре. Или в Microsoft Edge выберите **Параметры и другое (...)**  > **Другие инструменты** > **Средства разработчика**. В Google Chrome выберите **Customize and control Google Chrome** (Настройка и управление Google Chrome) и перейдите в :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/chromium-icon-settings.png" alt-text="меню параметров Google Chrome" border="false":::. > **Другие средства** > **Средства разработчика**.
1. Подготовьтесь к сбору трассировки браузера, задав параметры трассировки. Вам также нужно будет остановить процесс и удалить все сведения, собранные до начала воспроизведения проблемы. По умолчанию браузер сохраняет сведения о трассировке только для текущей загруженной страницы. Чтобы настроить в браузере сохранение всех данных трассировки, даже если при воспроизведении будет использоваться несколько страниц, сделайте следующее:
    1. В окне **Средства разработчика** выберите вкладку **Сеть**. Затем выберите **Сохранить журнал**.
    
       :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-preserve-log.png" alt-text="Раздел &quot;Средства разработчика&quot; с выбранной вкладкой &quot;Сеть&quot; и пунктом &quot;Сохранить журнал&quot;." :::

     2. Перейдите на вкладку **Консоль** и выберите **Параметры** > **Сохранить журнал**. 
   
           :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-console-settings.png" alt-text="Раздел &quot;Средства разработчика&quot; с выбранной вкладкой &quot;Консоль&quot; и пунктом &quot;Сохранить журнал&quot;." :::

        Выберите **Параметры** еще раз, чтобы закрыть раздел **Параметры консоли**.

3. Затем остановите процесс и выполните очистку всех текущих записей. Перейдите на вкладку **Сеть**, выберите **Остановить запись сетевого журнала** и щелкните **Очистить**.
   
   :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-stop-recording.png" alt-text="Раздел Developer tools (Средства разработчика) с выбранной вкладкой Network (Сеть) и пунктами Stop recording (Остановить запись) и Clear (Очистить)." :::
     
2. Теперь вы воспроизведете проблему, которая возникла в службе Power BI. Для начала в разделе **Средства разработчика** выберите вкладку **Сеть**. Выберите **Записать сетевой журнал**.

    > [!IMPORTANT]
    >Обновите страницу браузера в службе Power BI до начала воспроизведения проблемы, чтобы правильно записать трассировки.

   Воспроизведите шаги, которые привели к проблеме.

     :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-record-network-log.png" alt-text="Раздел Developer tools (Средства разработчика) с выбранной вкладкой Network (Сеть) и пунктом &quot;Запись сетевого журнала&quot;." :::

    При воспроизведении проблемы в окне **Средства разработчика** отобразится примерно следующее:

    :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-output.png" alt-text="Раздел &quot;Средства разработчика&quot; с вкладкой &quot;Сеть&quot; и выходными данными сеанса." :::
    
3. Воспроизведя проблему, вам нужно сохранить файлы журнала и присоединить их к запросу на поддержку.
    1. Чтобы экспортировать сетевой журнал, в разделе **Средства разработчика** выберите вкладку **Сеть**. Выберите **Остановить запись сетевого журнала**. Затем выберите **Экспорт HAR...** и сохраните файл.

         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-export-har.png" alt-text="Раздел &quot;Средства разработчика&quot; с выбранной вкладкой &quot;Сеть&quot; и пунктами &quot;Остановить запись&quot; и &quot;Экспорт HAR&quot;." :::

    2. Чтобы экспортировать выходные данные консоли, в разделе **Средства разработчика** выберите вкладку **Консоль**. Щелкните правой кнопкой мыши отображаемое сообщение, а затем выберите **Сохранить как...** и сохраните выходные данные консоли в текстовый файл.
    
         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-save-as.png" alt-text="Раздел &quot;Средства разработчика&quot; с выбранной вкладкой &quot;Консоль&quot; и пунктом &quot;Сохранить как&quot;." :::

   Упакуйте сохраненный файл HAR, выходные данные консоли и запись экрана, используя такой формат сжатия, как ZIP, и вложите файл в запрос на поддержку.

#### <a name="apple-safari"></a>[Apple Safari;](#tab/apple-safari)

В следующих шагах показано, как использовать средства для разработчиков в Apple Safari. Дополнительные сведения см. в статье о [средствах для разработчиков Safari](https://support.apple.com/guide/safari-developer/safari-developer-tools-overview-dev073038698/11.0/mac).

1. Выполнив вход, включите средства разработчика в Apple Safari:
    1. В заголовке страницы выберите **Safari** > **Preferences** (Настройки).
    
       :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-preferences.png" alt-text="Меню Apple Safari с выбранным пунктом Preferences (Настройки)." :::

    2. Выберите **Advanced** (Дополнительно), а затем в строке меню выберите пункт **Show Develop menu in menu bar** (Показывать меню "Разработка" в строке меню), чтобы включить средства разработчика.
    
       :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-show-develop-menu.png" alt-text="Меню Advanced (Дополнительно) в Safari с выбранным пунктом Show Develop menu in menu bar (Показывать меню &quot;Разработка&quot; в строке меню)." :::

2. Затем задайте параметры в разделе **Web Inspector** (Веб-инспектор), чтобы браузер хранил все данные трассировки. По умолчанию браузер сохраняет сведения о трассировке только для текущей загруженной страницы. После настройки этих параметров данные трассировки будут собираться, даже если при воспроизведении проблемы используется несколько страниц.

    1. Выберите **Develop** > **Show Web Inspector** (Разработка > Показать веб-инспектор).
    
        :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-web-inspector.png" alt-text="Меню Develop (Разработка) с выбранным параметром Show Web Inspector (Показать веб-инспектор)." :::

    2. Выберите **Network** > **Preserve Log** (Сеть > Сохранить журнал).
       
         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-network-preserve-log.png" alt-text="Меню Web Inspector (Веб-инспектор) с выбранными пунктами Network (Сеть) и Preserve Log (Сохранить журнал)." :::

    1. Выберите **Console** > **Preserve Log** (Консоль > Сохранить журнал).
   
       :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-console-preserve-log.png" alt-text="Меню Web Inspector (Веб-инспектор) с выбранными пунктами Console (Консоль) и Preserve Log (Сохранить журнал)." :::

3. После установки параметров выберите **Network** > **Clear Network Items** (Сеть > Очистить сетевые элементы), чтобы убедиться в том, что журналы содержат только сведения, связанные с воспроизведением проблемы.

    :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-clear-network-items.png" alt-text="Меню Web Inspector (Веб-инспектор) с выбранными пунктами Network (Сеть) и Clear Network Items (Очистить сетевые элементы)." :::


4. Теперь все готово к воспроизведению проблемы. 
    > [!IMPORTANT]
    >Обновите страницу браузера в службе Power BI до начала воспроизведения проблемы, чтобы правильно записать трассировки.

    Выполните описанные шаги, чтобы воспроизвести возникшую проблему. При воспроизведении проблемы в окне **Network** (Сеть) отобразится примерно следующее:

    :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-session-output.png" alt-text="Окно Network (Сеть) с выходными данными." :::

5. Воспроизведя проблему, вам нужно сохранить файлы журнала и присоединить их к запросу на поддержку.

    1. Чтобы экспортировать сетевой журнал, на вкладке **Network** (Сеть) выберите **Export** (Экспорт) и сохраните файл в формате HAR.

         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/safari-export.png" alt-text="Вкладка Network (Сеть) с выбранным пунктом Export (Экспорт)." :::

    2. Чтобы экспортировать выходные данные консоли, на панели **Develop tools** (Средства разработчика) выберите вкладку **Console** (Консоль) и разверните окно. Поместите курсор в начало выходных данных консоли, а затем выделите все содержимое выходных данных. Скопируйте выходные данные с помощью клавиш COMMAND-C и сохраните их в текстовом файле.

   Упакуйте сохраненный файл HAR, выходные данные консоли и запись экрана, используя такой формат сжатия, как ZIP, и вложите файл в запрос на поддержку.

#### <a name="firefox"></a>[Firefox](#tab/firefox)

В следующих шагах показано, как использовать средства для разработчиков в Firefox. Дополнительные сведения см. в документации, посвященной [средствам разработчика Firefox](https://developer.mozilla.org/docs/Tools).

1. Выполнив вход, нажмите клавишу F12 на клавиатуре. Или же в браузере Firefox выберите **Open menu** (Открыть меню) :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/firefox-menu.png" alt-text="значок меню Firefox" border="false":::. > **Web Developer** > **Toggle Tools** (Веб-разработчик > Включить средства). Средства отобразятся в нижней части экрана.

1. Затем вы зададите параметры в разделе **Inspector** (Инспектор), чтобы браузер хранил все данные трассировки. По умолчанию браузер сохраняет сведения о трассировке только для текущей загруженной страницы. После настройки этих параметров данные трассировки будут собираться, даже если при воспроизведении проблемы используется несколько страниц.

    1. В окне **Inspector** (Инспектор) выберите вкладку **Network** (Сеть). Затем выберите **Persist Logs** (Сохранить журналы).
    
       :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/firefox-network-persist-logs.png" alt-text="Средства Inspector (Инспектор) с выбранной вкладкой Network (Сеть) и пунктом Persist Logs (Сохранить журналы)." :::

     2. Перейдите на вкладку **Console** (Консоль) и выберите **Console settings** > **Persist Logs** (Параметры консоли > Сохранить журналы). 
   
           :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/firefox-console-persist-logs.png" alt-text="Средства Inspector (Инспектор) с выбранной вкладкой Console (Консоль) и пунктом Persist Logs (Сохранить журналы)." :::

3. Настроив параметры, выполните очистку всех текущих записей. Выберите вкладку **Network** (Сеть) и щелкните **Clear** (Очистить).
   
   :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/browser-trace-stop-recording.png" alt-text="Раздел Developer tools (Средства разработчика) с выбранной вкладкой Network (Сеть) и пунктами Stop recording (Остановить запись) и Clear (Очистить)." :::
     
2. Теперь все готово к воспроизведению проблемы. 
    > [!IMPORTANT]
    >Обновите страницу браузера в службе Power BI до начала воспроизведения проблемы, чтобы правильно записать трассировки.
 
    Выполните описанные шаги, чтобы воспроизвести возникшую проблему.
    
3. Воспроизведя проблему, вам нужно сохранить файлы журнала и присоединить их к запросу на поддержку.
    1. Чтобы экспортировать сетевой журнал, выберите **Network** > **HAR Export/Import** (Сеть > Экспорт и импорт HAR) и щелкните **Save All as HAR** (Сохранить все как HAR).

         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/firefox-save-har.png" alt-text="Вкладка Network (Сеть) с выделенным меню HAR Export/Import (Экспорт и импорт HAR) и пунктом Save All as HAR (Сохранить все как HAR)." :::

    2. Чтобы экспортировать выходные данные консоли, выберите вкладку **Console** (Консоль). Щелкните правой кнопкой мыши отображаемое сообщение, а затем выберите **Export Visible Messages To** (Экспорт видимых сообщений в) и сохраните выходные данные консоли в текстовый файл.
    
         :::image type="content" source="media/service-admin-capturing-additional-diagnostic-information-for-power-bi/firefox-export-visible-messages.png" alt-text="Вкладка Console (Консоль) с выделенным пунктом Export Visible Messages To (Экспорт видимых сообщений в)." :::

   Упакуйте сохраненный файл HAR, выходные данные консоли и запись экрана, используя такой формат сжатия, как ZIP, и вложите файл в запрос на поддержку.

---

Собрав файлы диагностики, вложите их в запрос на поддержку, чтобы помочь инженеру службы поддержки решить вашу проблему. Файл HAR будет содержать все сведения о сетевых запросах между окном браузера и службой Power BI, в том числе:

* идентификаторы действий для каждого запроса;

* точную метку времени для каждого запроса;

* все сведения об ошибках, возвращенные клиенту.

Эта трассировка также будет содержать данные, используемые для заполнения визуальных элементов, отображаемых на экране.

## <a name="next-steps"></a>Дальнейшие действия

* [Отслеживание работоспособности службы Power BI в Microsoft 365](service-admin-health.md)
* [Включение уведомлений о прерывании в работе служб](service-interruption-notifications.md)
* [Присоединиться к сообществу Power BI](https://community.powerbi.com/)
