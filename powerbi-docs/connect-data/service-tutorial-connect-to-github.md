---
title: Руководство. Подключение к репозиторию в GitHub с помощью Power BI
description: В этом учебнике вы подключитесь к реальным данным в службе GitHub с помощью Power BI, после чего служба Power BI автоматически создаст панели мониторинга и отчеты.
author: maggiesMSFT
ms.reviewer: SarinaJoan
ms.service: powerbi
ms.subservice: powerbi-service
ms.custom: connect-to-services
ms.topic: tutorial
ms.date: 10/30/2020
ms.author: maggies
LocalizationGroup: Connect to services
ms.openlocfilehash: 805b7805d932468e973805d9496a5b25d4391fdd
ms.sourcegitcommit: 8861dac6724202a5b3be456a6aff8f3584e0cccf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2020
ms.locfileid: "93132627"
---
# <a name="tutorial-connect-to-a-github-repo-with-power-bi"></a>Руководство. Подключение к репозиторию в GitHub с помощью Power BI
В этом руководстве вы подключаетесь к реальным данным — общедоступному репозиторию содержимого Power BI (также известному как *репозиторий* ) в службе GitHub. Power BI автоматически создает панель мониторинга и отчет с данными. Вы увидите ответы на такие вопросы, как: Сколько людей участвует в создании общедоступного репозитория Power BI? кто вносит наибольший вклад; в какой день недели содержимое добавляется наиболее активно; И другие вопросы. 

Вы также можете подключиться к собственному частному или общедоступному репозиторию GitHub. Статья [Подключение к GitHub с помощью Power BI](service-connect-to-github.md) объясняет, как использовать *приложение-шаблон* Power BI для подключения к репозиториям.

![Отчет GitHub в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-punch-card.png)

В этом руководстве выполняются следующие шаги:

> [!div class="checklist"]
> * зарегистрируете учетную запись GitHub, если у вас ее еще нет; 
> * войдете в учетную запись Power BI или зарегистрируете ее, если у вас ее еще нет;
> * откроете службу Power BI;
> * найдете приложение GitHub;
> * введете сведения для общедоступного репозитория Power BI в GitHub;
> * просмотрите панель мониторинга и отчет с данными GitHub;
> * очистите ресурсы, удалив приложение.

Если вы не зарегистрированы в Power BI, перед началом работы [пройдите бесплатную регистрацию](https://app.powerbi.com/signupredirect?pbi_source=web).

## <a name="prerequisites"></a>Предварительные требования

Для прохождения этого учебника требуется учетная запись GitHub. 

- [Зарегистрируйте учетную запись GitHub](/contribute/get-started-setup-github).


## <a name="how-to-connect"></a>Способы подключения
1. Войдите в службу Power BI (`https://app.powerbi.com`). 
2. В области навигации выберите **Приложения** , а затем — **Получить приложения**.
   
   ![Кнопка "Получить приложения" в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial.png) 

3. Выберите **Приложения** , в поле поиска введите **GitHub** и нажмите кнопку **Получить**.
   
   ![Кнопка "Получить" в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-app-source.png) 

4. В окне **Установить это приложение Power BI?** выберите **Установить**.
5. В окне **Новое приложение готово** выберите **Перейти к приложению**.
6. На экране **Начало работы с новым приложением** выберите **Подключиться**.

    ![Начало работы с новым приложением](media/service-tutorial-connect-to-github/power-bi-new-app-connect-get-started.png)

7. Введите имя и владельца репозитория. URL-адрес этого репозитория — https://github.com/MicrosoftDocs/powerbi-docs, поэтому в поле **Владелец репозитория** укажите **MicrosoftDocs** , а в поле **Репозиторий**  — **powerbi-docs**. 
   
    ![Имя репозитория Power BI в GitHub](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-connect.png)

5. Введите созданные учетные данные GitHub. Power BI может пропустить этот шаг, если вы уже вошли в GitHub в браузере. 

6. В качестве метода **проверки подлинности** оставьте для **oAuth2**\> **Войти**.

7. Следуйте инструкциям по проверке подлинности GitHub на экране. Предоставьте Power BI разрешение на доступ к данным GitHub.
   
   Теперь Power BI может подключаться к данным в GitHub.  Данные обновляются раз в день.

8. После импорта данных в Power BI отображается содержимое новой рабочей области GitHub. 
9. Нажмите на стрелку рядом с именем рабочей области в области навигации. Отображается рабочая область, содержащая панель мониторинга и отчет. 

    ![Приложение в области навигации](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-left-nav-expanded.png)

10. Щелкните **Дополнительные параметры** (...) рядом с именем панели мониторинга > **Переименовать**  > введите **Панель мониторинга GitHub**.
 
    ![Плитка GitHub в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-left-nav.png) 

8. Щелкните глобальный значок навигации, чтобы свернуть область навигации и освободить место на экране.

    ![Значок глобальной навигации](media/service-tutorial-connect-to-github/power-bi-global-navigation-icon.png)

10. Выберите вашу панель мониторинга GitHub.
    
    Панель мониторинга GitHub содержит динамические данные, поэтому в вашем случае значения могут быть другими.

    ![Панель мониторинга GitHub в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-new-dashboard.png)

    

## <a name="ask-a-question"></a>Задать вопрос

1. Установите курсор в поле **Задать вопрос о своих данных**. Power BI предлагает **Вопросы для начала работы**. 

1. Выберите **Количество пользователей**.
 
    ![Количество пользователей](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-qna-how-many-users.png)

13. Между **количество** и **пользователей** введите **запросов на вытягивание на**. 

     Power BI создаст линейчатую диаграмму с числом запросов на вытягивание по пользователям.

    ![Количество запросов на вытягивание на пользователя](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-qna-how-many-prs.png)


13. Нажмите на булавку, чтоб закрепить на панели мониторинга и выберите **Выход из вопросов и ответов**.

## <a name="view-the-github-report"></a>Просмотр отчета GitHub 

1. На панели мониторинга GitHub выберите гистограмму **Запросы на вытягивание по месяцам** , чтобы открыть связанный отчет.

    ![Гистограмма "Запросы на вытягивание по месяцам"](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-column-chart.png)

2. Выберите имя пользователя в диаграмме **Общее число запросов на вытягивание на пользователя**. В этом примере мы видим, что большая часть часов пришлась на февраль.

    ![Отчет GitHub в Power BI с выделенными данными по пользователю](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-cross-filter-total-prs.png)

3. Выберите вкладку **Перфокарта** , чтобы перейти к следующей странице отчета. 
 
    ![Страница "Перфокарта" отчета GitHub в Power BI](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-tues-3pm.png)

    Очевидно, что больше всего *фиксаций* приходится на 15:00 во вторник.

## <a name="clean-up-resources"></a>Очистка ресурсов

Завершив работу с учебником, вы можете удалить приложение GitHub. 

1. В области навигации выберите **Приложения**.
2. Наведите указатель на плитку GitHub и щелкните значок **Удалить** в виде корзины.

    ![Удаление приложения GitHub](media/service-tutorial-connect-to-github/power-bi-github-app-tutorial-delete.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы подключились к общедоступному репозиторию GitHub и получили данные, которые служба Power BI отформатировала в панели мониторинга и отчете. Вы получили ответы на некоторые вопросы, изучив панель мониторинга и отчет. Теперь вы можете узнать, как подключаться к другим службами, таким как Salesforce, Microsoft Dynamics и Google Analytics. 
 
> [!div class="nextstepaction"]
> [Подключение к GitHub с помощью приложения-шаблона Power BI](service-connect-to-github.md)
