# Escaping
Imagine you want to send the word `$nomention` but BDFD doesn’t let you, because that’s a function. Escaping allows you to do that!

The “escaped version” of `$nomention` is `%{DOL}%nomention`. So to send “$nomention” you do `$sendMessage[%{DOL}%nomention]`.

`$` => `%{DOL}%` \
`[` doesn’t need to get escaped. \
`;` => `\;` \
`]` => `\]` \
`\` => `\\`

Here’s another example: \
To send `$addButton[New row;Custom ID;Label;Style;Disabled;Emoji;Message ID]`, you should do:
```js
$sendMessage[%{DOL}%addButton[New Row\;Custom Id\;Label\;Style\;Disabled\;Emoji\;Message Id\]]
```
