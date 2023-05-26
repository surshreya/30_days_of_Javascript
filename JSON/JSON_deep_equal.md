
## JSON Deep Equal

Given two objects ```o1``` and ```o2```, check if they are **deeply equal**.

For two objects to be ***```deeply equal```***, they must contain the **same keys**, and the associated values must also be deeply equal. Two objects are also considered deeply equal if they pass the ```===``` equality check.

You may assume both objects are the output of JSON.parse. In other words, they are valid JSON.

Please solve it without using lodash's ```_.isEqual()``` function.
 

**Example 1**
```bash
Input: o1 = {"x":1,"y":2}, o2 = {"x":1,"y":2}
Output: true
Explanation: The keys and values match exactly.
```

**Example 2**
```bash
Input: o1 = {"y":2,"x":1}, o2 = {"x":1,"y":2}
Output: true
Explanation: Although the keys are in a different order, they still match exactly.
```

**Example 3**
```bash
Input: o1 = {"x":null,"L":[1,2,3]}, o2 = {"x":null,"L":["1","2","3"]}
Output: false
Explanation: The array of numbers is different from the array of strings.
```

**Example 4**
```bash
Input: o1 = true, o2 = false
Output: false
Explanation: true !== false
```

### Constraints
- 1 <= JSON.stringify(o1).length <= 105
- 1 <= JSON.stringify(o2).length <= 105
- maxNestingDepth <= 1000

## Solution

```javascript
/**
 * @param {any} o1
 * @param {any} o2
 * @return {boolean}
 */
var areDeeplyEqual = function(o1, o2) {
    if(o1 === o2) return true;

    if(typeof o1 !== 'object' || typeof o2 !== 'object') return false;
    if(Array.isArray(o1) !== Array.isArray(o2)) return false;
    if(Object.keys(o1).length !== Object.keys(o2).length) return false;

    for(const key in o1) {
        if(!areDeeplyEqual(o1[key], o2[key])) return false;
    }

    return true;
};
```