# Angular 20, Made with ❤️ by Hassan ELDash

## 📘 Section 1: Libraries vs Frameworks

- Library vs Framework theory
- Angular CLI setup
- Component structure
- Data binding types
- UI libraries (Bootstrap, Angular Material)
- Early Angular 20 references (e.g. standalone components)

---

#### 💡 Theoretical Background

**Library** vs **Framework** is a foundational concept in frontend development:

| Concept     | Library                                           | Framework                                                        |
| ----------- | ------------------------------------------------- | ---------------------------------------------------------------- |
| **Control** | You call it when needed (`you are in control`)    | It calls your code (`it is in control`) — "Inversion of Control" |
| **Purpose** | Solves specific problems (e.g., animations, HTTP) | Provides an entire structure for building applications           |
| **Example** | React (library for UI), Lodash, jQuery            | Angular, NestJS, Vue.js (opinionated), Express.js                |

---

#### 🎯 Types of Frameworks

1. **Opinionated Frameworks**: Pre-decide most tools and architecture
   → Angular, NestJS

   > "Do it the Angular way"

2. **Unopinionated Frameworks**: Let you pick tools
   → Express.js, Vue.js, React

---

### 🧠 Angular Overview

| Feature            | Description                                                   |
| ------------------ | ------------------------------------------------------------- |
| **Architecture**   | MVCS (Model-View-Component-Service)                           |
| **Language**       | TypeScript (Angular 2+ onwards)                               |
| **First Release**  | 2009 as AngularJS (v1.x, JavaScript-based)                    |
| **Modern Angular** | Rewritten in TypeScript since Angular 2 (2016)                |
| **Latest Version** | Angular 20 (2025), using Standalone Components (no NgModules) |

---

### 🗂️ Project Types

| App Type | Description                                                        |
| -------- | ------------------------------------------------------------------ |
| **MPA**  | Multi-Page Application (old way, full page reload per interaction) |
| **SPA**  | Single Page Application (modern way, Angular default)              |

Angular supports:

- **Client-Side Rendering (CSR)** ✅
- **Server-Side Rendering (SSR)** (via Angular Universal)
- **Static Site Generation (SSG)**

---

### ✅ Section 2: Setting Up Angular CLI

#### 📦 Step-by-Step Installation

```bash
npm install -g @angular/cli
```

> ✅ `-g` installs CLI globally on your system
> 📦 This gives you the `ng` command to generate and run Angular projects.

---

#### 🛠️ Create a New Angular App

```bash
ng new my-angular-app
```

You will be prompted with options:

