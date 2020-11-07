---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822953"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="7d510-101">В этом разделе мы добавим возможность создания событий в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d510-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-a-new-event-form"></a><span data-ttu-id="7d510-102">Создание новой формы события</span><span class="sxs-lookup"><span data-stu-id="7d510-102">Create a new event form</span></span>

1. <span data-ttu-id="7d510-103">Добавьте указанную ниже функцию в **ui.js** , чтобы отобразить форму для нового события.</span><span class="sxs-lookup"><span data-stu-id="7d510-103">Add the following function to **ui.js** to render a form for the new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a><span data-ttu-id="7d510-104">Создание события</span><span class="sxs-lookup"><span data-stu-id="7d510-104">Create the event</span></span>

1. <span data-ttu-id="7d510-105">Добавьте указанную ниже функцию в **graph.js** для чтения значений из формы и создания нового события.</span><span class="sxs-lookup"><span data-stu-id="7d510-105">Add the following function to **graph.js** to read the values from the form and create a new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. <span data-ttu-id="7d510-106">Сохраните изменения и обновите приложение.</span><span class="sxs-lookup"><span data-stu-id="7d510-106">Save your changes and refresh the app.</span></span> <span data-ttu-id="7d510-107">Щелкните элемент навигации по **календарю** , а затем нажмите кнопку **создать событие** .</span><span class="sxs-lookup"><span data-stu-id="7d510-107">Click the **Calendar** nav item, then click the **Create event** button.</span></span> <span data-ttu-id="7d510-108">Введите значения и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="7d510-108">Fill in the values and click **Create**.</span></span> <span data-ttu-id="7d510-109">Приложение возвращается в представление календаря после создания нового события.</span><span class="sxs-lookup"><span data-stu-id="7d510-109">The app returns to the calendar view once the new event is created.</span></span>

    ![Снимок экрана с формой создания события](images/create-event-01.png)
