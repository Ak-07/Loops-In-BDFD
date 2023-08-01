# Escaping
Imagine you want to send “$nomention” but BDFD doesn’t let you because it’s a function. Escaping allows you to do that!

The “escaped version” of `$nomention` is `%{DOL}%nomention`. So to send “$nomention” you do `$sendMessage[%{DOL}%nomention]`.

`$` => `%{DOL}%` \
`[` doesn’t need to be changed. \
`;` => `\;` \
`]` => `\]` \
`\` => `\\`

Here’s an example: \
To send `$addButton[New row;Custom ID;Label;Style;Disabled;Emoji;Message ID]`, you could do:
```js
$sendMessage[%{DOL}%addButton[New Row\;Custom Id\;Label\;Style\;Disabled\;Emoji\;Message Id\]]
```

> BDFD thinks `\\]` means “Backslash followed by an escaped `]`” instead of “Escaped backslash followed by a `]`” so it can break your code. You can instead use `$url[decode;%5C]` in these situations.
> 
> Example: \
> `$replaceText[\\;\\;\\]` throws an error, but `$replaceText[\\;\\;$url[decode;%5C]]` doesn’t.

# Other
You could escape `$` using `$$c[]` instead of `%{DOL}%`.

Example:
```js
$sendMessage[$$c[]nomention]
```

#

If your escaped code has a lot of `$$c[]` or `%{DOL}%` in it, you could use `/` or any other text in your escaped code, and replace it with `$`.

Example:
```
$replaceText[/nomention /yesmention /maybemention;/;$]
```

#

You don’t need to escape anything (except for `$`) if you put your code in an `$async` block, then get it using `$await`.

Example:
```js
$async[]
    $$c[]addButton[New Row;Custom Id;Label;Style;Disabled;Emoji;Message Id]
$endasync

$sendMessage[$await[]]
```

> Note: \
> In the example above, `$await[]` returns a new line character, 4 spaces, the escaped code, then another new line, but Discord automatically removes spaces at the start and end of messages, so in this `$sendMessage` example, there’s no need to use `$trimSpace`, but in other situations, you might need to use it.

# Example of combining a few of the tricks above

```
$async[]
    /if[/discriminator[]==0]
        It seems like you have switched to the new username system. You probably hate your new username, but I hope you like it.
    /else
        Why haven’t you switched to the new username system yet? The sooner you do, the more likely you are to get a username you like.
    /endif
$endasync

$eval[$replaceText[$trimSpace[$await[]];/;$]]
```
