promise.markdown


ES6

let's define a promise:

```
new Promise( (resolve, reject) {
	
}

)

```


```
<!-- define a promise -->
var isMomHappy = false;

var willIGetNewPhone = new Promise(
    function (resolve, reject) {
        if (isMomHappy) {
            var phone = {
                brand: 'iPhone',
                color: 'red'
            };
            resolve(phone); // fulfilled
        } else {
            var reason = new Error('mom is not happy');
            reject(reason); // reject
        }
    }
);

<!-- call promise -->
var askMom = function() {
    willIGetNewPhone
        .then(function(fulfilled) {      // 'fulfilled' is the params passed from the phone of resolve(phone)
            // yay, you got a new phone
            console.log(fulfilled);
            // output: {brand: 'iPhone', color: 'red'}
        }, function(error) {
            // oops, mom didn't buy it 
            console.log(error.message);
            // output: 'mom is not happy'
        })
        <!-- you can add more .then -->
};

askMom();
```
It has two status, resolve and reject.

.then : use catch fucntion can also handle error messages.

rewrite the add funciton in promise
```
let r1, r2, r3;
function addAsync(num1, num2) {
    // use ES6 fetch API, which returns a promise. Below line is an simulated function, not a real addup.
    return fetch(`http://www.example.com?num1=${num1}&num2=${num2}`)
            .then(x => x.json());
}

addAsync(1, 2)
    .then(result => {
        r1 = result;
        return r1;
    })
    .then(success => addAsync(success, 3))
    .then(success => {
        r2 = success;
        return r2;
    })
    .then(success => addAsync(success, 4))
    .then(success => {
        r3 = success;
        return r3;
    })
    .then(success => {
        console.log('total: ' + success);
        console.log(r1, r2, r3);
    });
```

promise sleep usage
```
var sleep = function (ms) {
    var promise = new Promise(function (resolve, reject) {
        setTimeout(function() {
            resolve('haha');
        }, ms);
    });
    return promise;
};


sleep(2000)
    .then(function(result) {
        console.log(result);
    });

    // 2 seconds later, `haha` is printed
```

sleep all
```
Promise.all([sleep(1000), sleep(2000)])
    .then(function() {
        console.log('ALL done');
    });
```
sleep race
```
Promise.race([sleep(1000), sleep(5000)])
    .then(function() {
        console.log('Race is won!');
    });

```






