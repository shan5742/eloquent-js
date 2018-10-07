# Chapter 3 - Functions

### Defining a function

A function definition is simply a binding where the value of the binding is a function.

###### example
```js
const square = function(x) {
  return x * x;
};

console.log(square(12));
// → 144
```

A function can accept parameters, single, multiple or none at all, just like the examples below taken from Chapter 2 of the book.
```js
const makeNoise = function() {
  console.log("Pling!");
};

makeNoise();
// → Pling!

const power = function(base, exponent) {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
};

console.log(power(2, 10));
// → 1024
```
Sometimes a function will produce a value, but othertimes it won't and will produce a *side effect* just like the `makeNoise` function above.

A **return** statement determines the value the function returns. When control comes across such a statement, it immediately jumps out of the current function and gives the returned value to the code that called the function. A return keyword without an expression after it will cause the function to return *undefined*. Functions that don’t have a return statement at all, such as `makeNoise`, similarly return undefined.

Parameters to a function behave like regular bindings, but their initial values are given by the caller of the function, not the code in the function itself.

### Bindings & Scopes

All bindings have a **scope**, a binding that is made outside of a function is available anywhere in the program - *globally* if you like. However bindings that are made inside a function are only available in that function aka *locally*.

### Nested Scope

JavaScript distinguishes not just global and local bindings. Blocks and functions can be created inside other blocks and functions, producing multiple degrees of locality.

For example, this function—which outputs the ingredients needed to make a batch of hummus—has another function inside it:
```js
const hummus = function(factor) {
  const ingredient = function(amount, unit, name) {
    let ingredientAmount = amount * factor;
    if (ingredientAmount > 1) {
      unit += "s";
    }
    console.log(`${ingredientAmount} ${unit} ${name}`);
  };
  ingredient(1, "can", "chickpeas");
  ingredient(0.25, "cup", "tahini");
  ingredient(0.25, "cup", "lemon juice");
  ingredient(1, "clove", "garlic");
  ingredient(2, "tablespoon", "olive oil");
  ingredient(0.5, "teaspoon", "cumin");
};
```

The code inside the ingredient function can see the factor binding from the outer function. But its local bindings, such as unit or ingredientAmount, are not visible in the outer function.
