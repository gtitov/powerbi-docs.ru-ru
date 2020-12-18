---
title: Руководство. Использование Cognitive Services в Power BI (предварительная версия)
description: В этом руководстве описано, как использовать Cognitive Services и потоки данных в Power BI.
author: davidiseminger
ms.author: davidi
ms.reviewer: SarinaJoan
ms.service: powerbi
ms.subservice: pbi-data-sources
ms.custom: connect-to-services
ms.topic: tutorial
ms.date: 02/20/2020
LocalizationGroup: Connect to services
ms.openlocfilehash: 22548c092e1407d1744a019c15cb0d29a94913eb
ms.sourcegitcommit: 772c65b7b440ab082510bf3f64b871d19139d451
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2020
ms.locfileid: "97353365"
---
# <a name="tutorial-use-cognitive-services-in-power-bi"></a>Руководство. Использование Cognitive Services в Power BI

Power BI предоставляет доступ к набору функций Azure Cognitive Services, которые дополняют ваши данные при самостоятельной подготовке данных для потоков данных. Сейчас поддерживаются службы [анализа тональности](/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis), [извлечения ключевых фраз](/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-keyword-extraction), [распознавания языка](/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-language-detection) и [добавления тегов к изображению](/azure/cognitive-services/computer-vision/concept-tagging-images). Преобразования выполняются в службе Power BI, для чего не требуется подписка на Azure Cognitive Services. Эта функция доступна в Power BI Premium.

