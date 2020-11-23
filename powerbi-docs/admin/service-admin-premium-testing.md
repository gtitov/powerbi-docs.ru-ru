---
title: Покупка Power BI Premium для тестирования
description: Узнайте, как приобрести Power BI Premium для тестирования и других целей
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-premium
ms.topic: how-to
ms.date: 11/11/2020
LocalizationGroup: Premium
ms.openlocfilehash: 28845a958edb516d6ecdaa3fedbaad62be723865
ms.sourcegitcommit: cc20b476a45bccb870c9de1d0b384e2c39e25d24
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "94520114"
---
# <a name="purchase-power-bi-premium-for-testing"></a>Покупка Power BI Premium для тестирования

В этой статье описывается, как приобрести номера SKU Power BI Premium A для сценариев тестирования и в тех случаях, когда отсутствуют разрешения, необходимые для приобретения номеров SKU P (роль глобального администратора Microsoft 365 или роль администратора выставления счетов). Для номеров SKU A не требуется фиксация обязательств по времени, а счета выставляются на почасовой основе. Номера SKU A можно приобрести на [портале Azure](https://portal.azure.com).

Дополнительные сведения о Power BI Premium см. в статье [Что такое Power BI Premium?](service-premium-what-is.md). Актуальные цены и сведения о планировании см. на [странице цен на Power BI](https://powerbi.microsoft.com/pricing/) и воспользуйтесь [калькулятором Power BI Premium](https://powerbi.microsoft.com/calculator/). Авторам содержимого по-прежнему требуется [лицензия Power BI Pro](service-admin-purchasing-power-bi-pro.md), даже если в организации используется Power BI Premium. Для организации необходимо приобрести по меньшей мере одну лицензию Power BI Pro. При использовании номеров SKU A _всем пользователям_, которые потребляют содержимое, также требуются лицензии Pro.

> [!NOTE]
> Если срок действия подписки Premium истекает, у вас есть 30 дней полного доступа к емкости. После этого ваше содержимое будет размещено в общей емкости. В общей емкости не поддерживаются модели, размер которых превышает 1 ГБ.

## <a name="purchase-a-skus-for-testing-and-other-scenarios"></a>Приобретение номеров SKU A для тестирования и других сценариев

Номера SKU A доступны в службе Power BI Embedded Azure. Номера SKU A можно использовать в следующих целях:

- Разрешить внедрение Power BI в сторонние приложения. Дополнительные сведения см. в разделе [Power BI Embedded](../developer/embedded/azure-pbie-what-is-power-bi-embedded.md).

- Тестировать функциональные возможности версии Premium перед приобретением номера SKU P.

- Создавать среды для разработки и тестирования параллельно с рабочей средой, в которой используются номера SKU P.

- Приобрести Power BI Premium даже в том случае, если вам не назначена роль глобального администратора Microsoft 365 или администратора выставления счетов.

> [!NOTE]
> Если вы приобрели номер SKU A4 или более высокий, вам будут доступны все преимущества версии Premium, за исключением неограниченного общего доступа к содержимому. При использовании номеров SKU A _всем пользователям_, которые потребляют содержимое, требуются лицензии Pro.

Чтобы приобрести номера SKU A на портале Azure, выполните следующие действия:

1. Войдите на [портал Azure](https://portal.azure.com) с использованием учетной записи, которой назначены как минимум разрешения администратора в Power BI.

1. Выполните поиск по запросу _Power BI Embedded_ и выберите эту службу в полученных результатах.

    ![Поиск на портале Azure](media/service-admin-premium-purchase/azure-portal-search.png)

1. Выберите **Создать Power BI Embedded**.

    ![Создание Power BI Embedded](media/service-admin-premium-purchase/create-power-bi-embedded.png)

1. На экране **Power BI Embedded** введите следующие сведения:

    - **Подписка**, в которой требуется создать службу Power BI Embedded.

    - **Физическое расположение**, в котором требуется создать группу ресурсов, содержащую службу. Для лучшей производительности это расположение должно находиться вблизи вашего клиента Active Directory для Power BI.

    - Существующая **группа ресурсов**, которую требуется использовать (также можно создать новую группу, как показано в примере).

    - **Администратор емкости Power BI**. Администратор емкости должен быть пользователем-членом или субъектом-службой в клиенте Azure AD.

    ![Подписка и группа ресурсов](media/service-admin-premium-purchase/subscription-resource-group.png)

1. Если вы хотите использовать все возможности Power BI Premium (за исключением неограниченного общего доступа), вам потребуется по крайней мере номер SKU A4. Выберите **Изменить размер**.

    ![Изменить размер емкости](media/service-admin-premium-purchase/change-capacity-size.png)

1. Выберите размер емкости: A4, A5 или A6, что соответствует P1, P2 и P3.

    ![Выбор емкости A3](media/service-admin-premium-purchase/select-a3-capacity.png)

1. Нажмите **Просмотр и создание**, проверьте выбранные параметры и нажмите **Создать**.

    ![Создайте ресурс](media/service-admin-premium-purchase/create-resource.png)

1. Процесс развертывания может занять несколько минут. После завершения выберите **Перейти к ресурсу**.

    ![Развертывание завершено](media/service-admin-premium-purchase/deployment-complete.png)

1. На экране управления проверьте заданные для службы параметры, в том числе настройки приостановки неиспользуемой службы.

    ![Управление емкостями](media/service-admin-premium-purchase/manage-capacity.png)

После приобретения емкости вы можете [управлять емкостями](service-admin-premium-manage.md#manage-capacity) и [назначать им рабочие области](service-admin-premium-manage.md#assign-a-workspace-to-a-capacity).

## <a name="next-steps"></a>Дальнейшие действия

[Что такое Power BI Premium?](service-premium-what-is.md)
[Как приобрести Power BI Premium](service-admin-premium-purchase.md)
[Настройка и управление емкостью в Power BI Premium](service-admin-premium-manage.md)\
[Страница цен на Power BI](https://powerbi.microsoft.com/pricing/)\
[Калькулятор Power BI Premium](https://powerbi.microsoft.com/calculator/)\
[Вопросы и ответы по Power BI Premium](service-premium-faq.md)\
[Технический документ по планированию развертывания Power BI Enterprise](https://aka.ms/pbienterprisedeploy)

Появились дополнительные вопросы? [Попробуйте задать вопрос в сообществе Power BI.](https://community.powerbi.com/)
