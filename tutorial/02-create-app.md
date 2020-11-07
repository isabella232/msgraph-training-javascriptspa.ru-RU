---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822941"
---
<!-- markdownlint-disable MD002 MD041 -->

Начните с создания пустого каталога для проекта. Это может быть HTTP-сервер или каталог на компьютере разработчика. Если он находится на вашем компьютере для разработки, необходимо скопировать его на сервер для тестирования или запустить HTTP-сервер на компьютере для разработки. Если у вас нет ни одного из этих элементов, в следующем разделе представлены инструкции.

## <a name="start-a-local-web-server-optional"></a>Запуск локального веб-сервера (необязательно)

> [!NOTE]
> Действия, описанные в этом разделе, требуют [Node.js](https://nodejs.org).

В этом разделе показано, как использовать [HTTP-Server](https://www.npmjs.com/package/http-server) для запуска простого сервера HTTP из командной строки.

1. Откройте интерфейс командной строки (CLI) в каталоге, созданном для проекта.
1. Выполните следующую команду, чтобы запустить веб-сервер в этом каталоге.

    ```Shell
    npx http-server -c-1
    ```

1. Откройте браузер и перейдите по адресу `http://localhost:8080` .

Вы должны увидеть **индекс/** страницу. Это подтверждает, что HTTP-сервер запущен.

![Снимок экрана со страницей индекса, обслуживаемой HTTP-Server.](images/run-web-server.png)

## <a name="design-the-app"></a>Проектирование приложения

В этом разделе показано, как создать базовую схему пользовательского интерфейса для приложения.

1. Создайте в корневом каталоге проекта новый файл с именем **index.html** и добавьте следующий код.

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    Этот параметр определяет базовую структуру приложения, в том числе панель навигации. Кроме того, добавляются следующие компоненты:

    - [Начальная](https://getbootstrap.com/) Загрузка и поддерживающая JavaScript
    - [фонтавесоме](https://fontawesome.com/)
    - [Moment.js](https://momentjs.com/)
    - [Библиотека проверки подлинности (Майкрософт) для JavaScript (MSAL.js) 2,0](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [Клиентская библиотека JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > Страница содержит фавикон ( `<link rel="shortcut icon" href="g-raph.png">` ). Вы можете удалить эту строку или скачать файл **g-raph.png** из [GitHub](https://github.com/microsoftgraph/g-raph).

1. Создайте новый файл с именем **Style. CSS** и добавьте приведенный ниже код.

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. Создайте новый файл с именем **auth.js** и добавьте следующий код.

    ```javascript
    function signIn() {
      // TEMPORARY
      updatePage({name: 'Megan Bowen', userName: 'meganb@contoso.com'});
    }

    function signOut() {
      // TEMPORARY
      updatePage();
    }
    ```

1. Создайте новый файл с именем **ui.js** и добавьте следующий код.

    ```javascript
    // Select DOM elements to work with
    const authenticatedNav = document.getElementById('authenticated-nav');
    const accountNav = document.getElementById('account-nav');
    const mainContainer = document.getElementById('main-container');

    const Views = { error: 1, home: 2, calendar: 3 };

    function createElement(type, className, text) {
      var element = document.createElement(type);
      element.className = className;

      if (text) {
        var textNode = document.createTextNode(text);
        element.appendChild(textNode);
      }

      return element;
    }

    function showAuthenticatedNav(user, view) {
      authenticatedNav.innerHTML = '';

      if (user) {
        // Add Calendar link
        var calendarNav = createElement('li', 'nav-item');

        var calendarLink = createElement('button',
          `btn btn-link nav-link${view === Views.calendar ? ' active' : '' }`,
          'Calendar');
        calendarLink.setAttribute('onclick', 'getEvents();');
        calendarNav.appendChild(calendarLink);

        authenticatedNav.appendChild(calendarNav);
      }
    }

    function showAccountNav(user) {
      accountNav.innerHTML = '';

      if (user) {
        // Show the "signed-in" nav
        accountNav.className = 'nav-item dropdown';

        var dropdown = createElement('a', 'nav-link dropdown-toggle');
        dropdown.setAttribute('data-toggle', 'dropdown');
        dropdown.setAttribute('role', 'button');
        accountNav.appendChild(dropdown);

        var userIcon = createElement('i',
          'far fa-user-circle fa-lg rounded-circle align-self-center');
        userIcon.style.width = '32px';
        dropdown.appendChild(userIcon);

        var menu = createElement('div', 'dropdown-menu dropdown-menu-right');
        dropdown.appendChild(menu);

        var userName = createElement('h5', 'dropdown-item-text mb-0', user.displayName);
        menu.appendChild(userName);

        var userEmail = createElement('p', 'dropdown-item-text text-muted mb-0', user.mail || user.userPrincipalName);
        menu.appendChild(userEmail);

        var divider = createElement('div', 'dropdown-divider');
        menu.appendChild(divider);

        var signOutButton = createElement('button', 'dropdown-item', 'Sign out');
        signOutButton.setAttribute('onclick', 'signOut();');
        menu.appendChild(signOutButton);
      } else {
        // Show a "sign in" button
        accountNav.className = 'nav-item';

        var signInButton = createElement('button', 'btn btn-link nav-link', 'Sign in');
        signInButton.setAttribute('onclick', 'signIn();');
        accountNav.appendChild(signInButton);
      }
    }

    function showWelcomeMessage(user) {
      // Create jumbotron
      var jumbotron = createElement('div', 'jumbotron');

      var heading = createElement('h1', null, 'JavaScript SPA Graph Tutorial');
      jumbotron.appendChild(heading);

      var lead = createElement('p', 'lead',
        'This sample app shows how to use the Microsoft Graph API to access' +
        ' a user\'s data from JavaScript.');
      jumbotron.appendChild(lead);

      if (user) {
        // Welcome the user by name
        var welcomeMessage = createElement('h4', null, `Welcome ${user.displayName}!`);
        jumbotron.appendChild(welcomeMessage);

        var callToAction = createElement('p', null,
          'Use the navigation bar at the top of the page to get started.');
        jumbotron.appendChild(callToAction);
      } else {
        // Show a sign in button in the jumbotron
        var signInButton = createElement('button', 'btn btn-primary btn-large',
          'Click here to sign in');
        signInButton.setAttribute('onclick', 'signIn();')
        jumbotron.appendChild(signInButton);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(jumbotron);
    }

    function showError(error) {
      var alert = createElement('div', 'alert alert-danger');

      var message = createElement('p', 'mb-3', error.message);
      alert.appendChild(message);

      if (error.debug)
      {
        var pre = createElement('pre', 'alert-pre border bg-light p-2');
        alert.appendChild(pre);

        var code = createElement('code', 'text-break text-wrap',
          JSON.stringify(error.debug, null, 2));
        pre.appendChild(code);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }

    function updatePage(view, data) {
      if (!view) {
        view = Views.home;
      }

      const user = JSON.parse(sessionStorage.getItem('graphUser'));

      showAccountNav(user);
      showAuthenticatedNav(user, view);

      switch (view) {
        case Views.error:
          showError(data);
          break;
        case Views.home:
          showWelcomeMessage(user);
          break;
        case Views.calendar:
          break;
      }
    }

    updatePage(Views.home);
    ```

1. Сохраните все изменения и обновите страницу. Теперь приложение должно выглядеть по-другому.

    ![Снимок экрана с переработанной домашней страницей](images/app-layout.png)
