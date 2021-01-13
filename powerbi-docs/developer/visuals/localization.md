---
title: Добавление языкового стандарта для визуальных элементов в Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Узнайте, как визуальные элементы могут определять языковой стандарт Power BI для локализации содержимого на соответствующем языке. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
manager: rkarlin
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: 4df09979eeae476578b247e729a31f5f5c9c9baa
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888220"
---
# <a name="add-the-locale-in-power-bi-for-power-bi-visuals"></a>Добавление языкового стандарта в Power BI для визуальных элементов Power BI

Визуальные элементы могут определять языковой стандарт Power BI для локализации содержимого на соответствующем языке.

Дополнительные сведения см. в статье [Поддерживаемые языки и страны (регионы) для Power BI](./../../fundamentals/supported-languages-countries-regions.md).

Например, получим языковой стандарт в примере визуального элемента "Линейчатая диаграмма".

![Локализация в примере визуального элемента "Линейчатая диаграмма"](media/localization/locale-in-samplebarchart.png)

Каждая из этих линейчатых диаграмм была создана с использованием особого языкового стандарта (английский, баскский и хинди), который указан в подсказке.

> [!NOTE]
> Диспетчер локализации в коде визуального элемента поддерживается, начиная с версии API 1.10.0.

## <a name="get-the-locale"></a>Получение языкового стандарта

Значение `locale` передается в виде строки во время инициализации визуального элемента. Если языковой стандарт в Power BI меняется, визуальный элемент создается заново с новым языковым стандартом. Полный пример кода см. в репозитории визуального элемента SampleBarChart с языковым стандартом.

Конструктор BarChart теперь имеет член locale, экземпляр которого создается в конструкторе с экземпляром locale узла.

```typescript
private locale: string;
...
this.locale = options.host.locale;
```

Поддерживаемые языковые стандарты

Строка языкового стандарта | Язык
--------------|----------------------
ar-SA | العربية (арабский)
bg-BG | български (болгарский)
ca-ES | català (каталанский)
cs-CZ | čeština (чешский)
da-DK | dansk (датский)
de-DE | Deutsche (немецкий)
el-GR | ελληνικά (греческий)
en-US | English (английский)
es-ES | español (испанский)
et-EE | eesti (эстонский)
eU-ES | Euskal (баскский)
fi-FI | suomi (финский)
fr-FR | français (французский)
gl-ES | galego (галисийский)
he-IL | עברית (иврит)
hi-IN | हिन्दी (хинди)
hr-HR | hrvatski (хорватский)
hu-HU | magyar (венгерский)
id-ID | Bahasa Indonesia (индонезийский)
it-IT | italiano (итальянский)
ja-JP | 日本の (японский)
kk-KZ | Қазақ (казахский)
ko-KR | 한국의 (корейский)
lt-LT | Lietuvos (литовский)
lv-LV | Latvijas (латышский)
ms-MY | Bahasa Melayu (малайский)
nb-NO | norsk (норвежский)
nl-NL | Nederlands (нидерландский)
pl-PL | polski (польский)
pt-BR | português (португальский)
pt-PT | português (португальский)
ro-RO | românesc (румынский)
ru-RU | русский (русский)
sk-SK | slovenský (словацкий)
sl-SI | slovenski (словенский)
sr-Cyrl-RS | српски (сербский)
sr-Latn-RS | srpski (сербский)
sv-SE | svenska (шведский)
th-TH | ไทย (тайский)
tr-TR | Türk (турецкий)
uk-UA | український (украинский)
vi-VN | tiếng Việt (вьетнамский)
zh-CN | 中国 (китайский, упрощенное письмо)
zh-TW | 中國 (китайский, традиционное письмо)

> [!NOTE]
> В приложении PowerBI Desktop свойство locale будет содержать язык установленной версии.

## <a name="localizing-the-property-pane-for-power-bi-visuals"></a>Локализация области свойств для визуальных элементов Power BI

Поля в области свойств можно локализовать, чтобы обеспечить согласованность. Это делает пользовательский визуальный элемент похожим на любой из основных визуальных элементов Power BI.

Например, для нелокализованного пользовательского визуального элемента, созданного с помощью команды `pbiviz new`, в области свойств будут отображаться следующие поля.

