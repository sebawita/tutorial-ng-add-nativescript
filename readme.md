# Tutorial

This tutorial introduces you to the essentials of a **code-sharing project**, which allows you to build both **web** and **native mobile** apps — for Android and iOS — from a single project.

The **native mobile** part is achieved with the help of NativeScript.

> [NativeScript](https://www.nativescript.org/) is an **open source** framework for building **truly native** mobile apps with **JavaScript**.
>
> Use **web skills** like: **TypeScript**, **Angular** and **CSS** and **get native UI &** **performance** on **iOS** and **Android**.

The objective is to share as much code as possible, and break the platform-specific code into separate files.

This usually means that we can share the code for:

- the **Routes** for the navigation
- the **Services** for the common business logic
- the **Component Class definition** for the common behaviour of each component

While, separating the code for:

- the **UI Layer** (**stylesheets** and **html**) — as you need to use different user interface components in web and NativeScript-built native apps
- the **NgModules** — so that we can import platform-specific modules, without creating conflicts (i.e. Angular Material Design — which is web only) between web and mobile

Here’s a diagram to show you what that looks like at a high level.

<img src="./img/0-project-structure.png?raw=true">

### Learn NativeScript

As part of this tutorial, we will look at NativeScript in the context of a code-sharing project.

However, you can also use NativeScript to build mobile apps without the web.

Check out this [tutorial](https://docs.nativescript.org/angular/start/introduction) on how to build mobile apps with NativeScript.



## Intro

As the basis of this tutorial, you will use a completed version of the Getting Started Tutorial for Angular.

If you don't have your version around, you can clone it from [https://github.com/sebawita/angular-getting-started/](https://github.com/sebawita/angular-getting-started/).

```
git clone https://github.com/sebawita/angular-getting-started.git
```

The idea is to add NativeScript to the Getting Started app, and then step by step convert all web components to also work in NativeScript.



## Setup

### Angular CLI

To take advantage of the automated migration commands for NativeScript Angular you will need to install the **Angular CLI**. Run the following command:

```
npm install --global @angular/cli
```

### NativeScript CLI

To build mobile apps with NativeScript you will need to install the **NativeScript CLI**. Run the following command:

```bash
npm install --global nativescript
```

<!--You can choose two ways of building your apps:-->

<!--a) **Preview** uses two companion apps — **NativeScript Playground** ([Android](https://play.google.com/store/apps/details?id=org.nativescript.play), [iOS](https://apps.apple.com/us/app/nativescript-playground/id1263543946)) and **NativeScript Preview** ( [Android](https://play.google.com/store/apps/details?id=org.nativescript.preview), [iOS](https://apps.apple.com/us/app/nativescript-preview/id1264484702)) — installed on your Android/iOS device. Then when you perform a build, the NativeScript CLI pushes the updates directly to the NativeScript Preview app.--> 

<!--b) **Local builds**: this perform a full Android/iOS build on your computer, which requires you to set up the Android SDK and/or XCode - [here is how](https://docs.nativescript.org/angular/start/quick-setup#full-setup) - and then deploys the app to a simulator or a connected device.-->

You can choose between two ways of building your apps:

### Local Builds

The NativeScript CLI performs a full Android/iOS build on your computer, and then deploys the app to a simulator or a connected device.

This requires you to set up the **Android SDK** and/or **XCode**. Here are the [full setup instructions](https://docs.nativescript.org/angular/start/quick-setup#full-setup).



> If you are not used to configuring the Android SDK and/or Xcode, you might be better off completing the tutorial using the Preview approach (see below).



Local builds are only required when:

- you want to deploy your app to a simulator
- you want to add a native plugin that is not included in the NativeScript Preview App
- you need to publish the app to the Apple AppStore or the Google Play



### Preview

The NativeScript CLI performs only the build of your Angular code while skipping the Android/iOS build, then it deploys your code to **NativeScript Preview** (a companion app hosting your app code).

To use preview, you need to install two companion apps on your Android/iOS device(s):

- **NativeScript Playground** ([Android](https://play.google.com/store/apps/details?id=org.nativescript.play), [iOS](https://apps.apple.com/us/app/nativescript-playground/id1263543946)) — used to scan a QR code provided by the NativeScript CLI
- **NativeScript Preview** ([Android](https://play.google.com/store/apps/details?id=org.nativescript.preview), [iOS](https://apps.apple.com/us/app/nativescript-preview/id1264484702)) — used to host display your app



## Overview of the migration steps



1. Migrate the project to a code-sharing structure
2. Update the {N} AppModule
3. Update the first component
4. Update the rest of the components
5. Etc.



## Add Mobile (OR) Ng Add NativeScript

First you need to convert the project to a code-sharing structure. 

Run the following `ng add` command from the root of your project:

```bash
ng add @nativescript/schematics
```

This command adds the **NativeScript-specific**:

- npm modules
- AppModule definition
- AppComponent definition
- TypeScript configuration

And as a result it allows you to build a NativeScript app from the same project.

However, this does not convert your components to work in a mobile app, as HTML **doesn't map** very well to Native Mobile UI components.

### Code Separation

Before you can start sharing code, you need to know how to separate the web code from the mobile code. This is important, so that you could easily create platform-specific code without creating conflicts.

To do that you can use a simple **naming convention**. By adding a **.tns** before the file extension, you can indicate that this file is NativeScript-specific, while the same file without the **.tns** extension is marked as web-specific. If we have just one file without the **.tns** extension, then this makes it a shared file.

<!--For example, you can notice that in the project there are two files:-->

<!-- - app.module.ts - the Entry Module file for web-->
<!-- - app.module**.tns**.ts - the Entry Module file for mobile-->

#### Component — Code-Sharing Format

The most common scenario is a component code. Usually we would have:

- **name.component.ts** — a shared file for the Component Class definition
- **name.component.html** — a web-specific template
- **name.component.tns.html** — a mobile-specific template
- **name.component.css** — a web-specific stylesheet
- **name.component.tns.css** — a mobile-specific stylesheet

<img src="./img/0-component-splitting.png?raw=true">

## First Run

Now is the best moment to test the new mobile app. This is done with the NativeScript CLI **preview** command.

From the root of the project run the following command:

```bash
tns preview --bundle
```

After a short moment, the CLI will present you with a QR Code. Scan it with the **NativeScript Playground** app, which will connect your project with the **NativeScript Preview** app.

As soon as you scan the QR Code, the CLI will bundle the TypeScript code from your project and push it to the **NativeScript Preview** app.



> If you have the local build configured, then you can perform the build locally with the following commands:
>
> - **Android**: `tns run android --bundle` 
>
> - **iOS**: `tns run ios --bundle` 



Your app should look something like this:

<img src="./img/1-first-run.png?raw=true" height="400">

You may notice that a big button with a text saying *"auto-generated works!"* is not what you had in your web project. Don't worry, this is just a demo component to show you that the mobile app works.

### Livesync

While the `tns preview --bundle` or `tns run [android/ios] --bundle` commands are active, any changes to the project will get automatically picked up by the NativeScript CLI and an update will be pushed to the app.

It is a good time to test it out.

Find the src/app/auto-generated/**auto-generated.component.tns.html** file and change the `text` value to `text="update now 😃"`.

<img src="./img/1-livesync.png?raw=true" height="400">

> This means that you don't need to re-run the build manually, as most of the times this will happen automatically. Just what you would expect from the `ng serve` command.

## Prepare NgModule for {N}

Before you start converting all components to NativeScript, you need to make sure that the NativeScript AppModule (**app.module.tns.ts**) imports all the required modules, which are used by the services in the project.

When you check **cart.service.ts** you will find that it Injects the **HttpClient**:

```typescript
  constructor(
    private http: HttpClient
  ) {}
```

In the web version of the AppModule, **HttpClient** is imported via **HttpClientModule**.

```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    HttpClientModule,
    ...
  ],
```



NativeScript provides a mobile specific implementation of the **HttpClient**, which is provided via **NativeScriptHttpClientModule**. 

Open **app.module.tns.ts** where you will find a commented import for **NativeScriptHttpClientModule** class (*line 13*). Uncomment it, and add **NativeScriptHttpClientModule** to @NgModule **imports**, like this:

```typescript
import { NativeScriptHttpClientModule } from 'nativescript-angular/http-client';

@NgModule({
  ...
  imports: [
    NativeScriptModule,
    AppRoutingModule,
    NativeScriptHttpClientModule
  ],
```



This is enough to make the **CartService** to work for both Web and Mobile, without any change required to the service itself.

Here is a high-level visualisation of how the right implementation of the **HttpClient** is provided to the service at build time.

<img src="./img/2-http-client.png?raw=true">



## Global NativeScript Styles

Next you should update the global stylesheet (**app.css**) for the mobile part of the project, as it will provide you with a common styling classes that you will use across the app.

**app.css**

```css
@import '~nativescript-theme-core/css/core.light.css';

/* .fa {
  font-family: "Font Awesome 5 Free", "fa-solid-900";
} */

ActionBar {
  background-color: #1976d2;
  color: white;
}

.action-bar-item {
  color: white;
  padding-right: 5;
}

.big-btn, .btn-red, .btn-green, .btn-blue, .btn-blue-outline {
  font-weight: bold;
  font-size: 18;
  padding: 10 30;
  border-radius: 25;
  margin: 20 10 0 10;
  width: 90%;
}
.btn-red {
  color: white;
  background-color: #ED4472;
}
.btn-green {
  color: white;
  background-color: #30CE91;
}
.btn-blue {
  color: white;
  background-color: #1976d2;
}
.btn-blue-outline {
  color: #1976d2;
  border-color: #1976d2;
  border-width: 2;
}

.title {
  color: #1976d2;
  font-size: 32;
  text-align: center;
  margin-bottom: 8;
}

.cart-item, .shipping-item {
  padding: 2 4;
  margin: 4;
  border-radius: 16;
  /* border-width: 2; */
  background-color: #EEEEEE;
}

.form {
  margin-top: 20px;
  width: 90%;
}

.form Label {
  color: #5a78e3;
  font-size: 20;
  font-weight: bold;
  margin: 5;
  position: top;
}

.form TextField {
  background-color: white;
  padding-left: 5;
  border-color: #5a78e3;
  border-width: 2;
  border-radius: 5;
}
```



## Migrating components

Next, you need to start converting each component, by providing the UI implementation for each.



Converting a web component to a shared component usually involves:

1.  Adding a `.tns.html` and a `.tns.css` files
2. Adding the component to the {N} AppModule **declarations**
3.  Update navigation configuration to display the component
4.  Providing template and styling code



The steps (1) and (2) can be easily automated with the little help from the Angular CLI and NativeScript Schematics:

```bash
ng generate migrate-component --name=cmp-name
```

or in short:

```bash
ng g mc --name=cpm-name
```



## Migrate Component - Product List

The first component that you should start with is the **Product List** component, as this is the first component that gets loaded when the app starts. Run the following command:

```bash
ng generate migrate-component --name=product-list
```

This will:

- generate **product-list.component.tns.html** with the commented out html from **product-list.component.html**
- generate an empty **product-list.component.tns.css**
- add the **ProductListComponent** to the **Declarations** of **app.module.tns.ts**

Like this:

```
src
└── app
    ├── product-list
    |   ├── product-list.component.html
    |   ├── product-list.component.tns.html <= create
    |   └── product-list.component.ts
    |   └── product-list.component.tns.css  <= create
    |   └── product-list.component.css
    ├── app.module.tns.ts                   <= update
    └── app.module.ts           
```

### Update mobile Router configuration

At this stage the **Router Configuration** for the web and mobile apps are kept separately. This is especially useful during the migration process, as at the beginning most of your components will be web only, so your mobile app won't be able to navigate to the components that have not been converted yet.

The **Product List** component can be added to the NativeScript Routes.

Open **app-routing.module.tns.ts** and replace the **Routes** array with:

```typescript
import { ProductListComponent } from '@src/app/product-list/product-list.component';

export const routes: Routes = [
  { path: '', component: ProductListComponent },
];
```

After you save, your project should update and look something like this:

<img src="./img/3-product-list-migrated.png?raw=true" height="400">

If that is the case, then you are on the right way to move forward.

### Update template

Now, you need to update the {N} UI template, to match the content from the web app.

> This tutorial won't dive too deep into building the UI using NativeScript components. You can check out the documentation to learn more about [UI Widgets](https://docs.nativescript.org/angular/ui/ng-ui-widgets/action-bar) and [NativeScript Layouts](https://docs.nativescript.org/angular/ui/layouts/layouts). There is also an [interactive tutorial for {N} layouts](https://www.nslayouts.com/).



Let's go quickly through the web template and convert it to {N}.

**product-list.component.html**

```html
<h2>Products</h2>

<div *ngFor="let product of products; index as productId">

  <h3>
    <a [title]="product.name + ' details'" [routerLink]="['/products', productId]">
      {{ product.name }}
    </a>
  </h3>
  <p *ngIf="product.description">
    Description: {{ product.description }}
  </p>

  <button (click)="share()">
    Share
  </button>

  <app-product-alerts [product]="product" (notify)="onNotify()">
  </app-product-alerts>
</div>
```



**Step #1**

First, you have:

```html
<h2>Products</h2>
```

This is clearly the title of the page. An `ActionBar` is the best component to serve as a title.

Add the following to **product-list.component.tns.html** at the top.

```html
<ActionBar title="Products">
</ActionBar>
```

Below you have a `StackLayout` container, which is used to hold the contents of the page. Remove the three labels that are inside, like this:

```html
<ActionBar title="Products">
</ActionBar>
<StackLayout>
	<!-- Page content goes here -->
</StackLayout>
```

> Please note that besides the **ActionBar**, a NativeScript template (the same rule also applies to **ng-template**) can only contain one component. This is why you need a Layout component, which contains all the other components.

**Step #2**

Then you have a `div` that is repeated with `*ngFor` for each **product** in the **products** array.

```html
<div *ngFor="let product of products; index as productId">
  ...
</div>
```



Although, you can use `*ngFor` in a mobile app, in most of the cases this is best handled by a `ListView` component, which helps with scrolling through the items and optimises GPU and memory handling for large data sources.

Add a list `ListView` component inside the `StackLayout`, like this:

```html
<StackLayout>
  <!-- Page content goes here -->
  <ListView [items]="products" class="list-group" height="100%">
    <ng-template let-product="item" let-productId="index">

    </ng-template>
  </ListView>
</StackLayout>
```



Note the following:

- `[items]` — is used to provide a **data source**, it can also be used with an `async` pipe, like this:

   ```html
  <ListView [items]="data | async">
  ```

- `let-product="item"` — is used to provide a **name** for each item in the array, in this case the name for each item is **product**,
- `let-productId="index" — is used to provide a name for **index** of the item, in this case the name of the index is **productId**



**Step 3**

Next, you need to reproduce the `div` and all of its contents:

**product-list.component.html**

```html
<div *ngFor="let product of products; index as productId">

  <h3>
    <a [title]="product.name + ' details'" [routerLink]="['/products', productId]">
      {{ product.name }}
    </a>
  </h3>
  <p *ngIf="product.description">
    Description: {{ product.description }}
  </p>

  <button (click)="share()">
    Share
  </button>

  <app-product-alerts [product]="product" (notify)="onNotify()">
  </app-product-alerts>
</div>
```



You can convert it to the {N} template by replacing:

- the `<div>` container with a `<StackLayout>`

  ```html
  <StackLayout class="list-group-item">
  
  </StackLayout>
  ```

- the `<h3><a>` product name&link with a `<Label>` — where **product.name** is provided with `[text]` and navigation path is provided with `[nsRouterLink]`:

  ```html
  <Label [nsRouterLink]="['/products', productId]"
    [text]="product.name" textWrap="true" class="title">
  </Label>
  ```

- the `p` element again with a `<Label>` where we can preserve the `*ngIf` directive and add a `text` property as follows:

```
<Label *ngIf="product.description"
        text="Description: {{ product.description }}" textWrap="true">
</Label>
```

- the `<button>` with a `<Button>` — where you use the `(tap)` event instead of the `(click)` event (as you don't click on touch screens), and the text of the button is provided with `[text]`:

  ```html
  <Button (tap)="share()" text="Share" class="btn-blue"></Button>
  ```

- the `<app-product-alerts>` component is not mobile ready yet, so just leave it as a comment:

  ```html
  <!--   
    <app-product-alerts [product]="product" (notify)="onNotify()">
    </app-product-alerts>
  -->
  ```



The whole template should look like this:

**product-list.component.tns.html**

```html
<ActionBar title="Products">
</ActionBar>
<StackLayout>
  <ListView [items]="products" class="list-group" height="100%">
    <ng-template let-product="item" let-productId="index">
      <StackLayout class="list-group-item">
        <Label [nsRouterLink]="['/products', productId]"
               [text]="product.name" textWrap="true" class="title">
        </Label>

        <Label *ngIf="product.description"
               text="Description: {{ product.description }}" textWrap="true">
        </Label>

        <Button (tap)="share()" text="Share" class="btn-blue"></Button>
        
        <!--   
          <app-product-alerts [product]="product" (notify)="onNotify()">
          </app-product-alerts>
        -->
      </StackLayout>
    </ng-template>
  </ListView>
</StackLayout>
```

After you save, the app should look like this:

<img src="./img/3-product-list-updated.png?raw=true" height="400">



## Migrate Component: Product Alerts

Next, you should tackle the **ProductAlerts** component, which is used as a presentation component in the **ProductList** template.

**Step 1**

First, run the migration schematic:

```bash
ng g mc --name=product-alerts
```



**Step 2**

Next — based on the web template — you need to update the mobile template:

**product-alerts.component.html**

```html
<p *ngIf="product.price > 700">
  <button (click)="notify.emit()">Notify Me</button>
</p>
```

You should update the mobile template like this:

**product-alerts.component.tns.html**

```html
<StackLayout *ngIf="product.price > 700">
  <Button (tap)="notify.emit()" text="Notify Me" class="btn-green"></Button>
</StackLayout>
```



**Step 3**

Open **product-list.component.tns.html** and remove the comments around `<app-product-alerts>`:

```html
<ActionBar title="Products">
</ActionBar>
<StackLayout>
  <ListView [items]="products" class="list-group" height="100%">
    <ng-template let-product="item" let-productId="index">
      <StackLayout class="list-group-item">
        <Label [nsRouterLink]="['/products', productId]"
               [text]="product.name" textWrap="true" class="title">
        </Label>

        <Label *ngIf="product.description"
               text="Description: {{ product.description }}" textWrap="true">
        </Label>

        <Button (tap)="share()" text="Share" class="btn-blue"></Button>
        
        <app-product-alerts [product]="product" (notify)="onNotify()">
        </app-product-alerts>
      </StackLayout>
    </ng-template>
  </ListView>
</StackLayout>
```



After you save all the files, your app should look like this:

<img src="./img/4-product-alerts.png?raw=true" height="400">

## Handling Web/Mobile specific code #1

When you test the **Share** and **Notify Me** buttons in a mobile application, you will get a long error, which will complain that `window.alert()` doesn't exist on the mobile platforms.

There are a few ways of handling this issue:

### Method 1

The `alert()` function is available without `window` for both web and mobile, so the easiest solution (*the recommended solution for this problem*) is to change `window.alert()` to `alert()`.

```typescript
share() {
  alert('The product has been shared!');
}

onNotify() {
  alert('You will be notified when the product goes on sale');
}
```

### Method 2

Create two files:

**utils.ts** — to re-export the window definition

```typescript
export default window;
```

**utils.tns.ts** — to provide a definition of window, containing the alert function

```typescript
export default { alert };
```



Then in the **product-list.component.ts** import `window`, like this:

```typescript
import window from '../utils';
```

This would keep the old implementation of `window` for web, and provide the new definition of `window` for mobile.

## Migrate Component: Product Details

The next component to migrate is the **Product Details** component. This is the component the app navigates to when you click/tap on a name of a phone.

You should be familiar with the routine:

**Step 1**

Run the migration schematic:

```bash
ng g migrate-component --name=product-details
```

**Step 2**

Update the navigation configuration in **app-routing.module.tns.ts**:

```typescript
import { ProductDetailsComponent } from '@src/app/product-details/product-details.component';

export const routes: Routes = [
  { path: '', component: ProductListComponent },
  { path: 'products/:productId', component: ProductDetailsComponent },
];
```

**Step 3**

Translate HTML to NativeScript template.

**product-details.component.html**

```html
<h2>Product Details</h2>

<div *ngIf="product">
  <h3>{{ product.name }}</h3>
  <h4>{{ product.price | currency }}</h4>
  <p>{{ product.description }}</p>

  <button (click)="addToCart(product)">Buy</button>
</div>
```



The above translates really nicely, as follows:

- `<h2>` => `ActionBar`

  ```html
  <ActionBar title="Product Details">
  </ActionBar>
  ```

- `<div>` => `<FlexboxLayout>` with items displayed in a column, and aligned in the center ([see docs for more info](https://docs.nativescript.org/ui/layouts/layout-containers#flexboxlayout)):

  ```html
  <FlexboxLayout flexDirection="column" alignItems="center" class="m-10">
    
  </FlexboxLayout>
  ```

  

- `<h3>`, `<h4>` and `<p>` => `<Label>`

  ```html
  <Label text="{{ product.name }}" class="title"></Label>
  <Label text="{{ product.price | currency }}" class="h2"></Label>
  <Label text="{{ product.description }}" textWrap="true" class="h3"></Label>
  ```

- `<button>` => `<Button>`

  ```html
  <Button (tap)="addToCart(product)" text="Buy" class="btn-green"></Button>
  ```



Like this:

**product-details.component.tns.html**

```html
<ActionBar title="Product Details">
</ActionBar>
<FlexboxLayout flexDirection="column" alignItems="center" class="m-10">
  <Label text="{{ product.name }}" class="title"></Label>
  <Label text="{{ product.price | currency }}" class="h2"></Label>
  <Label text="{{ product.description }}" textWrap="true" class="h3"></Label>

  <Button (tap)="addToCart(product)" text="Buy" class="btn-green"></Button>
</FlexboxLayout>
```



**Step 4**

Fix the call to `window.alert` in **product-details.component.ts**.

```typescript
  addToCart(product) {
    alert('Your product has been added to the cart!');
    this.cartService.addToCart(product);
  }
```



After you save all the files, and navigate to details, your app should look like this:

<img src="./img/5-product-details.png?raw=true" height="400">



## Migrate Component: Cart

Migrating the **Cart** component, is a little more challenging task, as it uses `FormBuilder`, which is not directly supported in NativeScript. This makes for a great example on how to handle web and mobile specific code.

### Handling Web/Mobile specific code #2

One of the best ways to handle a scenario like is this to extract the constructing of a `FormBuilder` to a service. Then have two implementations of the same service, one that uses `FormBuilder`, and the other that recreates the same functionality without a `FormBuilder`.



**Step 1**

Create a **Checkout Form** service:

```bash
ng generate service form/checkout-form
```

Remove `providedIn` from the directive definition, as you will provide this service directly in the **Cart** component.

Using Dependency Injection, request `FormBuilder`, then add a method called `prepareCheckoutForm()`, which should return a form with `name` and `address` properties. Like this:

**form/checkout-form.service.ts**

```typescript
import { Injectable } from '@angular/core';
import { FormBuilder } from '@angular/forms';

@Injectable()
export class CheckoutFormService {
  constructor(private formBuilder: FormBuilder) { }

  prepareCheckoutForm() {
    return this.formBuilder.group({
      name: '',
      address: ''
    });
  }
}
```



**Step 2**

Make a copy of **checkout-form.service.ts** and call it **checkout-form.service.tns.ts**.

In there you need to add an implementation of `CheckoutForm` class with `name` and `address` properties and the `reset()` method.

Then update the `prepareCheckoutForm()` in `CheckoutFormService` to return a new `CheckoutForm`.

Like this:

**form/checkout-form.service.tns.ts**

```typescript
import { Injectable } from '@angular/core';

export class CheckoutForm {
  public name = '';
  public address = '';

  public reset() {
    this.name = '';
    this.address = '';
  }
}

@Injectable()
export class CheckoutFormService {
  public prepareCheckoutForm() {
    return new CheckoutForm();
  }
}
```

**Step 3**

Finally, you need to update the **CartComponent** class to use the `CheckoutFormService`.

Add `CheckoutFormService` to the `@Component` => `providers`, like this:

**cart/cart.component.ts**

```typescript
import { CheckoutFormService } from '@src/app/form/checkout-form.service';

@Component({
  selector: 'app-cart',
  templateUrl: './cart.component.html',
  styleUrls: ['./cart.component.css'],
  providers: [CheckoutFormService]
})
```



Update the constructor to use `CheckoutFormService` instead of `FormBuilder`, like this:

**cart/cart.component.ts**

```typescript
  constructor(
    private cartService: CartService,
    private formService: CheckoutFormService
  ) {
    this.items = this.cartService.getItems();
    this.checkoutForm = this.formService.prepareCheckoutForm();
  }
```



Also, make sure to remove all references to `FormBuilder`.

**cart.component.ts** should look like this:

```typescript
import { Component } from '@angular/core';

import { CartService } from '@src/app/cart.service';
import { CheckoutFormService } from '@src/app/form/checkout-form.service';

@Component({
  selector: 'app-cart',
  templateUrl: './cart.component.html',
  styleUrls: ['./cart.component.css'],
  providers: [CheckoutFormService]
})
export class CartComponent {
  items;
  checkoutForm;

  constructor(
    private cartService: CartService,
    private formService: CheckoutFormService
  ) {
    this.items = this.cartService.getItems();
    this.checkoutForm = this.formService.prepareCheckoutForm();
  }

  onSubmit(customerData) {
    console.warn('Your order has been submitted', customerData);

    this.items = this.cartService.clearCart();
    this.checkoutForm.reset();
  }
}
```



#### Summary

Splitting platform specific functionality into separate files/services, allows you to handle code differences in an elegant fashion, whilst keeping the common functionality shared.

### Migrating the rest of the component

Finally, you can update the **Cart** component to be code-sharing ready.

**Step 1**

Run the migration schematic:

```bash
ng g migrate-component --name=cart
```

**Step 2**

Update the navigation configuration in **app-routing.module.tns.ts**:

```typescript
import { CartComponent } from '@src/app/cart/cart.component';

export const routes: Routes = [
  { path: '', component: ProductListComponent },
  { path: 'products/:productId', component: ProductDetailsComponent },
  { path: 'cart', component: CartComponent },
];
```

**Step 3**

Update **ProductList** template, to add a navigation link (`ActionItem`) for cart in the `ActionBar`.



**product-list.component.tns.html**

```html
<ActionBar title="Products">
  <ActionItem ios.position="right" [nsRouterLink]="['/cart']">
    <Label text="Cart 🛒" class="action-bar-item"></Label>
  </ActionItem>
</ActionBar>
```

The **Product List** should look like this:

<img src="./img/6-product-list-emoji.png?raw=true" height="400">

<!--
#### Use font icons

If you don't like the emoji for a shopping cart 🛒, you can use font icons instead.

[**Font Awesome**](https://fontawesome.com/icons?d=gallery) contains a lot of really nice icons, and the [shopping-cart](https://fontawesome.com/icons/shopping-cart?style=solid) icon is perfect for this app.

<img src="./img/6-font-icon-cart.png?raw=true">

**Step A**

Go to the [download page](https://fontawesome.com/download) and download icons **for Web**.



**Step B**

Create a `fonts` folder in `src`:

```
src
├── app
├── assets
├── environments
└── fonts                  <= new folder
```



**Step C**

Copy **webfonts/fa-solid-900.ttf** file into the **fonts** folder

```
src
├── app
├── assets
├── environments
└── fonts                  <= new folder
    └── fa-solid-900.ttf   <= font awesome
```



**Step D**

Add a css class for Font Awesome to **app.css**.

**app.css** already contains commented out class (`.fa`): 

```
/* .fa {
  font-family: "Font Awesome 5 Free", "fa-solid-900";
} */
```

Remove the comments:

**app.css**

```css
.fa {
  font-family: "Font Awesome 5 Free", "fa-solid-900";
}
```



**Step E**

In the **ProductList** template, update the `ActionItem` to use the `fa` css class, and display the icon code `f07a`, by providing text `&#xf07a;`, like this:

**product-list.component.tns.html**

```html
<ActionBar title="Products">
  <ActionItem ios.position="right" [nsRouterLink]="['/cart']">
    <Label text="&#xf07a; Cart" class="fa action-bar-item"></Label>
  </ActionItem>
</ActionBar>
```

*Might need to kill the build and run it again.*

Now, the **Product List** should look like this:

<img src="./img/6-product-list-icon.png?raw=true" height="400">

-->

**Step 4**



Translate HTML to NativeScript template.

**cart.component.html**

```html
<h3>Cart</h3>

<p>
  <a routerLink="/shipping">Shipping Prices</a>
</p>

<div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }} </span>
  <span>{{ item.price | currency }}</span>
</div>

<form [formGroup]="checkoutForm" (ngSubmit)="onSubmit(checkoutForm.value)">
  <div>
    <label>Name</label>
    <input type="text" formControlName="name">
  </div>

  <div>
    <label>Address</label>
    <input type="text" formControlName="address">
  </div>

  <button class="button" type="submit">Purchase</button>
</form>
```



The above translates really nicely, as follows:

- `<h3>` => `ActionBar`

  ```html
  <ActionBar title="Cart">
  </ActionBar>
  ```

As a container we could use a `StackLayout` and position it inside a `ScrollView` to provide a scrollable area when the content is larger than its bounds.

  ```html
  <ScrollView>
    <StackLayout>

    </StackLayout>
  </ScrollView>
  ```

Then:

```html
<p>
  <a routerLink="/shipping">Shipping Prices</a>
</p>
```

goes to

```html
<Button row="0"
  text="Shipping Prices" nsRouterLink="/shipping" class="btn btn-outline">
</Button>
```

and

```html
<div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }} </span>
  <span>{{ item.price | currency }}</span>
</div>
```

goes to

```html
<Label row="1" *ngIf="!items.length"
  text="No Items in the Cart" class="h2 text-center m-10">
</Label>

<StackLayout row="1" class="m-8">
  <GridLayout *ngFor="let item of items" columns="* auto" class="list-group cart-item">
    <Label col="0" [text]="item.name" class="list-group-item"></Label>
    <Label col="1" [text]="item.price | currency" class="list-group-item"></Label>
  </GridLayout>
</StackLayout>
```

The `form` could transfer from

```html
<form [formGroup]="checkoutForm" (ngSubmit)="onSubmit(checkoutForm.value)">
  <div>
    <label>Name</label>
    <input type="text" formControlName="name">
  </div>

  <div>
    <label>Address</label>
    <input type="text" formControlName="address">
  </div>

  <button class="button" type="submit">Purchase</button>
</form>
```

to

```html
<GridLayout row="2" rows="auto auto auto" columns="auto *" class="form">
  <Label row="0" col="0" text="Name"></Label>
  <TextField row="0" col="1" [(ngModel)]="checkoutForm.name" hint="name..."></TextField>
  <Label row="1" col="0" text="Address"></Label>
  <TextField row="1" col="1" [(ngModel)]="checkoutForm.address" hint="address..."></TextField>
</GridLayout>
<Button text="Purchase" (tap)="onSubmit(checkoutForm)" class="btn-green"></Button>
```

Before we can use the `ngModel` directive in data binding, we must import the `NativeScriptFormsModule` and add it to the Angular module's imports list.

Open **app.module.tns.ts** where you will find a commented import for **NativeScriptFormsModule** class (*line 10*). Uncomment it, and add **NativeScriptFormsModule** to @NgModule **imports**, like this:

```typescript
import { NativeScriptFormsModule } from 'nativescript-angular/forms';

@NgModule({
  ...
  imports: [
    NativeScriptModule,
    AppRoutingModule,
    NativeScriptHttpClientModule,
    NativeScriptFormsModule
  ],
```

Finally, the **cart.component.tns.html** should look like this:

```html
<ActionBar title="Cart">
</ActionBar>
<ScrollView>
  <StackLayout>
    <Button row="0" 
      text="Shipping Prices" nsRouterLink="/shipping" class="btn btn-outline">
    </Button>

    <Label row="1" *ngIf="!items.length"
      text="No Items in the Cart" class="h2 text-center m-10">
    </Label>

    <StackLayout row="1" class="m-8">
      <GridLayout *ngFor="let item of items" columns="* auto" class="list-group cart-item">
        <Label col="0" [text]="item.name" class="list-group-item"></Label>
        <Label col="1" [text]="item.price | currency" class="list-group-item"></Label>
      </GridLayout>
    </StackLayout>

    <GridLayout row="2" rows="auto auto auto" columns="auto *" class="form">
      <Label row="0" col="0" text="Name"></Label>
      <TextField row="0" col="1" [(ngModel)]="checkoutForm.name" hint="name..."></TextField>
      <Label row="1" col="0" text="Address"></Label>
      <TextField row="1" col="1" [(ngModel)]="checkoutForm.address" hint="address..."></TextField>
    </GridLayout>
    <Button text="Purchase" (tap)="onSubmit(checkoutForm)" class="btn-green"></Button>

  </StackLayout>
</ScrollView>
```

The **Cart** page should look like this:

<img src="./img/7-cart.png?raw=true" height="400">



## Migrate Component: Shipping

The final component to migrate is the **Shipping** component. This is the component the app navigates to during cart checkout for reviewing the available shipping options.

You could execute the routine:

**Step 1**

Run the migration schematic:

```bash
ng g migrate-component --name=shipping
```

**Step 2**

Update the navigation configuration in **app-routing.module.tns.ts**:

```typescript
import { ShippingComponent } from '@src/app/shipping/shipping.component';

export const routes: Routes = [
  { path: '', component: ProductListComponent },
  { path: 'products/:productId', component: ProductDetailsComponent },
  { path: 'cart', component: CartComponent },
  { path: 'shipping', component: ShippingComponent },
];
```

**Step 3**

Update the NativeScript template:

**shipping.component.tns.html**

```html
<ActionBar title="Shipping Prices">
</ActionBar>

<StackLayout class="m-8">
  <GridLayout *ngFor="let shipping of shippingCosts | async" rows="auto" columns="120 *"
    class="shipping-item list-group">
    <Label col="0" [text]="shipping.type" class="list-group-item"></Label>
    <Label col="1" [text]="shipping.price | currency" class="list-group-item"></Label>
  </GridLayout>
  
  <!-- <ListView [items]="shippingCosts | async" class="list-group" height="100%">
    <ng-template let-shipping="item">
      <GridLayout rows="auto" columns="120 *" class="shipping-item">
        <Label col="0" [text]="shipping.type" class="list-group-item"></Label>
        <Label col="1" [text]="shipping.price | currency" class="list-group-item"></Label>
      </GridLayout>
    </ng-template>
  </ListView> -->
</StackLayout>
```

Don't worry if the app doesn't work yet. Follow the below step before you test.

**Step 4**

NativeScript build process consists of two steps: bundling and building the native app. By default, some files do not include in the application's bundle such as fonts and images. The **webpack** bundler is explicitly instructed to copy these types of files to the native application in its configuration file.

Therefore, to make it possible for NativeScript to load **.json** files from the **assets** folder, you need to give information Webpack to copy the file into the native application. This can be done with the help of `CopyWebpackPlugin` like this:

```javascript
new CopyWebpackPlugin([ 
  { from: { glob: "assets/*.json" } },
])
```

As it is already in use, just open **webpack.config.js**, find the comment line `// Copy assets to out dir. Add your own globs as needed.`
and update as follows:

**webpack.config.js**

```javascript
// Copy assets to out dir. Add your own globs as needed.
new CopyWebpackPlugin([
  { from: { glob: "assets/*.json" } },
  { from: { glob: "fonts/**" } },
  { from: { glob: "**/*.jpg" } },
  { from: { glob: "**/*.png" } },
], { ignore: [`${relative(appPath, appResourcesFullPath)}/**`] }),
```

In order to apply the changes to the `webpack.config.js` file, we need to stop the currently running process and start it again to pick up its new configuration. So, go back to your console/terminal and execute again `tns preview --bundle`.
