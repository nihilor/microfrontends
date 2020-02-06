# Developing Microfrontends with Webcomponents

**Key message**: Webcomponents are the ideal basis for developing Microfrontends. They are an open standard, closing the gap between the business demand of maximum independency of and the currently dominant dependency on technology stacks.

1. [Introduction](#introduction)
    1. [Definition](#definition)
    1. [Why Microfrontends?](#why-microfrontends)
    1. [Principles of Microfrontends](#principles-of-microfrontends)
    1. [Why Webcomponents?](#why-webcomponents)
1. [Requirements](#requirements)
    1. [Registerable](#registerable)
    1. [Instantiatable](#instantiatable)
    1. [Configurable](#configurable)
    1. [Instructable](#instructable)
    1. [Observable](#observable)
    1. [Lifecyclable](#lifecyclable)
    1. [Customizable](#customizable)
1. [Conclusion](#conclusion)

## Introduction

Before we start, I will create a common understanding of microfrontends. And find some answers to the questions why we need microfrontends and why webcomponents may be the best solution.

### Definition

My definition of microfrontends:

> Microfrontends are self-contained software elements, composable to and integrateable into frontends – independently of the frontends architecture, technology stack, and functionality.  
&ndash; Mark Lubkowitz

### Why Microfrontends?

* Microfrontends achieve independency from architecture and technology stack.
* They are easily replaceable with other Microfrontends.
* They are easily reusable in other contexts.
* They may reduce costs, effort, and risk – and potentially increase development speed.
* They may solve organizational issues, for example the bottle neck of a frontend integration team.

### Principles of Microfrontends

* Microfrontends are self-reliant and free of dependencies to the environment.
* Microfrontends are self-contained and manage their own data models.
* Microfrontends provide an explicit, technical interface to its environment.
* Microfrontends prefer the composition of functionality over inheritance.
* Microfrontends are natively and seamlessly integrateable into nearly any environment.

### Why Webcomponents?

* Webcomponents are an official standard in its second iteration. Every modern webbrowser supports this standard.
* Webcomponents encapsulate the functionality, behaviour, and design – making them a strong foundation for Microfrontends.
* They are reusable and exchangeable.
* Webcomponents consist of further standards: Custom Element, Shadow DOM, HTML Template.
* Hence Webcomponents perfectly fit the Microfrontend Architecture Pattern.

## Requirements of Microfrontends

Microfrontends must be registerable, instantiatable, configurable, instructable, observable, lifecyclable, and customizable. Let's see, if Webcomponents meet these requirements.

### Registerable

* Custom Elements provide a central registry in the context of the webbrowser, making Webcomponents registerable and discoverable.
* A Polyfill for older webbrowser exists.
* The registry enforces a strict naming convention, requiring Webcomponents to contain at least one dash.
* Using prefixes, suffixes and dashes it‘s possible to establish a namespace convention – and must be done.
* Webcomponents can register themselves, or can be registered by other components.

```javascript
//  declare a new custom element based on HTML element
class TaskList extends HTMLElement {
    //  ...
}

//  register the custom element
customElements.define('task-list', TaskList);
```

### Instantiatable

* Webcomponents can be instantiated in two ways. First declaratively via HTML by writing down the Custom Elements name.
* The second way is imperative via JavaScript by creating a child element using the Custom Elements name.
* Webcomponents always call a constructor on instantiation.
* It‘s possible to create multiple instances of the same Custom Element in the same context.
* Using the constructor and dynamically loading the codebase makes versioning and more possible.

```html
<html>
    <body>
        <!-- 1. declarative -->
        <task-list id="personal"></task-list>
        <!-- 2. imperative -->
        <script type="text/javascript">
            let taskList = document.createElement('task-list');
            taskList.id = 'business';
            document.appendChild(taskList);
        </script>
    </body>
</html>
```

### Configurable

* Webcomponents fully support attributes. Thus, attributes are the perfect way to declaratively configure the Microfrontend via HTML.
* If exposed, the attributes are readable and writable via JavaScript the imperative style.
* Webcomponents can observe some of their attributes.
* That enables Microfrontends to react to configuration changes and also expose it.
* Attributes must only be used for simple and a small amount of data, enforcing a more technical interface.

```html
<task-list
     id="private"
     version="1.0"
     static="true"
     local="true"
></task-list>
```

### Instructable

* Webcomponents run in the context of a webbrowser. This provides access to the DOM – the combination of HTML and JavaScript.
* The DOM is the API!
* The DOM provides access to any element, attributes, and methods. It is a technical, explicit, consistent, and universal interface.
* Methods are great to instruct the Microfrontends.
* By invoking the methods of an element on a technical basis, it‘s possible to exchange arbitrary business data without changing the interface.

```javascript
let taskList = document.getElementById('personal');
taskList.clear();
taskList.add('Enjoy the OOP');
```

### Observable

* Once again: The DOM is the API. It provides different options to observe the Microfrontend.
* Other components can assign callback methods, that the Microfrontends invokes. But it‘s a bad practice.
* The Microfrontend can define and emit events that other components can register for. Good practice!
* It‘s possible to establish the publish-subscribe-pattern.
* The `MutationObserver` – an official language construct – can observe any element and custom element and reacts to any change in the DOM of the element.

```html
<task-list
    id="one"
    onchange="alert(document.getElementById('one').tasks)"
></task-list>
```

### Lifecyclable

* Due to the self-realiability of Microfrontends, a lifecycle is essential for the Microfrontend.
* Webcomponents provide three language elements that build the basis for a lifecycle: `constructor`, `connectedCallback`, `disconnectedCallback`.
* `constructor` is invoked on instantiation, `connectedCallback` as soon as the Microfrontend is connected to the DOM, `disconnectedCallback` when the element is dropped.

```javascript
class TaskList extends HTMLElement {
    //  ideal for instantiation
    constructor () {
    }
    //  inserted into the DOM
    connectedCallback () {
        this.boot();
    }
    //  observed attributes changed
    attributeChangedCallback (a, o, n) {
        //  ...
    }
    //  removed from the DOM
    disconnectedCallback () {
        this.stop();
    }
}
```

### Customizable

* Microfrontends must be reusable. So it‘s necessary for them to be customizable. The obvious solution is declaratively via HTML and via CSS.
* Customization requires strong separation of function and design so that style changes won‘t break the functionality.
* Style hooks can be realized with CSS Custom Element Properties. 
* Custom Elements can use CSS selectors to consider their context and to react appropriately. 
* Slots encourage the principle of composition. Specific elements, components, or even Microfrontends can be injected and used.

```html
<!-- Frontend -->
<style type="text/css">
    task-list { --primary-color: #009ba4; }
</style>
<!-- Microfrontend -->
<style type="text/css">
    :host { --primary-color: #a01441; }
    h1 { color: var(--primary-color); }
</style>
```

## Conclusion

1. Webcomponents cover all requirements of the Microfrontend Architecture Pattern. Additionally, they provide a fully native developing experience.
1. Microfrontends based on Webcomponents can, but must not, incorporate third party solutions. So they only depend on the execution environment, the Webbrowser, and the browser’s support of Webcomponents.
1. Webcomponents are the ideal basis to develop Microfrontends.

&copy; 2020 Mark Lubkowitz
