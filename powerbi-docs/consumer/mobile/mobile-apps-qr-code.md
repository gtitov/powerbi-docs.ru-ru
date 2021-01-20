---
title: Сканирование QR-кода Power BI на мобильном устройстве
description: QR-коды в Power BI могут связывать любой физический предмет с соответствующей информацией BI в мобильном приложении для устройств iPhone и Android.
author: paulinbar
ms.author: painbar
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-mobile
ms.topic: how-to
ms.date: 12/02/2019
ms.openlocfilehash: 96859efbaf86c8c6e9abf459500c38d49ee4f112
ms.sourcegitcommit: 1cad78595cca1175b82c04458803764ac36e5e37
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2021
ms.locfileid: "98565503"
---
# <a name="scan-a-power-bi-qr-code-from-your-mobile-device"></a>Сканирование QR-кода Power BI на мобильном устройстве
Применяется к:

| ![iPhone](./media/mobile-apps-qr-code/ios-logo-40-px.png) | ![iPad](./media/mobile-apps-qr-code/ios-logo-40-px.png) | ![Телефон Android](././media/mobile-apps-qr-code/android-logo-40-px.png) | ![Планшет Android](././media/mobile-apps-qr-code/android-logo-40-px.png) |
|:--- |:--- |:--- |:--- |
|iPhone |iPad |Телефоны под управлением Android |Планшеты Android |

QR-коды в Power BI могут связывать любой предмет реального времени с соответствующей информацией BI &#151; навигация или поиск не требуются.

Допустим, коллега [создал QR-код в службе Power BI](../../create-reports/service-create-qr-code-for-tile.md) для отчета или плитки на панели мониторинга, предоставил вам доступ к панели или отчету и поместил QR-код в ключевое расположение — например в электронную почту или определенную папку. 

Вы можете отсканировать QR-код для мгновенного доступа к соответствующей плитке или отчету прямо на телефоне с помощью сканера в приложении Power BI либо другого аналогичного сканера, установленного на вашем устройстве. 

Если ваши коллеги не предоставили вам доступ к отчету или панели мониторинга, запросить доступ можно непосредственно из мобильного приложения. 

> [!NOTE]
> Кроме того, можно [сосканировать QR-код отчета с помощью приложения Power BI для смешанной реальности](./mobile-hololens2-app.md#open-reports-with-qr-codes).

## <a name="scan-a-power-bi-qr-code-on-your-iphone-with-the-power-bi-scanner"></a>Сканирование QR-кода Power BI на устройстве iPhone с помощью сканера Power BI

1. На панели навигации вверху выберите **Дополнительные параметры** (...), а затем — пункт **Сканер**.

    ![Снимок экрана: элемент "Дополнительные параметры" в области навигации с выбором сканера](media/mobile-apps-qr-code/power-bi-scanner.png)

2. Если камера не включена, разрешите приложению Power BI ее использовать. Это нужно сделать один раз. 
 
3. Наведите сканер на QR-код Power BI. 
   
    ![Снимок экрана: выпуск новостей со сканером, направленным на QR-код Power BI](media/mobile-apps-qr-code/power-bi-align-qr-code.png)
4. Плитка или отчет появится на фоне в режиме дополненной реальности.
   
    ![Снимок экрана: отчета, отображаемый при наведении на выпуск новостей](media/mobile-apps-qr-code/power-bi-ios-qr-ar-scanner.png)

5. Коснитесь отчета или плитки, чтобы открыть их в режиме фокусировки, или вернитесь к сканеру.

### <a name="scan-a-qr-code-from-an-external-scanner-on-your-iphone"></a>Сканирование QR-кода с помощью внешнего сканера, установленного на устройстве iPhone
1. Откройте сканер на телефоне и наведите его на соответствующий QR-код Power BI, чтобы получить доступ к плитке или отчету. 
2. Если на вашем iPhone не установлено приложение Power BI, откроется [каталог Apple App Store, откуда вы сможете его скачать](https://go.microsoft.com/fwlink/?LinkId=522062).

## <a name="scan-a-power-bi-qr-code-on-your-android-device-with-the-power-bi-scanner"></a>Сканирование QR-кода Power BI на устройстве Android с помощью сканера Power BI

1. На панели навигации вверху выберите **Дополнительные параметры** (...), а затем — пункт **Сканер**.

    ![Снимок экрана: элемент "Дополнительные параметры" в области навигации с выбором сканера](media/mobile-apps-qr-code/power-bi-scanner.png)

2. Если камера не включена, разрешите приложению Power BI ее использовать. Это нужно сделать один раз. 

3. Наведите сканер на QR-код Power BI. 
   
    ![Снимок экрана: сканер, направленный на QR-код Power BI](media/mobile-apps-qr-code/pbi_iph_qrscan.png)
4. Плитка или отчет откроется в Power BI автоматически.
   
    ![Снимок экрана: отчет "Число возможностей" с гистограммой по месяцам и этапам продаж](media/mobile-apps-qr-code/power-bi-android-tile.png)

### <a name="scan-a-qr-code-from-an-external-scanner-on-your-android-device"></a>Сканирование QR-кода внешним сканером, установленным на устройстве Android
1. Откройте сканер на устройстве Android и наведите сканер на соответствующий QR-код Power BI, чтобы получить доступ к плитке или отчету. 
2. Если у вас не установлено приложение Power BI, откроется [каталог Google Play, где его можно будет скачать](https://go.microsoft.com/fwlink/?LinkID=544867). 

## <a name="next-steps"></a>Дальнейшие действия
* [Подключение к данным Power BI из реального мира](mobile-apps-data-in-real-world-context.md) с помощью мобильных приложений
* [Создание QR-кода для плитки в службе Power BI](../../create-reports/service-create-qr-code-for-tile.md)
* [Создание QR-кода для отчета в Power BI](../../create-reports/service-create-qr-code-for-report.md)
* Кроме того, можно [сосканировать QR-код с помощью приложения Power BI для смешанной реальности](./mobile-hololens2-app.md).
* У вас появились вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