1. Zoneless? → ❌ Choose `N` (unless you're experimenting)
2. Stylesheet format? → ✅ Choose `CSS`
3. Enable SSR/SSG? → ❌ Choose `N` for basic SPA

---

### 📁 Project Structure (Angular 20)

```plaintext
src/
  app/
    app.component.ts      → Component logic (TypeScript, Controller)
    app.component.html    → Template (View)
    app.component.css     → Stylesheet
    app.config.ts         → App bootstrap (Standalone configuration)
```

> 💡 Angular 20 uses **Standalone Components** — no `NgModule` required

---

### 🚀 Run the App

```bash
cd my-angular-app
ng serve -o
```

- `ng serve`: Runs built-in dev server
- `-o`: Opens browser on `http://localhost:4200`

---

### ⚙️ Build for Production

```bash
ng build
```

Produces:

```plaintext
dist/
  index.html
  main.js
  styles.css
  polyfills.js
```

---

## ✅ Section 3: Angular 20 Components — Standalone, CLI Generation, Decorators

### 📘 Theoretical Background

**Component** is the most fundamental building block in Angular. It’s a TypeScript class with metadata that controls:

- 📄 HTML template
- 🎨 Styles (CSS/SCSS)
- ⚙️ Logic and data (TS class)

---

### 🧩 What Makes a Component?

A component has 3 key parts (MVC View + Controller + Styles):

| File             | Role               | Example Path                       |
| ---------------- | ------------------ | ---------------------------------- |
| `component.ts`   | Controller (logic) | `src/app/home/home.component.ts`   |
| `component.html` | View (template)    | `src/app/home/home.component.html` |
| `component.css`  | Stylesheet         | `src/app/home/home.component.css`  |

> 🔁 These work together to control 1 piece of UI — a **self-contained unit**

---

### 🎯 Angular 20: Standalone Components

Angular 17+ introduced a **new era** of development:

✅ No more `NgModule`
✅ Each component declares what it imports
✅ Cleaner + faster app bootstrapping

---

### ✨ Minimal Standalone Component Example

#### ✅ Step-by-Step

```bash
ng g c components/header --standalone
```

> 🔧 `--standalone`: tells Angular to generate a standalone component
> 🧾 Result:

```plaintext
src/app/components/header/
  header.component.ts       ✅ TypeScript
  header.component.html     ✅ HTML
  header.component.css      ✅ Styles
  header.component.spec.ts  ❌ Test file (optional)
```

---

### 🔍 `@Component()` Decorator Explained

```ts
import { Component } from "@angular/core";

@Component({
  selector: "app-header", // used as <app-header></app-header>
  standalone: true, // no need to be declared in a module
  imports: [], // list of dependencies (e.g., RouterModule)
  templateUrl: "./header.component.html",
  styleUrls: ["./header.component.css"],
})
export class HeaderComponent {
  title = "My Angular App";
}
```

#### ✅ Syntax Breakdown

- `@Component({ ... })`: a special decorator function that tells Angular how to treat this class
- `selector`: defines the custom tag name
- `standalone: true`: required in Angular 17+ to avoid NgModule
- `imports`: you must manually list any used components/directives (like `NgIf`, `RouterLink`)
- `templateUrl`: path to the HTML view
- `styleUrls`: array of stylesheet paths

---

### 🧪 Embed a Component in Another Template

To use `<app-header>` in your root component:

#### 1. Add it to `imports` in `AppComponent`

```ts
// src/app/app.component.ts
import { Component } from "@angular/core";
import { HeaderComponent } from "./components/header/header.component";

@Component({
  selector: "app-root",
  standalone: true,
  imports: [HeaderComponent], // ✅ required for standalone components
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {}
```

#### 2. Use it in HTML like a normal tag

```html
<!-- app.component.html -->
<app-header></app-header>
<h1>Welcome to Angular 20!</h1>
```

---

### ✅ Recap

| Concept              | Summary                                                   |
| -------------------- | --------------------------------------------------------- |
| Component            | A UI block with template + logic + style                  |
| Standalone           | New default in Angular 17+ — no modules                   |
| CLI Generation       | `ng g c components/header --standalone`                   |
| Decorator            | `@Component()` adds metadata to control behavior          |
| Importing Components | You must import child components into the parent manually |
| Selector             | Used like custom HTML tags                                |

---

## ✅ Section 4: Angular 20 Data Binding — All Types with Step-by-Step Examples

### 📘 What is Data Binding?

Data binding is the mechanism that connects your **TypeScript class (Component logic)** to the **HTML view (template)**.

Angular provides multiple forms of data binding to help you:

- 🟢 Display dynamic content
- 🔵 Respond to user input
- 🟣 Sync values between HTML and class variables
- 🔴 Control styles/classes based on conditions

---

### 🔢 Angular’s Data Binding Types

| Type               | Syntax                     | Direction           | Purpose                   |
| ------------------ | -------------------------- | ------------------- | ------------------------- |
| Interpolation      | `{{ variable }}`           | One-way (TS ➝ HTML) | Show data                 |
| Property Binding   | `[property]="value"`       | One-way (TS ➝ HTML) | Set HTML attributes       |
| Event Binding      | `(event)="handler()"`      | One-way (HTML ➝ TS) | React to user actions     |
| Two-Way Binding    | `[(ngModel)]="variable"`   | Two-way             | Sync form input and model |
| Template Reference | `#ref`, `ref.value`        | Local to DOM        | Read DOM values           |
| Class Binding      | `[class.name]="condition"` | One-way (TS ➝ HTML) | Add/remove CSS classes    |
| Style Binding      | `[style.prop]="value"`     | One-way (TS ➝ HTML) | Apply styles dynamically  |

---

### ✅ 1. Interpolation: `{{ ... }}`

#### 🧠 Purpose: Display variable or expression in the template

#### ✅ Code:

```ts
// hello.component.ts
export class HelloComponent {
  username = "Hassan";
}
```

```html
<!-- hello.component.html -->
<h1>Hello, {{ username }}!</h1>
```

> 🧪 Output: **Hello, Hassan!**

---

### ✅ 2. Property Binding: `[property]="expression"`

#### 🧠 Purpose: Bind a value from TypeScript to an HTML attribute

```ts
export class PropertyComponent {
  imageUrl = "https://picsum.photos/200";
}
```

```html
<img [src]="imageUrl" alt="Random Image" />
```

> ✅ Avoids hardcoding attributes; works with dynamic values

---

### ✅ 3. Event Binding: `(event)="handler()"`

#### 🧠 Purpose: Respond to user input (click, input, change)

```ts
export class EventComponent {
  count = 0;

  increase() {
    this.count++;
  }
}
```

```html
<button (click)="increase()">Increment</button>
<p>You clicked {{ count }} times</p>
```

---

### ✅ 4. Two-Way Binding: `[(ngModel)]="variable"`

#### 🧠 Purpose: Sync between input field and class variable

> ⚠️ Requires `FormsModule` or `ReactiveFormsModule` in `imports`

#### ✅ Step-by-step:

1. Import `FormsModule` in parent component or main `AppComponent`:

```ts
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [FormsModule],
  ...
})
```

2. Use `[(ngModel)]` in HTML:

```ts
export class FormComponent {
  name = "";
}
```

```html
<input [(ngModel)]="name" placeholder="Enter your name" />
<p>Hello {{ name }}</p>
```

---

### ✅ 5. Template Reference: `#ref`

#### 🧠 Purpose: Access a DOM element directly

```html
<input #username type="text" /> <button (click)="sayHello(username.value)">Say Hello</button>
```

```ts
sayHello(name: string) {
  alert(`Hello ${name}`);
}
```

---

### ✅ 6. Class Binding: `[class.className]="condition"`

```ts
isActive = true;
```

```html
<div [class.active]="isActive">I'm active</div>
```

> Add/remove class dynamically

---

### ✅ 7. Style Binding: `[style.prop]="value"`

```ts
color = "red";
fontSize = "24px";
```

```html
<p [style.color]="color" [style.fontSize]="fontSize">Styled Text</p>
```

---

### 🔁 8. Structural Directives (Mentioned, not detailed here)

These modify the DOM structure:

- `*ngIf`
- `*ngFor`
- `[ngSwitch]`

We'll cover them in the **Directives section** soon.

---

### 🧪 ✅ Working Live Example (All Types Together)

```ts
export class BindingExampleComponent {
  name = "Hassan";
  age = 30;
  isActive = true;
  count = 0;
  color = "green";

  increase() {
    this.count++;
  }
}
```

```html
<h2>Hello {{ name }}!</h2>

<p [style.color]="color">Your age is {{ age }}</p>

<button (click)="increase()">+1</button>
<p>Count: {{ count }}</p>

<input [(ngModel)]="name" />
<p>Hello {{ name }}</p>

<div [class.active]="isActive">Active Box</div>
```

---

## ✅ Section 5: Angular 20 Directives — Built-in vs Custom (Revised with Detailed Examples)

### 📘 What is a Directive?

A **Directive** is a special instruction in Angular that adds behavior or modifies the DOM layout/appearance of an element.

There are 3 types of directives:

| Type           | Purpose                                | Examples                                    |
| -------------- | -------------------------------------- | ------------------------------------------- |
| **Component**  | A directive with a template (UI block) | `@Component()`                              |
| **Structural** | Alters DOM layout                      | `*ngIf`, `*ngFor`, `*ngSwitch`              |
| **Attribute**  | Alters behavior/appearance             | `[ngClass]`, `[ngStyle]`, `customHighlight` |

---

## ✅ 1. Structural Directives (with `*`)

> 🔧 Structural = adds/removes/modifies DOM structure

---

### ✅ 1.1 `*ngIf`

#### 🧠 Show/hide content based on a condition

```ts
showDetails = true;
```

```html
<button (click)="showDetails = !showDetails">Toggle</button>

<div *ngIf="showDetails">
  <p>These are the details!</p>
</div>
```

---

### ✅ 1.2 `*ngFor`

#### 🧠 Repeat an element for each item in a collection

```ts
fruits = ["Apple", "Banana", "Cherry"];
```

```html
<ul>
  <li *ngFor="let fruit of fruits; let i = index">{{ i + 1 }} - {{ fruit }}</li>
</ul>
```

---

### ✅ 1.3 `ngSwitch`, `*ngSwitchCase`, `*ngSwitchDefault`

#### 🧠 Conditional rendering based on value

```ts
selectedRole = "admin";
```

```html
<div [ngSwitch]="selectedRole">
  <p *ngSwitchCase="'admin'">Welcome, Admin!</p>
  <p *ngSwitchCase="'user'">Hello, User!</p>
  <p *ngSwitchDefault>Please login</p>
</div>
```

> ⚠️ Requires importing `CommonModule` if used in a standalone component.

```ts
import { CommonModule } from '@angular/common';

@Component({
  ...
  imports: [CommonModule]
})
```

---

## ✅ 2. Attribute Directives

> 🎨 Modify element **appearance or behavior** (without changing layout)

---

### ✅ 2.1 `[ngClass]`

```ts
isImportant = true;
```

```html
<p [ngClass]="{ 'important': isImportant }">Important Message!</p>
```

With CSS:

```css
.important {
  color: red;
  font-weight: bold;
}
```

---

### ✅ 2.2 `[ngStyle]`

```ts
styleObject = {
  color: "blue",
  fontSize: "18px",
};
```

```html
<p [ngStyle]="styleObject">Styled Text</p>
```

---

### ✅ 2.3 Custom Attribute Directive Example

Let’s build a custom directive that highlights any element on hover:

---

#### 🧱 Step-by-step: Create a Custom Directive

```bash
ng g directive directives/highlight
```

### 📁 Output:

```plaintext
src/app/directives/highlight.directive.ts
```

---

### ✅ highlight.directive.ts

```ts
import { Directive, ElementRef, HostListener } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
  standalone: true,
})
export class HighlightDirective {
  constructor(private el: ElementRef) {}

  @HostListener("mouseenter")
  onMouseEnter() {
    this.el.nativeElement.style.backgroundColor = "yellow";
  }

  @HostListener("mouseleave")
  onMouseLeave() {
    this.el.nativeElement.style.backgroundColor = "";
  }
}
```

---

### ✅ Use It in a Component

```ts
import { HighlightDirective } from './directives/highlight.directive';

@Component({
  ...
  imports: [HighlightDirective]
})
```

```html
<p appHighlight>Hover over me to see highlight</p>
```

---

## ✅ Summary Table

| Directive Type   | Example Syntax                | Description                          |
| ---------------- | ----------------------------- | ------------------------------------ |
| Structural       | `*ngIf`, `*ngFor`, `ngSwitch` | Add/remove/alter DOM                 |
| Attribute        | `[ngClass]`, `[ngStyle]`      | Change appearance or behavior        |
| Custom Directive | `[appHighlight]`              | Your own behavior via `@Directive()` |

---

## ✅ Section 6: Angular 20 Services, Dependency Injection (DI), and State Sharing

### 📘 What is a Service in Angular?

An Angular **Service** is a **reusable class** that contains logic or data you want to **share across components** — such as:

- Fetching data from an API
- Sharing state between components
- Performing calculations
- Logging or alert utilities

> Services follow the **Separation of Concerns** principle: UI logic stays in components, business/data logic goes into services.

---

### 🧠 What is Dependency Injection (DI)?

Angular has a built-in **Dependency Injection system** that:

- Creates service instances when needed
- Injects them into components or other services

This promotes **reusability**, **testability**, and **modularity**.

> DI means: Instead of a class creating its own dependencies, Angular gives (injects) them from outside.

---

## ✅ Step-by-Step: Create and Use a Service in Angular 20

### 🎯 Step 1: Generate a Service via CLI

```bash
ng g service services/counter
```

This creates:

```plaintext
src/app/services/counter.service.ts
```

---

### 🎯 Step 2: Write a Shared Service

```ts
// src/app/services/counter.service.ts
import { Injectable, signal } from "@angular/core";

@Injectable({
  providedIn: "root", // Automatically available everywhere
})
export class CounterService {
  // ✅ Angular 20 Signals for reactive state
  count = signal(0);

  increment() {
    this.count.update((c) => c + 1);
  }

  reset() {
    this.count.set(0);
  }
}
```

---

### 📘 Explanation:

| Line                   | Meaning                                            |
| ---------------------- | -------------------------------------------------- |
| `@Injectable({ ... })` | Tells Angular this class can be injected           |
| `providedIn: 'root'`   | Available globally in the app (singleton instance) |
| `signal(0)`            | Angular 20 reactive variable (auto-tracked)        |
| `update(fn)`           | Safely change the signal value                     |
| `set(value)`           | Set a new value directly                           |

---

### 🎯 Step 3: Use the Service in a Component

```ts
import { Component } from "@angular/core";
import { CounterService } from "../services/counter.service";

@Component({
  selector: "app-counter",
  standalone: true,
  template: `
    <h2>Count: {{ svc.count() }}</h2>
    <button (click)="svc.increment()">+1</button>
    <button (click)="svc.reset()">Reset</button>
  `,
  imports: [],
})
export class CounterComponent {
  constructor(public svc: CounterService) {}
}
```

---

### ✅ Explanation of How It Works

- `svc.count()` is a signal getter (like a function)
- Changes to `svc.count` **automatically re-render** the template
- You don’t need to use `@Input()` to pass count value — the service handles shared state globally!

---

## 🔁 Sharing State Between Components

Let’s say you want 2 components to reflect the **same counter**.

### Step-by-Step:

#### ✅ `component-a.component.ts`

```ts
@Component({
  selector: "component-a",
  standalone: true,
  template: `
    <h3>Component A Count: {{ svc.count() }}</h3>
    <button (click)="svc.increment()">A +</button>
  `,
  imports: [],
})
export class ComponentA {
  constructor(public svc: CounterService) {}
}
```

---

#### ✅ `component-b.component.ts`

```ts
@Component({
  selector: "component-b",
  standalone: true,
  template: `
    <h3>Component B Count: {{ svc.count() }}</h3>
    <button (click)="svc.increment()">B +</button>
  `,
  imports: [],
})
export class ComponentB {
  constructor(public svc: CounterService) {}
}
```

---

#### ✅ Final Output in `app.component.html`

```html
<component-a></component-a> <component-b></component-b>
```

> ✅ Any change made in one component updates the count in the other — they share the same reactive state from the service.

---

## 🔁 Optional: Share with `BehaviorSubject` Instead of Signals

```ts
// With RxJS
import { Injectable } from "@angular/core";
import { BehaviorSubject } from "rxjs";

@Injectable({ providedIn: "root" })
export class CounterRxService {
  count$ = new BehaviorSubject<number>(0);

  increment() {
    this.count$.next(this.count$.value + 1);
  }

  reset() {
    this.count$.next(0);
  }
}
```

> ⚠️ This requires `async` pipe in the template:

```html
<h2>Count: {{ svc.count$ | async }}</h2>
```

---

### ✅ Summary: Signals vs BehaviorSubject

| Feature         | `signal()` (Angular 20)    | `BehaviorSubject` (RxJS)         |              |
| --------------- | -------------------------- | -------------------------------- | ------------ |
| Built-in?       | ✅ Yes                     | ❌ No (external RxJS)            |              |
| Template access | `signal()` like `count()`  | \`                               | async\` pipe |
| Auto reactivity | ✅                         | ✅ with `async`                  |              |
| Clean syntax    | ✅ No subscriptions needed | ❌ Must subscribe or use `async` |              |

---

## ✅ Section 7: Angular 20 Routing System — Standalone Route Setup, Dynamic Params, and Lazy Loading

### 📘 What is Angular Routing?

Angular’s **router** lets you:

- 🔗 Navigate between views/components
- 📄 Load components by URL (like pages)
- 🧩 Pass route parameters
- 💤 Lazy-load feature modules/components

Angular 20 uses **standalone routing configuration** — you no longer need `AppRoutingModule`.

---

### ✅ Step-by-Step Routing Setup (Angular 20)

---

### 🎯 Step 1: Enable Routing in App

When generating the app with `ng new`, answer:

```
? Would you like to add Angular routing? Yes
```

If not added before, update `main.ts`:

---

### ✅ `main.ts` (Standalone App Entry Point)

```ts
import { bootstrapApplication } from "@angular/platform-browser";
import { provideRouter } from "@angular/router";
import { AppComponent } from "./app/app.component";
import { routes } from "./app/app.routes";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});
```

---

### 🎯 Step 2: Define Routes in `app.routes.ts`

Create the file:

```bash
src/app/app.routes.ts
```

```ts
import { Routes } from "@angular/router";
import { HomeComponent } from "./components/home.component";
import { AboutComponent } from "./components/about.component";

