---
layout: post
title: Valid Anagram
date: 2026-09-19 14:29:02 -0300
---
### Valid Anagram
<br>
In this challenge we receive 2 strings, `s` and `t`, and need to return `true` if `t` is an anagram of `s`, and `false` otherwise.

First of all, we need to understand what an anagram is.

After a quick search, Wikipedia says it's a word game where you rearrange the letters of one word or expression to produce another word or expression.

An example in English:

listen
silent

Both have the same letters, just rearranged.

Alright, now we know what an anagram is. Back to the problem.

___
<br>
Looking at example 1:

```ts
input: s = "anagram", t = "nagaram"
output: true
```

We can already spot the first pattern: if the strings have different lengths, it's impossible to be an anagram, so we can start there.

```ts
if(s.length !== t.length){
	return false
}
```

From this point on, we're only dealing with strings that have the same length.

After that, the second pattern becomes clear. For two strings to be anagrams, the count of each letter in `s` and `t` must be equal. If the counts are different, it's not an anagram.

So I need a data structure that can store each letter and how many times it appears. For that, we can start with an empty object.

```ts
countS = {};
```

Now I want to loop through all the characters in `s` to see how many times each one appears.

```ts
for(let i = 0; i < s.length; i++){
	countS[s[i]] = (countS[s[i]] || 0) + 1;
}
```

Imagine the empty object:

```ts
{}
```

When we access `countS[s[i]]` with `s = "anagram"`, we're accessing the key `s[i]`, or `s[0]` which is `a`.

```ts
{a: }
```

That's what we have at that point. 

But when we do `(countS[s[i]] || 0) + 1`, we're getting the current value stored under the key `a`. 

Since `a` doesn't exist yet, it returns `undefined`.

`|| 0` means: if the current value is falsy, use 0.

`+ 1` at the end gives us `0 + 1 = 1`.

So we end up with:

```ts
{a: 1}
```

On the second loop iteration, it's easier to follow.

```ts
s = "anagram"
{a: 1}
i = 1
s[i] = n
```

So the assignment creates a new entry in our object.

```ts
{a: 1, n: }
```

The key is `n`, and its value will be `(countS[s[i]] || 0) + 1`. We don't have `n` yet, so we hit the `|| 0` part. Then `0 + 1 = 1`.

```ts
{a: 1, n: 1}
```

We do that for every letter in `s`, finishing with:

```ts
countS = {
	a: 3,
	n: 1,
	g: 1,
	r: 1,
	m: 1
}
```

Now we know exactly what we have in `s`.

___
<br>
Now let's look at `t`.

Since `t` needs to have the same amount of each letter as `s`, we can take the opposite approach: for each letter in `t`, we decrease the count in `countS`.

Found an `a` in `t`? So `a: 3 - 1 = a: 2`. We do that for every letter.

If we can decrease the count for every letter in `t` without hitting the `if`, then both strings have the same letter counts and are anagrams.

```ts
for(let i = 0; i < t.length; i++){
	if (!countS[t[i]]) {
		return false;
	}
	countS[t[i]]--;
}
```

We loop through all letters in `t` and use the `if` to check `countS[t[i]]`.

```ts
t = "nagaram"
countS = {
	a: 3,
	n: 1,
	g: 1,
	r: 1,
	m: 1
}
i = 0
t[i] = n
countS[t[i]] = 1
```

So we decrease the value:

```ts
countS[t[i]]--;
```

```ts
countS = {
	a: 3,
	n: 0,
	g: 1,
	r: 1,
	m: 1
}
```

But if we enter the `if(!countS[t[i]])` condition, it means there are no occurrences of that letter left in `countS`. Either the letter doesn't exist, or its count already reached 0. In either case, it's not an anagram.

So we `return false`.

If we never hit the `if`, we exit the loop and reach `return true`, because every character in `t` had a matching count in `s`.

### Solution:

```ts
function isAnagram(s: string, t: string): boolean {

    if (s.length !== t.length){
        return false;
    }

    let countS = {};

    for(let i = 0; i < s.length; i++){
        countS[s[i]] = (countS[s[i]] || 0) + 1;
    }

    for (let i = 0; i < t.length; i++){
        if(!countS[t[i]]){
            return false;
        }
        countS[t[i]]--;
    }
    return true;
};
```

___
<br>
I'm sure there are other solutions (probably better ones), but that's how I got to the other side :))

We finish the challenge with a time complexity of `O(n)`.

cyaaa
