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
You can use `1eX-1` to get as many nines as you want, for example `1e3-1` is `999`, `1e4-1` is `9999`, etc., so you can replace the nines with code, then eval it. But the math functions have limits, so you can’t do things like `1e1000-1`, so what I do is, instead of `X`, I do `X**(2**3)**(-1)` (which is the same as `X**(1/8)` or `X**0.125`), and then square the amount of nines thrice, which is equivalent to taking the amount of nines to the power of eight, and it cancels out the `1/8` power. But because the output of `X**0.125` will most likely have decimals, and they will be removed, `1e(X**0.125)` is going to be smaller than we want, so we can instead do `1e(X**0.125+1)`, but that will be longer than we want, so we can use `$cropText` later to fix the amount of nines. In the next step, each `9` will be replaced by the entire list of nines, for example, every `9` in `9999` will be replaced with `9999` so it changes the value of the variable to `9999999999999999` which basically takes the number of nines to the power of two, we do this three times as mentioned earlier. In the next step, we use `$cropText` to make sure the amount of nines is the same as `$var[amount]`, then we replace each nine with a code, then eval it.