export const routes: Routes = [
  { path: "", component: HomeComponent }, // localhost:4200/
  { path: "about", component: AboutComponent }, // localhost:4200/about
];
```

---

### 🎯 Step 3: Create Components

```bash
ng g c components/home --standalone
ng g c components/about --standalone
```

---

### 🎯 Step 4: Add `<router-outlet />` in App Template

```html
<!-- app.component.html -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>

<router-outlet></router-outlet>
```

---

### 🎯 Step 5: Import RouterModule in AppComponent

```ts
import { Component } from "@angular/core";
import { RouterOutlet } from "@angular/router";
import { HomeComponent } from "./components/home.component";
import { AboutComponent } from "./components/about.component";

@Component({
  selector: "app-root",
  standalone: true,
  templateUrl: "./app.component.html",
  imports: [RouterOutlet, HomeComponent, AboutComponent],
})
export class AppComponent {}
```

---

### ✅ ✅ Your App is Now Routable!

URLs like:

- `http://localhost:4200/` → HomeComponent
- `http://localhost:4200/about` → AboutComponent

---

## ✅ Dynamic Route Parameters

Let’s say you want to view details of an item by ID:

---

### 🎯 Update Routes with Param

```ts
{ path: 'product/:id', component: ProductComponent }
```

---

### 🎯 ProductComponent

```bash
ng g c components/product --standalone
```

#### ✅ `product.component.ts`

```ts
import { Component } from "@angular/core";
import { ActivatedRoute } from "@angular/router";

@Component({
  selector: "app-product",
  standalone: true,
  template: `<h2>Product ID: {{ id }}</h2>`,
  imports: [],
})
export class ProductComponent {
  id: string | null = null;

  constructor(private route: ActivatedRoute) {
    this.route.paramMap.subscribe((params) => {
      this.id = params.get("id");
    });
  }
}
```

> 🧪 Visiting `/product/5` will display: **Product ID: 5**

---

## ✅ Lazy Loading Components in Angular 20

Lazy loading loads a component **only when needed**, improving performance.

---

### 🎯 Define Lazy Route

```ts
{
  path: 'lazy',
  loadComponent: () =>
    import('./components/lazy.component').then(m => m.LazyComponent)
}
```

---

### 🎯 Create Lazy Component

```bash
ng g c components/lazy --standalone
```

#### ✅ lazy.component.ts

```ts
@Component({
  selector: "app-lazy",
  standalone: true,
  template: `<h2>This is a lazy-loaded component!</h2>`,
  imports: [],
})
export class LazyComponent {}
```

> 🔥 Angular loads this file **only when `/lazy` is visited**

---

## ✅ Summary Table

| Feature                     | Syntax                                                    |
| --------------------------- | --------------------------------------------------------- |
| Basic Route                 | `{ path: '', component: HomeComponent }`                  |
| Param Route                 | `{ path: 'item/:id', component: ProductComponent }`       |
| Route Links                 | `<a routerLink="/about">About</a>`                        |
| Router Outlet               | `<router-outlet></router-outlet>`                         |
| Lazy Loading                | `loadComponent: () => import(...).then(m => m.Component)` |
| Navigation Programmatically | `this.router.navigate(['/path'])`                         |

---

## ✅ Section 8: Angular 20 Forms — Template-Driven vs Reactive Forms with Full Working Examples

### 📘 What Are Angular Forms?

Angular provides two powerful ways to build forms:

| Form Type          | Best For                        | How It Works                                 |
| ------------------ | ------------------------------- | -------------------------------------------- |
| ✅ Template-Driven | Simple forms, few fields        | Use directives in HTML + `ngModel` binding   |
| ✅ Reactive Forms  | Complex forms, validation logic | Use `FormGroup`, `FormControl` in TypeScript |

---

## ✅ 1. Template-Driven Forms

---

### 🧠 Theoretical Overview

- Defined mostly in the **HTML template**
- Relies on `[(ngModel)]` for two-way binding
- Validation is declared via attributes (`required`, `minlength`, etc.)
- Requires `FormsModule`

---

### ✅ Step-by-Step Setup

#### 🎯 Step 1: Import `FormsModule` in Component

```ts
import { FormsModule } from "@angular/forms";

@Component({
  selector: "app-contact-form",
  standalone: true,
  templateUrl: "./contact-form.component.html",
  imports: [FormsModule],
})
export class ContactFormComponent {
  name = "";
  email = "";

  submit() {
    alert(`Name: ${this.name}, Email: ${this.email}`);
  }
}
```

---

#### 🎯 Step 2: Create Template

```html
<!-- contact-form.component.html -->
<h2>Contact Us</h2>
<form (ngSubmit)="submit()">
  <label>
    Name:
    <input type="text" [(ngModel)]="name" name="name" required />
  </label>

  <label>
    Email:
    <input type="email" [(ngModel)]="email" name="email" required />
  </label>

  <button type="submit">Submit</button>
</form>

<p>Name: {{ name }}</p>
<p>Email: {{ email }}</p>
```

---

### ✅ Live Behavior

- Data is bound live via `[(ngModel)]`
- Submit handler is called with `(ngSubmit)`
- Fields are validated using `required` HTML attributes

---

## ✅ 2. Reactive Forms

---

### 🧠 Theoretical Overview

- Built entirely in **TypeScript**
- Full control over state and validation logic
- Scales better for large/complex forms
- Requires `ReactiveFormsModule`

---

### ✅ Step-by-Step Setup

#### 🎯 Step 1: Import ReactiveFormsModule

```ts
import { ReactiveFormsModule, FormGroup, FormControl, Validators } from "@angular/forms";

@Component({
  selector: "app-register",
  standalone: true,
  templateUrl: "./register.component.html",
  imports: [ReactiveFormsModule],
})
export class RegisterComponent {
  form = new FormGroup({
    username: new FormControl("", [Validators.required]),
    password: new FormControl("", [Validators.required, Validators.minLength(6)]),
  });

  submit() {
    console.log(this.form.value);
  }
}
```

---

#### 🎯 Step 2: Create Template

```html
<!-- register.component.html -->
<h2>Register</h2>
<form [formGroup]="form" (ngSubmit)="submit()">
  <label>
    Username:
    <input formControlName="username" />
    <span *ngIf="form.get('username')?.invalid && form.get('username')?.touched"> Username is required. </span>
  </label>

  <label>
    Password:
    <input type="password" formControlName="password" />
    <span *ngIf="form.get('password')?.errors?.['minlength']"> Min 6 characters required. </span>
  </label>

  <button type="submit" [disabled]="form.invalid">Submit</button>
</form>
```

---

### ✅ Explanation

| Concept            | Meaning                                        |
| ------------------ | ---------------------------------------------- |
| `FormGroup`        | Represents the entire form                     |
| `FormControl`      | Represents each input field                    |
| `Validators`       | Built-in rules (e.g., `required`, `minLength`) |
| `form.get('name')` | Access a control by name                       |
| `form.value`       | Get all input values                           |

---

## ✅ Comparison Table: Template-Driven vs Reactive

| Feature        | Template-Driven | Reactive                      |
| -------------- | --------------- | ----------------------------- |
| Setup Location | Mostly in HTML  | Mostly in TypeScript          |
| Best For       | Simple forms    | Complex, dynamic forms        |
| Validation     | HTML attributes | Programmatic via `Validators` |
| Form Control   | `[(ngModel)]`   | `FormControl`, `FormGroup`    |
| Module Needed  | `FormsModule`   | `ReactiveFormsModule`         |

---

## ✅ Summary Code Snippets

### Template-Driven:

```html
<input [(ngModel)]="email" name="email" required />
```

### Reactive:

```ts
new FormControl("", [Validators.required, Validators.minLength(4)]);
```

---

## ✅ Section 9: Angular 20 Signals + `resource()` — Full Reactive Data Fetching (No RxJS, No @Input)

### 📘 What Are Angular Signals?

> Signals are a **reactivity system** in Angular 20 that **tracks state and automatically updates the UI** when the state changes — without the need for RxJS or manual change detection.

---

### ✅ Key Signal Primitives:

| Signal API         | What it Does                                    | Angular 20 Example                        |
| ------------------ | ----------------------------------------------- | ----------------------------------------- |
| `signal(value)`    | Creates a reactive state signal                 | `count = signal(0)`                       |
| `count()`          | Get signal value (used like a getter)           | `{{ count() }}`                           |
| `count.set(val)`   | Sets a new value                                | `count.set(5)`                            |
| `count.update(fn)` | Updates value with a function                   | `count.update(c => c + 1)`                |
| `computed(fn)`     | Derived signal from other signals               | `total = computed(() => price() * qty())` |
| `effect(fn)`       | Runs function whenever dependent signals change | `effect(() => console.log(count()))`      |

---

## ✅ What is `resource()` in Angular 20?

> `resource()` is a built-in signal-based abstraction for **asynchronous data fetching** (like HTTP calls).
> It **reactively refetches** data when its `params()` signal changes.

---

## ✅ Real Example: Fetching Comments with `resource()` + `signal()`

We’ll now build a real example:

- Use `JSONPlaceholder` API
- Allow user to enter a Post ID
- Reactively fetch comments for that Post
- Show loading, error, and success states

---

### ✅ Step-by-Step Angular 20 Service with `resource()`

#### 🎯 1. Create Service

```bash
ng g service services/comments
```

---

### ✅ `comments.service.ts`

