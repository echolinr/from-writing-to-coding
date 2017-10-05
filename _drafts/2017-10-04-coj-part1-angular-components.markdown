---
layout: post
title:  "Angular Component"
date:   2017-10-04 21:53:36 -0700
categories: Angular
---

## Generate Angular components

generate a components named "problem-list" under `src/app/components` directory:

`ng g c problem-list`

It creates four files:

and updates app.module.ts

main.ts bootstrape(app.module) is the start

all componets must be added into declaration list of app.modules.ts if it wants to be loaded.

each component has
1. selector
2. templateUrl
3. styleUrl


Put problem list selector into app.compoennet.html, the it shows problem-list.html

#create a problem structure/schema
create a folder `data-structure` and create `problem.ts`

In this ts file, define problem schema:
export class Problem {
	 id:
	 name:
	 desc:
	 difficulty:
}


go to problem-list.component.ts, import Problem from `problem.ts`, and define a var problems: use Problem[] array

#Create some dummy data

create an array which contains five problems.

const PROBLEMS = [

]


# View: edit html file
we want to create a table format list. let's go to boostrap and copy a list-group component.

```html

```

export meaning:

Other files can call data in another file. if you don't want a file content to be used, just do not write export, then external files cannot import its data.


#ngFor

trasverse each item in an array. 
`*ngFor = "let problem of problems"`
this gets every item in problem array. if you print `problem.id`, it gives you their id one by one.

#add styles to the list

#use {{ }} to call params in javascript file.
e.g. use 


#add bootstrap

add with CDN
or `npm install bootsrap@3 --save`
 with `--save`, you can add this dependency to package.json

boostrap uses jQuery to bulid animation. we need to `npm install jquery`


#add bootstrap and jquery to stypes and script.
file: `/angular-cli.json`

css file to styles[]
.js files to script[]


ng serve === npm start, refer to package.json

to use CDN link, add the link address to `index.html`. Be careful, a production project should not use CDN links as the link may become invalid.





`it` inline test
`is` inline style