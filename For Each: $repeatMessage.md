> Before you can use any type of loops, you need to learn [how to escape code](../main/Escaping.md).

> Note: \
> This example is limited to 100 items at most. Change the `$repeatMessage`s to increase the limit to your need.

You should memorize this code.
```js
$textSplit[<LIST>;<SEPARATOR>]
$var[a;$cropText[$repeatMessage[10;$repeatMessage[10;a]];$getTextSplitLength]]
$eval[$replaceText[$var[a];a;<ESCAPED_CODE>]]
```
- Replace `<LIST>` with a list. (Example: `1, 2, 3`)
- Replace `<SEPARATOR>` with the separator. (Example: `, `)
- Replace `<ESCAPED_CODE>` with your escaped code.

The first item of the list is going to be `$splitText[1]`, the second is going to be `$splitText[2]`, etc., so you need to use a variable in your escaped code to know which item of the list you’ll be dealing with, and in this example, I’ll name that variable `i`.

To increase the value of the variable for each iteration, you might try something like this:
```js
$var[i;$sum[$var[i];1]]
```
But when `i` isn’t defined yet, using `$var[i]` will return nothing, and `$sum[;1]` will throw an error, so you can add a little zero behind `$var[i]` to fix this issue.
```js
$var[i;$sum[0$var[i];1]]
```
So each time this code gets executed, it’s something like `$sum[0;1]`, `$sum[01;1]`, `$sum[02;1]`, etc.

Example code:
```js
$var[code;
    %{DOL}%var[i\;%{DOL}%sum[0%{DOL}%var[i\]\;1\]\]
    %{DOL}%sendMessage[%{DOL}%splitText[%{DOL}%var[i\]\]\]
]

$textSplit[1 - 2 - 3; - ]
$var[a;$cropText[$repeatMessage[10;$repeatMessage[10;a]];$getTextSplitLength]]
$eval[$replaceText[$var[a];a;$var[code]]]
```
Output:
```js
1
2
3
```

# Actual usage example
Here is a code for converting a list of IDs to a list of usernames:
```js
$var[code;
    &var[i\;&sum[0&var[i\]\;1\]\]
    &var[c\;&splitText[&var[i\]\]\]
    &var[d\;&discriminator[&var[c\]\]\]

    &if[&var[d\]==0\]
        &sendMessage[@&username[&var[c\]\]\]
    &else
        &sendMessage[&username[&var[c\]\]#&var[d\]\]
    &endif
]

$var[code;$replaceText[$var[code];&;$]]

$textSplit[00000000000000000 11111111111111111 22222222222222222; ]
$var[a;$cropText[$repeatMessage[10;$repeatMessage[10;a]];$getTextSplitLength]]
$eval[$replaceText[$var[a];a;$var[code]]]
```
Output:
```js
@example
Example#0000
Example#1234
```

# Credits
[@Kurito](https://github.com/Kourito) told me about this.
