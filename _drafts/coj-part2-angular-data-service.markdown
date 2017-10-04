coj-part2-angular-data-service.markdown

#mock data file
with no database, we use a mock data: a file.

create a `mock-problems.ts` which contains the problems array.
```
import problem class
exprot const PROBLEMS: Problem[]
 = [
 	{},
 	{},
 	{},
 	{}
 ]
 ```


#create an angular service

`ng g s data` generates a service named "data". Two files are created:
data.service.ts
data.service.test.ts


#service must be added as a provider

go to app.module.ts
1. import dataservcie
2. provide: 
```
	providers:[ { provide: 'data', userClass: ''}]
```


#service must be injected into component
{Inject} from angular/core
and
pass service into constructior

in `problem-list.component.ts`: call data.service