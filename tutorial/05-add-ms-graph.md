---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822944"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="fd158-101">В этом упражнении вы добавите Microsoft Graph в приложение.</span><span class="sxs-lookup"><span data-stu-id="fd158-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="fd158-102">Для этого приложения вы будете использовать библиотеку [клиентской библиотеки JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) , чтобы совершать вызовы в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fd158-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="fd158-103">Получение событий календаря из Outlook</span><span class="sxs-lookup"><span data-stu-id="fd158-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="fd158-104">В этом разделе вы будете использовать клиентскую библиотеку Microsoft Graph для получения событий календаря для пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd158-104">In this section, you'll use the Microsoft Graph client library to get calendar events for the user.</span></span>

1. <span data-ttu-id="fd158-105">Создайте в корневом каталоге проекта новый файл с именем **timezones.js** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="fd158-105">Create a new file in the root of the project named **timezones.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    <span data-ttu-id="fd158-106">Этот код сопоставляет идентификаторы часового пояса Windows идентификаторам часовых поясов IANA для совместимости с moment.js.</span><span class="sxs-lookup"><span data-stu-id="fd158-106">This code maps Windows time zone identifiers to IANA time zone identifiers for compatibility with moment.js.</span></span>

1. <span data-ttu-id="fd158-107">Добавьте указанную ниже функцию в **graph.js**.</span><span class="sxs-lookup"><span data-stu-id="fd158-107">Add the following function to **graph.js**.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    <span data-ttu-id="fd158-108">Рассмотрите, что делает этот код.</span><span class="sxs-lookup"><span data-stu-id="fd158-108">Consider what this code is doing.</span></span>

    - <span data-ttu-id="fd158-109">URL-адрес, который будет вызываться — это `/me/calendarview` .</span><span class="sxs-lookup"><span data-stu-id="fd158-109">The URL that will be called is `/me/calendarview`.</span></span>
    - <span data-ttu-id="fd158-110">`header`Метод добавляет заголовок, `Prefer` указывающий предпочтительный часовой пояс пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd158-110">The `header` method adds a `Prefer` header specifying the user's preferred time zone.</span></span>
    - <span data-ttu-id="fd158-111">`query`Метод добавляет время начала и окончания для представления календаря.</span><span class="sxs-lookup"><span data-stu-id="fd158-111">The `query` method adds the start and end times for the calendar view.</span></span>
    - <span data-ttu-id="fd158-112">`select`Метод ограничит поля, возвращаемые для каждого события, только теми, которые будут реально использоваться в представлении.</span><span class="sxs-lookup"><span data-stu-id="fd158-112">The `select` method limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="fd158-113">`orderby`Метод сортирует результаты по времени начала, начиная с самого раннего события.</span><span class="sxs-lookup"><span data-stu-id="fd158-113">The `orderby` method sorts the results by the start time, with the earliest event being first.</span></span>
    - <span data-ttu-id="fd158-114">`top`Метод запрашивает до 50 событий в ответе.</span><span class="sxs-lookup"><span data-stu-id="fd158-114">The `top` method requests up to 50 events in the response.</span></span>

1. <span data-ttu-id="fd158-115">Откройте **ui.js** и добавьте указанную ниже функцию.</span><span class="sxs-lookup"><span data-stu-id="fd158-115">Open **ui.js** and add the following function.</span></span>

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. <span data-ttu-id="fd158-116">Обновите `switch` оператор в `updatePage` функции, чтобы он вызывался, `showCalendar` когда представление имеет значение `Views.calendar` .</span><span class="sxs-lookup"><span data-stu-id="fd158-116">Update the `switch` statement in the `updatePage` function to call `showCalendar` when the view is `Views.calendar`.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. <span data-ttu-id="fd158-117">Сохраните изменения и обновите приложение.</span><span class="sxs-lookup"><span data-stu-id="fd158-117">Save your changes and refresh the app.</span></span> <span data-ttu-id="fd158-118">Войдите и щелкните ссылку **Календарь** на панели навигации.</span><span class="sxs-lookup"><span data-stu-id="fd158-118">Sign in and click the **Calendar** link in the nav bar.</span></span> <span data-ttu-id="fd158-119">Если все работает, вы должны увидеть дамп событий JSON в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd158-119">If everything works, you should see a JSON dump of events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="fd158-120">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="fd158-120">Display the results</span></span>

<span data-ttu-id="fd158-121">В этом разделе будет обновлена `showCalendar` функция для отображения событий более удобным для пользователя способом.</span><span class="sxs-lookup"><span data-stu-id="fd158-121">In this section you will update the `showCalendar` function to display the events in a more user-friendly manner.</span></span>

1. <span data-ttu-id="fd158-122">Замените имеющуюся функцию `showCalendar` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="fd158-122">Replace the existing `showCalendar` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    <span data-ttu-id="fd158-123">В результате получается цикл по коллекции событий и добавляется строка таблицы для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="fd158-123">This loops through the collection of events and adds a table row for each one.</span></span>

1. <span data-ttu-id="fd158-124">Сохраните изменения и обновите приложение.</span><span class="sxs-lookup"><span data-stu-id="fd158-124">Save the changes and refresh the app.</span></span> <span data-ttu-id="fd158-125">Щелкните ссылку **Календарь** , после чего приложение должно отобразить таблицу событий для текущей недели.</span><span class="sxs-lookup"><span data-stu-id="fd158-125">Click on the **Calendar** link and the app should now render a table of events for the current week.</span></span>

    ![Снимок экрана с таблицей событий](./images/calendar-list.png)
