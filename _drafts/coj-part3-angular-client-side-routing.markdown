
# generate a problem-detail component

`ng g c problem-detail`

# add selector into `app.component.html`

#client side routing

use `angular-router` which is Angular's routing library.

create a router file `app.routes.ts`

Define the url path and its matching component. p
```app.routes.ts
const routes: Routes = [
 {
     path: '',
     redirectTo: 'problems',
     pathMatch: 'full'
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

#export routing



```
export const routing = RouterModule.forRoot(routes);
```

#add routing moduleinto app.module.ts

import routing

add it to `imports:[]`

Note: router/brower/ng is a module, added to `imports`; component is added to `declarations`; service is added to `provider`.

see app.moudle.ts:
```app.module.ts

@NgModule({
  declarations: [
    AppComponent,
    ProblemListComponent,
    ProblemDetailComponent
  ],
  imports: [
    BrowserModule,
    routing
  ],
  providers: [
    {
      provide: 'data',
      useClass: DataService
    }
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }

```
# add router into a view(add it to its container)

```app.component.html
<router-outlet></router-outlet>

```

add Angular Router to html. 

```
 [routerLink]="['/problems', problem.id]">
```


#render problem in newscard
import Problem

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


how to get problem.id and problem.name
use ActivedRoute and Pramas
```problem-detail.component.ts
import { ActivatedRoute, Params } from '@angular/router';


```


```

  ngOnInit() {
  	
    this.route.params.subscribe((params: Params) => {
      this.problem = this.data.getProblem(+params['id']);
    })
  }

```