![Локализация в области свойств](media/localization/property-pane.png)

Строки "Category Data" (Данные категорий) и "Measure Data" (Данные мер) определены в файле capabilities.json как `displayName`.

## <a name="how-to-localize-capabilities"></a>Локализация возможностей

Сначала добавьте ключ отображаемого имени для каждого отображаемого имени, которое необходимо локализовать. В этом примере:

```json
{
    "dataRoles": [
        {
            "displayName": "Category Data",
            "displayNameKey": "VisualCategoryDataNameKey1",
            "name": "category",
            "kind": "Grouping"
        },
        {
            "displayName": "Measure Data",
            "displayNameKey": "VisualMeasureDataNameKey2",
            "name": "measure",
            "kind": "Measure"
        }
    ]
}
```

Затем добавьте каталог stringResources. Он будет содержать все файлы со строковыми ресурсами для языковых стандартов, которые должен поддерживать визуальный элемент. В этом каталоге необходимо добавить JSON-файл для каждого языкового стандарта, который должен поддерживаться. Этот файл будет содержать сведения о языковом стандарте и локализованные строки для каждого элемента displayNameKey, который необходимо заменить.

Предположим, что должны поддерживаться арабский язык и иврит. В этом случае необходимо добавить два JSON-файла следующим образом:

![Локализованные строки в папке со строковыми ресурсами](media/localization/stringresources-files.png)

В каждом файле JSON определен один языковой стандарт (из приведенного выше списка поддерживаемых стандартов) и содержатся строковые значения для соответствующих ключей отображаемых имен. В нашем примере файл со строковыми ресурсами на иврите будет выглядеть следующим образом.

```json
{
    "locale": "he-IL",
    "values": {
        "VisualCategoryDataNameKey1": "קטגוריה",
        "VisualMeasureDataNameKey2": "יחידות מידה"
    }
}
```

Ниже описаны все необходимые действия для использования диспетчера локализации.

> [!NOTE]
> В настоящее время локализация не поддерживается при отладке разрабатываемого визуального элемента.

## <a name="setup-environment"></a>Настраиваете среду.

### <a name="desktop"></a>Рабочий стол

Чтобы использовать классическое приложение, скачайте локализованную версию Power BI Desktop с сайта https://powerbi.microsoft.com.

### <a name="web-service"></a>Веб-служба

Если вы используете веб-клиент службы в браузере, измените язык в параметрах:

![Локализация в веб-службе](media/localization/webservice-settings.png)

## <a name="resource-file"></a>Файл ресурсов

Добавьте файл resources.resjson в папку, имя которой совпадает с названием соответствующего языкового стандарта, в папке stringResources. В нашем примере это en-US и ru-RU.

![Новый файл RESJSON](media/localization/new-resjson.png)

После этого добавьте все нужные локализованные строки в файл resources.resjson, добавленный на предыдущем шаге.

```json
{
    ...
    "Role_Legend": "Обозначения",
    "Role_task": "Задача",
    "Role_StartDate": "Дата начала",
    "Role_Duration": "Длительность"
    ...
}
```

Вот пример файла resources.resjson для языкового стандарта en-US:

```json
{
    ...
    "Role_Legend": "Legend",
    "Role_task": "Task",
    "Role_StartDate": "Start date",
    "Role_Duration": "Duration"
    ...
}
```

Создайте экземпляр localizationManager в коде визуального элемента следующим образом:

```typescript
private localizationManager: ILocalizationManager;

constructor(options: VisualConstructorOptions) {
    this.localizationManager = options.host.createLocalizationManager();
}
```

## <a name="localizationmanager-usage-sample"></a>Пример использования localizationManager

Теперь в любом месте кода можно вызвать функцию getDisplayName диспетчера локализации с аргументом ключа строки, определенным в файле resources.resjson, чтобы получить необходимую строку:

```typescript
let legend: string = this.localization.getDisplayName("Role_Legend");
```

Для языкового стандарта en-US она возвращает строку "Legend", а для языкового стандарта ru-RU — строку "Обозначения".

## <a name="next-steps"></a>Дальнейшие действия

* [Узнайте, как использовать служебные программы форматирования для предоставления локализованных форматов.](utils-formatting.md)
