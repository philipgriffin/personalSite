---
layout: post
title: Drag and drop with Angular 7
tags:
- Angular
excerpt_separator: "<!-- more -->"

---
Dragging and dropping has never been easier! Lets make use of the Component Development Kit (CDK) along with Angular 7+ to make some draggable divs in less than a minute!

<!-- more -->

### CDK setup

Make sure you are on at least V7 of Angular. You can check this by running ```ng version``` from your chosen CLI (if you have the Angular CLI installed globally).

Start by creating a new project.
```
  ng new dragAndDropDemo
```

Right away we can install the CDK and then serve the app.
```
  npm i @angular/cdk -S
  ng serve
```

Now just navigate to your ```app.module.ts``` and add the ```DragDropModule``` import to the top of the file and also add it to your imports. See my complete file below.

```typescript
  import { BrowserModule } from "@angular/platform-browser";
  import { NgModule } from "@angular/core";
  import { AppComponent } from "./app.component";
  import { DragDropModule } from "@angular/cdk/drag-drop";

  @NgModule({
    declarations: [AppComponent],
    imports: [BrowserModule, DragDropModule],
    providers: [],
    bootstrap: [AppComponent]
  })
  export class AppModule {}
```

Navigate to your ```app.component.html``` and drop in the below HTML.
```html
  <div style="font-size: 100px;" cdkDrag>
    🍔
  </div>
```

With the ```cdkDrag``` directive we can now easily drag this div around!

See the result below.

<img style="border: 1px solid lightgray;" src="{{ site.baseurl }}/assets/images/dragDrop.gif" alt="Drag and drop gif">