<img src="images/angular.svg" width="400" class="center">

<span class="fill">

# Angular

</span>
<span class="fill">

#### Workshop

</span>

---

<!-- page_number: true -->

# Angular

Setting up the environment:

Requirements:

* Node.js [https://nodejs.org/en/download/current/](https://nodejs.org/en/download/current/)
* A JavaScript editor of your choice:
  * WebStorm [https://www.jetbrains.com/webstorm/](https://www.jetbrains.com/webstorm/)
  * VS Code [https://code.visualstudio.com/](https://code.visualstudio.com/)
  * Atom [https://atom.io/](https://atom.io/)

## 1. Create a base project

### 1.1. Install Angular CLI

Angular CLI is a simple way of generating Angular projects. Open a terminal and run:

```bash
npm install -g @angular/cli
```

### 1.2. Create an Angular application

```bash
ng new angular-tour-of-heroes
? Would you like to add Angular routing? No
? Which stylesheet format would you like to use? CSS
```

### 1.3. Start the application

```bash
cd angular-tour-of-heroes
ng serve --open
```

### 1.4. Edit the base application

Open the project in an editor or IDE and navigate to the `src/app` folder.

The base app is implemented in the following files:

1. app.component.ts - The component class code
2. app.component.html - The component template
3. app.component.css - The component private styles

---

### 1.5. Edit the application title

In the component class change the `title` value:

```typescript
title = 'Tour of Heroes';
```

In the template file replace the generated template:

```html
<h1>{{title}}</h1>
```

And in the global `styles.css` add some styles:

```css
/* Application-wide Styles */
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}

h2, h3 {
  color: #444;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
}

body {
  margin: 2em;
}

body, input[type="text"], button {
  color: #888;
  font-family: Cambria, Georgia;
}

/* everywhere else */
* {
  font-family: Arial, Helvetica, sans-serif;
}
```
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

----

## 2. Adding heroes

### 2.1. Create a heroes component using the CLI

```bash
ng generate component heroes
```

What changed?

1. A new folder called `heroes` was created in the project `src/app` folder.
2. Inside that folder a new component called `HeroesComponent` was created.
3. The `HeroesComponent` was declared in the `AppModule` metadata `declarations` property.

### 2.2. Edit the heroes component

Open the `heroes.component.ts` file and add a new `hero` property:

```typescript
hero = 'Windstorm';
```

Show the hero in the component `heroes.component.html` template:

```html
{{hero}}
```

And include the component in the app component template:

```html
<h1>{{title}}</h1>
<app-heroes></app-heroes>
```

Check the changes on your browser.

### 2.3. Add a heroes object

Create a `hero.ts` file and declare a new type:

```typescript
export class Hero {
  id: number;
  name: string;
}
```

---

### 2.4. Display the hero object

Replace the initial hero name in the hero component with and hero object:

```typescript
hero: Hero = {
  id: 1,
  name: 'Windstorm'
};
```

Edit the template to display the hero object:

```html
<h2>{{hero.name}} Details</h2>
<div><span>id: </span>{{hero.id}}</div>
<div><span>name: </span>{{hero.name}}</div>
```

Then format the hero to be upper case using the uppercase pipe:

```html
<h2>{{hero.name | uppercase}} Details</h2>
```

### 2.5. Add an hero editor

```html
<div>
  <label>name:
    <input [(ngModel)]="hero.name" placeholder="name">
  </label>
</div>
```

Replace the name div with the above code. Check your browser.

You'll notice the app has stopped working since the `[(ngModel)]` is declared in the `FormsModule` which is not imported into the application.

Open the `AppModule` and import the required module:

```typescript
import { FormsModule } from '@angular/forms';
...
imports: [
  BrowserModule,
  FormsModule
],
```

Save and check the browser again. Edit the value in the input to see the details changing.

---

## 3. Display a list of heroes

First we need a list of heroes to display.

### 3.1. Create a list of mock heroes

Add a file called `mock-heroes.ts` and add some heroes:

```typescript
import { Hero } from './hero';

export const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

### 3.2. Display the heroes

Import the heroes list in the heroes component:

```typescript
import { HEROES } from '../mock-heroes';
```

Declare a heroes property in the heroes component:

```typescript
heroes = HEROES;
```

Display the heroes using the `*ngFor` directive in the template above the hero details:

```html
<h2>My Heroes</h2>
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>
```

&nbsp;
&nbsp;

---

And style the heroes list:

```css
/* HeroesComponent's private CSS styles */
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.heroes li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
}
.heroes .text {
  position: relative;
  top: -3px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

&nbsp;
&nbsp;

---

### 3.3. Add hero selection

On the heroes template add an event binding for the hero click:

```html
<li *ngFor="let hero of heroes" (click)="onSelect(hero)">
```

On the heroes component rename the hero property to `selectedHero` and add an `onSelect` method to handle the click event:

```typescript
selectedHero: Hero;

onSelect(hero: Hero): void {
  this.selectedHero = hero;
}
```

And update the hero details template t use the new property:

```html
<h2>{{selectedHero.name | uppercase}} Details</h2>
<div><span>id: </span>{{selectedHero.id}}</div>
<div>
  <label>name:
    <input [(ngModel)]="selectedHero.name" placeholder="name">
  </label>
</div>
```

Check your browser, you'll get an error since the `selectedHero` is initially undefined. Clicking in an hero on the list will make the app work again.

To fix it let's make sure the hero details only shows if an hero is selected:

```html
<div *ngIf="selectedHero"> <!-- new line -->
  <h2>{{selectedHero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{selectedHero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="selectedHero.name"
             placeholder="name">
    </label>
  </div>
</div> <!-- new line -->
```

&nbsp;
&nbsp;

---

### 3.4. Style the select hero

On the hero list `<li>` use style binding to set a style:

```html
<li *ngFor="let hero of heroes"
  [class.selected]="hero === selectedHero"
  (click)="onSelect(hero)">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```

Browse through the heroes list and check how the application is working right now.

You should be able the select and edit the existing heroes.

# 4. Create master and detail components

Until now we have used a single component to implement the application logic. In a real application this is not maintainable.

Let's split the app into multiple components.

### 4.1. Add a details component

Add a new component to handle the hero details:

```bash
ng generate component hero-detail
```

### 4.2. Edit the component

Move the the hero details part from the master component template into the details and change the `selectedHero` reference to `hero`.

```html
<div *ngIf="hero">
  <h2>{{hero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{hero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="hero.name" placeholder="name"/>
    </label>
  </div>
</div>
```

&nbsp;

---

And style the hero details component:

```css
/*
  HeroDetailComponent's private CSS styles
*/
label {
  display: inline-block;
  width: 3em;
  margin: .5em 0;
  color: #607D8B;
  font-weight: bold;
}

input {
  height: 2em;
  font-size: 1em;
  padding-left: .4em;
  background: white;
  color: #607D8B;
  border: 1px solid #607D8B;
  border-radius: 4px;
}

button {
  margin-top: 20px;
  font-family: Arial;
  background-color: #eee;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  cursor: hand;
}

button:hover {
  background-color: #cfd8dc;
}

button:disabled {
  background-color: #eee;
  color: #ccc;
  cursor: auto;
}

```

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

---

### 4.3. Add an @Input() in the details component

Import the hero object:

```typescript
import { Hero } from '../hero';
```

Import the `Input` decorator:

```typescript
import { Component, OnInit, Input } from '@angular/core';
```

Add an hero property to the hero details component class:

```typescript
@Input() hero: Hero;
```

### 4.4. Use the hero details component

In the master heroes component, where the hero details where, add a reference to the created hero details component:

```html
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

The hero list template should look like this:

```html
<h2>My Heroes</h2>
<ul class="heroes">
  <li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
    (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

Check the app. You'll see that the app behaves in the same way as before.

## 5. Use services

Components shouldn't fetch or save data directly and they certainly shouldn't knowingly present fake data. They should focus on presenting data and delegate data access to a service.

---

### 5.1. Create a service

Use the CLI to create a service

```bash
ng generate service hero
```

A skeleton service is created in the project `src/app` folder, open it:

```typescript
import { Injectable } from '@angular/core';
@Injectable({
  providedIn: 'root',
})
export class HeroService {
  constructor() { }
}
```

On the `AppModule` you can check that the services is not registered in the providers. That's because of the `providedIn` in the `@Injectable` metadata. This will cause Angular to create a single shared instance os the service to be created.

### 5.2. Edit the heroes component

Delete the `HEROES` import and import the `HeroesService`:

```typescript
import { HeroService } from '../hero.service';
```

Replace the `heroes` property definition with a simple declaration:

```typescript
heroes: Hero[];
```

Inject the `HeroesService`:

```typescript
constructor(private heroService: HeroService) { }
```

Add a method to call the service:

```typescript
getHeroes(): void {
  this.heroes = this.heroService.getHeroes();
}
```

&nbsp;

---

And call it on the component initialization callback:

```typescript
ngOnInit() {
  this.getHeroes();
}
```

### 5.3. Handle asynchronous data

The way we are calling the service will only handle synchronous calls. Since most of the applications get data from some Wb API we need to handle the call asynchronously.

On the service import the required RxJS operators and classes:

```typescript
import { Observable, of } from 'rxjs';
```

And return the `HEROES` data has an observable:

```typescript
getHeroes(): Observable<Hero[]> {
  return of(HEROES);
}
```

Edit the heroes component to subscribe to the observable:

```typescript
getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
}
```

## 6. Display messages

Let's add a service to display a message at the bottom os the screen.

### 6.1. Create a messages component

```bash
ng generate component messages
```

### 6.2. Add the messages service to the app component

```html
<h1>{{title}}</h1>
<app-heroes></app-heroes>
<app-messages></app-messages>
```

---

### 6.1. Create a messages service

```bash
ng generate service messages
```

### 6.2. Edit the messages service

Add a messages property:

```typescript
messages: string[] = [];
```

Add a `add` and a `clear` method:

```typescript
add(message: string) {
  this.messages.push(message);
}
 
clear() {
  this.messages = [];
}
```

Import it in the heroes service:

```typescript
import { MessageService } from './message.service';
```

Inject it into the heroes service:

```typescript
constructor(private messageService: MessageService) { }
```

And send a message from the service

```typescript
getHeroes(): Observable<Hero[]> {
  this.messageService.add('HeroService: fetched heroes');
  return of(HEROES);
}
```

### 6.3. Display the message from the messages service

In the messages component import the messages service:

```typescript
import { MessageService } from './message.service';
```

---

Inject it into the messages component:

```typescript
constructor(public messageService: MessageService) { }
```

Edit the messages component template and bind it to the messages service:

```html
<div *ngIf="messageService.messages.length">
  <h2>Messages</h2>
  <button class="clear" (click)="messageService.clear()">
    Clear
  </button>
  <div *ngFor='let message of messageService.messages'>
    {{message}}
  </div>
</div>
```

And style the messages component;

```css
/* MessagesComponent's private CSS styles */
h2 {
  color: red;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
}
body {
  margin: 2em;
}
body, input[text], button {
  color: crimson;
  font-family: Cambria, Georgia;
}
button.clear {
  font-family: Arial;
  background-color: #eee;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  cursor: hand;
}
button:hover {
  background-color: #cfd8dc;
}
button:disabled {
  background-color: #eee;
  color: #aaa;
  cursor: auto;
}
```
---

```css
button.clear {
  color: #888;
  margin-bottom: 12px;
}
```

## 7. Navigating in the app

Navigation in Angular applications is done by routing.

### 7.1. Add a routing module

In the command line execute the CLI:

```bash
ng generate module app-routing --flat --module=app
```

This will generate a base routing module:

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: []
})
export class AppRoutingModule { }
```

### 7.2. Add routes

Edit the routing module to remove the imported modules and exports. Then import the required routing dependencies:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

@NgModule({
  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```

&nbsp;
&nbsp;
&nbsp;

---

Add a route to the heroes component:

```typescript
import { HeroesComponent }      from './heroes/heroes.component';

const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
```

Import the routing module and configure it with the routes:

```typescript
@NgModule({
  imports: [ RouterModule.forRoot(routes) ],
  exports: [ RouterModule ]
})
```

Replace the heroes component in the app template with a router outlet:

```html
<h1>{{title}}</h1>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

Try the app. You'll no longer see the heroes list because the list is the the `/heroes` path and not the root.

### 7.3. Add navigation links

Add a navigation bar to the app component template:

```html
<h1>{{title}}</h1>
<nav>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

Try the app and click the link, the heroes list will be displayed and you'll notice that the application path has changed to 'http://localhost:4200/heroes'.

### 7.4. Add a dashboard

Add a new dashboard component

```bash
ng generate component dashboard
```

---

Replace the dashboard template content:

```html
<h3>Top Heroes</h3>
<div class="grid grid-pad">
  <a *ngFor="let hero of heroes" class="col-1-4">
    <div class="module hero">
      <h4>{{hero.name}}</h4>
    </div>
  </a>
</div>
```

Add the component properties:

```typescript
export class DashboardComponent implements OnInit {
  heroes: Hero[] = [];

  constructor(private heroService: HeroService) {
  }

  ngOnInit() {
    this.getHeroes();
  }

  getHeroes(): void {
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes.slice(1, 5));
  }
}
```

And style the component:

```css
/* DashboardComponent's private CSS styles */
[class*='col-'] {
  float: left;
  padding-right: 20px;
  padding-bottom: 20px;
}
[class*='col-']:last-of-type {
  padding-right: 0;
}
a {
  text-decoration: none;
}
*, *:after, *:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
h3 {
  text-align: center;
  margin-bottom: 0;
}
```

---

```css
h4 {
  position: relative;
}
.grid {
  margin: 0;
}
.col-1-4 {
  width: 25%;
}
.module {
  padding: 20px;
  text-align: center;
  color: #eee;
  max-height: 120px;
  min-width: 120px;
  background-color: #607d8b;
  border-radius: 2px;
}
.module:hover {
  background-color: #eee;
  cursor: pointer;
  color: #607d8b;
}
.grid-pad {
  padding: 10px 0;
}
.grid-pad > [class*='col-']:last-of-type {
  padding-right: 20px;
}
@media (max-width: 600px) {
  .module {
    font-size: 10px;
    max-height: 75px;
  }
}
@media (max-width: 1024px) {
  .grid {
    margin: 0;
  }
  .module {
    min-width: 60px;
  }
}
```

### 7.5. Add routes to the dashboard

Edit the app routing module and import the dashboard component:

```typescript
import {
  DashboardComponent
} from './dashboard/dashboard.component';
```

---

Add a new route:

```typescript
const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent },
  { path: 'heroes', component: HeroesComponent }
];
```

Add a default route that redirects the root path to the dashboard:

```typescript
const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent },
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'heroes', component: HeroesComponent }
];
```

And add a dashboard link to the app component:

```html
<h1>{{title}}</h1>
<nav>
  <a routerLink="/dashboard">Dashboard</a>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

Try the app.

### 7.6. Add navigation to the details:

Start by deleting the hero details from the hero component.

Edit the app routing module and import the hero details component:

```typescript
import {
  HeroDetailComponent
}  from './hero-detail/hero-detail.component';
```

Add a new route:

```typescript
{ path: 'detail/:id', component: HeroDetailComponent },
```

---

On the dashboard component template add routes to the hero details:

```html
<a *ngFor="let hero of heroes" class="col-1-4"
    routerLink="/detail/{{hero.id}}">
  <div class="module hero">
    <h4>{{hero.name}}</h4>
  </div>
</a>
```

Edit the hero component details template to use a link:

```html
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <a routerLink="/detail/{{hero.id}}">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </a>
  </li>
</ul>
```

Remove dead code from the heroes component. The remaining component should look like this:

```typescript
export class HeroesComponent implements OnInit {
  heroes: Hero[];

  constructor(private heroService: HeroService) { }

  ngOnInit() {
    this.getHeroes();
  }

  getHeroes(): void {
    this.heroService.getHeroes()
    .subscribe(heroes => this.heroes = heroes);
  }
}
```

In the hero details component we need to get the selected hero ID. So import the router required dependencies:

```typescript
import { ActivatedRoute } from '@angular/router';
import { Location } from '@angular/common';

import { HeroService }  from '../hero.service';
```

&nbsp;

---

Inject the required services in the hero details component constructor:

```typescript
constructor(
  private route: ActivatedRoute,
  private heroService: HeroService,
  private location: Location
) {}
```

Extract the ID from the route and call the heroes service with the ID:

```typescript
ngOnInit(): void {
  this.getHero();
}

getHero(): void {
  const id = +this.route.snapshot.paramMap.get('id');
  this.heroService.getHero(id)
    .subscribe(hero => this.hero = hero);
}
```

Add the method to the heroes service:

```typescript
getHero(id: number): Observable<Hero> {
  this.messageService.add(`HeroService: fetched hero id=${id}`);
  return of(HEROES.find(hero => hero.id === id));
}
```

Add an action to return from the hero details to the source path:

```html
<button (click)="goBack()">go back</button>
```

And in the hero details handle the action:

```typescript
goBack(): void {
  this.location.back();
}
```

Clean up by removing the `@Input` decorator from the `hero` property.

## 8. Request heroes from a service

To do this we will be using the Angular `HttpClient`.

&nbsp;

---

#### 8.1. Import the client

In the app module import the `HttpClient`:

```typescript
import { HttpClientModule } from '@angular/common/http';
```

And add it to the modules imports:

```typescript
imports: [
  BrowserModule,
  FormsModule,
  HttpClientModule,
  AppRoutingModule
],
```

### 8.2. Generate sample server

For simplicity let's simulate a server using the Angular In-memory We API.

Add the npm package:

```bash
npm install angular-in-memory-web-api --save
```

In the app module import the required dependencies:

```typescript
import {
  HttpClientInMemoryWebApiModule
} from 'angular-in-memory-web-api';
import { InMemoryDataService }  from './in-memory-data.service';
```

Initialize the in-memory module:

```typescript
imports: [
  BrowserModule,
  FormsModule,
  HttpClientModule,
  HttpClientInMemoryWebApiModule.forRoot(InMemoryDataService, {
    dataEncapsulation: false
  }),
  AppRoutingModule
],
```

Generate a in-memory support service:

```bash
ng generate service InMemoryData
```

---

Add in-memory logic:

```typescript
import { InMemoryDbService } from 'angular-in-memory-web-api';
import { Injectable } from '@angular/core';
import { Hero } from "./heroes/hero";

@Injectable({
  providedIn: 'root',
})
export class InMemoryDataService implements InMemoryDbService {
  createDb() {
    const heroes = [
      { id: 11, name: 'Mr. Nice' },
      { id: 12, name: 'Narco' },
      { id: 13, name: 'Bombasto' },
      { id: 14, name: 'Celeritas' },
      { id: 15, name: 'Magneta' },
      { id: 16, name: 'RubberMan' },
      { id: 17, name: 'Dynama' },
      { id: 18, name: 'Dr IQ' },
      { id: 19, name: 'Magma' },
      { id: 20, name: 'Tornado' }
    ];
    return { heroes };
  }

  genId(heroes: Hero[]): number {
    return heroes.length > 0 ?
      Math.max(...heroes.map(hero => hero.id)) + 1 : 11;
  }
}
```

### 8.3. Edit the heroes service

Import the `HttpClient`:

```typescript
import { HttpClient, HttpHeaders } from '@angular/common/http';
```

And inject it:

```typescript
constructor(private http: HttpClient,
  private messageService: MessageService) { }
```

Add a logger service:

```typescript
private log(message: string) {
  this.messageService.add(`HeroService: ${message}`);
}
```

---

Add an API URL:

```typescript
private heroesUrl = 'api/heroes';
```

And change the heroes method to use the client:

```typescript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl);
}
```

Import the RxJS operators for error handling:

```typescript
import { catchError, map, tap } from 'rxjs/operators';
```

And catch the errors:

```typescript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl)
    .pipe(
      catchError(this.handleError('getHeroes', []))
    );
}
```

Add the method to handle the errors:

```typescript
private handleError<T> (operation = 'operation', result?: T) {
  return (error: any): Observable<T> => {
    console.error(error);
    this.log(`${operation} failed: ${error.message}`);
    return of(result as T);
  };
}
```

Tap into the observable to log the messages after getting the heroes:

```typescript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl)
    .pipe(
      tap(_ => this.log('fetched heroes')),
      catchError(this.handleError('getHeroes', []))
    );
}
```

---

And change the get hero details method to use the same logic:

```typescript
getHero(id: number): Observable<Hero> {
  const url = `${this.heroesUrl}/${id}`;
  return this.http.get<Hero>(url)
    .pipe(
      tap(_ => this.log(`fetched hero id=${id}`)),
      catchError(this.handleError<Hero>(`getHero id=${id}`))
    );
}
```

Browse the app. You'll notice some delay since the `HttpClientInMemoryWebApiModule` will delay the response simulating a real Web request.

### 8.4. Update existing heroes

Right now, since we are using a mock server, when you make changes to a hero and go back to the list changes are lost. Let's save teh changes to the service.

Edit the hero details component template and add a save component:

```html
<button (click)="save()">save</button>
```

Handle the button click on the component:

```typescript
save(): void {
  this.heroService.updateHero(this.hero)
    .subscribe(() => this.goBack());
}
```

Edit the heroes service and add a update method:

```typescript
updateHero (hero: Hero): Observable<any> {
  return this.http.put(this.heroesUrl, hero, httpOptions).pipe(
    tap(_ => this.log(`updated hero id=${hero.id}`)),
    catchError(this.handleError<any>('updateHero'))
  );
}
```

Declare the `httpOptions` with headers information to set the content type as JSON:

```typescript
const httpOptions = {
  headers: new HttpHeaders({ 'Content-Type': 'application/json' })
};
```

---

Now if you browse the application, edit an hero and save before pressing back the hero will also be updated in the list.

### 8.5. Add new heroes

Edit the heroes component template and add an input after the header:

```html
<div>
  <label>Hero name:
    <input #heroName />
  </label>
  <!-- (click) passes input value to add()
    and then clears the input -->
  <button (click)="add(heroName.value); heroName.value=''">
    add
  </button>
