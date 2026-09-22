---
layout: post
title: Contains Duplicate
date: 2026-09-22 18:19:21 -0300
---
### Contains Duplicate
<br>
Here we go again, grinding some LeetCode problems :))

Today we are going to solve the Contains Duplicate problem:
https://leetcode.com/problems/contains-duplicate/

Basically, we need to find out if the array contains a duplicate.

```ts
Input: nums = [1,2,3,1]
Output: true
```

So, obviously like the previous problems, it is not the best approach to iterate through the entire array.

And unlike the other problems we solved, this time I do not need to worry about the index, just the value itself.

After a quick search, I found out that we can use a set.

`const set = new Set<number>();`

We can gradually save the numbers in the set, but if `set.has` returns that the number already exists in the set, we know we have a duplicate.

Like this:

```ts
for(let i = 0; i < nums.length; i++){
	if(set.has(nums[i])){
		return true
	}
	set.add(nums[i]);
	}
```

Here we are saying to the set: is `nums[i]` in the set? No? Then store it in the set.

___
<br>
Tracing through an example:

```js
nums = [1,2,3,1]

loop 1
i = 0
nums[i] = 1
set = {}
set.has(1) // false
set.add(1)

loop 2
i = 1
nums[i] = 2
set = {1}
set.has(2) // false
set.add(2)

loop 3
i = 2
nums[i] = 3
set = {1,2}
set.has(3) // false
set.add(3)

loop 4
i = 3
nums[i] = 1
set = {1,2,3}
set.has(1) // true
```

So we return `true` because we have a duplicate.

If none of the numbers exist in the set after checking all of them, we return `false`.

___
<br>
### Solution
<br>
```ts
function containsDuplicate(nums: number[]): boolean {
    const set = new Set<number>();

    for (let i = 0; i < nums.length; i++) {
        if (set.has(nums[i])) {
            return true;
        }

        set.add(nums[i]);
    }

    return false;
}
```
