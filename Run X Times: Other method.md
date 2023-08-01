> Before you can use any type of loops, you need to learn [how to escape code](../main/Escaping.md).

You should memorize this code.
```js
$var[amount;<NUMBER_OF_TIMES>]

$async[code]
    <CODE_HERE>
$endasync

$var[x;$sum[1e$calculate[$var[amount]**0.125+1];-1]]
$eval[$repeatMessage[3;$$c[]var[x\;$$c[]replaceText[$$c[]var[x\]\;9\;$$c[]var[x\]\]\]]]
$eval[$replaceText[$cropText[$var[x];$var[amount];];9;$trimSpace[$await[code]]]]
```
- Replace `<NUMBER_OF_TIMES>` with a positive integer.
- Replace `<CODE_HERE>` with code.

Example code:
```js
$var[amount;696]

$async[code]
    $$c[]clear[100]
$endasync

$var[x;$sum[1e$calculate[$var[amount]**0.125+1];-1]]
$eval[$repeatMessage[3;$$c[]var[x\;$$c[]replaceText[$$c[]var[x\]\;9\;$$c[]var[x\]\]\]]]
$eval[$replaceText[$cropText[$var[x];$var[amount];];9;$trimSpace[$await[code]]]]
```
This code deletes the last 69,600 non-pinned messages sent in the last 2 weeks.

# Curious to know how it works?
I’ll write this section soon.