```ts
import { Injectable, signal, resource } from "@angular/core";

export interface Comment {
  postId: number;
  id: number;
  name: string;
  email: string;
  body: string;
}

@Injectable({ providedIn: "root" })
export class CommentsService {
  // ✅ Reactive state signal for postId
  postId = signal(1);

  // ✅ Angular 20 resource for async API calls
  commentsResource = resource<Comment[]>({
    params: () => ({ postId: this.postId() }),
    loader: async ({ params, abortSignal }) => {
      const res = await fetch(`https://jsonplaceholder.typicode.com/comments?postId=${params.postId}`, { signal: abortSignal });
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      const data = await res.json();
      return Array.isArray(data) ? data : [];
    },
  });
}
```

---

### ✅ Step-by-Step UI Component to Display Comments

#### 🎯 2. Generate Component

```bash
ng g c components/comments --standalone
```

---

### ✅ `comments.component.ts`

```ts
import { Component } from "@angular/core";
import { NgIf, NgFor, AsyncPipe } from "@angular/common";
import { CommentsService } from "../services/comments.service";

@Component({
  selector: "app-comments",
  standalone: true,
  templateUrl: "./comments.component.html",
  styleUrls: ["./comments.component.css"],
  imports: [NgIf, NgFor],
})
export class CommentsComponent {
  constructor(public svc: CommentsService) {}
}
```

---

### ✅ `comments.component.html`

```html
<h2>Fetch Comments</h2>

<label>
  Post ID:
  <input type="number" [value]="svc.postId()" (input)="svc.postId.set($any($event.target).valueAsNumber)" />
</label>

<div [@if]="svc.commentsResource.state === 'loading'">⏳ Loading comments...</div>

<div [@if]="svc.commentsResource.state === 'error'">❌ Error: {{ svc.commentsResource.error?.message }}</div>

<ul [@if]="svc.commentsResource.state === 'success'">
  <li *ngFor="let c of svc.commentsResource.data()"><strong>{{ c.name }}</strong>: {{ c.body }}</li>
</ul>
```

---

### ✅ Explanation of `resource()` states:

| State     | Description                                 |
| --------- | ------------------------------------------- |
| `loading` | Request in progress                         |
| `success` | Request succeeded and `data()` is available |
| `error`   | An error occurred; accessible via `.error`  |

---

### ✅ All Together — App Structure Summary

- 🧠 `signal()` tracks `postId`
- 🔄 `resource()` automatically calls `fetch()` when `postId()` changes
- 🧾 UI updates based on the reactive state — no need for RxJS or manual subscriptions

---

## ✅ Comparison: `resource()` vs RxJS Observable

| Feature        | `resource()`              | `Observable` (RxJS)                        |
| -------------- | ------------------------- | ------------------------------------------ |
| Reactive       | ✅ yes (Signal based)     | ✅ yes (Observable based)                  |
| Built-in       | ✅ Angular Core           | ❌ Needs RxJS                              |
| Tracks params  | ✅ auto via `params()`    | ❌ manual via `switchMap`, `combineLatest` |
| Cancelable     | ✅ `abortSignal` built-in | ✅ via `takeUntil`                         |
| Simpler syntax | ✅ yes                    | ❌ more verbose                            |

---

## ✅ Section 10: Angular 20 Full CRUD with Signals + `resource()` — (GET, POST, PUT, DELETE)

## 🧩 Project Goal

We’ll manage a list of fake posts using the [JSONPlaceholder API](https://jsonplaceholder.typicode.com/posts):

- GET posts
- POST new post
- PUT (update) post
- DELETE post

---

## ✅ 1. Step-by-Step Setup: Angular Service with Full CRUD

---

### 🎯 1. Create `posts.service.ts`

```bash
ng g service services/posts
```

---

### ✅ `posts.service.ts`

```ts
import { Injectable, signal, resource } from "@angular/core";

export interface Post {
  id: number;
  title: string;
  body: string;
}

@Injectable({ providedIn: "root" })
export class PostsService {
  // Signal to re-trigger reload after mutations
  refreshKey = signal(0);

  // ✅ Fetch all posts (re-runs when refreshKey changes)
  postsResource = resource<Post[]>({
    params: () => this.refreshKey(),
    loader: async ({ abortSignal }) => {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
        signal: abortSignal,
      });
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      return await res.json();
    },
  });

  // ✅ Add a new post (POST)
  async addPost(post: Partial<Post>) {
    await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(post),
    });
    this.refreshKey.update((x) => x + 1); // Trigger reload
  }

  // ✅ Update post (PUT)
  async updatePost(post: Post) {
    await fetch(`https://jsonplaceholder.typicode.com/posts/${post.id}`, {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(post),
    });
    this.refreshKey.update((x) => x + 1); // Trigger reload
  }

  // ✅ Delete post
  async deletePost(id: number) {
    await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`, {
      method: "DELETE",
    });
    this.refreshKey.update((x) => x + 1); // Trigger reload
  }
}
```

---

## ✅ 2. Create Component UI

```bash
ng g c components/post-crud --standalone
```

---

### ✅ `post-crud.component.ts`

```ts
import { Component } from "@angular/core";
import { NgIf, NgFor, AsyncPipe } from "@angular/common";
import { PostsService, Post } from "../services/posts.service";
import { FormsModule } from "@angular/forms";

@Component({
  selector: "app-post-crud",
  standalone: true,
  templateUrl: "./post-crud.component.html",
  styleUrls: ["./post-crud.component.css"],
  imports: [NgIf, NgFor, FormsModule],
})
export class PostCrudComponent {
  constructor(public svc: PostsService) {}

  // Form state
  newPostTitle = "";
  newPostBody = "";
  editMode = false;
  selectedPost: Post | null = null;

  // Create
  async addPost() {
    await this.svc.addPost({
      title: this.newPostTitle,
      body: this.newPostBody,
    });
    this.newPostTitle = "";
    this.newPostBody = "";
  }

  // Start edit
  edit(post: Post) {
    this.selectedPost = { ...post };
    this.editMode = true;
  }

  // Submit edit
  async update() {
    if (this.selectedPost) {
      await this.svc.updatePost(this.selectedPost);
      this.editMode = false;
      this.selectedPost = null;
    }
  }

  // Cancel edit
  cancel() {
    this.editMode = false;
    this.selectedPost = null;
  }

  // Delete
  async remove(id: number) {
    if (confirm("Delete this post?")) {
      await this.svc.deletePost(id);
    }
  }
}
```

---

### ✅ `post-crud.component.html`

```html
<h2>Angular 20 CRUD with Signals + Resource()</h2>

<form *ngIf="!editMode" (ngSubmit)="addPost()">
  <input [(ngModel)]="newPostTitle" name="title" placeholder="Title" required />
  <textarea [(ngModel)]="newPostBody" name="body" placeholder="Body" required></textarea>
  <button type="submit">Add Post</button>
</form>

<form *ngIf="editMode" (ngSubmit)="update()">
  <input [(ngModel)]="selectedPost!.title" name="editTitle" />
  <textarea [(ngModel)]="selectedPost!.body" name="editBody"></textarea>
  <button type="submit">Update</button>
  <button type="button" (click)="cancel()">Cancel</button>
</form>

<hr />

<div *ngIf="svc.postsResource.state === 'loading'">Loading posts...</div>
<div *ngIf="svc.postsResource.state === 'error'">Error: {{ svc.postsResource.error?.message }}</div>

<ul *ngIf="svc.postsResource.state === 'success'">
  <li *ngFor="let post of svc.postsResource.data()">
    <h4>{{ post.title }}</h4>
    <p>{{ post.body }}</p>
    <button (click)="edit(post)">Edit</button>
    <button (click)="remove(post.id)">Delete</button>
  </li>
</ul>
```

---

## ✅ Feature Summary

| Feature        | Signal-Based Implementation                        |
| -------------- | -------------------------------------------------- |
| **State**      | `signal()` to track `refreshKey`                   |
| **Fetch**      | `resource()` tracks signal changes automatically   |
| **Create**     | `addPost()` uses POST and updates signal           |
| **Update**     | `updatePost()` uses PUT and triggers signal        |
| **Delete**     | `deletePost()` uses DELETE and triggers signal     |
| **Reactivity** | Full reactive refresh without RxJS or manual logic |

---

## ✅ Section 11: Angular 20 Signals + Forms + Routing Combined — Real App Integration Example

---

### 📘 Objective

Build a real-world app that uses:

✅ `signal()` and `resource()` for reactivity
✅ `FormsModule` for user input
✅ Angular Standalone Routing to navigate between:

- **Post List View**
- **Add Post Form View**
- **Edit Post View**

This simulates a real CRUD app navigation without using RxJS or NgModules.

---

## 🗂️ Folder Structure

```
src/
  app/
    app.routes.ts          ✅ Routing setup
    main.ts                ✅ Bootstrap entry
    components/
      post-list.component.ts
      post-form.component.ts
    services/
      posts.service.ts     ✅ Central signal-based store
```

---

## ✅ 1. Routing Configuration (`app.routes.ts`)

```ts
import { Routes } from "@angular/router";
import { PostListComponent } from "./components/post-list.component";
import { PostFormComponent } from "./components/post-form.component";

export const routes: Routes = [
  { path: "", component: PostListComponent },
  { path: "add", component: PostFormComponent },
  { path: "edit/:id", component: PostFormComponent },
];
```

---

## ✅ 2. Bootstrap Routing in `main.ts`

```ts
import { bootstrapApplication } from "@angular/platform-browser";
import { provideRouter } from "@angular/router";
import { AppComponent } from "./app/app.component";
import { routes } from "./app/app.routes";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});
```

---

## ✅ 3. Shared Signal-Based Service (`posts.service.ts`)

> Already created in Section 10 with:

- `postsResource`
- `addPost()`
- `updatePost()`
- `deletePost()`

We’ll now extend it with `getPostById(id: number)`:

```ts
getPostById(id: number): Promise<Post> {
  return fetch(`https://jsonplaceholder.typicode.com/posts/${id}`).then(res => res.json());
}
```

---

## ✅ 4. Post List Component (`post-list.component.ts`)

```ts
import { Component } from "@angular/core";
import { RouterModule } from "@angular/router";
import { NgIf, NgFor } from "@angular/common";
import { PostsService } from "../services/posts.service";

