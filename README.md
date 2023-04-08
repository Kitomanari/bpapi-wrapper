# BPAPI

[![NPM: Version](https://img.shields.io/npm/v/@nightnutsky/bpapi?logo=npm&style=for-the-badge)](https://www.npmjs.com/package/@nightnutsky/bpapi)
[![GitHub: Stars](https://img.shields.io/github/stars/NightNutSky/bpapi?logo=github&style=for-the-badge)](https://github.com/NightNutSky/bpapi/stargazers)
[![GitHub: Source Code](https://img.shields.io/badge/Source%20Code-GitHub-green?logo=github&style=for-the-badge)](https://github.com/NightNutSky/bpapi)

BPAPI allows you to retrieve and work with information from [BDFD](https://botdesignerdiscord.com) [Public API](https://nilpointer-software.github.io/bdfd-wiki/nightly/resources/api.html) more easier.

# Install
```sh
npm i @nightnutsky/bpapi
```

# Get Started
To get started, you should import/require BPAPI:
- JavaScript
    - Require all functions:
        ```js
        const bpapi = require("@nightnutsky/bpapi");
        ```
    - Require particular function(s):
        ```js
        const { functionInfo } = require("@nightnutsky/bpapi");
        ```
- TypeScript
    - Import all functions:
        ```ts
        import * as bpapi from "@nightnutsky/bpapi";
        ```
    - Import particular function(s):
        ```ts
        import { functionInfo } from "@nightnutsky/bpapi";
        ```
## Code Examples

### functionInfo()
```js
/**
 * 
 * @param functionTag A tag (i.e `$addButton[]`, `$nomention`) of the function. Supports non-completed tags (i.e `$addBu` will be represented as `$addButton[]`)
 * @returns A promise containing information about the specified function. If could't find the function, `undefined` is returned.
 */
functionInfo('$replaceT').then(info => {
    if (info) {
        const tag = info.tag,
        description = info.description,
        intents = info.intents;

        console.log(`${tag}:\nDescription: ${description}\nIntents: ${intents}`);
    } else {
        console.log('Could not find the specified function!')
    }
});
```

### functionList()
```js
/**
 * 
 * @returns A promise containing an array of functions with their information
 */
functionList().then(list => {
    console.log('Functions That Require Intents:');
    for (const functionInfo of list) {
        if (functionInfo.intents != 'None') {
            const tag = functionInfo.tag,
            intents = functionInfo.intents;

            console.log(`${tag}: ${intents} Intent`);
        }
    }
});
```

### functionTagList()
```js
/**
 * 
 * @returns A promise containing an array of function tags
 */
functionTagList().then(tagList => {
    console.log('Functions That Start With "n":');
    for (const functionTag of tagList) {
        if (functionTag.includes('$n')) {
            console.log(functionTag);
        }
    }
});
```
## TypeScript Specials
If you ever worked with TypeScript, then you know that you can (and sometimes must) assign types for your consts, etc.

If you want to work with plain BDFD Public API, for example, do request to the `api/function_list` endpoint  yourself, BPAPI can help you using one of its type - `PublicAPIResponse`.\
Import this type and assign it to the request's response.

> Original BDFD Public API's response is a bit different and contains unused or deprecated (and now unused) properties. Unlike BDFD Public API, BPAPI only shows actual and a bit modified properties for your comfort.

| Showcase |
| :------: |
| ![Showcase](https://user-images.githubusercontent.com/70456337/230720560-c425f057-d09c-4e91-8f68-8f9312d07455.png) |
| ![Showcase](https://user-images.githubusercontent.com/70456337/230720600-f89d6185-ae72-47c8-ab37-cee6f1d6a9e5.png) |


## Raw Returns

<details><summary>Expand</summary>

### functionInfo()
```json
{
    "tag": "$replaceText[Text;Sample;New;(Amount)]",
    "description": "Replaces 'sample' from 'text' to 'new' 'how many' times. Set 'how many' to -1 to replace everything",
    "arguments": [
        {
            "name": "Text",
            "type": "String",
            "required": true,
            "empty": true
        },
        {
            "name": "Sample",
            "type": "String",
            "required": true,
            "empty": true
        },
        {
            "name": "New",
            "type": "String",
            "required": true,
            "empty": true
        },
        {
            "name": "Amount",
            "type": "Integer",
            "required": false
        }
    ],
    "intents": "None",
    "premium": false
}
```

### functionList()
```json
[   
    ...,
    {
        "tag": "$userJoinedDiscord[User ID;(Format)]",
        "description": "Returns date when given user joined discord. You can also give your own date format",
        "arguments": [
            {
                "name": "User ID",
                "type": "Snowflake",
                "required": true
            },
            {
                "name": "Format",
                "description": "Uses GoLang date format",
                "type": "String",
                "required": false
            }
        ],
        "intents": "None",
        "premium": false
    },
    {
        "tag": "$userJoined[User ID;(Format)]",
        "description": "Returns date when given user joined the guild. You can also give your own date format",
        "arguments": [
            {
                "name": "User ID",
                "type": "Snowflake",
                "required": true
            },
            {
                "name": "Format",
                "description": "Uses GoLang date format",
                "type": "String",
                "required": false
            }
        ],
        "intents": "Members",
        "premium": false
    },
    ...
]
```

### functionTagList()
```json
[
    ...,
    "$userInfo[]",
    "$userJoinedDiscord[]",
    "$userJoined[]",
    "$userLeaderboard[]",
    "$userPerms[]",
    "$userReacted[]",
    "$userRoles[]",
    "$userServerAvatar[]",
    "$username",
    "$username[]",
    "$varExistError[]",
    "$varExists[]",
    "$var[]",
    "$variablesCount[]",
    "$webhookAvatarURL[]",
    "$webhookColor[]",
    "$webhookContent[]",
    "$webhookCreate[]",
    "$webhookDelete[]",
    "$webhookDescription[]",
    "$webhookFooter[]",
    "$webhookSend[]",
    "$webhookTitle[]",
    "$webhookUsername[]",
    "$year"
]
```

</details>