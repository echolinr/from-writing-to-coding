callback-js.markdown


```javascript
setTimeout(function() {
		console.log("hehe");
	}, 3000);
console.log("xxxx");
```

output"
```
xxxx
hehe
```
\'hehe\' is printed after 3000 ms. 

Callback is a function.
in the example about, 
```
function() {
		console.log("hehe");
	},
```
is a callback function.


Exmaple
```
function greet(callback) {
    console.log('Hello!');
    callback();
}

greet(function() {
    console.log('The callback is invoked!');
});

greet(function() {
    console.log('A different callback is invoked!');
});

```
output:
```
Hello!
The callback is invoked!
Hello!
A different callback is invoked!
```


// callback with feed parameter
```
function greet(callback) {
    console.log('Hello!');
    var data = {
        name: "Payson Wu"
    };
    callback(data);
}

greet(function(data) {
    console.log('The callback is invoked!');
    console.log(data);
});

greet(function(data) {
    console.log('A different callback is invoked!');
    console.log(data.name);
});
```
output:
```
Hello!
The callback is invoked!
{name: "Payson Wu"}
Hello!
A different callback is invoked!
Payson Wu
```


what if we have multiple callbacks inside callbacks,which creates a hooked evenets. 

```

let resultA, resultB, resultC;

function add(num1, num2) {
    return num1 + num2;
}

resultA = add(1, 2); // you get resultA = 3 immediately
resultB = add(resultA, 3); //you get resultB = 6 immediately
resultC = add(resultB, 4); // you get resultC = 10 immediately

console.log('total' + resultC);
console.log(resultA, resultB, resultC);


```


callback hell
A three callbacks
```
addAsync(1, 2, success => {
    // callback 1
    resultA1 = success; // you get result = 3 here

    addAsync(resultA1, 3, success => {
        // callback 2
        resultB1 = success; // you get result = 6 here
        
        addAsync(resultB1, 4, success => {
            // callback 3
            resultC1 = success; // you get result = 10 here

            console.log('total: ' + resultC1);
            console.log(resultA1, resultB1, resultC1);
        });
    });
});

```


A callback hell with more embedded callbacks
```
doSomethingAsync1(function() {
    doSomethingAsync2(function() {
        doSomethingAsync3(function() {
            doSomethingAsync4(function() {
                doSomethingAsync5(function() {
                });
            });
        });
    });
});
```


That is why we need promise.









