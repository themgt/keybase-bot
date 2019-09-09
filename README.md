# keybase-bot

Keybase bot-scripting for Node.js - now written all in TypeScript! Send encrypted data all over this world.

[![npm](https://img.shields.io/npm/v/keybase-bot.svg)](https://www.npmjs.com/package/keybase-bot)
[![Travis CI](https://travis-ci.org/keybase/keybase-bot.svg?branch=master)](https://travis-ci.org/keybase/keybase-bot)

This module is a side-project/work in progress and may change or have crashes, but feel free to play with it. As long as you have a Keybase account, you can use this module to script basic Keybase commands such as sending and reading messages and attachments, managing teams, and even sending Lumens on the Stellar network.

- [Installation](#installation)
- [Hello World](#hello-world)
- [API](#api)
- [Contributions](#contributions)

## Installation

1.  Install Node.js 8 or above.
2.  Make sure that you have Keybase [installed](https://keybase.io/download) and running.
3.  Install `keybase-bot`.
    ```bash
    npm install keybase-bot
    # or
    yarn add keybase-bot
    ```

You're ready to make your first Keybase bot!

## Hello world via your Keybase bot

Let's make a bot that says hello to the Keybase user [kbot](https://keybase.io/kbot).

We recommend either creating a dedicated Keybase account for the bot, or if you decide to reuse your own account at the very least create a dedicated paperkey so you can revoke it later if the machines rise up.

```javascript
const Bot = require('keybase-bot')

const bot = new Bot()
const username = 'your username'
const paperkey = 'your paperkey'
bot
  .init(username, paperkey, {verbose: false})
  .then(() => {
    console.log(`Your bot is initialized. It is logged in as ${bot.myInfo().username}`)

    const channel = {name: 'kbot,' + bot.myInfo().username, public: false, topicType: 'chat'}
    const message = {
      body: `Hello kbot! This is ${bot.myInfo().username} saying hello from my device ${bot.myInfo().devicename}`,
    }

    bot.chat
      .send(channel, message)
      .then(() => {
        console.log('Message sent!')
        bot.deinit()
      })
      .catch(error => {
        console.error(error)
        bot.deinit()
      })
  })
  .catch(error => {
    console.error(error)
    bot.deinit()
  })
```

To run the above bot, you want to save that code into a file and run it with node:

```bash
node <my-awesome-file-name>.js
```

This code is also in [`demos/hello-world.js`](demos/hello-world.js), if you want to take a look in there. There are also some other cool bots in the demos directory, including a bot that tells you how many unread messages you have and a bot that does math for you and your friends. You can write a bot in any language that can compile to JavaScript and run on Node.js. We have some ES7+ (with `async/await`) demos in [`demos/ES7`](demos/es7) and even a bot in [Iced CoffeeScript](http://maxtaco.github.io/coffee-script/)! (in [`demos/iced`](demos/iced))

## Development

All the source of this library is now written in TypeScript. If you're working on the library, please use `yarn` to install the necessary modules, and then run `yarn build` to build the JavaScript library files. Finally, make a test config file in `__tests__/` (look at `__tests__/test.config.ts` as an example) and run `yarn test`. If everything passes, you haven't broken everything horribly.

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

- [Bot](#bot)
  - [Bot](#bot-1)
    - [Examples](#examples)
  - [init](#init)
    - [Parameters](#parameters)
    - [Examples](#examples-1)
  - [initFromRunningService](#initfromrunningservice)
    - [Parameters](#parameters-1)
    - [Examples](#examples-2)
  - [myInfo](#myinfo)
    - [Examples](#examples-3)
  - [deinit](#deinit)
    - [Examples](#examples-4)
  - [adminDebugLogInfo](#admindebugloginfo)
    - [Parameters](#parameters-2)
    - [Examples](#examples-5)
  - [adminDebugLogError](#admindebuglogerror)
    - [Parameters](#parameters-3)
    - [Examples](#examples-6)
- [Bot](#bot-2)
  - [Bot](#bot-3)
    - [Examples](#examples-7)
  - [init](#init-1)
    - [Parameters](#parameters-4)
    - [Examples](#examples-8)
  - [initFromRunningService](#initfromrunningservice-1)
    - [Parameters](#parameters-5)
    - [Examples](#examples-9)
  - [myInfo](#myinfo-1)
    - [Examples](#examples-10)
  - [deinit](#deinit-1)
    - [Examples](#examples-11)
  - [adminDebugLogInfo](#admindebugloginfo-1)
    - [Parameters](#parameters-6)
    - [Examples](#examples-12)
  - [adminDebugLogError](#admindebuglogerror-1)
    - [Parameters](#parameters-7)
    - [Examples](#examples-13)
- [Bot Types](#bot-types)
- [Chat](#chat)
  - [joinChannel](#joinchannel)
    - [Parameters](#parameters-8)
    - [Examples](#examples-14)
  - [leaveChannel](#leavechannel)
    - [Parameters](#parameters-9)
    - [Examples](#examples-15)
  - [getUnfurlSettings](#getunfurlsettings)
    - [Examples](#examples-16)
  - [setUnfurlSettings](#setunfurlsettings)
    - [Parameters](#parameters-10)
    - [Examples](#examples-17)
  - [loadFlip](#loadflip)
    - [Parameters](#parameters-11)
    - [Examples](#examples-18)
  - [advertiseCommands](#advertisecommands)
    - [Parameters](#parameters-12)
    - [Examples](#examples-19)
  - [clearCommands](#clearcommands)
    - [Parameters](#parameters-13)
    - [Examples](#examples-20)
  - [listCommands](#listcommands)
    - [Parameters](#parameters-14)
    - [Examples](#examples-21)
  - [list](#list)
    - [Parameters](#parameters-15)
    - [Examples](#examples-22)
  - [listChannels](#listchannels)
    - [Parameters](#parameters-16)
    - [Examples](#examples-23)
  - [read](#read)
    - [Parameters](#parameters-17)
    - [Examples](#examples-24)
  - [send](#send)
    - [Parameters](#parameters-18)
    - [Examples](#examples-25)
  - [createChannel](#createchannel)
    - [Parameters](#parameters-19)
    - [Examples](#examples-26)
  - [attach](#attach)
    - [Parameters](#parameters-20)
    - [Examples](#examples-27)
  - [download](#download)
    - [Parameters](#parameters-21)
    - [Examples](#examples-28)
  - [react](#react)
    - [Parameters](#parameters-22)
    - [Examples](#examples-29)
  - [delete](#delete)
    - [Parameters](#parameters-23)
    - [Examples](#examples-30)
  - [watchChannelForNewMessages](#watchchannelfornewmessages)
    - [Parameters](#parameters-24)
    - [Examples](#examples-31)
  - [watchAllChannelsForNewMessages](#watchallchannelsfornewmessages)
    - [Parameters](#parameters-25)
    - [Examples](#examples-32)
- [Chat Types](#chat-types)
- [Wallet](#wallet)
  - [balances](#balances)
    - [Examples](#examples-33)
  - [history](#history)
    - [Parameters](#parameters-26)
    - [Examples](#examples-34)
  - [details](#details)
    - [Parameters](#parameters-27)
    - [Examples](#examples-35)
  - [lookup](#lookup)
    - [Parameters](#parameters-28)
    - [Examples](#examples-36)
  - [send](#send-1)
    - [Parameters](#parameters-29)
    - [Examples](#examples-37)
  - [batch](#batch)
    - [Parameters](#parameters-30)
    - [Examples](#examples-38)
  - [cancel](#cancel)
    - [Parameters](#parameters-31)
    - [Examples](#examples-39)
- [Wallet Types](#wallet-types)
- [default](#default)
- [default](#default-1)
- [default](#default-2)
- [ClientBase](#clientbase)
- [Service](#service)
- [Team](#team)
  - [create](#create)
    - [Parameters](#parameters-32)
    - [Examples](#examples-40)
  - [addMembers](#addmembers)
    - [Parameters](#parameters-33)
    - [Examples](#examples-41)
  - [removeMember](#removemember)
    - [Parameters](#parameters-34)
    - [Examples](#examples-42)
  - [listTeamMemberships](#listteammemberships)
    - [Parameters](#parameters-35)
    - [Examples](#examples-43)
- [AdminDebugLogger](#admindebuglogger)

### Bot

A Keybase bot.

#### Bot

Create a bot. Note you can't do much too exciting with your bot after you instantiate it; you have to initialize it first.

##### Examples

```javascript
const bot = new Bot()
```

#### init

Initialize your bot by starting an instance of the Keybase service and logging in using oneshot mode.

##### Parameters

- `username` The username of your bot's Keybase account.
- `paperkey` The paperkey of your bot's Keybase account.
- `options` The initialization options for your bot.

##### Examples

```javascript
bot.init('username', 'paperkey')
```

#### initFromRunningService

Initialize your bot by using an existing running service with a logged in user.

##### Parameters

- `homeDir` The home directory of this currently running service. Leave blank to use the default homeDir for your system.
- `options` The initialization options for your bot.

##### Examples

```javascript
bot.initFromRunningService()
```

#### myInfo

Get info about your bot!

##### Examples

```javascript
const info = bot.myInfo()
```

Returns **any** – Useful information like the username, device, and home directory of your bot. If your bot isn't initialized, you'll get `null`.

#### deinit

Deinitializes the bot by logging out, stopping the keybase service, and removing any leftover login files made by the bot. This should be run before your bot ends.

##### Examples

```javascript
bot.deinit()
```

#### adminDebugLogInfo

If bot is initialized with an optional directory `adminDebugDirectory`, this will let you write info text into it.

##### Parameters

- `text`

##### Examples

```javascript
bot.adminDebugLogInfo('My bot is ready to go.')
```

#### adminDebugLogError

If bot is initialized with an optional directory `adminDebugDirectory`, this will let you write error text into it.

##### Parameters

- `text`

##### Examples

```javascript
bot.adminDebugLogInfo('My bot is ready to go.')
```

### Bot

#### Bot

Create a bot. Note you can't do much too exciting with your bot after you instantiate it; you have to initialize it first.

##### Examples

```javascript
const bot = new Bot()
```

#### init

Initialize your bot by starting an instance of the Keybase service and logging in using oneshot mode.

##### Parameters

- `username` The username of your bot's Keybase account.
- `paperkey` The paperkey of your bot's Keybase account.
- `options` The initialization options for your bot.

##### Examples

```javascript
bot.init('username', 'paperkey')
```

#### initFromRunningService

Initialize your bot by using an existing running service with a logged in user.

##### Parameters

- `homeDir` The home directory of this currently running service. Leave blank to use the default homeDir for your system.
- `options` The initialization options for your bot.

##### Examples

```javascript
bot.initFromRunningService()
```

#### myInfo

Get info about your bot!

##### Examples

```javascript
const info = bot.myInfo()
```

Returns **any** – Useful information like the username, device, and home directory of your bot. If your bot isn't initialized, you'll get `null`.

#### deinit

Deinitializes the bot by logging out, stopping the keybase service, and removing any leftover login files made by the bot. This should be run before your bot ends.

##### Examples

```javascript
bot.deinit()
```

#### adminDebugLogInfo

If bot is initialized with an optional directory `adminDebugDirectory`, this will let you write info text into it.

##### Parameters

- `text`

##### Examples

```javascript
bot.adminDebugLogInfo('My bot is ready to go.')
```

#### adminDebugLogError

If bot is initialized with an optional directory `adminDebugDirectory`, this will let you write error text into it.

##### Parameters

- `text`

##### Examples

```javascript
bot.adminDebugLogInfo('My bot is ready to go.')
```

### Bot Types

A collection of types used by the bot.

### Chat

The chat module of your Keybase bot. For more info about the API this module uses, you may want to check out `keybase chat api`.

#### joinChannel

Joins a team conversation.

##### Parameters

- `channel` The team chat channel to join.

##### Examples

```javascript
bot.chat.listConvsOnName('team_name').then(async teamConversations => {
  for (const conversation of teamConversations) {
    if (conversation.memberStatus !== 'active') {
      await bot.chat.join(conversation.channel)
      console.log('Joined team channel', conversation.channel)
    }
  }
})
```

#### leaveChannel

Leaves a team conversation.

##### Parameters

- `channel` The team chat channel to leave.

##### Examples

```javascript
bot.chat.listConvsOnName('team_name').then(async teamConversations => {
  for (const conversation of teamConversations) {
    if (conversation.memberStatus === 'active') {
      await bot.chat.leave(conversation.channel)
      console.log('Left team channel', conversation.channel)
    }
  }
})
```

#### getUnfurlSettings

Gets current unfurling settings

##### Examples

```javascript
bot.chat.getUnfurlSettings().then(mode => console.log(mode))
```

#### setUnfurlSettings

Sets the unfurling mode
In Keybase, unfurling means generating previews for links that you're sending
in chat messages. If the mode is set to always or the domain in the URL is
present on the whitelist, the Keybase service will automatically send a preview
to the message recipient in a background chat channel.

##### Parameters

- `mode` the new unfurl mode

##### Examples

```javascript
bot.chat
  .setUnfurlMode({
    mode: 'always',
  })
  .then(mode => console.log('mode updated!'))
```

#### loadFlip

Loads a flip's details

##### Parameters

- `conversationID` conversation ID received in API listen.
- `flipConversationID` flipConvID from the message summary.
- `messageID` ID of the message in the conversation.
- `gameID` gameID from the flip message contents.

##### Examples

```javascript
// check demos/es7/poker-hands.js
```

#### advertiseCommands

Publishes a commands advertisement which is shown in the "!" chat autocomplete.

##### Parameters

- `advertisement` details of the advertisement

##### Examples

```javascript
await bot.chat.advertiseCommands({
  advertisements: [
    {
      type: 'public',
      commands: [
        {
          name: '!echo',
          description: 'Sends out your message to the current channel.',
          usage: '[your text]',
        },
      ],
    },
  ],
})
```

#### clearCommands

Clears all published commands advertisements.

##### Parameters

- `advertisement` advertisement parameters

##### Examples

```javascript
await bot.chat.clearCommands()
```

#### listCommands

Lists all commands advertised in a channel.

##### Parameters

- `lookup` either conversation id or channel

##### Examples

```javascript
const commandsList = await bot.chat.listCommands({
  channel: channel,
})
console.log(commandsList)
// prints out something like:
// {
//   commands: [
//     {
//       name: '!helloworld',
//       description: 'sample description',
//       usage: '[command arguments]',
//       username: 'userwhopublished',
//     }
//   ]
// }
```

#### list

Lists your chats, with info on which ones have unread messages.

##### Parameters

- `options` An object of options that can be passed to the method.

##### Examples

```javascript
bot.chat.list({unreadOnly: true}).then(chatConversations => console.log(chatConversations))
```

Returns **any** An array of chat conversations. If there are no conversations, the array is empty.

#### listChannels

Lists conversation channels in a team

##### Parameters

- `name` Name of the team
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
bot.chat.listChannels('team_name').then(chatConversations => console.log(chatConversations))
```

Returns **any** An array of chat conversations. If there are no conversations, the array is empty.

#### read

Reads the messages in a channel. You can read with or without marking as read.

##### Parameters

- `channel` The chat channel to read messages in.
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
alice.chat.read(channel).then(messages => console.log(messages))
```

Returns **any** A summary of data about a message, including who send it, when, the content of the message, etc. If there are no messages in your channel, then an error is thrown.

#### send

Send a message to a certain channel.

##### Parameters

- `channel` The chat channel to send the message in.
- `message` The chat message to send.
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
const channel = {name: 'kbot,' + bot.myInfo().username, public: false, topicType: 'chat'}
const message = {body: 'Hello kbot!'}
bot.chat.send(channel, message).then(() => console.log('message sent!'))
```

#### createChannel

Creates a new blank conversation.

##### Parameters

- `channel` The chat channel to create.

##### Examples

```javascript
bot.chat.createChannel(channel).then(() => console.log('conversation created'))
```

#### attach

Send a file to a channel.

##### Parameters

- `channel` The chat channel to send the message in.
- `filename` The absolute path of the file to send.
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
bot.chat.attach(channel, '/Users/nathan/my_picture.png').then(() => console.log('Sent a picture!'))
```

#### download

Download a file send via Keybase chat.

##### Parameters

- `channel` The chat channel that the desired attacment to download is in.
- `messageId` The message id of the attached file.
- `output` The absolute path of where the file should be downloaded to.
- `options` An object of options that can be passed to the method

##### Examples

```javascript
bot.chat.download(channel, 325, '/Users/nathan/Downloads/file.png')
```

#### react

Reacts to a given message in a channel. Messages have messageId's associated with
them, which you can learn in `bot.chat.read`.

##### Parameters

- `channel` The chat channel to send the message in.
- `messageId` The id of the message to react to.
- `reaction` The reaction emoji, in colon form.
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
bot.chat.react(channel, 314, ':+1:').then(() => console.log('Thumbs up!'))
```

#### delete

Deletes a message in a channel. Messages have messageId's associated with
them, which you can learn in `bot.chat.read`. Known bug: the GUI has a cache,
and deleting from the CLI may not become apparent immediately.

##### Parameters

- `channel` The chat channel to send the message in.
- `messageId` The id of the message to delete.
- `options` An object of options that can be passed to the method.

##### Examples

```javascript
bot.chat.delete(channel, 314).then(() => console.log('message deleted!'))
```

#### watchChannelForNewMessages

Listens for new chat messages on a specified channel. The `onMessage` function is called for every message your bot receives. This is pretty similar to `watchAllChannelsForNewMessages`, except it specifically checks one channel. Note that it receives messages your own bot posts, but from other devices. You can filter out your own messages by looking at a message's sender object.
Hides exploding messages by default.

##### Parameters

- `channel` The chat channel to watch.
- `onMessage` A callback that is triggered on every message your bot receives.
- `onError` A callback that is triggered on any error that occurs while the method is executing.
- `options` Options for the listen method.

##### Examples

```javascript
// Reply to all messages between you and `kbot` with 'thanks!'
const channel = {name: 'kbot,' + bot.myInfo().username, public: false, topicType: 'chat'}
const onMessage = message => {
  const channel = message.channel
  bot.chat.send(channel, {body: 'thanks!!!'})
}
bot.chat.watchChannelForNewMessages(channel, onMessage)
```

#### watchAllChannelsForNewMessages

This function will put your bot into full-read mode, where it reads
everything it can and every new message it finds it will pass to you, so
you can do what you want with it. For example, if you want to write a
Keybase bot that talks shit at anyone who dares approach it, this is the
function to use. Note that it receives messages your own bot posts, but from other devices.
You can filter out your own messages by looking at a message's sender object.
Hides exploding messages by default.

##### Parameters

- `onMessage` A callback that is triggered on every message your bot receives.
- `onError` A callback that is triggered on any error that occurs while the method is executing.
- `options` Options for the listen method.

##### Examples

```javascript
// Reply to incoming traffic on all channels with 'thanks!'
const onMessage = message => {
  const channel = message.channel
  bot.chat.send(channel, {body: 'thanks!!!'})
}
bot.chat.watchAllChannelsForNewMessages(onMessage)
```

### Chat Types

A collection of types used by the Chat module.

### Wallet

The wallet module of your Keybase bot. For more info about the API this module uses, you may want to check out `keybase wallet api`.

#### balances

Provides a list of all accounts owned by the current Keybase user.

##### Examples

```javascript
bot.wallet.balances().then(accounts => console.log(accounts))
```

Returns **any** An array of accounts. If there are no accounts, the array is empty.

#### history

Provides a list of all transactions in a single account.

##### Parameters

- `accountId` The id of an account owned by a Keybase user.

##### Examples

```javascript
bot.wallet.history('GDUKZH6Q3U5WQD4PDGZXYLJE3P76BDRDWPSALN4OUFEESI2QL5UZHCK').then(transactions => console.log(transactions))
```

Returns **any** An array of transactions related to the account.

#### details

Get details about a particular transaction

##### Parameters

- `transactionId` The id of the transaction you would like details about.

##### Examples

```javascript
bot.wallet.details('e5334601b9dc2a24e031ffeec2fce37bb6a8b4b51fc711d16dec04d3e64976c4').then(details => console.log(details))
```

Returns **any** An object of details about the transaction specified.

#### lookup

Lookup the primary Stellar account ID of a Keybase user.

##### Parameters

- `name` The name of the user you want to lookup. This can be either a Keybase username or a username of another account that is supported by Keybase if it is followed by an '@<service>'.

##### Examples

```javascript
const lookup1 = bot.wallet.lookup('patrick')
// 'patrick' on Keybase is 'patrickxb' on twitter
const lookup2 = bot.wallet.lookup('patrcikxb@twitter')
// Using Lodash's `isEqual` since objects with same values aren't equal in JavaScript
_.isEqual(lookup1, lookup2) // => true
```

Returns **any** An object containing the account ID and Keybase username of the found user.

#### send

Send lumens (XLM) via Keybase with your bot!

##### Parameters

- `recipient` Who you're sending your money to. This can be a Keybase user, stellar address, or a username of another account that is supported by Keybase if it is followed by an '@<service>'.
- `amount` The amount of XLM to send.
- `currency` Adds a currency value to the amount specified. For example, adding 'USD' would send
- `message` The message for your payment

##### Examples

```javascript
bot.wallet.send('nathunsmitty', '3.50') // Send 3.50 XLM to Keybase user `nathunsmitty`
bot.wallet.send('nathunsmitty@github', '3.50') // Send 3.50 XLM to GitHub user `nathunsmitty`
bot.wallet.send('nathunsmitty', '3.50', 'USD') // Send $3.50 worth of lumens to Keybase user `nathunsmitty`
bot.wallet.send('nathunsmitty', '3.50', 'USD', 'Shut up and take my money!') // Send $3.50 worth of lumens to Keybase user `nathunsmitty` with a memo
```

Returns **any** The trasaction object of the transaction.

#### batch

Send lumens (XLM) via Keybase to more than one user at once. As opposed to the normal bot.wallet.send
command, this can get multiple transactions into the same 5-second Stellar ledger.

##### Parameters

- `batchId` example, if sending a bunch of batches for an airdrop, you could pass them all `airdrop2025`.
- `payments` an array of objects containing recipients and XLM of the form {"recipient": "someusername", "amount": "1.234", "message", "hi there"}

##### Examples

```javascript
bot.wallet.batch('airdrop2040', [
  {recipient: 'a1', amount: '1.414', message: 'hi a1, yes 1'},
  {recipient: 'a2', amount: '3.14159', message: 'hi a2, yes 2'},
])
```

Returns **any** an object

#### cancel

If you send XLM to a Keybase user who has not established a wallet, you can cancel the payment before the recipient claims it and the XLM will be returned to your account.

##### Parameters

- `transactionId` The id of the transaction to cancel.

##### Examples

```javascript
bot.wallet
  .cancel('e5334601b9dc2a24e031ffeec2fce37bb6a8b4b51fc711d16dec04d3e64976c4')
  .then(() => console.log('Transaction successfully canceled!'))
```

### Wallet Types

A collection of types used by the Wallet module.

### default

### default

### default

### ClientBase

### Service

### Team

The team module of your Keybase bot. For more info about the API this module uses, you may want to check out `keybase team api`.

#### create

Create a new Keybase team or subteam

##### Parameters

- `creation` the name of the team to create

##### Examples

```javascript
bot.team.create({team: 'phoenix'}).then(res => console.log(res))
```

Returns **any** \-

#### addMembers

Add a bunch of people with different privileges to a team

##### Parameters

- `additions` an array of the users to add, with privs

##### Examples

```javascript
bot.team
  .addMembers({
    team: 'phoenix',
    emails: [{email: 'alice@keybase.io', role: 'writer'}, {email: 'cleo@keybase.io', role: 'admin'}],
    usernames: [{username: 'frank', role: 'reader'}, {username: 'keybaseio@twitter', role: 'writer'}],
  })
  .then(res => console.log(res))
```

Returns **any** \-

#### removeMember

Remove someone from a team

##### Parameters

- `removal` object with the `team` name and `username`

##### Examples

```javascript
bot.team.removeMember({team: 'phoenix', username: 'frank'}).then(res => console.log(res))
```

Returns **any** \-

#### listTeamMemberships

List a team's members

##### Parameters

- `team` an object with the `team` name in it

##### Examples

```javascript
bot.team.listTeamMemberships({team: 'phoenix'}).then(res => console.log(res))
```

Returns **any** \-

### AdminDebugLogger

## Contributions

Make sure that you have Node, Yarn, and the Keybase application installed. We also use developer tools such as [EditorConfig](https://editorconfig.org), [ESLint](https://eslint.org), [Flow](https://flow.org), and [Prettier](https://prettier.io) so you'll probably want to make sure that your development is configured to use those tools somewhere in your code writing process.

### Setting up the source code

1.  Clone this repo.
2.  Install dependencies with `yarn`.
3.  Build the bot in watch mode with `yarn dev`.
4.  Build the bot for production with `yarn build`.
5.  Build the docs for the bot with `yarn docs`.

That's it. We accept changes via Pull Requests; please make sure that any changes you make build successfully and pass Flow, Prettier, and ESLint checks. We'd also really appreciate it if your PR could follow the [Conventional Commit](https://www.conventionalcommits.org) specification. If you're adding a new feature, please add/update tests, demos, documentation, and whatever else makes sense to go with it. If you have any questions about contributing, please feel free to ask a maintainer!

### Running Tests

We run tests using [Jest](https://jestjs.io/). All tests are run against actual Keybase processes that are created and destroyed during testing and ping the actual Keybase server to do things like send messages and XLM. To facilitate this, the tests read a file in `__tests__/test.config.ts` that contains usernames, paperkeys, and team names that are used during testing. You'll need three test Keybase accounts, two teams, and some Stellar Lumens to run all tests.

1.  Copy `__tests__/tests.config.example.ts` as `__tests__/tests.config.ts`. Note that `__tests__/tests.config.ts` should **NOT** be version controlled, as it will contain paper keys!
2.  Edit `__tests__/tests.config.ts` as it specifies, replacing the placeholder values with actual usernames, paperkeys, and team names.
3.  Run `yarn test`. Everything should pass!

### Generating Types

Most of the types the bot uses are generated from definitions defined in the [`protocol/`](https://github.com/keybase/client/tree/master/protocol) directory inside the Keybase client repo. This ensures that the types that the bot uses are consistent across bots and always up to date with the output of the API.

To build the types for the TypeScript bot, you'll need to clone the `client` repo. This requires [Go](https://golang.org/) and your [GOPATH](https://github.com/golang/go/wiki/SettingGOPATH) to be set up.

```shell
go get github.com/keybase/client/go/keybase
```

and install the necessary dependencies for compiling the protocol files. This requires [node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com).

```shell
cd client/protocol
yarn install
```

Then you can generate the types by using the provided Makefile in this repo.

```shell
cd path/to/keybase-bot
make
```

Should you need to remove all the types for some reason, you can run `make clean`.

### Release

We automatically generate a CHANGELOG and version (using [Semantic Versioning](https://semver.org)) `keybase-bot` with [`standard-version`](https://github.com/conventional-changelog/standard-version). To cut a new release:

1.  Make sure all commits that are to be included in the release are squash-merged into `master` branch.
2.  On your local copy of the bot, checkout `master` and ensure it's up to date with `origin/master`.
3.  Run `standard-version` with the command `yarn release`.
4.  Push the new git tags to `origin`. (`git push --follow-tags origin master`)
5.  Publish to npm with `yarn publish`.

## License

BSD-3-Clause
