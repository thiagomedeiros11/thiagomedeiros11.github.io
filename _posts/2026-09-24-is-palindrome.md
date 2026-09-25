---
layout: post
title: Is Palindrome
date: 2026-09-24 20:02:21 -0300
---

Hiho

Let's solve another LeetCode problem today.
https://leetcode.com/problems/valid-palindrome

The name is Valid Palindrome.

First, we need to understand what the heck a palindrome even is XD

With a quick search on Wikipedia:

Palindrome:
A word, sentence, or number that remains the same when read backwards

Examples:
ovo
radar
arara

Seems kinda simple, right?

I have to look at the first and the last characters.

Here's a quick example:

`Input: s = "arara";`

I can use two pointers:

```ts
let left = 0; // first character
let right = s.length - 1;   // s.length = 5, so that's why - 1
```

```ts
a  rar  a
/\     /\
left / right
```

I iterate over the string with a while loop, comparing the last index with the first one, as long as `left < right`.

```ts
while(left < right) {
    if(s[left] !== s[right]){
        return false;
    }
    right--; // move the right pointer one character to the left
    left++;  // move the left pointer one character to the right
}
```

___
<br>
Loop 1:

```ts
while left < right
s = arara
left = 0
right = 4

s[left] = a
s[right] = a

s[left] !== s[right] // false

right--; // 3
left++;  // 1

left = 1
right = 3
```

___
<br>
Loop 2:

```ts
s = arara
left = 1
right = 3

s[left] = r
s[right] = r

s[left] !== s[right] // false

right--; // 2
left++;  // 2

left = 2
right = 2
```

___
<br>
Loop 3:

```ts
while left < right // breaks the while since left is not < right anymore
```

At that point, there's no need to check the middle character.
Reading it backwards will still result in the same palindrome.

So I return `true`.

___
<br>
So the problem is solved, right? WRONGGG

If we have an input like this:

`Input: s = "A man, a plan, a canal: Panama"`

Our algorithm will fail, because now we have commas and spaces.

We can see that the input is still a palindrome after removing the commas and spaces:

`amanaplanacanalpanama`

To clean up the string, we'll need the beauty of the feared regex :)))

The goal is to remove spaces, remove commas, and transform everything to lowercase with the `.toLowerCase()` method.

`(/[^a-z0-9]/gi, "")`

That's exactly what we need. Let's break it down to understand better.

Regex Breakdown:
`/ /` -> delimits the regular expression

`[]` -> defines a set of characters

`^` -> means NOT when used as the first character inside []

`a-z` -> between a and z

`0-9` -> between 0 and 9

`g` -> global, searches every occurrence, not just the first

`i` -> ignores uppercase and lowercase

`""` -> replaces the matches with an empty string, effectively removing them

Now we have the complete solution for this challenge:

### Solution
<br>

```ts
function isPalindrome(s: string): boolean {

    let value = s.replace(/[^a-z0-9]/gi, "").toLowerCase();
    let left = 0;
    let right = value.length - 1;

    while (left < right){
        if(value[left] !== value[right]){
            return false;
        }

        right--;
        left++;
    }

    return true;
};
```
