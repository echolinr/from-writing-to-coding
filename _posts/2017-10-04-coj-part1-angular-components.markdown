---
layout: post
title:  "First Angular Component "
date:   2017-10-04 21:53:36 -0700
categories: Angular
---

## Generate Angular components

To generate a components named "problem-list" under `src/app/components` directory: `ng g c problem-list`
* `g` stands for generate;
* `c` is for component.
* `it`: inline template;
* `is`: inline style, no css file generated

It creates four files:
* x.component.css   -- Style
* x.component.html  -- View
* x.component.spec.ts   -- Test
* x.component.ts -- Control

It also updates `app.module.ts`, which is in bootfile because in `main.ts`, `bootstrap(app.module)` specifies that the bootfile is `app.module`.

All Angular components must be added into `declaration` list of app.modules.ts if it wants to be loaded.

Now let's take a look at the new component.ts file:
each component has
1. selector - component
2. templateUrl - html
3. styleUrl - css

```ts
Component({
  selector: 'app-problem-list',
  templateUrl: './problem-list.component.html',
  styleUrls: ['./problem-list.component.css']
})
```

Put problem list selector into 'app.compoennet.html':
```html
<app-problem-list><app-problem-list/>
```

## Create a data structure (the problem schema)

Create a folder 'data-structure' and create 'problem.ts':

In this typescript file, define problem schema:
```typescript
export class Problem {
    id: number;
    name: string;
    desc: string;
    difficulty: string;
}
```

## Add a var in class

Go to `problem-list.component.ts`, import { Problem}  from `problem.ts`.
Add a variable 	`problem` of Schema Problem.

```ts
export class ProblemListComponent implements OnInit {
  problems: Problem[];
  ...
```
## Create some dummy data

Create a file containing dummy data: an array which contains five problems. Call it `mock-problems.ts`.
Note: remember to export module.
```ts
import { Problem } from './data-structure/problem';
export const PROBLEMS: Problem[] = [
  {
    id: 1,
    name: "Two Sum",
    desc:

	...
    id: 5,
	name: "..."
	desc: `Given an array of n integer with duplicate number, and a moving window(size k), move the window at each iteration from the start of the array, find the maximum number inside the window at each moving.`,
    difficulty: "super"
  }
];
```
To process the data, we need service. You need to see the next post for service generation.

## View: create a list

We want to create a table format list. let's go to boostrap and copy a list-group component.
```html
<div class="container">
  <div class="list-group">
    <a class="list-group-item" >
		Cras justo odio
    </a>
  </div>
</div>
```
## What does `export` mean?
If you others need to call a class in a call, you need to export the class.
Other files can call data in another file. if you don't want a file content to be used, just do not write export, then external files cannot import its data.

## use {{ }} to call params in javascript file.
For example, {{problem.difficulty}}


## `ngFor`: render item in a list/array
`ngFor` is Angular's for loop. It trasverses each item in an array.
The syntax is:
`*ngFor = "let problem of problems"` problem is the self-defined name to present each item in this array.
`problem.desc` is the description value of a problem.

This gets every item in problem array. if you print `problem.id`, it gives you their id one by one.`problem.desc` is the description value of a problem.

## add styles to the list
I do not show css here. Just import and copy some from bootstrap.
'pull-left label difficulty diff-' + easy or medium or hard is a data-binding (due to Angular)
```html
<div class="container">
  <div class="list-group">
    <a class="list-group-item" *ngFor="let problem of problems">
      <span class="{{'pull-left label difficulty diff-' + problem.difficulty.toLocaleLowerCase()}}">
        {{problem.difficulty}}
      </span>
      <strong class="title">{{problem.id}}. {{problem.name}}</strong>
    </a>
  </div>
</div>

```



## install and add bootstrap

1. add with CDN

To use CDN link, add the link address to `index.html`. Be careful, a production project should not use CDN links as the link may become invalid.

2. or `npm install bootsrap@3 --save`
with `--save`, you can add this dependency to package.json


Boostrap uses jQuery to support animation. we need to `npm install jquery`.


3. add bootstrap and jquery to stypes and script.
* Open file: `/angular-cli.json`

* Add css file to styles[]
```ts
      "styles": [
        "styles.css",
        "../node_modules/bootstrap/dist/css/bootstrap.min.css"
      ],
```
* Add javascript files to script[]
```ts
      "scripts": [
        "../node_modules/jquery/dist/jquery.js",
        "../node_modules/bootstrap/dist/js/bootstrap.js"
      ],
```
jquery must be located before bootstrap as it is bootstrap's dependency.



## Run serve

`ng serve`
`ng serve` === `npm start`, refer to package.json
```json
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```
