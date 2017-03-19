## React Intro

---

## Angular Intro

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

---

## Angular Challenges

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
- Angular CLI: create an app with best practices
- Simplest way to get started:

  ```
  npm install -g @angular/cli
  ng new PROJECT_NAME
  cd PROJECT_NAME
  ng serve
  ```

- Your app is running at localhost:4200
- ng generate: scaffolding for components, pipes, services, etc
- what else: `ng build` (webpack), `ng test` (jasmine/karma), `ng e2e` (protractor), `ng lint`, `ng build`, `ng eject`

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
- Instead of MVC, encapsulate everything inside small, simple components
- Decorators separate Angular-specific code from generic JS code:

```js
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: '<h1>{{title}}</h1>',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title: string = 'This is a string.';
}
```

- Components should be small, simple, encapsulated, easy to test
- Each component gets its own scope (JS and CSS)
- Use services to store/retrieve data

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
- Example of a basic template:

```html
<ul>
  <li *ngFor="let item of items" (click)="itemClick(item)">Name: {{item.name}}</li>
</ul>
```
- It's HTML with enhancements: `*` changes UI, `()` inputs, `[]` outputs, `([])` for two-way bindings, and `{{}}` for data bindings.
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

## Communication between components
**1. Parent -> child input binding.** Parent template contains:

```html
<child-component [myInput]=3></child-component>
```

Child component:

```js
export class child-component { @Input() myInput: number; }
```

**2. Parent listens for event from child.** Parent component template:

```html
<child-component (myInput)="processInput($event)"></child-component>
```

Child component:

```js
export class childComponent {
  @Output() myOutput: new EventEmitter<number>();
  ...
  this.myOutput.emit(3);
}
```

---

## Data store
- Optional: ngrx/store
- Entire application state in one immutable data structure
- Reducer functions take you from one state to the next
- Use with onPush change detection for increased speed
- Can also use Redux (or any other store you prefer)

---

## Change detection and DOM updates
- How does it work? Angular maintains a directed tree of components and their relationships. Stable, fast, predictable.
- By default, Angular checks all components in the tree with each event.
- With immutables, Angular can check only subtrees where an input has changed (onPush). Even faster

---

## Types with TypeScript
- TypeScript: compiler which adds strong typing to JS (you get ES6 too). `.ts -> .js`
- Can start with an existing codebase and gradually add types.
- Example:

```ts
let myNumber: number = 42;
let author: string = 'Douglas Adams';
author = 5; // Compile time error: Type 'number' is not assignable to type 'string'
```

- Create object interfaces like:

```ts
interface Bird {
  name: string;
  speed: number;
}
```

- Improve function legibility and error checking:
```ts
function addAmountToEachItem(amount: number, items: number[]): number[] {
  return items.map(i => i + amount);
}
```

- VS Code or atom-typescript provide great linting, jump to definition, autofill, peek features

---

## Observables
- Promises solve callback hell. Observables solve it for streams of data
- RxJS implements observables in Angular
- Rich set of FP helpers. Like Underscore, but for streams
- Angular's router and HTTP services use them
- Many operators: map, filter, merge, scan, etc
- Subscribe to websocket or mouse movements + transform stream
- Simple example:
```js
const testSubject = new Rx.Subject();
const basicScan = testSubject
  .startWith(0)
  .scan((acc, curr) => acc + curr);
const subscribe = basicScan.subscribe(val => console.log('Accumulated total:', val));
testSubject.next(1); //1
testSubject.next(2); //3
testSubject.next(3); //6
```
(Source: https://gist.github.com/btroncone/d6cf141d6f2c00dc6b35)

---

## Dependency Injection
- Easy mocking, clean separation between modules
- Solves the banana/gorilla/jungle problem
- In this example, the PersonService is injected:

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
- Real vs mock? Component doesn't know the difference
- Common use: http services in unit tests
- Can use Angular's DI in React too: http://blog.mgechev.com/2017/01/30/implementing-dependency-injection-react-angular-element-injectors/

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
- Small, tightly-scoped components with no side effects
- Component tree with DOM diffing
- A single source of state
- Strong types
- Functional or reactive programming
