VuePressやってみた
====

- 静的サイトジェネレーター。
- Markdownを書くだけでシンプルな静的サイトが作成でき、ドキュメント内でVueコンポーネントを使えるのが特徴です。

https://app.codegrid.net/entry/2018-vuepress-1#vue-

## 0. 公式
https://vuepress.vuejs.org/

## 1. セットアップ

$ yarn create vuepress-site study-vuepress

```
yarn create v1.16.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning "@vue/cli > jscodeshift@0.9.0" has unmet peer dependency "@babel/preset-env@^7.1.6".
warning "@vue/cli-service-global > @vue/babel-preset-app@4.1.2" has unmet peer dependency "@babel/core@*".
[4/4] 🔨  Building fresh packages...

success Installed "create-vuepress-site@0.4.2-beta" with binaries:
      - create-vuepress-site
? What's the name of your project? study-vuepress
? What's the description of your project?
? What's your email? kondo_yuichi_gn@cyberagent.co.jp
? What's your name? kondo
? What's the repo of your project?
   create study-vuepress/docs/.gitignore
   create study-vuepress/docs/package.json
   create study-vuepress/docs/src/.vuepress/components/demo-component.vue
   create study-vuepress/docs/src/.vuepress/components/Foo/Bar.vue
   create study-vuepress/docs/src/.vuepress/components/OtherComponent.vue
   create study-vuepress/docs/src/.vuepress/config.js
   create study-vuepress/docs/src/.vuepress/enhanceApp.js
   create study-vuepress/docs/src/.vuepress/styles/index.styl
   create study-vuepress/docs/src/.vuepress/styles/palette.styl
   create study-vuepress/docs/src/config/README.md
   create study-vuepress/docs/src/guide/README.md
   create study-vuepress/docs/src/guide/using-vue.md
   create study-vuepress/docs/src/index.md
📋 Copied to clipboard, just use Ctrl+V
✨ File Generate Done
✨  Done in 46.22s.
```

### 中身見てみる

$ ll study-vuepress

```
total 0
drwxr-xr-x  5 b05357  CATK\Domain Users   160B 11  5 13:41 docs
```

$ tree study-vuepress/docs -a

```
study-vuepress/docs
├── .gitignore
├── package.json
└── src
    ├── .vuepress
    │   ├── components
    │   │   ├── Foo
    │   │   │   └── Bar.vue
    │   │   ├── OtherComponent.vue
    │   │   └── demo-component.vue
    │   ├── config.js
    │   ├── enhanceApp.js
    │   └── styles
    │       ├── index.styl
    │       └── palette.styl
    ├── config
    │   └── README.md
    ├── guide
    │   ├── README.md
    │   └── using-vue.md
    └── index.md

7 directories, 13 files

```

## 2. ローカルで立ち上げる

$ yarn

$ yarn dev

```
success [14:24:13] Build 807838 finished in 6921 ms!
> VuePress dev server listening at http://localhost:8080/
```

### ビルド

$ yarn build

```
success Generated static files in src/.vuepress/dist.
```

## 3. GitHub Pagesでホスティング

`gh-pages` ブランチに `src/.vuepress/dist` をpushすると

https://kondo-yuichi-gn.github.io/study-vuepress/　
で見れる


- github で study-vuepress リポジトリを作る
- github 管理する

```
$ git init
$ git remote add origin git@github.com:kondo-yuichi-gn/study-vuepress.git
$ git add .
$ git branch -M main
$ git commit -m "first commit"
$ git push -u origin main
```

- `push-dir` っていうのを入れると 特定のディレクトリのみpushできるらしい

参考：https://app.codegrid.net/entry/2018-vuepress-1#github-pages-

$ yarn add push-dir

- package.ison

```
  "scripts": {
    "dev": "vuepress dev src",
    "build": "vuepress build src",
+  "deploy": "push-dir --dir=./src/.vuepress/dist --branch=gh-pages --cleanup"
```

$ yarn deploy

```
yarn run v1.16.0
$ push-dir --dir=./src/.vuepress/dist --branch=gh-pages --cleanup
✨  Done in 5.20s.
```

https://kondo-yuichi-gn.github.io/study-vuepress/


- /docs/src/.vuepress/config.js

```
module.exports = {
+  base: '/study-vuepress/',
```
