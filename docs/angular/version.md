## Angular 2

- Angular 2 is similar to 3, 4, 5, ... 9

- New version every 6 months release, it doesn't change anything

---

## Set Up first project

- `npm install -g @angular/cli@latest`


![](img/2020-12-27-15-57-22.png)

- cd to `my-first-app`

- run `npm serve`

- open the browser `http://localhost:4200/`

![](img/2020-12-27-16-15-11.png)

- try to change.

- now try to change **title**

![](img/2020-12-27-16-16-42.png)

---

### Let's do something more fancy

- clear everything from `app.component.html`

```html
<input type="text">
<p>{{name}}</p>
```

- edit `app.component.ts`

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  name = 'Hello World!';
}
```

![](img/2020-12-27-16-33-55.png)

---

- edit `app.module.ts`

```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import {FormsModule} from '@angular/forms';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

- edit `app.component.html`

```html
<input type="text" [(ngModel)]="name">
<p>{{name}}</p>
```

![](img/2020-12-27-16-48-43.png)

---

## Angular Structure

![](img/2020-12-27-16-51-09.png)

---

## A Basic Project Setup using Bootstrap for Styling

- import `bootstrap`

- `npm install --save bootstrap@3`

![](img/2020-12-27-16-56-24.png)

- now we import `bootstrap` to my project
- `angular.json` import => `node_modules/bootstrap/dist/css/bootstrap.min.css`

![](img/2020-12-27-17-26-10.png)

- since we have installed `bootstrap`, we can find it from `node_modules`

![](img/2020-12-27-17-05-01.png)

- this is same to `React`

![](img/2020-12-27-17-43-06.png)

- then we can see that it imports bootstrap









