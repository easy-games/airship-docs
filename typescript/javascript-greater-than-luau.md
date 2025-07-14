---
description: Equivalent JavaScript functions/libraries in the Airship Luau ecosystem.
---

# Javascript -> Luau

## About

Airship uses the [Luau Runtime](https://github.com/luau-lang/luau) to run scripts from the cloud. This means all TypeScript files are compiled to Luau instead of JavaScript and there are a few gotcha's when expecting a JavaScript function or library to exist. This page should help cover the conversion from JavaScript expectations to Luau.

### Console Logging

* `console.log` -> `print`
* `console.warn` -> `warn`
* `console.error` -> `error`

```typescript
print("Hello world");
print("anything", "can be", "listed", 10, true, false);

warn("This is a warning");

error("This is an error");
print("This won't print because the above error halted execution");
```

{% hint style="info" %}
Unlike in JavaScript, calling `error` will halt execution of the current Luau thread.
{% endhint %}

### Strings

The Luau [string](https://luau-lang.org/library#string-library) library is available for use. A few extra functions have been added to the string library to help it reach more equivalency to JavaScript:

* `string.trim(str)`
* `string.trimStart(str)`
* `string.trimEnd(str)`

{% hint style="info" %}
More string utils can be found in the `StringUtils` global.
{% endhint %}

### Math

Instead of the JavaScript `Math` library, the Luau [math](https://luau-lang.org/library#math-library) library is available.

```typescript
print(math.floor(32.5)); // -> 32
```

### ToString

Use the global `tostring()` function to convert any value to a string.

* `obj.toString()` -> `tostring(obj)`

```typescript
const num = 32.5;
const numAsStr = tostring(num);
```

### ParseInt and ParseFloat

In Luau, all numbers are treated as double floats. As such, there is only one equivalent function to parse values into numbers: `tonumber()`.

* `parseInt(value)` -> `tonumber(value)`
* `parseFloat(value)` -> `tonumber(value)`

```typescript
const n0 = tonumber("32");
const n1 = tonumber("40.5");

if (typeIs(n0, "number") && typeIs(n1, "number")) {
    print(n0 + n1) // 72.5
}
```

If the value cannot be converted to a number, `nil` is returned instead (which we can check as `undefined` in TypeScript).

### Null

The `null` value is not used in unity-ts. Instead, use `undefined`. In Luau, this is equivalent to `nil`.

### Throw

Throwing an exception is equivalent to calling the `error` function. Both compile down to the same Luau code.

```typescript
// Both equivalent:
throw "Some Error";
error("Some Error");
```

### Iterating custom objects and enums (Object.entries)

Arrays, Maps and Sets will work as expected and are handled by the compiler. Custom objects and enums however work differently.

In Luau, if we want to iterate over the keys/values of objects (e.g. get all the values of an enum) - we use the `pairs` function. Think of this like the Luau equivalent of `Object.entries`.

<pre class="language-typescript"><code class="lang-typescript"><strong>const obj = {
</strong><strong>    a: 10,
</strong><strong>    b: true,
</strong><strong>    c: "Hello, World!",
</strong><strong>}
</strong><strong>
</strong><strong>for (const [key, value] in pairs(obj)) {
</strong>    // key will be whatever the key type of the object is
    // value will be the value type of the given key on the object
}

export enum ExampleEnum {
    A,
    B,
    C,
}

for (const [key, value] of pairs(ExampleEnum)) {
    // key will be the name of the given enum item (a string)
    // value will be the value of the enum item (string or number, depending on enum)
}
</code></pre>

### for..in loops

for..in loops are not supported, you should refer to the above documentation for how to grab keys from objects

### Timeouts and Intervals

Luau's coroutine system is much different than the event loop found in JavaScript. The `task` library contains helpful functions for scheduling and spawning new Luau coroutine threads.

#### SetTimeout

Use `task.delay` to schedule a new thread to run in the future.

```typescript
task.delay(3, () => {
    print("Delayed 3 seconds");
});
```

Using `task.wait` will also cause a delay; however, it will yield the current thread for the number of seconds, rather than scheduling a new thread for the future.

```typescript
task.wait(3);
print("Delayed the current thread for 3 seconds");
```

#### SetInterval

There is no direct equivalent function to `setInterval`, but the behavior can be easily reproduced in a few different ways:

```typescript
// Custom setInterval function:
function setInterval(fn: Callback, interval: number) {
    return task.delay(interval, () => {
        while (true) {
            fn();
            task.wait(interval);
        }
    });
}

setInterval(() => {
    print("tick");
}, 3);
```

```typescript
// Simple interval loop:
const interval = 3;
task.spawn(() => {
    while (true) {
        task.wait(interval);
        // Foo
    }
});
```

### Clearing Timeouts and Intervals

Use `task.cancel` to stop a scheduled or already-running coroutine thread. All thread scheduling functions (`task.spawn/defer/delay`) return a "thread" object, which can be fed into the `cancel` function.

```typescript
const thread = task.delay(3, () => {
    print("Hello?");
});

// Immediately cancel the thread:
task.cancel(thread);
```

```typescript
const thread = task.spawn(() => {
    while (true) {
        doSomething();
        task.wait(1);
    }
});

// Stop the above loop after 3 seconds:
task.wait(3);
task.cancel(thread);
```

### JSON

* `JSON.parse` -> `json.decode`
* `JSON.stringify` -> `json.encode`

<pre class="language-typescript"><code class="lang-typescript"><strong>// Common JavaScript:
</strong><strong>const jsonString = JSON.stringify(anyObject);
</strong>const obj = JSON.parse(jsonString);

// Airship:
const jsonString = json.encode(anyObject);
const obj = json.decode(jsonString);
</code></pre>

Since JSON objects are inherently unknown in shape, `json.decode` will return an `unknown` type. If desired, a generic type can be used on the `decode` function, but note that this **does not** enforce the type.

```typescript
interface Hello {
    hello: string;
}

// Generic used as a type hint, but this does not cause any runtime type checking:
const obj = json.decode<Hello>(`{"hello": "world"}`);
print(obj.hello);
```

#### Empty Objects and Arrays

In Luau, the `table` type is used for both objects and arrays. While unity-ts lets you specify between various data structures (objects, arrays, maps, sets), they call compile down into Luau tables.

As such, `json.encode` cannot differentiate between an empty object and an empty array. Any empty structure will be encoded as an empty JSON array: `[]`.

```typescript
print(json.encode([])); // []
print(json.encode({})); // []
```

### Signed Bitwise operations

In short, bitwise operations will be equivalent to JavaScript's. However, this is different than what would usually be expected from Luau.

By default, any TypeScript bitwise operations go through the `sbit32` library. Luau ships with an unsigned `bit32` library, but signed bitwise operations mesh better within Unity, as C#'s bitwise operations are also signed.

In general terms, this means that bitwise operations should be expected to be equivalent to what you would already expect from JavaScript. However, if you are coming from a Luau background, please note the difference here.

The `bit32` and `sbit32` libraries can also be directly used if desired.

```typescript
print(19 | -3); // -1
print(sbit32.bor(19, -3)); // -1
print(bit32.bor(19, -3)); // 4294967295
```

### Passing a method to a function

In Luau, methods are handled quite differently to JavaScript. When you call a method, the calling object is passed as the first parameter implicitly (through `object:Method(...)`) or explicitly through `object.Method(object, ...)`.&#x20;

In unity-ts, if you try passing a method directly as an argument (e.g. `doThingWithAMethod(object.Method)`) you will end up with "Cannot index method without calling it!"

The best way to deal with this, is to explicitly "bind" a function to `object`

```typescript
// Simple "bound function", like JS' function.bind(object)
const boundFn = () => object.Method();
// and if you need to pass args:
const boundFnWithArgs = (value: string) => object.Method(value);
```

This will ensure that Luau will call it as a method attached to `object` when you call the bound function

### Other

All [Luau libraries](https://luau.org/library) are available for use.
