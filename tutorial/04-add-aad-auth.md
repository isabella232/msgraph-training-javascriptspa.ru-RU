---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822902"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="aa0e6-101">В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="aa0e6-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="aa0e6-103">На этом этапе библиотека [библиотеки проверки подлинности (Майкрософт](https://github.com/AzureAD/microsoft-authentication-library-for-js) ) будет интегрирована в приложение.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-103">In this step you will integrate the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-js) library into the application.</span></span>

1. <span data-ttu-id="aa0e6-104">Создайте новый файл в корневом каталоге с именем **config.js** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-104">Create a new file in the root directory named **config.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    <span data-ttu-id="aa0e6-105">Замените `YOUR_APP_ID_HERE` идентификатором приложения на портале регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aa0e6-106">Если вы используете систему управления версиями (например, Git), то в дальнейшем будет полезно исключить файл **config.js** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-106">If you're using source control such as git, now would be a good time to exclude the **config.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="aa0e6-107">Откройте **auth.js** и добавьте следующий код в начало файла.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-107">Open **auth.js** and add the following code to the beginning of the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a><span data-ttu-id="aa0e6-108">Реализация входа</span><span class="sxs-lookup"><span data-stu-id="aa0e6-108">Implement sign-in</span></span>

<span data-ttu-id="aa0e6-109">В этом разделе вы реализуете `signIn` функции и `signOut` функции.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-109">In this section you'll implement the `signIn` and `signOut` functions.</span></span>

1. <span data-ttu-id="aa0e6-110">Замените имеющуюся функцию `signIn` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-110">Replace the existing `signIn` function with the following.</span></span>

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

    <span data-ttu-id="aa0e6-111">В этом временном коде отображается маркер доступа после успешного входа.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-111">This temporary code will display the access token after a successful login.</span></span>

1. <span data-ttu-id="aa0e6-112">Замените имеющуюся функцию `signOut` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-112">Replace the existing `signOut` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. <span data-ttu-id="aa0e6-113">Сохраните изменения и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-113">Save your changes and refresh the page.</span></span> <span data-ttu-id="aa0e6-114">После входа вы увидите окно с сообщением об ошибке, в котором отображается маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-114">After you sign in, you should see an error box that shows the access token.</span></span>

## <a name="get-the-users-profile"></a><span data-ttu-id="aa0e6-115">Получение профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="aa0e6-115">Get the user's profile</span></span>

<span data-ttu-id="aa0e6-116">В этом разделе `signIn` функция используется для получения профиля пользователя из Microsoft Graph с помощью маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-116">In this section you'll improve the `signIn` function to use the access token to get the user's profile from Microsoft Graph.</span></span>

1. <span data-ttu-id="aa0e6-117">Добавьте указанную ниже функцию в **auth.js** , чтобы получить маркер доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-117">Add the following function in **auth.js** to retrieve the user's access token.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. <span data-ttu-id="aa0e6-118">Создайте в корневом каталоге проекта новый файл с именем **graph.js** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-118">Create a new file in the root of the project named **graph.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    <span data-ttu-id="aa0e6-119">Этот код создает поставщика авторизации, который упаковывает `getToken` метод в **auth.js** , и инициализирует клиент Graph с этим поставщиком.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-119">This code creates an authorization provider that wraps the `getToken` method in **auth.js** , and initializes the Graph client with this provider.</span></span>

1. <span data-ttu-id="aa0e6-120">Добавьте указанную ниже функцию в **graph.js** , чтобы получить профиль пользователя.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-120">Add the following function in **graph.js** to get the user's profile.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. <span data-ttu-id="aa0e6-121">Замените имеющуюся функцию `signIn` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-121">Replace the existing `signIn` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. <span data-ttu-id="aa0e6-122">Сохраните изменения и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-122">Save your changes and refresh the page.</span></span> <span data-ttu-id="aa0e6-123">После входа в систему необходимо вернуться на домашнюю страницу, но пользовательский интерфейс должен измениться, чтобы показать, что вы выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-123">After you sign in, you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

    ![Снимок экрана домашней страницы после входа](./images/user-signed-in.png)

1. <span data-ttu-id="aa0e6-125">Щелкните аватар пользователя в правом верхнем углу, чтобы получить доступ к ссылке **выхода** .</span><span class="sxs-lookup"><span data-stu-id="aa0e6-125">Click the user avatar in the top right corner to access the **Sign out** link.</span></span> <span data-ttu-id="aa0e6-126">При нажатии кнопки **выйти** сбрасывается сеанс и возвращается на домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-126">Clicking **Sign out** resets the session and returns you to the home page.</span></span>

    ![Снимок экрана с раскрывающимся меню со ссылкой "выйти"](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="aa0e6-128">Хранение и обновление маркеров</span><span class="sxs-lookup"><span data-stu-id="aa0e6-128">Storing and refreshing tokens</span></span>

<span data-ttu-id="aa0e6-129">На этом шаге приложение имеет маркер доступа, который отправляется в `Authorization` заголовке вызовов API.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-129">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="aa0e6-130">Это маркер, который позволяет приложению получать доступ к Microsoft Graph от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-130">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="aa0e6-131">Однако этот маркер кратковременно используется.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-131">However, this token is short-lived.</span></span> <span data-ttu-id="aa0e6-132">Срок действия маркера истечет через час после его выдачи.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-132">The token expires an hour after it is issued.</span></span> <span data-ttu-id="aa0e6-133">В этом случае маркер обновления становится полезен.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-133">This is where the refresh token becomes useful.</span></span> <span data-ttu-id="aa0e6-134">Маркер обновления позволяет приложению запросить новый маркер доступа, не требуя от пользователя повторного входа.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-134">The refresh token allows the app to request a new access token without requiring the user to sign in again.</span></span>

<span data-ttu-id="aa0e6-135">Так как приложение использует библиотеку MSAL, нет необходимости внедрять логику хранения или обновления маркеров.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-135">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="aa0e6-136">MSAL кэширует маркер в сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-136">MSAL caches the token in the browser session.</span></span> <span data-ttu-id="aa0e6-137">`acquireTokenSilent`Метод сначала проверяет кэшированный маркер, и если срок его действия не истек, он возвращается.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-137">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="aa0e6-138">Если срок действия истек, он использует кэшированный маркер обновления, чтобы получить новый.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-138">If it is expired, it uses the cached refresh token to obtain a new one.</span></span> <span data-ttu-id="aa0e6-139">Клиентский объект Graph вызывает `getToken` метод в **auth.js** для каждого запроса, гарантируя, что у него есть обновленный маркер.</span><span class="sxs-lookup"><span data-stu-id="aa0e6-139">The Graph client object calls the `getToken` method in **auth.js** on every request, ensuring that it has an up-to-date token.</span></span>
