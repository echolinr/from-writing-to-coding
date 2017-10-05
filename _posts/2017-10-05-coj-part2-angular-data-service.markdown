---
layout: post
title:  "First Angular Service"
date:   2017-10-05 01:53:36 -0700
categories: Angular
---

## Mock data file
Without any database, we use a mock data: a file.

Create `mock-problems.ts` which contains the problems array. I have covered this in the previous post.


## Create an Angular service

`ng g s data` generates a service named "data". Two files are created:
* data.service.ts
* data.service.test.ts
A new service module looks like this:
```ts
import { Injectable } from '@angular/core';
@Injectable()
export class DataService {
   constructor() { }
}
```

## Service must be provided in 'app.module.ts'

Go to app.module.ts
1. import dataservcie
2. provide: 
```ts
...
import { DataService } from './services/data.service';
...
@NgModule({
	...
  providers: [
    {
      provide: 'data',
      useClass: DataService
    }
  ],
...
export class AppModule { }

```
## Write services

1. Import Problem schema and mock data
```ts
import { Problem } from '../data-structure/problem';
import { PROBLEMS } from '../mock-problems';

@Injectable()
export class DataService {
  problems: Problem[] = PROBLEMS;
  constructor() { }
}
```
2. Write 'getProblems' and 'getProblem(id)' function/service:
```ts
  constructor() { }

  getProblems(): Problem[] {
    return this.problems;
  }
  getProblem(id: number): Problem {
    return this.problems.find( (problem) => problem.id === id);
  }
```

## Service must be injected into component
In `problem-list.component.ts`: call data.service
1. {Inject} from angular/core:
```ts
import { Component, OnInit, Inject } from '@angular/core';
```
2. pass service into constructior
```ts
constructor(@Inject('data') private dataService) { }
```
3. pass service's function to component's ngOnit function

```ts
  ngOnInit() {
    this.getProblems();
  }

  getProblems(): void {
    this.problems = this.dataService.getProblems();
  }
```



