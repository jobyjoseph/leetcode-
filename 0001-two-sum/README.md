# 1. Two Sum

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

 

**Constraints:**

- 2 <= `nums.length` <= 10<sup>4</sup>
- -10<sup>9</sup> <= `nums[i]` <= 10<sup>9</sup>
- -10<sup>9</sup> <= `target` <= 10<sup>9</sup>
- **Only one valid answer exists.**

 
Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

# Solutions

## 1. Brute force approach

```javascript
var twoSum = function(nums, target) {
    // first loop to track first index
    for(let i = 0; i < nums.length; i++) {
        // second nested loop to track second index
        for(let j = i + 1; j < nums.length; j++) {
            let sum = nums[i] + nums[j];
            if(sum === target) {
                return [i, j]
            }
        }
    }
};
```
Time complexity is **O(n<sup>2</sup>)** because there is a nested for loop.

Space complexity is **O(1)** because as the input array size increases, the memory used by the program is not increasing.

<img src="./brute-force-performance.png" style="width: 600px" alt="Brute force performance"/>

## 2. Using Dictionary

```javascript
var twoSum = function(nums, target) {
    // set dictionary
    const hashSet = {}
    for(let i = 0; i < nums.length; i++) {
        hashSet[nums[i]] = i;
    }
    
    for(let j = 0;  j < nums.length; j++) {
        const remainingTarget = target - nums[j];
        if(hashSet[remainingTarget] && hashSet[remainingTarget] !== j) {
            return[j, hashSet[remainingTarget]]
        }
    }
};
```

Time complexity is **O(n)** as there are only 2 independent linear loops are running. A nested loop is not there.

Space complexity is **O(n)** because as the input array size increases, the used dictionary size also increases linearly.

<img src="./hashset-performance.png" style="width: 600px" alt="Hashset performance"/>

## 3. More optimized hash table

```javascript
var twoSum = function(nums, target) {
    var myMap = new Map();
    for( i=0; i<nums.length;i++){
        if(myMap.has(target-nums[i])){
            return [myMap.get(target-nums[i]),i]
        }
        else{
            myMap.set(nums[i],i)
        }
    }
    return []
};
```

We reduced to single loop. Also we are not waiting for the complete hashtable to be constructed. Once the correct index is found, it is returned.

Time complexity is **O(n)** as there is still a loop.

Space complexity is **O(n)** because as the input array size increases, the used dictionary size also increases linearly.

<img src="./optimized-hashtable.png" style="width: 600px" alt="Optimized hashtable performance"/>