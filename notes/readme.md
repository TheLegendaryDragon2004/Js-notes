# Important things about js  

## Behaviour 1  
```js
const obj1 = {first: 20, second: 30, first: 50};
```

Answer: {first: 50, second: 30}

Explanation: In JavaScript object literals, if you define a property key more than once, the last value assigned to that key will be its final value. The first declaration first: 20 is overwritten by the later declaration first: 50.