</div>
```

In the component code handle the click event:

```typescript
add(name: string): void {
  name = name.trim();
  if (!name) { return; }
  this.heroService.addHero({ name } as Hero)
    .subscribe(hero => {
      this.heroes.push(hero);
    });
}
```

Add some styles for the input in the component private styles:

```css
label {
  display: inline-block;
  margin: .5em 0;
  color: #607D8B;
  font-weight: bold;
}

input {
  height: 2em;
  font-size: 1em;
  padding-left: .4em;
  background: white;
  color: #607D8B;
  border: 1px solid #607D8B;
  border-radius: 4px;
  display: block;
}
```

---

```css
button {
  background-color: #eee;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  cursor: hand;
  font-family: Arial;
}
 
button:hover {
  background-color: #cfd8dc;
}
```

Edit the heroes service and add an `add` method:

```typescript
addHero (hero: Hero): Observable<Hero> {
  return this.http.post<Hero>(this.heroesUrl, hero, httpOptions).pipe(
    tap((hero: Hero) => this.log(`added hero w/ id=${hero.id}`)),
    catchError(this.handleError<Hero>('addHero'))
  );
}
```

### 8.6. Delete heroes

Finally we should be able to delete heroes too, so let's add a delete button to each hero on the list:

```html
<button class="delete" title="delete hero"
  (click)="delete(hero)">x</button>
