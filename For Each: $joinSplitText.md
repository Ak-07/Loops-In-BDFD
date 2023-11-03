> Before you can use any type of loops, you need to learn [how to escape code](../main/Escaping.md).

You should memorize this code.
```js
$textSplit[<ESCAPED_CODE>;<ELEMENT>]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;<LIST>];$url[encode;<INPUT_SEPARATOR>]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2]<OUTPUT_SEPARATOR>$var[1]]$var[2]]]
```
- Replace `<ESCAPED_CODE>` with your escaped code.
- Replace `<ELEMENT>` with whatever text you wanted.
- Replace `<LIST>` with a list. (Example: `1, 2, 3`)
- Replace `<INPUT_SEPARATOR>` with the separator. (Example: `, `)
- Replace `<OUTPUT_SEPARATOR>` with what you want the outputs to be separated with.

Example code:
```js
$textSplit[Meow;Element]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;1, 2, 3];$url[encode;, ]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2] - $var[1]]$var[2]]]
```
Output:
```js
Meow - Meow - Meow
```

#

What the `<ELEMENT>` option means: \
If you replace `<ELEMENT>` with `Test`, then you can use `%{DOL}%url[decode\;Test\]` in your escpaed code to “get” the current item of the list. So if `<ELEMENT>` is replaced with `Meow` then the code `%{DOL}%randomText[%{DOL}%url[decode\;Meow\]\;UwU\]` will replace some items of the list with “UwU” without changing the other items.

Example code:
```js
$textSplit[<%{DOL}%url[decode\;Test\]>;Test]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;1 - 2 - 3];$url[encode; - ]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2]...$var[1]]$var[2]]]
```
Output:
```js
<1>...<2>...<3>
```

#

:warning: You can’t use `<ELEMENT>` more than once in your escaped code.

Example code:
```js
$textSplit[<%{DOL}%url[decode\;Test\]/%{DOL}%url[decode\;Test\]>;Test]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;1, 2, 3];$url[encode;, ]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2] - $var[1]]$var[2]]]
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

This can be fixed by storing the current item in a variable:
```js
$textSplit[%{DOL}%var[c\;%{DOL}%url[decode\;Element\]\]<%{DOL}%var[c\]/%{DOL}%var[c\]>;Element]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;1, 2, 3];$url[encode;, ]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2] - $var[1]]$var[2]]]
```
Output:
```js
<1/1> - <2/2> - <3/3>
```

# Actual usage example
Here is a code for converting a list of IDs to a list of usernames:
```js
$var[n;$url[decode;%0A]] $c[// %0A is a new-line character.]
$var[list;00000000000000000 11111111111111111 22222222222222222]

$textSplit[%{DOL}%var[c\;%{DOL}%url[decode\;?\]\]%{DOL}%var[d\;%{DOL}%discriminator[%{DOL}%var[c\]\]\]%{DOL}%replaceText[%{DOL}%if[%{DOL}%var[d\]==0\]@.%{DOL}%else.#%{DOL}%var[d\]%{DOL}%endif\;.\;%{DOL}%username[%{DOL}%var[c\]\]\];?]
$var[1;$splitText[1]]
$var[2;$splitText[2]]

$textSplit[$url[encode;$var[list]];$url[encode; ]]
$url[decode;$eval[$var[1]$joinSplitText[$var[2]$var[n]$var[1]]$var[2]]]
```
Output:
```js
@example
Example#0000
Example#1234
```
