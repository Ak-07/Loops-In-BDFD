> Before you can use any type of loops, you need to learn [how to escape code](../main/Escaping.md).

`$onMessageDelete` gets triggered every time a message gets deleted, so you can make an `$onMessageDelete` command send a message then delete it, which will make it trigger itself.

To make sure it doesn't get triggered when others delete a message, you could store the ID of the message the bot sends before deleting it, and when the code gets triggered, it would check if that message was sent by the bot or not, but for that, you need a variable, in this example, I'll call it `loop`.

If you make the bot check if the deleted message was originally sent by the loop code itself, the loop won't start, so there'll also be a command called `!start`, which will be useful sometimes because node restarts can break your loop.

Trigger: `$onMessageDelete[$getServerVar[loop]]`
```js
$nomention
$onlyIf[$messageID==$getChannelVar[loop];]

INSERT CODE HERE

$replyIn[1234s]
$var[id;$sendMessage[.;true]]
$setChannelVar[loop;$var[id]]
$deleteMessage[$channelID;$var[id]]
```
Edit the `$replyIn[1234s]` to whatever duration you want, and if it's more than 40 minutes, do something like `$replyIn[40m] $replyIn[8m]` to make it wait 48 minutes between each execution. However, durations longer than `3s` are probably not going to survive a node restart, the amount I usually do is `2s`.

Trigger: `!start`
```js
$nomention
$onlyForIDs[$botOwnerID;]
$setServerVar[loop;$channelID]
$setChannelVar[loop;$messageID]
$deleteMessage[$channelID;$messageID]
```
