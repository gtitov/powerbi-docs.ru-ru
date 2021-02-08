---
title: Внедрение содержимого в приложение встроенной аналитики Power BI для более эффективной бизнес-аналитики для вашей организации
description: Узнайте, как выполнять интеграцию Power BI в приложение с помощью программного обеспечения и средств встроенной аналитики, а также средств встроенной бизнес-аналитики. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: tutorial
ms.custom: seodec18
ms.date: 12/17/2020
ms.openlocfilehash: fbae63597ecf4ff36783ad83785f87c242359f90
ms.sourcegitcommit: 2e81649476d5cb97701f779267be59e393460097
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "99494995"
---
# <a name="tutorial-embed-power-bi-content-using-a-sample-embed-for-your-organization-application"></a>Руководство. Внедрение содержимого Power BI с помощью примера *внедрения для организации*

Встроенная аналитика Power BI позволяет внедрять в приложение содержимое Power BI, такое как отчеты, панели мониторинга и плитки.

Из этого руководства вы узнаете, как выполнять следующие задачи:

>[!div class="checklist"]
>* Настройте внедренную среду.
>* Настройте пример приложения *внедрения для организации* (также известный как *User Owns Data*).

Для работы с приложением пользователям потребуется входить в Power BI.

Решение "Внедрение для организации" обычно используется предприятиями и крупными организациями и предназначено для внутренних пользователей.

## <a name="code-sample-specifications"></a>Спецификации примера кода

В этом руководстве содержатся инструкции по настройке примера приложения *внедрения для организации* на одной из следующих платформ.

* .NET Framework
* .NET Core
* React TypeScript

>[!NOTE]
>Примеры для *.NET Core* и *.NET Framework* позволяют конечному пользователю просматривать любую панель мониторинга, отчет или плитку Power BI , к которым у него есть доступ в службе Power BI. Пример для *React TypeScript* позволяет внедрить только один отчет, к которому у пользователя уже есть доступ в службе Power BI.

Примеры кода поддерживают следующие браузеры:

* Microsoft Edge
* Google Chrome
* Mozilla Firefox;

## <a name="prerequisites"></a>Предварительные условия

Прежде чем приступить к работе с этим руководством, убедитесь, что у вас есть как Power BI, так и указанные ниже зависимости кода.

* **Зависимости Power BI**

    * Собственный [клиент Azure Active Directory](create-an-azure-active-directory-tenant.md).

    * Одна из следующих лицензий:

        * [Power BI Pro](../../admin/service-admin-purchasing-power-bi-pro.md)

        * [Premium на пользователя (PPU)](../../admin/service-premium-per-user-faq.md)

    >[!NOTE]
    >Для [переноса в рабочую среду](move-to-production.md) потребуется одна из следующих конфигураций:
    >* все пользователи с лицензией Pro;
    >* все пользователи с лицензией PPU;
    >* [емкость](embedded-capacity.md). Эта конфигурация позволяет всем пользователям иметь бесплатные лицензии.