@Component({
  selector: "post-list",
  standalone: true,
  template: `
    <h2>Posts</h2>
    <a routerLink="/add">➕ Add New</a>
    <div *ngIf="svc.postsResource.state === 'loading'">Loading...</div>
    <ul *ngIf="svc.postsResource.state === 'success'">
      <li *ngFor="let post of svc.postsResource.data()">
        <b>{{ post.title }}</b> - <a [routerLink]="['/edit', post.id]">Edit</a>
      </li>
    </ul>
  `,
  imports: [NgIf, NgFor, RouterModule],
})
export class PostListComponent {
  constructor(public svc: PostsService) {}
}
```

---

## ✅ 5. Post Form Component (`post-form.component.ts`)

```ts
import { Component, OnInit } from "@angular/core";
import { ActivatedRoute, Router, RouterModule } from "@angular/router";
import { FormGroup, FormControl, Validators, ReactiveFormsModule } from "@angular/forms";
import { PostsService } from "../services/posts.service";
import { NgIf } from "@angular/common";

@Component({
  selector: "post-form",
  standalone: true,
  templateUrl: "./post-form.component.html",
  styleUrls: ["./post-form.component.css"],
  imports: [ReactiveFormsModule, RouterModule, NgIf],
})
export class PostFormComponent implements OnInit {
  form = new FormGroup({
    id: new FormControl<number | null>(null),
    title: new FormControl("", Validators.required),
    body: new FormControl("", Validators.required),
  });

  editing = false;

  constructor(private route: ActivatedRoute, private router: Router, private svc: PostsService) {}

  async ngOnInit() {
    const id = this.route.snapshot.paramMap.get("id");
    if (id) {
      this.editing = true;
      const post = await this.svc.getPostById(+id);
      this.form.patchValue(post);
    }
  }

  async submit() {
    if (this.form.invalid) return;

    const post = this.form.value;
    if (this.editing && post.id != null) {
      await this.svc.updatePost(post as any);
    } else {
      await this.svc.addPost(post);
    }

    this.router.navigateByUrl("/");
  }
}
```

---

### ✅ `post-form.component.html`

```html
<h2>{{ editing ? 'Edit Post' : 'Add New Post' }}</h2>

<form [formGroup]="form" (ngSubmit)="submit()">
  <label>
    Title:
    <input formControlName="title" />
  </label>
  <br />
  <label>
    Body:
    <textarea formControlName="body"></textarea>
  </label>
  <br />
  <button type="submit">{{ editing ? 'Update' : 'Create' }}</button>
</form>

<a routerLink="/">⬅ Back to List</a>
```

---

## ✅ 6. Root App Component (`app.component.ts`)

```ts
import { Component } from "@angular/core";
import { RouterOutlet } from "@angular/router";

@Component({
  selector: "app-root",
  standalone: true,
  template: `<router-outlet />`,
  imports: [RouterOutlet],
})
export class AppComponent {}
```

---

## 🧪 Live Navigation Behavior

- `/` → shows post list with edit links
- `/add` → new post form
- `/edit/:id` → loads post and lets you update

All **forms and routes are fully signal-reactive**, no RxJS, no `NgModule`, no `@Input()`.

---

## ✅ Summary

| Feature         | Implemented With                                    |
| --------------- | --------------------------------------------------- |
| Routing         | Standalone `Routes` + `RouterOutlet`                |
| State Sharing   | `signal()` inside Service                           |
| API Interaction | `resource()` for GET, `fetch()` for POST/PUT/DELETE |
| Form Logic      | `ReactiveFormsModule` in standalone                 |
| Navigation      | `routerLink`, `router.navigateByUrl()`              |

---

## ✅ Section 12: Angular Signals Store Pattern — Global Reactive State with `signal()`, `computed()`, and `effect()`

### 📘 What Is a Signal Store?

A **Signal Store** is a lightweight and modern approach to global state management in Angular 20 using the built-in reactivity primitives:

| Tool         | Role                                              |
| ------------ | ------------------------------------------------- |
| `signal()`   | Writable reactive variable (acts like `useState`) |
| `computed()` | Auto-calculated, derived reactive value           |
| `effect()`   | Runs a side-effect when dependencies change       |

You can **replace libraries like NgRx or Akita** for many apps with just Signals!

---

## 🧠 Why Use a Signal Store?

- ✅ Manage global state (auth, theme, cart, etc.)
- ✅ Fully reactive and lazy
- ✅ No external packages
- ✅ No selectors, reducers, boilerplate

---

## ✅ Example Scenario: Auth Store (User Login State)

We’ll build a shared `AuthStoreService`:

- `user = signal<User | null>`
- `isLoggedIn = computed(() => !!user())`
- `effect(() => console.log('User changed:', user()))`

---

## ✅ Step-by-Step Implementation

---

### 🎯 Step 1: Create `auth-store.service.ts`

```bash
ng g service services/auth-store
```

---

### ✅ `auth-store.service.ts`

```ts
import { Injectable, signal, computed, effect } from "@angular/core";

export interface User {
  id: number;
  name: string;
  email: string;
}

@Injectable({ providedIn: "root" })
export class AuthStoreService {
  // 🟢 1. Base reactive signal
  private _user = signal<User | null>(null);

  // ✅ 2. Public getter
  user = this._user.asReadonly();

  // 🧠 3. Derived signal
  isLoggedIn = computed(() => !!this._user());

  // 🔁 4. Reactive side effect
  constructor() {
    effect(() => {
      console.log("🔔 Auth changed:", this._user());
    });
  }

  // 🆕 Login (simulate)
  login(fakeUser: User) {
    this._user.set(fakeUser);
  }

  // 🚪 Logout
  logout() {
    this._user.set(null);
  }
}
```

---

## ✅ Step 2: Use Store in Any Component

---

### 🎯 `auth-panel.component.ts`

```ts
import { Component } from "@angular/core";
import { NgIf } from "@angular/common";
import { AuthStoreService } from "../services/auth-store.service";

@Component({
  selector: "app-auth-panel",
  standalone: true,
  imports: [NgIf],
  template: `
    <h3>Auth Panel</h3>
    <div *ngIf="auth.isLoggedIn(); else loginBlock">
      ✅ Logged in as: {{ auth.user()?.name }}
      <button (click)="auth.logout()">Logout</button>
    </div>

    <ng-template #loginBlock>
      <button (click)="login()">Login</button>
    </ng-template>
  `,
})
export class AuthPanelComponent {
  constructor(public auth: AuthStoreService) {}

  login() {
    this.auth.login({ id: 1, name: "Hassan", email: "hassan@example.com" });
  }
}
```

---

## ✅ Explanation of What’s Happening

| Feature         | Code                                 | Purpose                         |                          |
| --------------- | ------------------------------------ | ------------------------------- | ------------------------ |
| Writable Signal | \`signal\<User                       | null>(null)\`                   | Holds current user state |
| Computed Signal | `computed(() => !!_user())`          | Derives isLoggedIn boolean      |                          |
| Effect          | `effect(() => console.log(_user()))` | Reacts to any user login/logout |                          |
| Readonly        | `.asReadonly()`                      | Exposes safe user signal        |                          |

---

## 🧠 Tips for Scaling a Signal Store

You can create larger stores for:

- 🛒 Cart items → `items = signal<Product[]>`
- 🧾 Totals → `computed(() => totalPrice())`
- 📦 Product filters → `filter = signal<string>()`
- 🎨 Theme → `theme = signal<'dark' | 'light'>`

✅ All of these can update UIs automatically without manual subscriptions.

---

## ✅ Bonus: Sharing Signal Store Across Lazy-Loaded Routes

Signal stores in Angular 20 are globally available by default (via `providedIn: 'root'`), so lazy-loaded routes **automatically** get the same instance!

No state duplication.

---

## ✅ Section 13: Angular 20 — Real Global Cart with Signals, Routing, and Computed Totals

## 🛍️ App Goal

We’ll simulate an eCommerce cart app with:

- 🟢 `/products`: product list with “Add to Cart”
- 🛒 `/cart`: view cart, remove items, see total
- 📦 Shared state between both views using `CartStoreService`

---

## ✅ Step-by-Step Breakdown

---

### ✅ 1. Define Product Interface

```ts
export interface Product {
  id: number;
  name: string;
  price: number;
}
```

---

### ✅ 2. Create `cart-store.service.ts`

```bash
ng g service services/cart-store
```

---

### ✅ `cart-store.service.ts`

```ts
import { Injectable, signal, computed } from "@angular/core";
import { Product } from "../models/product.model";

export interface CartItem extends Product {
  quantity: number;
}

@Injectable({ providedIn: "root" })
export class CartStoreService {
  private _items = signal<CartItem[]>([]);

  items = this._items.asReadonly();

  totalQuantity = computed(() => this._items().reduce((sum, item) => sum + item.quantity, 0));

  totalPrice = computed(() => this._items().reduce((sum, item) => sum + item.price * item.quantity, 0));

  addToCart(product: Product) {
    const existing = this._items().find((item) => item.id === product.id);
    if (existing) {
      this._items.update((items) => items.map((item) => (item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item)));
    } else {
      this._items.update((items) => [...items, { ...product, quantity: 1 }]);
    }
  }

  removeFromCart(productId: number) {
    this._items.update((items) => items.filter((i) => i.id !== productId));
  }

  clearCart() {
    this._items.set([]);
  }
}
```

---

## ✅ 3. Create Product List View (`product-list.component.ts`)

```bash
ng g c components/product-list --standalone
```

---

### ✅ `product-list.component.ts`

```ts
import { Component } from '@angular/core';
import { CartStoreService } from '../services/cart-store.service';
import { RouterModule } from '@angular/router';

@Component({
  selector: 'product-list',
  standalone: true,
  template: `
    <h2>🛍️ Product List</h2>
    <ul>
      <li *ngFor="let p of products">
        {{ p.name }} - ${{ p.price }}
        <button (click)="add(p)">Add to Cart</button>
      </li>
    </ul>
    <a routerLink="/cart">Go to Cart ({{ cart.totalQuantity() }})</a>
  `,
  imports: [RouterModule],
})
export class ProductListComponent {
  products = [
    { id: 1, name: 'Laptop', price: 1000 },
    { id: 2, name: 'Mouse', price: 50 },
    { id: 3, name: 'Keyboard', price: 70 }
  ];

  constructor(public cart: CartStoreService) {}

