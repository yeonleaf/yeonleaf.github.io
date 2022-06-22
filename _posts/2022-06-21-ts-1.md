---
title: "Invalid configuration object. configuration.mode should be one of these:"
excerpt: ""

categories:
    - trouble-shooting
tags:
    - [proj, webpack]

toc: true

date: 2022-06-21
last_modified_at: 
---

[document1](https://webpack.kr/configuration/mode/)

이미 package.json에서
```json
  "scripts": {
    "prod": "webpack --env=production",
    "dev": "webpack-dev-server --env=development",
    "start": "npm run dev",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
CLI의 인수로 mode 옵션을 사용하고 있는데

```js
const path = require('path')

module.exports = (env) => {
    let clientPath = path.resolve(__dirname, 'src/main/clients');

    return {
        mode: !env ? 'development' : env,
        ...
    }
}
```

webpack.config.js에서도 mode 옵션을 주기 때문에 발생하는 에러였다.