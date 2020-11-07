---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822941"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="be6e5-101">Начните с создания пустого каталога для проекта.</span><span class="sxs-lookup"><span data-stu-id="be6e5-101">Start by creating an empty directory for the project.</span></span> <span data-ttu-id="be6e5-102">Это может быть HTTP-сервер или каталог на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="be6e5-102">This can be on an HTTP server, or a directory on your development machine.</span></span> <span data-ttu-id="be6e5-103">Если он находится на вашем компьютере для разработки, необходимо скопировать его на сервер для тестирования или запустить HTTP-сервер на компьютере для разработки.</span><span class="sxs-lookup"><span data-stu-id="be6e5-103">If it is on your development machine, you'll need to copy it to a server for testing, or run an HTTP server on your development machine.</span></span> <span data-ttu-id="be6e5-104">Если у вас нет ни одного из этих элементов, в следующем разделе представлены инструкции.</span><span class="sxs-lookup"><span data-stu-id="be6e5-104">If you don't have either of those, the next section provides instructions.</span></span>

## <a name="start-a-local-web-server-optional"></a><span data-ttu-id="be6e5-105">Запуск локального веб-сервера (необязательно)</span><span class="sxs-lookup"><span data-stu-id="be6e5-105">Start a local web server (optional)</span></span>

> [!NOTE]
> <span data-ttu-id="be6e5-106">Действия, описанные в этом разделе, требуют [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="be6e5-106">The steps in this section require [Node.js](https://nodejs.org).</span></span>

<span data-ttu-id="be6e5-107">В этом разделе показано, как использовать [HTTP-Server](https://www.npmjs.com/package/http-server) для запуска простого сервера HTTP из командной строки.</span><span class="sxs-lookup"><span data-stu-id="be6e5-107">In this section you will use [http-server](https://www.npmjs.com/package/http-server) to run a simple HTTP server from the command line.</span></span>

1. <span data-ttu-id="be6e5-108">Откройте интерфейс командной строки (CLI) в каталоге, созданном для проекта.</span><span class="sxs-lookup"><span data-stu-id="be6e5-108">Open your command-line interface (CLI) in the directory you created for the project.</span></span>
1. <span data-ttu-id="be6e5-109">Выполните следующую команду, чтобы запустить веб-сервер в этом каталоге.</span><span class="sxs-lookup"><span data-stu-id="be6e5-109">Run the following command to start a web server in that directory.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="be6e5-110">Откройте браузер и перейдите по адресу `http://localhost:8080` .</span><span class="sxs-lookup"><span data-stu-id="be6e5-110">Open your browser and browse to `http://localhost:8080`.</span></span>

<span data-ttu-id="be6e5-111">Вы должны увидеть **индекс/** страницу.</span><span class="sxs-lookup"><span data-stu-id="be6e5-111">You should see an **Index of /** page.</span></span> <span data-ttu-id="be6e5-112">Это подтверждает, что HTTP-сервер запущен.</span><span class="sxs-lookup"><span data-stu-id="be6e5-112">This confirms that the HTTP server is running.</span></span>

![Снимок экрана со страницей индекса, обслуживаемой HTTP-Server.](images/run-web-server.png)

## <a name="design-the-app"></a><span data-ttu-id="be6e5-114">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="be6e5-114">Design the app</span></span>

<span data-ttu-id="be6e5-115">В этом разделе показано, как создать базовую схему пользовательского интерфейса для приложения.</span><span class="sxs-lookup"><span data-stu-id="be6e5-115">In this section you'll create the basic UI layout for the application.</span></span>

1. <span data-ttu-id="be6e5-116">Создайте в корневом каталоге проекта новый файл с именем **index.html** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="be6e5-116">Create a new file in the root of the project named **index.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    <span data-ttu-id="be6e5-117">Этот параметр определяет базовую структуру приложения, в том числе панель навигации.</span><span class="sxs-lookup"><span data-stu-id="be6e5-117">This defines the basic layout of the app, including a navigation bar.</span></span> <span data-ttu-id="be6e5-118">Кроме того, добавляются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="be6e5-118">It also adds the following:</span></span>

    - <span data-ttu-id="be6e5-119">[Начальная](https://getbootstrap.com/) Загрузка и поддерживающая JavaScript</span><span class="sxs-lookup"><span data-stu-id="be6e5-119">[Bootstrap](https://getbootstrap.com/) and its supporting JavaScript</span></span>
    - [<span data-ttu-id="be6e5-120">фонтавесоме</span><span class="sxs-lookup"><span data-stu-id="be6e5-120">FontAwesome</span></span>](https://fontawesome.com/)
    - [<span data-ttu-id="be6e5-121">Moment.js</span><span class="sxs-lookup"><span data-stu-id="be6e5-121">Moment.js</span></span>](https://momentjs.com/)
    - [<span data-ttu-id="be6e5-122">Библиотека проверки подлинности (Майкрософт) для JavaScript (MSAL.js) 2,0</span><span class="sxs-lookup"><span data-stu-id="be6e5-122">Microsoft Authentication Library for JavaScript (MSAL.js) 2.0</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [<span data-ttu-id="be6e5-123">Клиентская библиотека JavaScript для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="be6e5-123">Microsoft Graph JavaScript Client Library</span></span>](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > <span data-ttu-id="be6e5-124">Страница содержит фавикон ( `<link rel="shortcut icon" href="g-raph.png">` ).</span><span class="sxs-lookup"><span data-stu-id="be6e5-124">The page includes a favicon, (`<link rel="shortcut icon" href="g-raph.png">`).</span></span> <span data-ttu-id="be6e5-125">Вы можете удалить эту строку или скачать файл **g-raph.png** из [GitHub](https://github.com/microsoftgraph/g-raph).</span><span class="sxs-lookup"><span data-stu-id="be6e5-125">You can remove this line, or you can download the **g-raph.png** file from [GitHub](https://github.com/microsoftgraph/g-raph).</span></span>

1. <span data-ttu-id="be6e5-126">Создайте новый файл с именем **Style. CSS** и добавьте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="be6e5-126">Create a new file named **style.css** and add the following code.</span></span>

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. <span data-ttu-id="be6e5-127">Создайте новый файл с именем **auth.js** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="be6e5-127">Create a new file named **auth.js** and add the following code.</span></span>

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

1. <span data-ttu-id="be6e5-128">Создайте новый файл с именем **ui.js** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="be6e5-128">Create a new file named **ui.js** and add the following code.</span></span>

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

1. <span data-ttu-id="be6e5-129">Сохраните все изменения и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="be6e5-129">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="be6e5-130">Теперь приложение должно выглядеть по-другому.</span><span class="sxs-lookup"><span data-stu-id="be6e5-130">Now, the app should look very different.</span></span>

    ![Снимок экрана с переработанной домашней страницей](images/app-layout.png)
