
##   Convert Object to JSON String

Given an object, return a valid JSON string of that object. You may assume the object only inludes strings, integers, arrays, objects, booleans, and null. The returned string should not include extra spaces. The order of keys should be the same as the order returned by Object.keys().

```Please solve it without using the built-in JSON.stringify method.```

**Example 1**
```bash
Input: object = {"y":1,"x":2}
Output: {"y":1,"x":2}
Explanation: 
Return the JSON representation.
Note that the order of keys should be the same as the order returned by Object.keys().
```

**Example 2**
```bash
Input: object = {"a":"str","b":-12,"c":true,"d":null}
Output: {"a":"str","b":-12,"c":true,"d":null}
Explanation:
The primitives of JSON are strings, numbers, booleans, and null.
```

**Example 3**
```bash
Input: object = {"key":{"a":1,"b":[{},null,"Hello"]}}
Output: {"key":{"a":1,"b":[{},null,"Hello"]}}
Explanation:
Objects and arrays can include other objects and arrays.
```

**Example 4**
```bash
Input: object = true
Output: true
Explanation:
Primitive types are valid inputs.
```

### Constraints
- object includes strings, integers, booleans, arrays, objects, and null
- 1 <= JSON.stringify(object).length <= 105
- maxNestingLevel <= 1000
- all strings will only contain alphanumeric characters

## Solution

***Using Divide and Conquer***
```javascript
/**
 * @param {any} object
 * @return {string}
 */
var jsonStringify = function(object) {
    if(object === null) return 'null';

    if(typeof object === 'string') return `"${object}"`;

    if(typeof object === 'number' || typeof object === 'boolean') 
        return`${object}`;

    if(Array.isArray(object)) {
        const nestedObj = object.map(ele => jsonStringify(ele));
        return `[${nestedObj.join(',')}]`;
    }

    if(typeof object === 'object') {
        const keys = Object.keys(object);
        const keyValue = keys.map(k => `"${k}":${jsonStringify(object[k])}`);
        return `{${keyValue.join(",")}}`;
    }
};
```
