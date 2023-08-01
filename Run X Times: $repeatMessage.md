> Before you can use any type of loops, you need to learn [how to escape code](../main/Escaping.md).

You can use the `$repeatMessage[Amount;Text]` function to repeat your code, but the limit for `Amount` is 10, so for amounts larger than 10, you need to use `$repeatMessage` multiple times.

This example deletes the last 5,600 non-pinned messages sent in the last 2 weeks:
```js
$eval[$repeatMessage[7;$repeatMessage[8;%{DOL}%clear[100\]]]]
```
It repeats `%{DOL}%clear[100\]` 56 times (7 x 8 = 56), which is where the number 5,600 comes from.

This doesn’t work for prime numbers, because you can’t convert them to a multiplication of multiple numbers smaller than 10, but instead, you can subtract one from the amount, repeat it, and add the code to the end again.
```js
$async[]
    %{DOL}%clear[100\]
$endasync

$eval[$repeatMessage[3;$repeatMessage[4;$await[]]]$await[]]
```
This repeats the code 12 times, then adds the code to the end again to make it 13 times.

For amounts that are annoying to do with this method, I recommend you use [a more advanced method](../main/Run%20X%20Times%3A%20Other%20method.md).
