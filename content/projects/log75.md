---
title: log75
date: 2020-07-14
description: A convenient, lightweight text logging utility for Node.js
project:
    language: js
    repo: https://github.com/wait-what/log75
    featured: true
---

Log75 is a convenient, lightweight and customizable logging utility for Node.js

![PREVIEW](./preview.png)

## Message types
There are 6 message types available out of the box:
- Blank
- Debug
- Done
- Info
- Warn
- Error

You can easily add more message types by extending the class.

## Tables
Log75 can create neat looking tables for you!

```js
logger.info(
    logger.table(
        'You can make\n' +
        'cool tables!'
    )
)
```

![PREVIEW](./table.png)

```js
logger.table([
    'And ones with',
    'a separator'
], 'info')
```

![PREVIEW](table-with-separator.png)
