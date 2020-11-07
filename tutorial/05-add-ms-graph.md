---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822944"
---
<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы добавите Microsoft Graph в приложение. Для этого приложения вы будете использовать библиотеку [клиентской библиотеки JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) , чтобы совершать вызовы в Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Получение событий календаря из Outlook

В этом разделе вы будете использовать клиентскую библиотеку Microsoft Graph для получения событий календаря для пользователя.

1. Создайте в корневом каталоге проекта новый файл с именем **timezones.js** и добавьте следующий код.

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    Этот код сопоставляет идентификаторы часового пояса Windows идентификаторам часовых поясов IANA для совместимости с moment.js.

1. Добавьте указанную ниже функцию в **graph.js**.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    Рассмотрите, что делает этот код.

    - URL-адрес, который будет вызываться — это `/me/calendarview` .
    - `header`Метод добавляет заголовок, `Prefer` указывающий предпочтительный часовой пояс пользователя.
    - `query`Метод добавляет время начала и окончания для представления календаря.
    - `select`Метод ограничит поля, возвращаемые для каждого события, только теми, которые будут реально использоваться в представлении.
    - `orderby`Метод сортирует результаты по времени начала, начиная с самого раннего события.
    - `top`Метод запрашивает до 50 событий в ответе.

1. Откройте **ui.js** и добавьте указанную ниже функцию.

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

1. Обновите `switch` оператор в `updatePage` функции, чтобы он вызывался, `showCalendar` когда представление имеет значение `Views.calendar` .

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. Сохраните изменения и обновите приложение. Войдите и щелкните ссылку **Календарь** на панели навигации. Если все работает, вы должны увидеть дамп событий JSON в календаре пользователя.

## <a name="display-the-results"></a>Отображение результатов

В этом разделе будет обновлена `showCalendar` функция для отображения событий более удобным для пользователя способом.

1. Замените имеющуюся функцию `showCalendar` указанным ниже кодом.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    В результате получается цикл по коллекции событий и добавляется строка таблицы для каждой из них.

1. Сохраните изменения и обновите приложение. Щелкните ссылку **Календарь** , после чего приложение должно отобразить таблицу событий для текущей недели.

    ![Снимок экрана с таблицей событий](./images/calendar-list.png)
