babel 配置
****

yarn add @babel/core @babel/preset-env babel-loader

.babelrc
```
// presets，也就是一堆plugins的预设，起到方便的作用
{
  "presets": [
    "@babel/preset-env"
  ]
}


{
  "presets": ["env"],
  "plugins": ["transform-decorators-legacy"]
}

```