Выполняемые Cognitive Services преобразования поддерживаются при [самостоятельной подготовке данных для потоков данных](https://powerbi.microsoft.com/blog/introducing-power-bi-data-prep-wtih-dataflows/). Воспользуйтесь пошаговыми примерами для текстовой аналитики и добавления тегов к изображениям ниже, чтобы начать работу.

Из этого руководства вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * импорт данных в поток данных;
> * оценка тональности и извлечение ключевых фраз из текстового столбца в потоке данных;
> * подключение к результатам из Power BI Desktop.


## <a name="prerequisites"></a>Предварительные требования

Для работы с этим руководством вам нужно следующее: 

- Учетная запись Power BI. Если вы не зарегистрированы в Power BI, перед началом работы [пройдите бесплатную регистрацию](https://app.powerbi.com/signupredirect?pbi_source=web).
- Доступ к емкости Power BI Premium с включенной рабочей нагрузкой ИИ. По умолчанию для предварительной версии эта рабочая нагрузка отключена. Если вы используете емкость Premium, но Аналитика ИИ не отображается, обратитесь к своему администратору емкости Premium, чтобы включить рабочую нагрузку ИИ на портале администрирования.

## <a name="text-analytics"></a>Текстовая аналитика

Выполните шаги в этом разделе, чтобы пройти посвященную текстовой аналитике часть этого руководства.

### <a name="step-1-apply-sentiment-scoring-in-power-bi-service"></a>Шаг 1. Применение оценки тональности в службе Power BI

Чтобы начать работу, перейдите в рабочую область Power BI с емкостью Premium и создайте поток данных с помощью кнопки **Создать** в верхнем правом углу экрана.

![Снимок экрана: рабочая область Power BI с кнопкой "Создать" и выбранным элементом "Панель мониторинга".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_01.png)

В диалоговом окне потока данных доступны несколько вариантов создания потока данных. Выберите **Добавить новые сущности**. Затем выберите **Текст/CSV** из меню источников данных.

![Снимок экрана: панель выбора источника данных с источником "Текст/CSV".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_02.png)

Вставьте этот URL-адрес в поле URL-адреса: [https://pbiaitutorials.blob.core.windows.net/textanalytics/FabrikamComments.csv](https://pbiaitutorials.blob.core.windows.net/textanalytics/FabrikamComments.csv) и нажмите кнопку **Далее**.

![Снимок экрана: страница "Подключение к источнику данных", на которой вводится URL-адрес.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_03.png)

Данные теперь готовы для текстовой аналитики, и мы можем применить функции оценки тональности и извлечения ключевых фраз к столбцу с комментариями клиентов.

В редакторе Power Query выберите **Аналитика ИИ**

![Снимок экрана: страница "Изменение запросов" с выделенным элементом "Вся аналитика".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_04.png)

Разверните папку **Cognitive Services** и выберите нужную функцию. В этом примере используется оценка тональности в столбце комментариев, но вы можете выполнить эти же шаги, чтобы запустить распознавание языка и извлечение ключевых фраз.

![Снимок экрана: страница "Вызов функции" с выбранной функцией.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_05.png)

После выбора функции отобразятся обязательные и необязательные поля. Чтобы оценить тональность в примерах отзывов, выберите столбец с отзывами в качестве текстовых входных данных. Язык и региональные параметры (в формате ISO) указывать необязательно. Например, введите en, если нужно, чтобы язык текст распознавался как английский. Если поле оставлено пустым, Power BI определит язык входного значения, прежде чем начинать оценку тональности.

![Снимок экрана: диалоговое окно "Вызов функции" с раскрывающимся меню "текст".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_06.png)

Теперь нажмите **Вызвать**, чтобы выполнить функцию. В таблицу будет добавлен новый столбец с оценкой тональности для каждой строки. Вы можете вернуться к **Аналитике ИИ**, чтобы аналогичным способом извлечь ключевые фразы из текста отзывов.

После завершения преобразований измените имя запроса на "Комментарии клиентов" и нажмите **Готово**.

![Снимок экрана: страница "Изменение запросов" с выделенным элементом "Имя".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_07.png)

Затем нажмите **Сохранить**, чтобы сохранить поток данных, и присвойте ему имя Fabrikam. Нажмите кнопку **Обновить сейчас**, которая отобразилась после сохранения потока данных.

![Снимок экрана: кнопка "Сохранить".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_08.png)

Сохранив и обновив поток данных, вы можете использовать его в отчете Power BI.

### <a name="step-2-connect-from-power-bi-desktop"></a>Шаг 2. Подключение из Power BI Desktop

Откройте Power BI Desktop. На вкладке ленты "Главная" выберите **Получить данные**.

Перейдите к пункту **Потоки данных Power BI (бета-версия**) в разделе Power BI и выберите **Подключить**.

![Снимок экрана: панель "Получение данных" с выбранным элементом "Потоки данных Power BI".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_09.png)

Так как это предварительная версия функции, соединитель отобразит запрос на принятие соответствующих условий. Примите условия и войдите с помощью учетной записи своей организации.

![Снимок экрана: сообщение входа для вашей учетной записи организации.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_10.png)

Выберите поток данных, который вы только что создали. Перейдите к таблице "Комментарии клиентов" и щелкните **Загрузить**.

![Снимок экрана: страница "Навигатор" с выбранной таблицей "Комментарии клиентов".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_11.png)

После загрузки данных вы можете приступить к созданию отчета.

## <a name="image-tagging"></a>Добавление тегов к изображениям

Перейдите в рабочую область Power BI с емкостью Premium. Создайте поток данных с помощью кнопки **Создать** в правом верхнем углу экрана.

![Снимок экрана: рабочая область Power BI с кнопкой "Создать" и выбранным элементом "Поток данных".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_12.png)

Выберите **Добавить новые сущности**.

![Снимок экрана: параметр добавления новых сущностей для начала создания рабочего процесса.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_13.png)

Когда вам будет предложено выбрать источник данных, выберите **Пустой запрос**.

![Снимок экрана: панель выбора источника данных с источником "Пустой запрос".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_14.png)

Скопируйте запрос ниже в редактор запросов и нажмите кнопку "Далее". Вы можете заменить пути URL-адресов ниже другими изображениями или добавить дополнительные строки. Функция *Web.Contents* импортирует изображение по указанному URL-адресу в двоичном виде. Если вам доступен источник данных с изображениями, которые хранятся в двоичном виде, вы можете использовать их напрямую.


```python
let
  Source = Table.FromRows({
  { Web.Contents("https://images.pexels.com/photos/87452/flowers-background-butterflies-beautiful-87452.jpeg") },
  { Web.Contents("https://upload.wikimedia.org/wikipedia/commons/5/53/Colosseum_in_Rome%2C_Italy_-_April_2007.jpg") }}, { "Image" })
in
  Source
```

![Снимок экрана: страница "Подключение к источнику данных" с запросом и кнопкой "Далее".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_15.png)

При запросе учетных данных выберите *анонимный вход*.

![Снимок экрана: страница "Изменение запросов", на которой можно указать учетные данные.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_16.png)

Отобразится следующее изображение.

![Снимок экрана: диалоговое окно ввода учетных данных, в котором можно указать тип проверки подлинности.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_17.png)

Запрос учетных данных будет отображаться для каждой отдельной веб-страницы.

Выберите **Аналитика ИИ** в редакторе запросов.

![Снимок экрана: страница "Изменение запросов" с выделенным элементом "Вся аналитика" и одним отображаемым предупреждением.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_18.png)

Затем войдите с помощью своей **учетной записи в организации**.

![Снимок экрана: диалоговое окно ввода учетных данных, в котором можно указать учетную запись в организации.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_19.png)

Выберите функцию "Добавление тегов к изображению", введите _[Двоичный]_ в поле столбца и _en_ в поле языка и региональных параметров. 

> [!NOTE]
> Сейчас вы не сможете выбрать столбец в раскрывающемся списке. Такая возможность будет в ближайшем будущем добавлена в закрытой предварительной версии.

![Снимок экрана: страница "Вызов функции" с выбранной функцией "TagImages".](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_20.png)

В редакторе функций удалите кавычки, в которые заключено имя столбца. 

> [!NOTE]
> Удаление кавычек — это временное решение. Полноценная функциональность будет в ближайшем будущем добавлена в предварительной версии.

![Снимок экрана: редактор функций с выделенным фрагментом Image без кавычек.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_21.png)

Эта функция возвращает запись в формате разделенных запятыми списка тегов и в виде записи json. Нажмите кнопку "Развернуть", чтобы добавить в таблицу одну или обе этих записи в виде столбцов.

![Снимок экрана: кнопка "Развернуть" с двумя стрелками, направленными в противоположные стороны.](media/service-tutorial-using-cognitive-services/tutorial-using-cognitive-services_22.png)

Нажмите **Готово** и сохраните поток данных. Обновив первый поток данных, вы можете подключить его из Power BI Desktop с помощью соединителей потоков данных. (См. шаги на стр. 5 этого документа.)

## <a name="clean-up-resources"></a>Очистка ресурсов

Если запрос вам больше не нужен, удалите его, щелкнув его имя правой кнопкой мыши в редакторе Power Query и нажав **Удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы применили функции оценки тональности и добавления тегов к изображениям для потока данных Power BI. Подробнее о Cognitive Services в Power BI можно узнать в следующих статьях:

* [Документация по службам Azure Cognitive Services](/azure/cognitive-services/).
* Начало работы [с самостоятельной подготовкой данных для потоков данных](../transform-model/dataflows/dataflows-introduction-self-service.md).
* Дополнительные сведения о [Power BI Premium](https://powerbi.microsoft.com/power-bi-premium/).

Также рекомендуем ознакомиться со следующими статьями.

* [Руководство. Использование моделей Машинного обучения Azure в Power BI](service-aml-integrate.md)
* [Интеграция Машинного обучения Azure в Power BI (предварительная версия)](../transform-model/dataflows/dataflows-machine-learning-integration.md)
* [Использование Cognitive Services в Power BI (предварительная версия)](../transform-model/dataflows/dataflows-machine-learning-integration.md)