```

The heroes component template list should look like this:

```html
<ul class="heroes">
  <li *ngFor="let hero of heroes">
    <a routerLink="/detail/{{hero.id}}">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </a>
    <button class="delete" title="delete hero"
      (click)="delete(hero)">x</button>
  </li>
</ul>
```

&nbsp;
&nbsp;

---

Handle the click on the heroes component:

```typescript
delete(hero: Hero): void {
  this.heroes = this.heroes.filter(h => h !== hero);
  this.heroService.deleteHero(hero).subscribe();
}
```

**Note** about the above code. The subscribe method does nothing. This is not an error. An observable by rule does nothing until something subscribes it, so you must always call subscribe.

Style the delete button:

```css

li {
  display: flex;
}
li a {
  flex-grow: 1;
}
button.delete {
  position: relative;
  background-color: gray !important;
  color: white;
}
```

Add a delete method to the heroes service:

```typescript
deleteHero (hero: Hero | number): Observable<Hero> {
  const id = typeof hero === 'number' ? hero : hero.id;
  const url = `${this.heroesUrl}/${id}`;

  return this.http.delete<Hero>(url, httpOptions).pipe(
    tap(_ => this.log(`deleted hero id=${id}`)),
    catchError(this.handleError<Hero>('deleteHero'))
  );
}
```

## 9. Search heroes

As a final exercise we will use observable operators to optimize and minimize the number of similar HTTP requests.

To do this we will include a hero search feature in the application dashboard.

&nbsp;

---

### 9.1. Add search to dashboard

Generate a new search component:

```bash
ng generate component hero-search
```

Edit the search component template:

```html
    <div id="search-component">
      <h4>Hero Search</h4>
      <input #searchBox id="search-box"
             (input)="search(searchBox.value)" />
      <ul class="search-result">
        <li *ngFor="let hero of heroes$ | async" >
          <a routerLink="/detail/{{hero.id}}">
            {{hero.name}}
          </a>
        </li>
      </ul>
    </div>