  add(product: any) {
    this.cart.addToCart(product);
  }
}
```

---

## ✅ 4. Create Cart View (`cart.component.ts`)

```bash
ng g c components/cart --standalone
```

---

### ✅ `cart.component.ts`

```ts
import { Component } from '@angular/core';
import { CartStoreService } from '../services/cart-store.service';
import { NgFor, NgIf } from '@angular/common';
import { RouterModule } from '@angular/router';

@Component({
  selector: 'cart',
  standalone: true,
  imports: [NgFor, NgIf, RouterModule],
  template: `
    <h2>🛒 Your Cart</h2>

    <div *ngIf="cart.items().length === 0">
      Cart is empty.
      <br /><a routerLink="/">Back to Products</a>
    </div>

    <ul *ngIf="cart.items().length > 0">
      <li *ngFor="let item of cart.items()">
        {{ item.name }} ({{ item.quantity }}) - ${{ item.price }} each
        <button (click)="cart.removeFromCart(item.id)">Remove</button>
      </li>
    </ul>

    <p *ngIf="cart.items().length > 0">
      🧾 Total: ${{ cart.totalPrice() }}
    </p>

    <button *ngIf="cart.items().length > 0" (click)="cart.clearCart()">Clear Cart</button>
  `
})
export class CartComponent {
  constructor(public cart: CartStoreService) {}
}
```

---

## ✅ 5. Configure Routes (`app.routes.ts`)

```ts
import { Routes } from "@angular/router";
import { ProductListComponent } from "./components/product-list.component";
import { CartComponent } from "./components/cart.component";

export const routes: Routes = [
  { path: "", component: ProductListComponent },
  { path: "cart", component: CartComponent },
];
```

---

## ✅ 6. App Bootstrap (`main.ts` + `app.component.ts`)

### ✅ `main.ts`

```ts
import { bootstrapApplication } from "@angular/platform-browser";
import { AppComponent } from "./app/app.component";
import { provideRouter } from "@angular/router";
import { routes } from "./app/app.routes";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});
```

### ✅ `app.component.ts`

```ts
import { Component } from "@angular/core";
import { RouterOutlet } from "@angular/router";

@Component({
  selector: "app-root",
  standalone: true,
  template: `<router-outlet />`,
  imports: [RouterOutlet],
})
export class AppComponent {}
```

---

## ✅ Feature Summary

| Feature             | Signal-Based Implementation             |
| ------------------- | --------------------------------------- |
| Global State        | `signal<CartItem[]>` in service         |
| Derived Totals      | `computed()` for price and quantity     |
| Add/Remove Items    | `update()` with immutable logic         |
| Share Across Routes | `providedIn: 'root'` gives global scope |

---

## 🎯 This Mimics:

- Real app shopping cart logic
- Lightweight state management
- Navigation + inter-component reactivity

All using **Angular 20 Signals Only** — no `NgRx`, `RxJS`, or `NgModule`.

---

## ✅ Section 14: Angular 20 – Add `localStorage` to Signals (Cart Persistence)

### 📘 Objective

We’ll connect `signal()` to `localStorage` so that:

- 🟢 Cart contents are saved across page reloads
- 🔄 Cart rehydrates when the app loads
- 🔔 All changes to the signal automatically update localStorage

✅ No external library
✅ Pure Angular 20 + Web APIs
✅ Works in any component using the same signal

---

## ✅ Why Persist Signal State?

By default, signals store data in memory. But when the user reloads the page, it’s lost.
To persist it:

- Save to `localStorage` on every change
- Rehydrate from `localStorage` on app start

---

## ✅ Step-by-Step: Persistent Cart with `signal()` + `localStorage`

---

### ✅ 1. Extend `CartStoreService`

We'll now revise `cart-store.service.ts`.

---

### ✅ Full Updated `cart-store.service.ts` with Persistence

```ts
import { Injectable, signal, computed, effect } from "@angular/core";
import { Product } from "../models/product.model";

export interface CartItem extends Product {
  quantity: number;
}

const STORAGE_KEY = "cart-items";

@Injectable({ providedIn: "root" })
export class CartStoreService {
  // 🟢 1. Rehydrate from localStorage (if available)
  private loadInitial(): CartItem[] {
    const raw = localStorage.getItem(STORAGE_KEY);
    try {
      return raw ? JSON.parse(raw) : [];
    } catch {
      return [];
    }
  }

  // 🧠 2. Reactive signal with initial data
  private _items = signal<CartItem[]>(this.loadInitial());

  // ✅ 3. Public readonly access
  items = this._items.asReadonly();

  // 🧮 4. Derived signals
  totalQuantity = computed(() => this._items().reduce((sum, item) => sum + item.quantity, 0));

  totalPrice = computed(() => this._items().reduce((sum, item) => sum + item.price * item.quantity, 0));

  // 🧩 5. Auto-sync with localStorage
  constructor() {
    effect(() => {
      const json = JSON.stringify(this._items());
      localStorage.setItem(STORAGE_KEY, json);
    });
  }

  // 🟢 6. Add to cart
  addToCart(product: Product) {
    const existing = this._items().find((i) => i.id === product.id);
    if (existing) {
      this._items.update((items) => items.map((i) => (i.id === product.id ? { ...i, quantity: i.quantity + 1 } : i)));
    } else {
      this._items.update((items) => [...items, { ...product, quantity: 1 }]);
    }
  }

  // 🗑️ 7. Remove item
  removeFromCart(id: number) {
    this._items.update((items) => items.filter((i) => i.id !== id));
  }

