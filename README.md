# rs-style-monads-ts
> Rust style monads in Typescript

# Option
Sometimes called `Maybe` in other languages. [Maybe](https://hackage.haskell.org/package/base-4.17.0.0/docs/Data-Maybe.html) a => <Nothing, Just a>

```typescript
import * as O from './option';

const a = O.Some(2);
console.log(O.isSome(a)) // true

const b = O.Some(5);
console.log(O.map(arr, (a) => a * 2)); // { _tag: 'Some', value: 10 }

```
## Methods
- isSome
- isNone
- unwrapOrDefault 
- map
- mapOrElse

# Result
Sometimes called `Either` in other languages. [Either](https://hackage.haskell.org/package/base-4.17.0.0/docs/Data-Either.html) a b => <Left a, Right b>

```typescript
import * as R from './result'

// before
export const main = () => {
  try {
    const a = "abc"; // enter the some str
    const b = f(a);
    let c;
    try {
      c = g(b);
    } catch (error) {
      c = 3;
    }
    const d = h(c);
    program(d); // true or false
  } catch (error) {
    handleError(error); // error handling
  }
};

// after
const main = () => {
  const a = "test"; // enter the some str
  const b = f(a);
  const c = R.flatMap(b, (b_) => R.ok(R.unwrapOrDefault(g(b_), (e) => 3)));
  const d = R.flatMap(c, (_c) => h(_c));
  const result = R.map(d, (_d) => program(_d)); // true or false
  R.unwrapOrDefault(result, (e) => handleError(e)); // error handling 
};
```

## Methods (exists in rust)
- isOk 
- isErr
- unwrapOrDefault
- unwrapOrElse
- map
- mapOrElse

## Ts Methods (Not exists in rust)
- keepOk
- flat
- flatMap

# Rust Reference 
- [Option](https://doc.rust-lang.org/std/option/enum.Option.html#)
- [Result](https://doc.rust-lang.org/std/result/enum.Result.html#)