```

Style the search component:

```css
/* HeroSearch private styles */
.search-result li {
  border-bottom: 1px solid gray;
  border-left: 1px solid gray;
  border-right: 1px solid gray;
  width: 195px;
  height: 16px;
  padding: 5px;
  background-color: white;
  cursor: pointer;
  list-style-type: none;
}
.search-result li:hover {
  background-color: #607D8B;
}
.search-result li a {
  color: #888;
  display: block;
  text-decoration: none;
}
.search-result li a:hover {
  color: white;
}
.search-result li a:active {
  color: white;
}
```

---

```css
#search-box {
  width: 200px;
  height: 20px;
}
ul.search-result {
  margin-top: 0;
  padding-left: 0;
}
input {
  background: white;
  color: #607D8B;
  border: 1px solid #607D8B;
  border-radius: 4px;
}
```

Edit the search component code:

```typescript
import { Component, OnInit } from '@angular/core';
import { Observable, Subject } from 'rxjs';
import {
  debounceTime, distinctUntilChanged, switchMap
} from 'rxjs/operators';
import { Hero } from '../heroes/hero';
import { HeroService } from '../hero.service';

@Component({
  selector: 'app-hero-search',
  templateUrl: './hero-search.component.html',
  styleUrls: ['./hero-search.component.css']
})
export class HeroSearchComponent implements OnInit {
  heroes$: Observable<Hero[]>;
  private searchTerms = new Subject<string>();

