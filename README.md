## fis3-typescript-vue-hackernews-2.0

使用 FIS3 和 TypeScript 实现 vue-hackernews-2.0

### 目标
使用 FIS3 生态的一套工具, 通过实现 vue-hackernews-2.0, 让大家了解到 FIS3 一样可以支持 npm 模块加载, vue 单文件编译等, 同时可以结合 FIS3 的特点, 形成一个前端工程化的小 demo

### 特性
- 整个项目使用 TypeScript 完成
- 支持在项目中使用 async, await, 以及 generator, 并通过 typescript 编译为 es5/es3 代码
- 通过 fis3-parser-vue-component 支持 vue 单文件编译, 可以通过对应parser在style, script, template标签使用 lang 属性. 具体见 [fis-conf.js](fis-conf.js) 中的配置
    - style 例如 scss, less, stylus 等, 并支持同 vueify 以及 vue-loader 功能一致的 scoped 属性
    - script 例如 babel, typescript
    - template 例如 jade 等
- 通过 fis3-hook-node_modules 支持加载 npm 模块
- 支持 localStorage 缓存前端模块, 使用修改版的 [mod.js](src/plugins/mod/mod.js)
- 支持模块合并打包, 具体配置见 [fis-conf.js](fis-conf.js) 中关于 packTo 的配置
- 支持 git commit 之前, ESLint, TSLint 以及检查 git commit msg 格式, 详见 [.git-hooks](.git-hooks)
- 支持开发时, 修改代码后自动刷新页面
- 支持 dev 环境下, 使用 vconsole 控制台
- 支持单元测试, 使用 karma + mocha + chai, 测试用例与测试文件放在一起, 并以 `.spec.ts` 结尾

### 模块合并打包

- mod.js 通过 fis3 的 `__inline` 功能, 内联到 `index.html` 中
- **全局依赖**的 npm 依赖模块, 通过在 `src/runtimes/packages.json` 中定义, fis3 编译时, 会将出现在此文件中的模块打包成 `runtimes/packages.js`, 如果没在此文件中定义, 则采用正常的异步加载策略
- 全局的项目依赖模块, 统一放在 `runtimes` 文件夹下, 编译时, 打包为 `runtimes/runtimes.js` 文件
- `boot.js` 和 `app.js` 项目启动文件, 打包为 `init.js`
- 通过 router 异步加载的各个 view 下的所有文件, 分别合并进以各自的文件夹命名的文件中, 合成 `views/NAME-pack.js`

### Development

```sh
npm run yarn
npm run dev
```

### Build

```
npm run build
```

### Test
```
npm run test:unit
```

### 感谢
绝大代码部分来自 vue-hacker-news-2.0, 删除了SSR部分, 并将代码改为 ts, 以及适合于 FIS3 处理

### License
MIT
