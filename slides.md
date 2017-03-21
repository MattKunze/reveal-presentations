## React Intro

---

## Angular Intro

* Component-based web application framework
* Includes everything most apps require (routing, HTTP, testing, etc)
* Standards, best practices, style guide
* Cleaner + faster than Angular 1, adds cool features
* Native too: NativeScript (mobile), Electron (desktop)

---

## React Benefits

* Small API Surface Area
* Uni-directional dataflow
* Universal programming methods - server-side rendering, react-native, react-vr
* 'Just JavaScript'
* Community-driven solutions

---

## React Challenges

* Fragmentation
* Boilerplate
* App/module composition

---

## Angular Benefits

* Getting started is easy: everything's included
* Standardization: easy to jump into existing projects
* DI keeps components isolated and testing clean
* TypeScript surfaces errors, documents code, enables great tooling
* HTML-like template syntax familiar to most developers, designers

---

## Angular Challenges

* Diverging from defaults takes more work
* Default bundle a bit large (~400k not gzipped)
* Some template errors surface at runtime, not compile time
* TypeScript requires a bit more code

---

## React CLI

Many starter kits and templates, `create-react-app` is probably the easiest
to get started:

```
npm i -g create-react-app
create-react-app new-app
```

---

## Angular CLI
- Angular CLI creates an app with best practices:

  ```
  npm install -g @angular/cli
  ng new PROJECT_NAME
  cd PROJECT_NAME
  ng serve
  ```

- Visit localhost:4200. Reloads on change
- `ng generate`: scaffolding for components, pipes, services, etc. 
- `ng build` (webpack), `ng test` (jasmine/karma), `ng e2e` (protractor),
`ng lint`, `ng eject`

---

## React Components

* Components are basically render functions that transform state into how it
should appear in the UI

* React has an ES6 class that can be extended (this also supports lifecycle
methods)

```js
class SimpleComponent extends React.Component {
  render() {
    return (
      <div className="simple-component">
        <a href='#' onClick={this.props.onClick}>Click {this.props.title}</a>
      </div>
    )
  }
}
```

---

## Stateless Functional Components

Simple components can simply be render functions with no additional noise:

```js
const SimpleComponent = ({ title, onClick }) = {
  return (
    <div className="simple-component">
      <a href='#' onClick={onClick}>Click {props.title}</a>
    </div>
  )
}
```

---

## Angular Components
- Instead of MVC, use small, simple components:

  ```js
  import { Component } from '@angular/core';

  @Component({
    selector: 'show-title',
    template: '<h1>{{title}}</h1>',
    styles: ['h1 { font-size: 3rem; }']
  })
  export class ShowTitleComponent {
    title: string = 'This is a string.';
  }
  ```

- Each component gets its own scope (JS and CSS)
- Easy to understand and test (services get injected)

---

## JSX

JSX is an optional preprocessor that supports formatting DOM output that looks
like HTML.

* Curly-brackets escape back to JS so you can use regular looping,
  conditionals, assignment, etc

```js
const SimpleComponent = ({ title, onClick }) = {
  return (
    React.createElement( 'div', { className: "simple-component" },
      React.createElement( 'a', { href: '#', onClick: onClick },
        'Title: ' + title
      )
    )
  )
}
```

---

## Angular Templates
- Templates are HTML with enhancements:

  ```html
  <ul>
    <li *ngFor="let item of items"
      (click)="itemClick(item)">Name: {{item.name}}</li>
  </ul>
  ```
- `*` for UI changes, `()` for event binding, `[]` for property binding, `[()]`
for two-way binding, and `{{}}` for data binding.
- Look is familiar to most devs and designers

---

## Component State

Components have information passed from parents (`props`) and optionally
local information managed by the component (`state`)

* `props` and `state` are just POJOS and you can manage the data however you
  want (plain JS, immutable, whatever)
* Ideally most components are stateless

---

## Communication Between Components

---

## Angular Parent -> Child
* Parent component template contains input binding:

  ```html
  <child-component [myInput]=3></child-component>
  ```

* Child component takes input:

  ```js
  export class child-component {
    @Input() myInput: number;
  }
  ```

---

## Angular Child -> Parent
* Parent component template contains:

  ```html
  <child-component (myOutput)="processInput($event)">
  </child-component>
  ```

* Child component emits event for parent to catch:

  ```js
  export class childComponent {
    @Output() myOutput: new EventEmitter<number>();

    ...
    this.myOutput.emit(3);
  }
  ```
* EventEmitter is basically an RxJS observable

---

## Data store
- Optional: ngrx/store (RxJS, more to come)
- Entire app state in one immutable data structure
- Reducer functions go from one state to the next
- Can also use Redux (or any other store you prefer)

---

## Change detection and DOM updates
- Angular maintains a directed tree of components and their relationships.
- Stable, fast, predictable.
- By default, Angular checks all components in the tree with each event.
- With immutables, Angular can check only subtrees where an input has changed (onPush). Even faster

---

## Types with TypeScript
- Adds strong typing to JS. Can gradually add types
- Examples:

  ```ts
  let myNumber: number = 42;
  let author: string = 'Douglas Adams';
  author = 5; // Compile time error: Type 'number' is not assignable to type 'string'

  interface Bird { // Ensure object has particular structure + types
    name: string;
    speed: number;
  }

  function addAmountToEachItem(amount: number, items: number[]): number[] {
    return items.map(i => i + amount);
  }
  ```

- VS Code: linting, jump to definition, autofill, peek features

---

## Observables
- Callbacks -> Promises -> Observables (streams)
- RxJS: rich set of FP helpers (Underscore for streams)
- Angular's router, HTTP services use observables
- Subscribe + transform stream (map, filter, scan...)
  ```js
  const testSubject = new Rx.Subject();
  const basicScan = testSubject
    .startWith(0)
    .scan((acc, curr) => acc + curr);
  const subscribe = basicScan.subscribe(val => console.log(val));
  testSubject.next(1); //1
  testSubject.next(2); //3
  testSubject.next(3); //6

  // Source: https://gist.github.com/btroncone/d6cf141d6f2c00dc6b35
  ```

---

## Dependency Injection
- DI helps solve banana/gorilla/jungle problem:

  ```js
  @Component({
    selector: 'person-list',
    providers: [PersonService]
  })
  export class personListComponent {
    people: Person[];
    constructor(personService: PersonService) {
      this.people = peopleService.getPeople();
    }
  }
  ```
- When testing, mock PersonService + inject mock
- Common mock: http services in unit tests
- React can use it too! See http://blog.mgechev.com/

---

## ReactNative

ReactNative offers a similar programming environment, but you end up with a
'Native' app (ie: not a webview running DOM nodes)

* Better performance, especially with animations and transitions
* Backend runs JavaScript so you don't need Swift/Java/Objective-C
* Separate UI components for iOS and Android

---

## Mobile
- Two options for mobile apps: Ionic and NativeScript
- Both have cli tools -- easy to get started
- Ionic: mobile apps with Angular and Cordova (Ionic 2 uses Angular 2)
- Ionic interface components = HTML/CSS/JS
- NativeScript: Angular 2 native apps with native interfaces
- NativeScript is fast, but there's more to maintain

---

## Trends
- Small, tightly-scoped components
- Component tree with DOM diffing
- A single source of state (Redux)
- Strong types (TypeScript, Flow)
- Functional programming (composable functions, immutables)
