---
layout: post
title: Contains Duplicate
date: 2026-09-22 18:19:21 -0300
---
### Contains Duplicate

Here we go again, grinding some LeetCode problems :))

Today we are going to solve the Contains Duplicate problem:
https://leetcode.com/problems/contains-duplicate/

Basically, we need to find out if the array contains a duplicate.

```ts
Input: nums = [1,2,3,1]
Output: true
```

At first, I thought that the obvious approach would be to compare each number with the others.

Something like:

```ts
for (let i = 0; i < nums.length; i++){
    for (let j = 0; < nums.length; j++){
        //compare nums[i] with nums[j]
    }
}
```
The problem with this approach is that we may end up comparing many elements with each other, resulting in O(n²) time complexity.

So instead of comparing the numbers against each other, We can use a Set to keep track of the numbers I have already seen.

`const set = new Set<number>();`

As I iterate throught the array, I check wherer the current number already exists in the set.

If it does, I know that i found a duplicate and can immediately return `true`.

If it does not, I add the number to the set and continue.

Like this:

```ts
for (let i = 0; i < nums.length; i++) {
    if (set.has(nums[i])){
        return true;
    }
    set.add(nums[i]);
}
```

So, I am still iterating throught the array, but only once.

The important difference is that I am no longer comparing each number with every other number.

The Set gives me an way to check whether I have already seen a value.

___
<br>

### Tracing through an example:

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

So we return `true` because we found a duplicate.

Notice that in this particular example, we **did iterate through the entire array**.

However, we don't necessarily have to.

For example:

```js
nums = [1,2,1,3,4,5]
```

The algorithm would stop at the second `1`:

```text
1 → add
2 → add
1 → already exists → return true
```

We never need to check `3`, `4`, or `5`.

This means the algorithm can stop early when a duplicate is found, but in the worst case it still needs to iterate through the entire array.

The important improvement is that we reduced the time complexity from **O(n²)** to **O(n)**.

___
<br>

### Solution

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
