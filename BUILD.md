# 构建问题记录

### 如何构建

```shell
npm install
# for macos
npm run dist:mac

# README.md for more details
```

### 已知部分构建问题

1. 无法解析github.com问题

```plaintext
$ npm install
npm ERR! code 1
npm ERR! path /Users/xxxx/listen1_desktop/node_modules/electron
npm ERR! command failed
npm ERR! command sh -c node install.js
npm ERR! RequestError: getaddrinfo ENOTFOUND github.com
npm ERR!     at ClientRequest.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/got/source/request-as-event-emitter.js:178:14)
npm ERR!     at Object.onceWrapper (node:events:472:26)
npm ERR!     at ClientRequest.emit (node:events:377:35)
npm ERR!     at ClientRequest.origin.emit (/Users/xxxx/listen1_desktop/node_modules/@szmarczak/http-timer/source/index.js:37:11)
npm ERR!     at TLSSocket.socketErrorListener (node:_http_client:447:9)
npm ERR!     at TLSSocket.emit (node:events:365:28)
npm ERR!     at emitErrorNT (node:internal/streams/destroy:193:8)
npm ERR!     at emitErrorCloseNT (node:internal/streams/destroy:158:3)
npm ERR!     at processTicksAndRejections (node:internal/process/task_queues:83:21)

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/xxxx/.npm/_logs/2021-05-28T12_07_57_649Z-debug.log
```

you need run `npm install` with a proxy:

```shell
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
npx cross-env ELECTRON_GET_USE_PROXY=true GLOBAL_AGENT_HTTPS_PROXY=$https_proxy npm install
```

2. 执行`npm run dist:mac`报错版本兼容问题

```plaintext
• downloaded      url=https://github.com/electron/electron/releases/download/v12.0.9/electron-v12.0.9-darwin-x64.zip duration=19.762s
  • map async       taskCount=251
  • exited          command=app-builder code=0 pid=62754
  • async task error  error=editions-autoloader-none-broadened: Unable to determine a suitable edition, even after broadening.
  ⨯ editions-autoloader-none-broadened: Unable to determine a suitable edition, even after broadening.  stackTrace=
                                                                                                          Error: editions-autoloader-none-broadened: Unable to determine a suitable edition, even after broadening.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:317:21)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                          ↳ Error: editions-autoloader-none-suitable: Unable to determine a suitable edition, as none were suitable.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:327:19)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: editions-autoloader-edition-incompatible: The edition [TypeScript source code made to be compatible with Deno] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:301:25)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: editions-autoloader-edition-incompatible: The edition [TypeScript compiled against ES2019 for Node.js 12 || 14 || 15 with Import for modules] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:301:25)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: editions-autoloader-edition-incompatible: The edition [TypeScript compiled against ES2019 for Node.js 10 || 12 || 14 || 15 with Require for modules] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:301:25)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: editions-autoloader-edition-incompatible: The edition [TypeScript compiled against ESNext for Node.js 14 || 15 with Require for modules] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:301:25)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: editions-autoloader-edition-incompatible: The edition [TypeScript compiled against ES2019 for web browsers with Import for modules] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:301:25)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                          ↳ Error: editions-autoloader-edition-incompatible: The edition [TypeScript source code with Import for modules] is not compatible with this environment.
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at isCompatibleEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:252:19)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:287:4)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                          ↳ Error: editions-autoloader-invalid-engines: The edition had no engines to compare against the environment
                                                                                                              at new Errlop (/Users/xxxx/listen1_desktop/node_modules/errlop/edition-es5/index.js:61:18)
                                                                                                              at Object.errtion (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/util.js:23:14)
                                                                                                              at isCompatibleEngines (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:183:19)
                                                                                                              at isCompatibleEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:250:10)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:287:4)
                                                                                                              at determineEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:312:12)
                                                                                                              at solicitEdition (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:350:16)
                                                                                                              at Object.requirePackage (/Users/xxxx/listen1_desktop/node_modules/editions/edition-es5/index.js:364:9)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/istextorbinary/index.cjs:4:38)
                                                                                                              at Module._compile (node:internal/modules/cjs/loader:1109:14)
                                                                                                              at Object.Module._extensions..js (node:internal/modules/cjs/loader:1138:10)
                                                                                                              at Module.load (node:internal/modules/cjs/loader:989:32)
                                                                                                              at Function.Module._load (node:internal/modules/cjs/loader:829:14)
                                                                                                              at Module.require (node:internal/modules/cjs/loader:1013:19)
                                                                                                              at require (node:internal/modules/cjs/helpers:93:18)
                                                                                                              at Object.<anonymous> (/Users/xxxx/listen1_desktop/node_modules/app-builder-lib/electron-osx-sign/util.js:135:22)
```

修复方法：
把`electron-builder`降级到`22.10.4`，具体为：
修改`package.json`内容：

```json
    "devDependencies": {
    // ...
    "electron-builder": "22.10.4",
    // ...
  }
```

重新安装依赖和执行构建：

```shell
rm -rf node_modules

npm install
# or with proxy
npx cross-env ELECTRON_GET_USE_PROXY=true GLOBAL_AGENT_HTTPS_PROXY=$https_proxy npm install

npm run dist:mac
```

3.`git submodule update`卡住问题

手动更新`.gitmodules`文件，修改url使用https方式。如下所示：
```text
[submodule "app/listen1_chrome_extension"]
	path = app/listen1_chrome_extension
	url = https://github.com/10fish/listen1_chrome_extension.git

```

### 参考文章

1. <https://forum.snapcraft.io/t/electron-7-and-above-fails-to-install-with-getaddrinfo-enotfound-github-com-on-launchpad-build-snapcraft-io/20432>
2. <https://stackoverflow.com/questions/67018894/error-while-electron-js-builder-on-an-existing-react-js-based-project>
3. <https://github.com/electron-userland/electron-builder/issues/5668>