  constructor(private heroService: HeroService) {
  }
  
  search(term: string): void {
    this.searchTerms.next(term);
  }

  ngOnInit(): void {
    this.heroes$ = this.searchTerms.pipe(
      debounceTime(300),
      distinctUntilChanged(),
      switchMap((term: string) => this.heroService.searchHeroes(term))
    );
  }
}
```

&nbsp;

---

Notice the declaration of the heroes array:

```typescript
heroes$: Observable<Hero[]>;
```

This is an observable that is not subscribed in the code. Why will this work? The answer is in the template `async` pipe that handles the subscription in the template:

```html
<li *ngFor="let hero of heroes$ | async" >
```

We also use a `Subject` that when called will invoke the search method in the service:

```typescript
private searchTerms = new Subject<string>();

search(term: string): void {
  this.searchTerms.next(term);
}
```

It will be called when the search input value changes:

```html
<input #searchBox id="search-box"
       (input)="search(searchBox.value)" />
```

The `Subject` has some chained operators to minimize the amount of calls to the service:

```typescript
this.heroes$ = this.searchTerms.pipe(
  debounceTime(300),
  distinctUntilChanged(),
  switchMap((term: string) => this.heroService.searchHeroes(term))
);
```

* `debounceTime(300)` waits until the flow of new string events pauses for 300 milliseconds before passing along the latest string. You'll never make requests more frequently than 300ms.
* `distinctUntilChanged()` ensures that a request is sent only if the filter text changed.
* `switchMap()` calls the search service for each search term that makes it through debounce and distinctUntilChanged. It cancels and discards previous search observables, returning only the latest search service observable.

---

Add a search method to the heroes service:

```typescript
searchHeroes(term: string): Observable<Hero[]> {
  if (!term.trim()) {
    // if not search term, return empty hero array.
    return of([]);
  }
  return this.http.get<Hero[]>(`${this.heroesUrl}/?name=${term}`)
    .pipe(
      tap(_ => this.log(`found heroes matching "${term}"`)),
      catchError(this.handleError<Hero[]>('searchHeroes', []))
    );
}
```

And edit the dashboard template to add the search component:

```html
<h3>Top Heroes</h3>
<div class="grid grid-pad">
  <a *ngFor="let hero of heroes" class="col-1-4"
      routerLink="/detail/{{hero.id}}">
    <div class="module hero">
      <h4>{{hero.name}}</h4>
    </div>
  </a>
</div>

<app-hero-search></app-hero-search>
```

And try it!

Done!

For full documentations check the Angular guide at [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart)

There's a lot more to know about what was discussed where discussed here and other. I recommend you check:

* Forms [https://angular.io/guide/forms-overview](https://angular.io/guide/forms-overview)
* Observables [https://angular.io/guide/observables](https://angular.io/guide/observables)
* Routing & Navigation [https://angular.io/guide/router](https://angular.io/guide/router)
* Animations [https://angular.io/guide/animations](https://angular.io/guide/animations)

And explore all the other documentation which includes Security, Service Workers, Internationalization, Server-side Rendering, etc.

&nbsp;
