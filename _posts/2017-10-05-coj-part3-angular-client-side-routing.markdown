---
layout: post
title:  "Second Component and Angular Routing"
date:   2017-10-05 02:53:36 -0700
categories: Angular
---
## Generate a problem-detail component

1. `ng g c problem-detail`

It auto adds selector into 'app.module.ts

2. Add its selector to view 'app.component.html' to show the new component
```html
<app-problem-list />
<app-problem-detail />
```
## Angular Router

Client side routing: use 'angular-router' which is Angular's routing library.

1. Create a ts file `app.routes.ts`

2. Import Angular Router

```ts
import { Routes, RouterModule } from "@angular/router";
```

3. Define the url path and its matching component. 
```ts
const routes: Routes = [
 {
     path: '',
     redirectTo: 'problems',
     pathMatch: 'full'  // 100% match
 },
 {
     path: 'problems',
     component: ProblemListComponent
 },
 <!-- pass a value  -->
 {
     path: 'problems/:id',
     component: ProblemDetailComponent
 },
 <!-- all other non-hit url: error expression -->
 {
     path: '**',
     redirectTo: 'problems'
 }
];
```
As some paths directs to problem-list or problem-detail component, we need to import them.
```ts
import { ProblemListComponent } from './components/problem-list/problem-list.component';
import { ProblemDetailComponent } from './components/problem-detail/problem-detail.component';

```

4. export routing
```ts
export const routing = RouterModule.forRoot(routes);
```
5. Add routing modulein to 'app.module.ts'
```ts
import { routing } from './app.routes';

@NgModule({
...
  imports: [
    BrowserModule,
    routing
  ],
...
```
 
Note: router/brower/ng is a module, added to `imports`; component is added to `declarations`; service is added to `provider`.

## Render router in 'app.component.html'
```html
<router-outlet></router-outlet>
```


## Add router into a view (add it to its container)
 
RouterLink: one-way binding. 
Add router to view ('problem-detail.component.html'):
```html
...
    <a class="list-group-item" *ngFor="let problem of problems"
     [routerLink]="['/problems', problem.id]">
...
```

## Render problem in 
1. import  mock data
```ts
import { Problem } from 'app/data-structure/problem';
```
Only one problem:
```ts
...
export class ProblemDetailComponent implements OnInit {
  problem: Problem;
...
```
2. Write view (problem-detail.component.html):
```html
<!-- ngIf: render only when problem exists -->
<div class = "container" *ngIf = "problem">
<!-- responsive -->
  <div class="col-xs-12 col-md-4">
    <h2>
      {{problem.id}}. {{problem.name}}
    </h2>
    <p>
      {{problem.desc}}
    </p>

  </div>
</div>
```
3. call 'getProblem()' to retrieve data.

Import Angular's libaray to allow data passing"
```ts
import { ActivatedRoute, Params } from '@angular/router';
```
4. Inject service.
```ts
  constructor(
    private route: ActivatedRoute,
    @Inject('data') private data
  ) { }
```

5. Use 'Prams'to get problem.id and problem.name ('problem-detail.component.ts')
```ts

  ngOnInit() {
    this.route.params.subscribe((params: Params) => {
      this.problem = this.data.getProblem(+params['id']); // '+' sign can convert string to number. 
    })
  }

```


