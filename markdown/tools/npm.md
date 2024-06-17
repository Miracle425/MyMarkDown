# 安装electron失败解决方法

```shell
npm install -g cnpm --registry=https://registry.npmmirror.com
cnpm install electron --save-dev
```

显示安装进度

```shell
npm config set loglevel=http
```

```shell
npm config set registry https://registry.npmmirror.com #用于npm
yarn config set registry https://registry.npmmirror.com #用于yarn
```

如何打包electron

```shell
pnpm install electron-builder --save-dev
```

```json
"build": "electron-builder"
```

这一句要加上，不然打包不会成功

```shell
npm install pnpm
```