  // 🔄 8. Clear all
  clearCart() {
    this._items.set([]);
  }
}
```

---

## ✅ Explanation

| Line/Block                      | Role                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| `loadInitial()`                 | Reads and parses JSON from `localStorage`                    |
| `signal<CartItem[]>(initial)`   | Creates signal with persisted data                           |
| `effect(() => { ... })`         | Runs on every signal change and saves JSON to `localStorage` |
| `JSON.stringify(this._items())` | Converts cart to string before saving                        |
| `localStorage.setItem()`        | Writes string to browser's localStorage                      |

---

## ✅ Persistence Lifecycle

1. 🧠 On app start: `CartStoreService` loads existing cart
2. 🌀 Whenever you call `addToCart()`, `removeFromCart()`...
3. 🔁 Signal changes → triggers `effect()`
4. 💾 Cart saved in `localStorage`
5. 🔁 After reload, cart is restored automatically

---

## ✅ Final Result

| Action          | Effect                                     |
| --------------- | ------------------------------------------ |
| Add item        | Cart updates + auto-saved                  |
| Remove item     | Cart updates + auto-saved                  |
| Refresh browser | Cart reloaded from `localStorage`          |
| Clear cart      | Signal reset + cleared from `localStorage` |

---

## ✅ Section 15: Angular 20 – PWA Features (Installable, Offline, Manifest, Splash)

## 🧠 What is a PWA?

A **Progressive Web App** is a web application enhanced with features traditionally reserved for native apps:

| Feature         | Description                            |
| --------------- | -------------------------------------- |
| Installable     | Add to Home Screen / Desktop           |
| Offline Support | Caching with Service Workers           |
| Fast Loading    | Cache-first strategy                   |
| Manifest File   | Controls app icon, splash, theme, etc. |
| Mobile First    | Looks like a native app when launched  |

---

## ✅ Step-by-Step: Convert Angular App to a PWA

---

### 🎯 Step 1: Install Angular PWA Support

```bash
ng add @angular/pwa
```

This will automatically:

- Add a **Service Worker** configuration (`ngsw-config.json`)
- Add `manifest.webmanifest`
- Register Angular’s built-in PWA engine

---

### 🎯 Step 2: Verify PWA Files Created

#### 📁 Files added:

```plaintext
src/
  manifest.webmanifest        ✅ PWA metadata
  ngsw-config.json            ✅ Caching rules
  assets/icons/*              ✅ Icons for all screen sizes
```

#### ✅ `angular.json` is updated with:

```json
"serviceWorker": true
```

In the production build config.

---

### 🎯 Step 3: Add Basic Info to `manifest.webmanifest`

```json
{
  "name": "AngularCartApp",
  "short_name": "Cart",
  "theme_color": "#1976d2",
  "background_color": "#fafafa",
  "display": "standalone",
  "orientation": "portrait",
  "start_url": "/",
  "scope": "/",
  "icons": [
    {
      "src": "assets/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "assets/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

---

### 🎯 Step 4: Edit Splash + Theme in `index.html`

```html
<!-- index.html -->
<meta name="theme-color" content="#1976d2" />
<link rel="manifest" href="manifest.webmanifest" />
```

To control splash background, set:

```html
<meta name="apple-mobile-web-app-capable" content="yes" /> <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```

---

### 🎯 Step 5: Configure Service Worker Caching (`ngsw-config.json`)

Default `ngsw-config.json`:

```json
{
  "index": "/index.html",
  "assetGroups": [
    {
      "name": "app",
      "installMode": "prefetch",
      "resources": {
        "files": ["/favicon.ico", "/index.html", "/*.css", "/*.js"]
      }
    },
    {
      "name": "assets",
      "installMode": "lazy",
      "updateMode": "prefetch",
      "resources": {
        "files": ["/assets/**", "/*.(png|jpg|svg|webp)"]
      }
    }
  ]
}
```

> ✅ This means:

- HTML/CSS/JS files are cached **immediately**
- Assets (images, fonts) are lazy-loaded and cached on first load

---

### 🎯 Step 6: Build the App for Production

```bash
ng build --configuration production
```

> ✅ This generates a `dist/` folder with:

- Service worker enabled
- Manifest linked
- All assets fingerprinted and cache-managed

---

### 🎯 Step 7: Serve the App Locally with Service Worker

Angular's dev server doesn’t support SW.
To test the PWA offline:

#### ✅ Option 1: Use `http-server` locally

```bash
npm install -g http-server
http-server dist/your-project-name
```

Then visit:
👉 `http://localhost:8080`

---

#### ✅ Option 2: Deploy to Firebase or GitHub Pages

Firebase and GitHub support PWAs natively — you can follow this in the next section for hosting.

---

## ✅ Test in Browser

1. Open Chrome DevTools → Application tab
2. Check **Manifest** tab → shows app icon, name
3. Install the PWA using the **“Install” button in address bar**
4. Turn off network → refresh → app still works offline if cached

---

## ✅ Optional: Add Install Prompt (Custom Button)

```ts
@HostListener('window:beforeinstallprompt', ['$event'])
onBeforeInstallPrompt(e: any) {
  this.deferredPrompt = e;
  e.preventDefault();
}

promptInstall() {
  if (this.deferredPrompt) {
    this.deferredPrompt.prompt();
    this.deferredPrompt.userChoice.then(() => {
      this.deferredPrompt = null;
    });
  }
}
```

> 🔔 You can show your own “Install App” button using this.

---

## ✅ Section 16: Angular 20 — Deploy PWA to Firebase Hosting or GitHub Pages (Step-by-Step)

---

We’ll cover **both options**, starting with Firebase Hosting (more powerful), then GitHub Pages (great for demos).

---

## ✅ Option 1: Deploy Angular 20 PWA to Firebase Hosting

---

### 📦 Step 1: Install Firebase CLI

```bash
npm install -g firebase-tools
```

> ✅ This gives you access to the `firebase` command

---

### 🔐 Step 2: Login to Firebase

```bash
firebase login
```

- Opens browser to login with Google
- Links your Firebase CLI to your account

---

### 🏗️ Step 3: Initialize Firebase Hosting

In the **root of your Angular project**, run:

```bash
firebase init hosting
```

✅ Choose:

- **"Use an existing project"** (or create one)
- **"dist/your-app-name"** as the public directory
- **Configure as a single-page app** → ✅ Yes
- Do not overwrite `index.html` → ❌ No

> If your app folder is named `my-cart-app`, use:

```
? What do you want to use as your public directory?
> dist/my-cart-app
```

---

### ⚙️ Step 4: Build Angular for Production

```bash
ng build --configuration production
```

> ✅ Output goes into `dist/your-app-name`

---

### 🚀 Step 5: Deploy to Firebase

```bash
firebase deploy
```

📢 You’ll see:

```
✔ Deploy complete!

Project Console: https://console.firebase.google.com/project/your-project-id
Hosting URL: https://your-project-id.web.app
```

> ✅ Your PWA is now live with offline support, install prompt, and fast caching.

---

## ✅ Option 2: Deploy Angular 20 PWA to GitHub Pages

---

### 🎯 Step 1: Install Angular GitHub Deploy Tool

```bash
ng add angular-cli-ghpages
```

---

### 🛠️ Step 2: Build the App

```bash
ng build --configuration production --base-href "https://<username>.github.io/<repo-name>/"
```

> Replace `<username>` and `<repo-name>` with your actual GitHub info.

---

### 🚀 Step 3: Deploy to GitHub Pages

```bash
npx angular-cli-ghpages --dir=dist/<your-project-name>
```

📢 Output:

```
✔ Successfully published via angular-cli-ghpages!
🌐 https://your-username.github.io/your-repo/
```

---

### 🧠 GitHub Pages Tips

| Requirement              | Solution                                         |
| ------------------------ | ------------------------------------------------ |
| Only `index.html` route  | Use Angular 404 fallback: `index.html` as base   |
| PWA works?               | ✅ Yes, full service worker & manifest supported |
| Repo name = project name | Must match unless using custom domain            |

---

## ✅ Section 17: Angular 20 SEO, Meta Tags, Title Management for PWA / SPA

---

## 🧠 Why Is SEO Hard in SPAs?

Single Page Applications (SPAs) load a minimal `index.html`, and update the page dynamically with JavaScript — so:

- 🕷️ **Search engines** might not see full content (unless SSR or prerendering is used)
- 🧠 **Meta tags and titles** are static unless updated programmatically

---

## ✅ Angular SEO Tools (for SPAs)

Angular provides built-in tools to solve this:

| Feature                      | Angular Service / Tool                   |
| ---------------------------- | ---------------------------------------- |
| Set `<title>`                | `Title` from `@angular/platform-browser` |
| Set `<meta>` tags            | `Meta` from `@angular/platform-browser`  |
| Set `<link rel="canonical">` | `Meta.addTag()`                          |
| Support for SSR              | ✅ Optional (via Angular Universal)      |

---

## ✅ Step-by-Step: Dynamic Meta Tags + Page Titles in Angular 20

---

### 🎯 Step 1: Inject `Title` and `Meta` in Your Component

```ts
import { Component } from "@angular/core";
import { Title, Meta } from "@angular/platform-browser";

@Component({
  selector: "app-about",
  standalone: true,
  template: `<h2>About Page</h2>`,
})
export class AboutComponent {
  constructor(private title: Title, private meta: Meta) {
    this.title.setTitle("About Us | Angular PWA");
    this.meta.addTags([
      { name: "description", content: "Learn more about our Angular PWA app." },
      { name: "keywords", content: "Angular, PWA, SEO, Meta Tags" },
      { name: "robots", content: "index, follow" },
    ]);
  }
}
```

---

### ✅ What This Does:

| Tag Generated                           | Description                        |
| --------------------------------------- | ---------------------------------- |
| `<title>`                               | Sets browser tab + search preview  |
| `<meta name="description">`             | Appears in search results/snippets |
| `<meta name="keywords">` (optional now) | Old SEO (mostly ignored now)       |
| `<meta name="robots">`                  | Tells crawlers to index the page   |

---

### 🧠 Optional: Canonical Link (for duplicate content prevention)

```ts
this.meta.addTag(
  {
    rel: "canonical",
    href: "https://yourdomain.com/about",
  },
  true
);
```

You can also inject it manually in `index.html`.

---

### 🧠 Optional: Update Meta Dynamically (e.g. Blog Post Details)

```ts
ngOnInit() {
  const post = { title: 'Angular 20 Tips', desc: 'Best practices for Angular 20' };
  this.title.setTitle(post.title);
  this.meta.updateTag({ name: 'description', content: post.desc });
}
```

---

### 🎯 Step 2: Set Default Global Tags in `index.html`

```html
<head>
  <title>Angular PWA</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="theme-color" content="#1976d2" />
  <meta name="author" content="Hassan El-Dash" />
  <meta name="description" content="Modern Angular 20 PWA with signals and offline support." />
  <meta property="og:title" content="Angular 20 PWA" />
  <meta property="og:image" content="assets/icons/icon-512x512.png" />
  <meta property="og:description" content="Installable Angular app with modern features." />
  <link rel="manifest" href="manifest.webmanifest" />
</head>
```

> 🔁 These serve as fallbacks before route-specific tags are injected.

---

## ✅ Bonus: Social Media Preview Tags

Use **Open Graph (Facebook, LinkedIn)** and **Twitter Cards**:

```html
<!-- Open Graph -->
<meta property="og:title" content="Angular Cart App" />
<meta property="og:description" content="Offline-ready Angular 20 shopping cart." />
<meta property="og:image" content="assets/icons/icon-512x512.png" />
<meta property="og:url" content="https://yourdomain.com/" />

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Angular Cart App" />
<meta name="twitter:description" content="Built with Angular 20 Signals and PWA." />
<meta name="twitter:image" content="assets/icons/icon-512x512.png" />
```

---

## 🧠 Optional: SSR or Pre-rendering for Full SEO

To make search engines **see actual content**, consider:

| Method              | Description                          |
| ------------------- | ------------------------------------ |
| Angular Universal   | Server-side rendering for each route |
| Scully (deprecated) | Static site generator for Angular    |
| Prerendering (CLI)  | Angular built-in SSG via CLI in v16+ |

We’ll cover SSR/prerendering later if needed.

---

## ✅ Summary

| Goal                    | Tool Used                            |
| ----------------------- | ------------------------------------ |
| Set dynamic title       | `Title.setTitle()`                   |
| Set/change meta tags    | `Meta.addTags()`, `Meta.updateTag()` |
| Social media preview    | Open Graph + Twitter meta tags       |
| Default app description | `index.html` meta fallback           |
| Route-specific metadata | Each component’s constructor/init    |

---

## ✅ Section 18: Angular 20 – Animations, Scroll Behavior, and Accessibility

## 🧩 Part 1: Angular Animations

### 📘 What Are Angular Animations?

Angular animations use the `@angular/animations` module with a **declarative API** to control:

- Transitions (enter/leave, expand/shrink)
- Element state (open/close, show/hide)
- Fine-grained timing, easing, and coordination

---

### ✅ Step-by-Step: Basic Fade Animation on Route Change

---

### 🎯 Step 1: Install & Enable Animations

Already included if you used Angular CLI.

In `main.ts`, enable animations:

```ts
import { provideAnimations } from "@angular/platform-browser/animations";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes), provideAnimations()],
});
```

> ✅ Use `provideNoopAnimations()` for testing/staging with no animation.

---

### 🎯 Step 2: Add Animation to Component

```ts
import { Component } from "@angular/core";
import { trigger, transition, style, animate } from "@angular/animations";

@Component({
  selector: "animated-box",
  standalone: true,
  template: `
    <div *ngIf="visible" @fadeInOut class="box">I fade in and out!</div>
    <button (click)="toggle()">Toggle</button>
  `,
  styles: [
    `
      .box {
        width: 300px;
        padding: 1rem;
        background: #1976d2;
        color: white;
        margin-top: 1rem;
      }
    `,
  ],
  animations: [trigger("fadeInOut", [transition(":enter", [style({ opacity: 0 }), animate("400ms ease-in", style({ opacity: 1 }))]), transition(":leave", [animate("400ms ease-out", style({ opacity: 0 }))])])],
})
export class AnimatedBoxComponent {
  visible = true;
  toggle() {
    this.visible = !this.visible;
  }
}
```

✅ Works with `*ngIf` and `ngFor`.

---

### ✅ Animation Triggers You Can Use

| Trigger Phase | Meaning                  |
| ------------- | ------------------------ |
| `:enter`      | Element inserted in DOM  |
| `:leave`      | Element removed from DOM |
| `* => *`      | Any state transition     |
| `void => *`   | Initial render           |

---

## 🧩 Part 2: Scroll Behavior on Route Change

---

### 🎯 Enable Scroll Position Restoration in Routes

In `main.ts`:

```ts
import { provideRouter, withViewTransition, withComponentInputBinding, withEnabledBlockingInitialNavigation, withNavigationErrorHandler, withRouterConfig } from "@angular/router";

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(
      routes,
      withRouterConfig({
        scrollPositionRestoration: "enabled", // ✅ automatic scroll to top
        anchorScrolling: "enabled", // ✅ support #hash links
      })
    ),
    provideAnimations(),
  ],
});
```

> ✅ This automatically:

- Scrolls to top on route change
- Scrolls to anchor (`#section2`) if present

---

## 🧩 Part 3: Accessibility (ARIA Roles + Keyboard Nav)

---

### 🎯 Best Practices in Angular

#### ✅ Use ARIA Roles

```html
<nav role="navigation" aria-label="Main Menu">
  <a routerLink="/">Home</a>
  <a routerLink="/cart">Cart</a>
</nav>
```

---

#### ✅ Use `<button>` Not `<div (click)>`

```html
<!-- ✅ Good: Accessible with keyboard -->
<button (click)="doSomething()">OK</button>

<!-- ❌ Avoid -->
<div (click)="doSomething()">Click</div>
```

---

#### ✅ Manage Focus Programmatically (optional)

```ts
@ViewChild('inputBox') inputBox!: ElementRef;

ngAfterViewInit() {
  this.inputBox.nativeElement.focus();
}
```

```html
<input #inputBox />
```

---

#### ✅ Avoid Hard-to-Read Color Combinations

Use sufficient contrast:

- ✅ White on dark blue
- ❌ Light gray on white

---

#### ✅ Use `aria-live` for dynamic alerts

```html
<p aria-live="polite">Cart total: {{ total }}</p>
```

This notifies screen readers of changes.

---

## ✅ Summary Table

| Feature                     | Angular API / HTML                        |
| --------------------------- | ----------------------------------------- |
| Fade animations             | `@angular/animations` trigger             |
| Scroll to top on navigation | `scrollPositionRestoration: 'enabled'`    |
| ARIA roles                  | `role="navigation"`, `aria-label`         |
| Keyboard nav                | Use native buttons, `tabindex`, `focus()` |
| Live updates                | `aria-live="polite"`                      |

---

## ✅ Section 19: Angular 20 Form Validation Best Practices (Reactive + Template + Signal Sync)

## 🧩 Part 1: Template-Driven Form Validation (with `FormsModule`)

---

### 📘 When to Use

✅ Good for small/simple forms
✅ Minimal TypeScript logic
❌ Not suited for dynamic rules or deeply nested forms

---

### ✅ Step-by-Step

#### 🎯 Import `FormsModule` in Component

```ts
import { FormsModule } from '@angular/forms';

@Component({
  standalone: true,
  imports: [FormsModule],
  ...
})
```

---

### ✅ Template Example

```html
<form #userForm="ngForm" (ngSubmit)="submit()" novalidate>
  <label>
    Name:
    <input name="name" [(ngModel)]="name" required minlength="3" #nameField="ngModel" />
  </label>
  <div *ngIf="nameField.invalid && nameField.touched">
    <small *ngIf="nameField.errors?.['required']">Name is required.</small>
    <small *ngIf="nameField.errors?.['minlength']">Minimum 3 characters.</small>
  </div>

  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```

---

### ✅ Key Best Practices

| Pattern                     | Why?                            |
| --------------------------- | ------------------------------- |
| `novalidate` on `<form>`    | Prevents browser default styles |
| `#nameField="ngModel"`      | Gets `NgModel` validation info  |
| `form.invalid` / `.touched` | Clean validation UX             |
| `disabled` on submit        | Prevents invalid submission     |

---

## 🧩 Part 2: Reactive Form Validation (with `ReactiveFormsModule`)

---

### 📘 When to Use

✅ Complex/dynamic forms
✅ Programmatic control over rules
✅ Best for enterprise apps

---

### ✅ Step-by-Step

#### 🎯 Import `ReactiveFormsModule` in Component

```ts
import { ReactiveFormsModule, FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  standalone: true,
  imports: [ReactiveFormsModule],
  ...
})
```

---

### ✅ Component Setup

```ts
form = new FormGroup({
  email: new FormControl("", [Validators.required, Validators.email]),
  password: new FormControl("", [Validators.required, Validators.minLength(6)]),
});
```

---

### ✅ Template Example

```html
<form [formGroup]="form" (ngSubmit)="submit()" novalidate>
  <label>
    Email:
    <input formControlName="email" />
  </label>
  <div *ngIf="form.get('email')?.invalid && form.get('email')?.touched">
    <small *ngIf="form.get('email')?.errors?.['required']">Email is required.</small>
    <small *ngIf="form.get('email')?.errors?.['email']">Invalid email.</small>
  </div>

  <label>
    Password:
    <input type="password" formControlName="password" />
  </label>
  <div *ngIf="form.get('password')?.invalid && form.get('password')?.touched">
    <small *ngIf="form.get('password')?.errors?.['required']">Password is required.</small>
    <small *ngIf="form.get('password')?.errors?.['minlength']">Min 6 characters.</small>
  </div>

  <button type="submit" [disabled]="form.invalid">Login</button>
</form>
```

---

### ✅ Common Validators

| Validator                   | Syntax                     |
| --------------------------- | -------------------------- |
| `Validators.required`       | Requires a non-empty value |
| `Validators.email`          | Valid email address        |
| `Validators.min(n)`         | Minimum numeric value      |
| `Validators.max(n)`         | Maximum numeric value      |
| `Validators.minLength(n)`   | String length check        |
| `Validators.pattern(regex)` | Regex pattern              |

---

## 🧩 Part 3: Angular 20 Signal-Based Form Sync (Advanced Bonus)

---

### ✅ Use `signal()` to reflect form status in UI elsewhere

```ts
form = new FormGroup({
  email: new FormControl('', Validators.required)
});

formStatus = signal<string>('Invalid');

constructor() {
  effect(() => {
    this.formStatus.set(this.form.valid ? 'Valid ✅' : 'Invalid ❌');
  });
}
```

Now use anywhere:

```html
<p>Form status: {{ formStatus() }}</p>
```

> 🔁 Signal tracks form validity reactively with zero RxJS or subscriptions.

---

## ✅ Summary: Best Practices

| Do ✅                                    | Don’t ❌                                 |
| ---------------------------------------- | ---------------------------------------- |
| Use `novalidate` on form tag             | Don’t rely on browser-native tooltips    |
| Show errors only after `touched`/`dirty` | Don’t show all errors on load            |
| Disable submit if `form.invalid`         | Don’t allow submit on incomplete data    |
| Use signals for live UI reflection       | Avoid manual form syncing with side vars |

---

## ✅ Section 20: Angular 20 Form UX Enhancements

📋 Input Masking | 🔎 Autocomplete | ➕ Dynamic Fields | ⌨️ Keyboard UX

---

## 🧩 Part 1: Input Masking (Phone, Dates, etc.)

### 🎯 Why?

✅ Prevents invalid input
✅ Helps users format data as they type
✅ Especially useful for phone numbers, dates, card numbers

---

### ✅ Option 1: Use `ngx-mask` (Most Popular Library)

---

### 🎯 Step 1: Install `ngx-mask`

```bash
npm install ngx-mask --save
```

---

### 🎯 Step 2: Provide the Mask Plugin

In `main.ts`:

```ts
import { provideNgxMask } from "ngx-mask";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes), provideNgxMask()],
});
```

---

### 🎯 Step 3: Use in Template

```html
<input mask="0000-0000-0000-0000" placeholder="Credit Card" />
<input mask="(000) 000-0000" placeholder="Phone Number" />
<input mask="00/00/0000" placeholder="Date (dd/mm/yyyy)" />
```

> ✅ Mask is automatically enforced as the user types.

---

## 🧩 Part 2: Autocomplete for Inputs

### ✅ Native HTML5 Autocomplete

```html
<input name="city" [(ngModel)]="city" list="cityList" placeholder="Enter City" />
<datalist id="cityList">
  <option *ngFor="let c of cities" [value]="c"></option>
</datalist>
```

```ts
cities = ["Cairo", "Alexandria", "Giza", "Luxor"];
```

---

### ✅ Autocomplete for Reactive Forms

You can create a custom dropdown (see Part 4 below) or use Angular Material's `mat-autocomplete` with `ReactiveFormsModule`.

---

## 🧩 Part 3: Dynamic Fields (Add/Remove Form Items)

### ✅ Real Example: Dynamic List of Emails

```ts
form = new FormGroup({
  emails: new FormArray([
    new FormControl('', Validators.email)
  ])
});

get emails(): FormArray {
  return this.form.get('emails') as FormArray;
}

addEmail() {
  this.emails.push(new FormControl('', Validators.email));
}

removeEmail(i: number) {
  this.emails.removeAt(i);
}
```

```html
<form [formGroup]="form">
  <div formArrayName="emails">
    <div *ngFor="let ctrl of emails.controls; let i = index">
      <input [formControlName]="i" placeholder="Email #{{ i + 1 }}" />
      <button (click)="removeEmail(i)" type="button">Remove</button>
    </div>
  </div>
  <button (click)="addEmail()" type="button">Add Another Email</button>
</form>
```

✅ Great for surveys, order items, multiple phones, etc.

---

## 🧩 Part 4: Keyboard UX Best Practices

### ✅ Trap Focus for Modals

Use `tabindex="0"` on focusable divs or implement a focus trap to prevent tabbing outside of modals.

```html
<div tabindex="0">Focusable area</div>
```

---

### ✅ Keyboard Shortcuts (Optional)

```ts
@HostListener('document:keydown.control.s', ['$event'])
saveShortcut(e: KeyboardEvent) {
  e.preventDefault();
  this.submit();
}
```

✅ Add `Ctrl+S` save, or `Esc` cancel.

---

### ✅ Auto Focus First Field

```ts
@ViewChild('firstInput') input!: ElementRef;

ngAfterViewInit() {
  this.input.nativeElement.focus();
}
```

```html
<input #firstInput />
```

---

## ✅ UX Enhancement Summary

| Feature            | Tool / API                   | Description                     |
| ------------------ | ---------------------------- | ------------------------------- |
| Input Masking      | `ngx-mask`                   | Format input as you type        |
| Autocomplete       | Native `datalist` / Material | Suggest input values            |
| Dynamic Fields     | `FormArray`                  | Repeatable form groups          |
| Keyboard Shortcuts | `@HostListener()`            | Enable keyboard-based actions   |
| Autofocus          | `@ViewChild()` + `focus()`   | Jump cursor to important fields |

---

Made with ❤️ by Hassan ELDash
