---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822953"
---
<!-- markdownlint-disable MD002 MD041 -->

В этом разделе мы добавим возможность создания событий в календаре пользователя.

## <a name="create-a-new-event-form"></a>Создание новой формы события

1. Добавьте указанную ниже функцию в **ui.js** , чтобы отобразить форму для нового события.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a>Создание события

1. Добавьте указанную ниже функцию в **graph.js** для чтения значений из формы и создания нового события.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. Сохраните изменения и обновите приложение. Щелкните элемент навигации по **календарю** , а затем нажмите кнопку **создать событие** . Введите значения и нажмите кнопку **создать**. Приложение возвращается в представление календаря после создания нового события.

    ![Снимок экрана с формой создания события](images/create-event-01.png)
