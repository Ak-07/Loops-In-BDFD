```js
$var[amount;NUMBER OF TIMES]

$async[code]
    CODE HERE
$endasync

$var[x;$sum[1e$calculate[$var[amount]**0.125+1];-1]]
$eval[$repeatMessage[3;$$c[]var[x\;$$c[]replaceText[$$c[]var[x\]\;9\;$$c[]var[x\]\]\]]]
$eval[$replaceText[$cropText[$var[x];$var[amount];];9;$trimSpace[$await[code]]]]
```