* **Зависимости кода**

    # <a name="net-core"></a>[.NET Core](#tab/net-core)

    * [Пакет SDK для .NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core) (или более поздней версии)
    
    * Интегрированная среда разработки (IDE) Мы рекомендуем использовать одну из следующих:

        * [Visual Studio](https://visualstudio.microsoft.com/)

        * [Visual Studio Code](https://code.visualstudio.com/)

    # <a name="net-framework"></a>[.NET Framework](#tab/net-framework)

    * [.NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/)
    
    * [Visual Studio](https://visualstudio.microsoft.com/)

    # <a name="react-typescript"></a>[React TypeScript](#tab/react)

    * Текстовый редактор

    * Терминал командной строки (или PowerShell)

---

## <a name="method"></a>Метод

Чтобы создать пример приложения *внедрения для организации*, выполните указанные ниже действия.

1. [Зарегистрируйте приложение Azure AD](#step-1---register-an-azure-ad-application).

2. [Создайте рабочую область Power BI](#step-2---create-a-power-bi-workspace).

3. [Создание отчет Power BI и опубликуйте его](#step-3---create-and-publish-a-power-bi-report).

4. [Получите значения параметров внедрения](#step-4---get-the-embedding-parameter-values).

5. [Внедрите свое содержимое](#step-5---embed-your-content).

## <a name="step-1---register-an-azure-ad-application"></a>Шаг 1. Регистрация приложения в Azure AD

Регистрация приложения в Azure AD позволяет создать для него удостоверение.

[!INCLUDE[Register Azure AD app](../../includes/embed-tutorial-register-app.md)]

## <a name="step-2---create-a-power-bi-workspace"></a>Шаг 2. Создание рабочей области Power BI

[!INCLUDE[Create a Power BI workspace](../../includes/embed-tutorial-create-workspace.md)]

## <a name="step-3---create-and-publish-a-power-bi-report"></a>Шаг 3. Создание и публикация отчета Power BI

[!INCLUDE[Create a Power BI report](../../includes/embed-tutorial-create-report.md)]

## <a name="step-4---get-the-embedding-parameter-values"></a>Шаг 4. Получение значений параметров внедрения

Чтобы внедрить содержимое, необходимо получить значения для ряда параметров. Необходимые значения зависят от языка примера приложения, который вы хотите использовать. В таблице ниже перечислены значения параметров, необходимые для каждого примера.

|Параметр  |.NET Core  |.NET Framework  |React TypeScript |
|---------|---------|---------|---------|
|[Идентификатор клиента](#client-id) |![Область применения](../../media/yes.png) |![Область применения](../../media/yes.png)         |![Область применения](../../media/yes.png) |
|[Секрет клиента](#workspace-id) |![Область применения](../../media/yes.png) |![Область применения](../../media/yes.png) |![Неприменимо.](../../media/no.png) |
|[Идентификатор рабочей области]() |![Неприменимо.](../../media/no.png) |![Неприменимо.](../../media/no.png) |![Область применения](../../media/yes.png) |
|[Идентификатор отчета]() |![Неприменимо.](../../media/no.png) |![Неприменимо.](../../media/no.png) |![Область применения](../../media/yes.png) |

### <a name="client-id"></a>Идентификатор клиента

>[!TIP]
>**Область применения:** ![Применяется к:](../../media/yes.png).NET Core ![Применяется к:](../../media/yes.png).NET Framework ![Применяется к:](../../media/yes.png)React TypeScript

[!INCLUDE[Get the client ID](../../includes/embed-tutorial-client-id.md)]

### <a name="client-secret"></a>Секрет клиента

>[!TIP]
>**Область применения:** ![Применяется к:](../../media/yes.png).NET Core ![Применяется к:](../../media/yes.png).NET Framework ![Не применяется к:](../../media/no.png)React TypeScript

[!INCLUDE[Get the client secret](../../includes/embed-tutorial-client-secret.md)]

### <a name="workspace-id"></a>Идентификатор рабочей области

>[!TIP]
>**Область применения:** ![Не применяется к:](../../media/no.png).NET Core ![Не применяется к:](../../media/no.png).NET Framework ![Применяется к:](../../media/yes.png)React TypeScript

[!INCLUDE[Get the workspace ID](../../includes/embed-tutorial-workspace-id.md)]

### <a name="report-id"></a>Идентификатор отчета

>[!TIP]
>**Область применения:** ![Не применяется к:](../../media/no.png).NET Core ![Не применяется к:](../../media/no.png).NET Framework ![Применяется к:](../../media/yes.png)ReactTypeScript

[!INCLUDE[Get the report ID](../../includes/embed-tutorial-report-id.md)]

## <a name="step-5---embed-your-content"></a>Шаг 5. Внедрение содержимого

Пример приложения внедрения Power BI позволяет создать приложение Power BI *внедрения для организации*.

Выполните указанные ниже действия, чтобы изменить пример приложения *внедрения для организации*, внедрив отчет Power BI.

[!INCLUDE[Embedding steps](../../includes/embed-tutorial-embedding-steps.md)]

4. В зависимости от языка, который должен использоваться приложением, откройте одну из следующих папок:

    * .NET Core
    * .NET Framework
    * React-TS

    >[!NOTE]
    >Примеры приложений *внедрения для организации* поддерживают только перечисленные выше платформы. Примеры приложений на *Java*, *Node JS* и *Python* поддерживают только решение *[внедрения для клиентов](embed-sample-for-customers.md)* .

# <a name="net-core"></a>[.NET Core](#tab/net-core)

### <a name="configure-your-azure-ad-app"></a>Настройка приложения Azure AD

[!INCLUDE[Configure the Azure AD authentication options](../../includes/embed-tutorial-org-azure-ad-app.md)]

5. В разделе *Конфигурации платформы* откройте платформу *Веб* и в разделе **URI перенаправления** добавьте `https://localhost:5000/signin-oidc`.

    > [!NOTE]
    >Если у вас нет платформы **Веб**, выберите **Добавить платформу** и в окне *Настройка платформ* выберите **Веб**.

6. Сохраните изменения.

:::image type="content" source="media/embed-sample-for-your-organization/azure-ad-net-configurations.png" alt-text="Снимок экрана: конфигурации проверки подлинности для приложения Azure AD с кодом URI веб-перенаправления для примера приложения .NET Core.":::

### <a name="configure-the-sample-embedding-app"></a>Настройка примера приложения для внедрения

1. Откройте папку **Внедрение для организации**.

2. Откройте *пример приложения внедрения для организации* одним из приведенных ниже методов.

    * Если вы используете [Visual Studio](https://visualstudio.microsoft.com/), откройте файл **UserOwnsData.sln**.

    * Если вы используете [Visual Studio Code](https://code.visualstudio.com/), откройте папку **UserOwnsData**.

3. Откройте файл **appsettings.json** и введите следующие значения параметров:

    * `ClientId` — используйте [идентификатор клиента](#client-id);

    * `ClientSecret` — используйте [секрет клиента](#client-secret).

### <a name="run-the-sample-app"></a>Запуск примера приложения

1. Запустите проект, выбрав соответствующий параметр:

    * Если вы используете **Visual Studio**, выберите **IIS Express** (воспроизвести).

    * Если вы используете **Visual Studio Code**, выберите **Выполнить > Начать отладку**.

[!INCLUDE[The embedded application sample app interface](../../includes/embed-tutorial-org-sample-app.md)]

# <a name="net-framework"></a>[.NET Framework](#tab/net-framework)

### <a name="configure-your-azure-ad-app"></a>Настройка приложения Azure AD

[!INCLUDE[Configure the Azure AD authentication options](../../includes/embed-tutorial-org-azure-ad-app.md)]

5. В разделе *Конфигурации платформы* настройте указанные ниже параметры.

    1. Для платформы *Веб* в разделе **URI перенаправления** добавьте `https://localhost:44300/`.

        > [!NOTE]
        >Если у вас нет платформы **Веб**, выберите **Добавить платформу** и в окне *Настройка платформ* выберите **Веб**.
    
    2. В разделе *Неявное предоставление разрешения и гибридные потоки* включите параметр **Токен идентификатора**.
    
6. Сохраните изменения.

:::image type="content" source="media/embed-sample-for-your-organization/azure-ad-framework-configurations.png" alt-text="Снимок экрана: конфигурации проверки подлинности для приложения Azure AD с кодом URI веб-перенаправления и выбранным маркером доступа для примера приложения .NET Framework.":::

### <a name="configure-the-sample-embedding-app"></a>Настройка примера приложения для внедрения

1. Откройте папку **Внедрение для организации**.

2. В [Visual Studio](https://visualstudio.microsoft.com/) откройте файл **UserOwnsData.sln**.

3. Откройте файл **Web.config** и введите следующие значения параметров:

    * `clientId` — используйте [идентификатор клиента](#client-id);

    * `clientSecret` — используйте [секрет клиента](#client-secret).

### <a name="run-the-sample-app"></a>Запуск примера приложения

1. Запустите проект, выбрав **IIS Express** (воспроизвести).

[!INCLUDE[The embedded application sample app interface](../../includes/embed-tutorial-org-sample-app.md)]

# <a name="react-typescript"></a>[React TypeScript](#tab/react)

### <a name="configure-your-azure-ad-app"></a>Настройка приложения Azure AD

[!INCLUDE[Configure the Azure AD authentication options](../../includes/embed-tutorial-org-azure-ad-app.md)]

5. В разделе *Конфигурации платформы* настройте платформу **Веб** указанным ниже образом.

    1. В разделе **URI перенаправления** добавьте `https://localhost:3000` и нажмите **Настроить**.

        > [!NOTE]
        >Если у вас нет платформы **Веб**, выберите **Добавить платформу** и в окне *Настройка платформ* выберите **Веб**.

    2. В разделе *Неявное предоставление разрешения и гибридные потоки* включите оба параметра:
        * **Маркеры доступа в Azure Active Directory**
        * **Маркеры идентификации**
    
6. Сохраните изменения.

:::image type="content" source="media/embed-sample-for-your-organization/azure-ad-react-configurations.png" alt-text="Снимок экрана: конфигурации проверки подлинности для приложения Azure AD с кодом URI веб-перенаправления, установленным в значение localhost 3000.":::

### <a name="configure-the-sample-embedding-app"></a>Настройка примера приложения для внедрения

1. Откройте папку **Внедрение для организации** > **UserOwnsData** > **src**.

2. В текстовом редакторе откройте файл **Config.ts** и введите следующие значения параметров:

    * `clientId` — используйте [идентификатор клиента](#client-id);

    * `workspaceId` — используйте [идентификатор рабочей области](#client-secret);

    * `reportId` — используйте [идентификатор отчета](#report-id).

3. Сохраните файл.

### <a name="run-the-sample-app"></a>Запуск примера приложения

1. Откройте терминал и перейдите к папке **Внедрение для организации** > **UserOwnsData**.

2. Выполните следующую команду, чтобы установить необходимые зависимости:

   `npm install`

3. Запустите приложение с помощью следующей команды:

   `npm run start`

    >[!NOTE]
    >При первом входе вам будет предложено предоставить приложению разрешения Azure AD.

---

## <a name="developing-your-application"></a>Разработка приложения

После настройки и запуска примера приложения *внедрения для клиентов* можно приступить к разработке собственного приложения.

[!INCLUDE[Move to production](../../includes/embed-tutorial-production.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
>[Перенос в рабочую среду](move-to-production.md)

>[!div class="nextstepaction"]
>[Внедрение для клиентов](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Внедрение отчетов с разбивкой на страницы для клиентов](embed-paginated-reports-customers.md)

> [!div class="nextstepaction"]
>[Внедрение отчетов с разбивкой на страницы для организации](embed-paginated-reports-organization.md)

>[!div class="nextstepaction"]
>[Спросить в сообществе Power BI](https://community.powerbi.com/)