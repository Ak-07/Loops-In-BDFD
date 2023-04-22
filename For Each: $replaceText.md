> Before you can use any type of loops, you need to learn [how to escape code](..).

You should memorize this code.
```js
$textSplit[<ESCAPED_CODE>;<ELEMENT>]
$eval[$splitText[1]$replaceText[<LIST>;<INPUT_SEPARATOR>;$splitText[2]<OUTPUT_SEPARATOR>$splitText[1]]$splitText[2]]
```
- Replace `<ESCAPED_CODE>` with your escaped code.
- Replace `<ELEMENT>` with whatever text you wanted.
- Replace `<LIST>` with a list. (Example: `1, 2, 3`)
- Replace `<INPUT_SEPARATOR>` with the separator. (Example: `, `)
- Replace `<OUTPUT_SEPARATOR>` with what you want the outputs to be separated with.

Example code:
```js
$textSplit[Meow;Element]
$eval[$splitText[1]$replaceText[1, 2, 3;, ;$splitText[2] - $splitText[1]]$splitText[2]]
```
Output:
```js
Meow - Meow - Meow
```

#

What the `<ELEMENT>` option means:
If you replace `<ELEMENT>` with `Test`, then you can use the word `Test` in your escpaed code to “get” the current item of the list.

Example code:
```js
$textSplit[<Test>;Test]
$eval[$splitText[1]$replaceText[1, 2, 3;, ;$splitText[2] - $splitText[1]]$splitText[2]]
```
Output:
```js
<1> - <2> - <3>
```

#

⚠️ You can’t use the `<ELEMENT>` keyword more than once in your escaped code.

Example code:
```js
$textSplit[<Test/Test>;Test]
$eval[$splitText[1]$replaceText[1, 2, 3;, ;$splitText[2] - $splitText[1]]$splitText[2]]
```
Expected output:
```js
<1/1> - <2/2> - <3/3>
```
Actual output:
```js
<1/ - <2/ - <3/
```

#

You can fix this by making a variable for your current element:
```js
$textSplit[%{DOL}%var[c\;Element\]<%{DOL}%var[c\]/%{DOL}%var[c\]>;Element]
$eval[$splitText[1]$replaceText[1, 2, 3;, ;$splitText[2] - $splitText[1]]$splitText[2]]
```
Output:
```js
<1/1> - <2/2> - <3/3>
```

# Actual usage example
Here is a code for converting a list of IDs to a list of usernames:
```js
$var[n;$url[decode;%0A]] $c[<== THIS IS A NEW LINE CHARACTER]

$var[list;1234567890123456789 2345678901234567890 3456789012345678901]

$textSplit[%{DOL}%var[c\;Element\]%{DOL}%try%{DOL}%username[%{DOL}%var[c\]\]#%{DOL}%discriminator[%{DOL}%var[c\]\]%{DOL}%endtry;Element]
$eval[$splitText[1]$replaceText[$var[list]; ;$splitText[2]$var[n]$splitText[1]]$splitText[2]]
```
Output:
```js
User#0000
User#0000
User#0000
```
