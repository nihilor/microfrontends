# Developing Microfrontends with Webcomponents

**Key message**: Webcomponents are the ideal basis for developing Microfrontends. They are an open standard, closing the gap between the business demand of maximum independency of and the currently dominant dependency on technology stacks.

## Definition

My definition of micro-frontends is:

> Microfrontends are self-contained software elements, composable to and integrateable into frontends – independently of the frontends architecture, technology stack, and functionality.

## Why Microfrontends?

* Microfrontends achieve independency from architecture and technology stack.
* They are easily replaceable with other Microfrontends.
* They are easily reusable in other contexts.
* They may reduce costs, effort, and risk – and potentially increase development speed.

## Principles of Microfrontends

* Microfrontends are self-reliant and free of dependencies to the environment.
* Microfrontends are self-contained and manage their own data models.
* Microfrontends provide an explicit, technical interface to its environment.
* Microfrontends prefer the composition of functionality over inheritance.
* Microfrontends are natively and seamlessly integrateable into nearly any environment.

## Why Webcomponents?

* Webcomponents are an official standard in its second iteration. Every modern webbrowser supports this standard.
* Webcomponents encapsulate the functionality, behaviour, and design – making them a strong foundation for Microfrontends.
* They are reusable and exchangeable.
* Webcomponents consist of further standards: Custom Element, Shadow DOM, HTML Template.
* Hence Webcomponents perfectly fit the Microfrontend Architecture Pattern.

## Requirements of Microfrontends

* Registerable
* Instantiatable
* Configurable
* Instructable
* Observable
* Lifecycleable
* Customizable

## Registerable

* Custom Elements provide a central registry in the context of the webbrowser, making Webcomponents registerable and discoverable.
* A Polyfill for older webbrowser exists.
* The registry enforces a strict naming convention, requiring Webcomponents to contain at least one dash.
* Using prefixes, suffixes and dashes it‘s possible to establish a namespace convention – and must be done.
* Webcomponents can register themselves, or can be registered by other components.

## Instantiatable

* Webcomponents can be instantiated in two ways. First declaratively via HTML by writing down the Custom Elements name.
* The second way is imperative via JavaScript by creating a child element using the Custom Elements name.
* Webcomponents always call a constructor on instantiation.
* It‘s possible to create multiple instances of the same Custom Element in the same context.
* Using the constructor and dynamically loading the codebase makes versioning and more possible.

## Configurable

* Webcomponents fully support attributes. Thus, attributes are the perfect way to declaratively configure the Microfrontend via HTML.
* If exposed, the attributes are readable and writable via JavaScript the imperative style.
* Webcomponents can observe some of their attributes.
* That enables Microfrontends to react to configuration changes and also expose it.
* Attributes must only be used for simple and a small amount of data, enforcing a more technical interface.

## Instructable

* Webcomponents run in the context of a webbrowser. This provides access to the DOM – the combination of HTML and JavaScript.
* The DOM is the API!
* The DOM provides access to any element, attributes, and methods. It is a technical, explicit, consistent, and universal interface.
* Methods are great to instruct the Microfrontends.
* By invoking the methods of an element on a technical basis, it‘s possible to exchange arbitrary business data without changing the interface.

## Observable

* Once again: The DOM is the API. It provides different options to observe the Microfrontend.
* Other components can assign callback methods, that the Microfrontends invokes. But it‘s a bad practice.
* The Microfrontend can define and emit events that other components can register for. Good practice!
* It‘s possible to establish the publish-subscribe-pattern.
* The `MutationObserver` – an official language construct – can observe any element and custom element and reacts to any change in the DOM of the element.

## Lifecyclable

* Due to the self-realiability of Microfrontends, a lifecycle is essential for the Microfrontend.
* Webcomponents provide three language elements that build the basis for a lifecycle: `constructor`, `connectedCallback`, `disconnectedCallback`.
* `constructor` is invoked on instantiation, `connectedCallback` as soon as the Microfrontend is connected to the DOM, `disconnectedCallback` when the element is dropped.

## Customizable

* Microfrontends must be reusable. So it‘s necessary for them to be customizable. The obvious solution is declaratively via HTML and via CSS.
* Customization requires strong separation of function and design so that style changes won‘t break the functionality.
* Style hooks can be realized with CSS Custom Element Properties. 
* Custom Elements can use CSS selectors to consider their context and to react appropriately. 
* Slots encourage the principle of composition. Specific elements, components, or even Microfrontends can be injected and used.

## Conclusion

1. Webcomponents cover all requirements of the Microfrontend Architecture Pattern. Additionally, they provide a fully native developing experience.
1. Microfrontends based on Webcomponents can, but must not, incorporate third party solutions. So they only depend on the execution environment, the Webbrowser, and the browser’s support of Webcomponents.
1. Webcomponents are the ideal basis to develop Microfrontends.

&copy; 2020 Mark Lubkowitz
