# ECMAScript proposal: Class instantianting using generic type
- [Motivation](#motivation)
- [High-level API](#high-level-api)
- [FAQ](#faq)

## Motivation

The main idea of this proposal is adding support for class instantianting using generics (Generic type is used as constructor) and also providing type constraint;
Such feature makes sense when we have more than 2 classes and we don't want to duplicate similar instance create methods. Approach is useful when we perform reflection.

```js
	function createObj<T: new T()> () {
		return new T();
	}
	// or
	function createTwoObj<T: new T(), F: new F()> () { 
		return [
			new T, new F()
		]
	}

```
## High-level API

```js

class CoffeeCup {}

class DrinkFactory {
	static createDozensOfDrinks<T: new T()>(amount: number) {
		return Array(amount).fill(null)
			.map(() => new T());
	}
}

const coffeeCups = DrinkFactory.createDozensOfDrinks<CoffeeCup>(10);

```

```
