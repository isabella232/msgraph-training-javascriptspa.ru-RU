---
ms.openlocfilehash: 9b9b118c2d95710a5a3f9a1afe4d03a6185b4b14
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822932"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="381ce-101">Выполнение завершенного проекта</span><span class="sxs-lookup"><span data-stu-id="381ce-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="381ce-102">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="381ce-102">Prerequisites</span></span>

<span data-ttu-id="381ce-103">Чтобы запустить завершенный проект в этой папке, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="381ce-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="381ce-104">[Node.js](https://nodejs.org) установлен на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="381ce-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="381ce-105">Если у вас нет Node.js, посетите предыдущую ссылку для получения вариантов загрузки.</span><span class="sxs-lookup"><span data-stu-id="381ce-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="381ce-106">( **Примечание:** это руководство было написано с узлом версии 12.16.1.</span><span class="sxs-lookup"><span data-stu-id="381ce-106">( **Note:** This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="381ce-107">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="381ce-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="381ce-108">Личная учетная запись Майкрософт с почтовым ящиком на Outlook.com или рабочей или учебной учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="381ce-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="381ce-109">Если у вас нет учетной записи Майкрософт, у вас есть несколько вариантов для получения бесплатной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="381ce-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="381ce-110">Вы можете [зарегистрироваться для создания новой личной учетной записи Майкрософт](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="381ce-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="381ce-111">Вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.</span><span class="sxs-lookup"><span data-stu-id="381ce-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="381ce-112">Регистрация веб-приложения с помощью центра администрирования Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="381ce-112">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="381ce-113">Откройте браузер и перейдите к [Центру администрирования Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="381ce-113">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="381ce-114">Войдите с помощью **личной учетной записи** (т.е. учетной записи Microsoft) или **рабочей (учебной) учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="381ce-114">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="381ce-115">Выберите **Azure Active Directory** на панели навигации слева, затем выберите **Регистрация приложений** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="381ce-115">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="381ce-116">Снимок экрана с регистрациями приложений</span><span class="sxs-lookup"><span data-stu-id="381ce-116">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

    > <span data-ttu-id="381ce-117">**Примечание:** Пользователи Azure AD B2C могут видеть только **регистрации приложений (прежних версий)**.</span><span class="sxs-lookup"><span data-stu-id="381ce-117">**Note:** Azure AD B2C users may only see **App registrations (legacy)**.</span></span> <span data-ttu-id="381ce-118">В этом случае перейдите непосредственно к [https://aka.ms/appregistrations](https://aka.ms/appregistrations) .</span><span class="sxs-lookup"><span data-stu-id="381ce-118">In this case, please go directly to [https://aka.ms/appregistrations](https://aka.ms/appregistrations).</span></span>

1. <span data-ttu-id="381ce-119">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="381ce-119">Select **New registration**.</span></span> <span data-ttu-id="381ce-120">На странице **Зарегистрировать приложение** задайте необходимые значения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="381ce-120">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="381ce-121">Введите **имя** `JavaScript Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="381ce-121">Set **Name** to `JavaScript Graph Tutorial`.</span></span>
    - <span data-ttu-id="381ce-122">Введите **поддерживаемые типы учетных записей** для **учетных записей в любом каталоге организаций и личных учетных записей Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="381ce-122">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="381ce-123">В разделе **URI адрес перенаправления** введите значение в первом раскрывающемся списке `Single-page application (SPA)` и задайте значение `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="381ce-123">Under **Redirect URI** , set the first drop-down to `Single-page application (SPA)` and set the value to `http://localhost:8080`.</span></span>

    ![Снимок страницы "регистрация приложения"](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="381ce-125">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="381ce-125">Choose **Register**.</span></span> <span data-ttu-id="381ce-126">На странице **учебника по графике JavaScript** СКОПИРУЙТЕ значение **идентификатора Application (Client)** и сохраните его, он понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="381ce-126">On the **JavaScript Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="381ce-128">Выберите **Проверка подлинности** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="381ce-128">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="381ce-129">Нахождение **неявного раздела предоставления** и включение **маркеров доступа** и **маркеров ID**.</span><span class="sxs-lookup"><span data-stu-id="381ce-129">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="381ce-130">Выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="381ce-130">Choose **Save**.</span></span>

    ![Снимок экрана с неявным разделом предоставления](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a><span data-ttu-id="381ce-132">Настройка примера</span><span class="sxs-lookup"><span data-stu-id="381ce-132">Configure the sample</span></span>

1. <span data-ttu-id="381ce-133">Переименуйте файл **./граф-туториал/config.example.js** в **/граф-туториал/config.js**.</span><span class="sxs-lookup"><span data-stu-id="381ce-133">Rename the **./graph-tutorial/config.example.js** file to **./graph-tutorial/config.js**.</span></span>
1. <span data-ttu-id="381ce-134">Измените файл **./граф-туториал/config.js** и внесите следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="381ce-134">Edit the **./graph-tutorial/config.js** file and make the following changes.</span></span>
    1. <span data-ttu-id="381ce-135">Замените `YOUR_APP_ID_HERE` **идентификатором приложения** , полученным на портале регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="381ce-135">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="381ce-136">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="381ce-136">Run the sample</span></span>

1. <span data-ttu-id="381ce-137">Выполните следующую команду в командной панели CLI, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="381ce-137">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="381ce-138">Откройте браузер и перейдите по адресу `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="381ce-138">Open a browser and browse to `http://localhost:8080`.</span></span>
