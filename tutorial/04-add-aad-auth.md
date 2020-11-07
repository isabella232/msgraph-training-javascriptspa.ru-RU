---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822902"
---
<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD. Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph. На этом этапе библиотека [библиотеки проверки подлинности (Майкрософт](https://github.com/AzureAD/microsoft-authentication-library-for-js) ) будет интегрирована в приложение.

1. Создайте новый файл в корневом каталоге с именем **config.js** и добавьте следующий код.

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    Замените `YOUR_APP_ID_HERE` идентификатором приложения на портале регистрации приложений.

    > [!IMPORTANT]
    > Если вы используете систему управления версиями (например, Git), то в дальнейшем будет полезно исключить файл **config.js** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.

1. Откройте **auth.js** и добавьте следующий код в начало файла.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a>Реализация входа

В этом разделе вы реализуете `signIn` функции и `signOut` функции.

1. Замените имеющуюся функцию `signIn` указанным ниже кодом.

    ```javascript
    async function signIn() {
      // Login
      try {
        // Use MSAL to login
        const authResult = await msalClient.loginPopup(msalRequest);
        console.log('id_token acquired at: ' + new Date().toString());
        // Save the account username, needed for token acquisition
        sessionStorage.setItem('msalAccount', authResult.account.username);
        // TEMPORARY
        updatePage(Views.error, {
          message: 'Login successful',
          debug: `Token: ${authResult.accessToken}`
        });
      } catch (error) {
        console.log(error);
        updatePage(Views.error, {
          message: 'Error logging in',
          debug: error
        });
      }
    }
    ```

    В этом временном коде отображается маркер доступа после успешного входа.

1. Замените имеющуюся функцию `signOut` указанным ниже кодом.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. Сохраните изменения и обновите страницу. После входа вы увидите окно с сообщением об ошибке, в котором отображается маркер доступа.

## <a name="get-the-users-profile"></a>Получение профиля пользователя

В этом разделе `signIn` функция используется для получения профиля пользователя из Microsoft Graph с помощью маркера доступа.

1. Добавьте указанную ниже функцию в **auth.js** , чтобы получить маркер доступа пользователя.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. Создайте в корневом каталоге проекта новый файл с именем **graph.js** и добавьте следующий код.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    Этот код создает поставщика авторизации, который упаковывает `getToken` метод в **auth.js** , и инициализирует клиент Graph с этим поставщиком.

1. Добавьте указанную ниже функцию в **graph.js** , чтобы получить профиль пользователя.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. Замените имеющуюся функцию `signIn` указанным ниже кодом.

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. Сохраните изменения и обновите страницу. После входа в систему необходимо вернуться на домашнюю страницу, но пользовательский интерфейс должен измениться, чтобы показать, что вы выполнили вход.

    ![Снимок экрана домашней страницы после входа](./images/user-signed-in.png)

1. Щелкните аватар пользователя в правом верхнем углу, чтобы получить доступ к ссылке **выхода** . При нажатии кнопки **выйти** сбрасывается сеанс и возвращается на домашнюю страницу.

    ![Снимок экрана с раскрывающимся меню со ссылкой "выйти"](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a>Хранение и обновление маркеров

На этом шаге приложение имеет маркер доступа, который отправляется в `Authorization` заголовке вызовов API. Это маркер, который позволяет приложению получать доступ к Microsoft Graph от имени пользователя.

Однако этот маркер кратковременно используется. Срок действия маркера истечет через час после его выдачи. В этом случае маркер обновления становится полезен. Маркер обновления позволяет приложению запросить новый маркер доступа, не требуя от пользователя повторного входа.

Так как приложение использует библиотеку MSAL, нет необходимости внедрять логику хранения или обновления маркеров. MSAL кэширует маркер в сеансе браузера. `acquireTokenSilent`Метод сначала проверяет кэшированный маркер, и если срок его действия не истек, он возвращается. Если срок действия истек, он использует кэшированный маркер обновления, чтобы получить новый. Клиентский объект Graph вызывает `getToken` метод в **auth.js** для каждого запроса, гарантируя, что у него есть обновленный маркер.
