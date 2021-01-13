---
title: Отладка визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: В этой статье описывается отладка визуальных элементов Power BI. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: how-to
ms.date: 02/14/2020
ms.openlocfilehash: 0005fe6cfd14f0377cdd7ff648aaa3c5cc96a751
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97888381"
---
# <a name="how-to-debug-power-bi-visuals"></a>Отладка визуальных элементов Power BI

На этой странице показаны некоторые советы по отладке в процессе создания визуального элемента. Он включает в себя основные шаги и показывает различия между стандартными интерфейсными приложениями и отладкой визуального элемента Power BI.
После прочтения статьи вы сможете выполнять отладку визуальных элементов Power BI с помощью точек останова, исключений журнала и перехвата исключений в Chrome и Edge.

## <a name="using-breakpoints"></a>Использование точек останова

Так как JavaScript визуального элемента перегружается при каждом обновлении визуального элемента, при обновлении визуального элемента отладки будут потеряны любые добавленные точки останова. В качестве обходного решения используйте инструкции `debugger` в коде. Рекомендуется отключить автоматическую перезагрузку при использовании `debugger` в коде.

```typescript
public update(options: VisualUpdateOptions) {
    console.log('Visual update', options);
    debugger;
    this.target.innerHTML = `<p>Update count: <em>${(this.updateCount</em></p>`;
}
```


## <a name="showing-exceptions"></a>Отображение исключений

При работе с визуальными элементами вы заметите, что все ошибки "поглощаются" службой Power BI. Это преднамеренная функция Power BI, предотвращающая нестабильную работу всех приложений.

В качестве обходного решения добавьте код для перехвата и регистрации исключений или задайте для отладчика прерывание на перехваченных исключениях.


## <a name="log-exceptions"></a>Журнал исключений

Чтобы вести журнал исключений в визуальном элементе Power BI, добавьте следующий код в визуальный элемент, чтобы определить декоратор для ведения журнала исключений.

```typescript
export function logExceptions(): MethodDecorator {
    return function (target: Object, propertyKey: string, descriptor: TypedPropertyDescriptor<any>): TypedPropertyDescriptor<any> {
        return {
            value: function () {
                try {
                    return descriptor.value.apply(this, arguments);
                } catch (e) {
                    console.error(e);
                    throw e;
                }
            }
        }
    }
}
```
Затем этот декоратор можно использовать для любой функции, чтобы просмотреть журнал ошибок.

```typescript
@logExceptions()
public update(options: VisualUpdateOptions) {
```

## <a name="break-on-exceptions"></a>Остановка на исключениях

Браузер можно также настроить на остановку на перехваченных исключениях. Это останавливает выполнение кода везде, где происходит ошибка, и позволяет выполнять отладку отсюда.

### <a name="edge"></a>Microsoft Edge

1. Откройте средства разработчика (F12).
2. Перейдите на вкладку **Отладчик**.
3. Щелкните значок **останавливать на исключениях** (шестиугольник со значком паузы).
4. Выберите **Останавливать при любых исключениях**.

![Снимок экрана: вкладка "Отладчик" с выбранным элементом "Останавливать при любых исключениях".](media/visuals-how-to-debug/how-to-debug-edge.png)

## <a name="chrome"></a>Chrome

1. Откройте средства разработчика (F12).
2. Перейдите на вкладку **Источники**.
3. Щелкните значок **останавливать на исключениях** (шестиугольник со значком останова).
4. Установите флажок **Pause On Caught Exceptions** (Приостановить на перехваченных исключениях).

![Снимок экрана: вкладка "Источники" с выбранным элементом Pause On Caught Exceptions (Приостановить при перехваченных исключениях).](media/visuals-how-to-debug/how-to-debug-chrome.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Устранение неполадок с визуальными элементами Power BI](power-bi-custom-visuals-troubleshoot.md)
* Дополнительные сведения см. в статье [Визуальные элементы Power BI: вопросы и ответы](power-bi-custom-visuals-faq.md#organizational-power-bi-visuals)
