# DataType Math

The API exposed to Airship contains data types from Unity such as (and not limited to) `Vector3`, `Vector2` and `Quaternion`.

Due to limitations with TypeScript, there is no operator overloading functionality.

To get around this and do mathematical operations on datatypes, the following methods are available where applicable:

* `a.add(b)` (a + b)
* `a.sub(b)` (a - b)
* `a.mul(b)` (a \* b)
* `a.div(b)` (a / b)

```typescript
const v1 = new Vector3(1,0,1);
const v2 = Vector3.up; //(0,1,0)
const v3 = v1.add(v2); //Equals (1,1,1)
```
