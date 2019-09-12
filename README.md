
# start

安装依赖
```
> npm i
```

开发环境
```
> npm run dev
```

打包
```
> npm run build
```

# 在webpack下适配配置

在项目下安装
```
npm i postcss-import postcss-px-to-viewport postcss-write-svg postcss-cssnext postcss-viewport-units cssnano --save-dev
```
修改 postcss.config.js
```
module.exports = { 
  plugins: [ 
    require('autoprefixer')({    // 浏览器加前缀
     /*...options*/
      broswers: [
        'defaults',
        'not ie < 11',
        'last 7 versions',
        '> 1%',
        'iOS 7',
        'last 3 iOS versions'
      ]
    }),
    require('postcss-import'),
    require('postcss-write-svg')({
      uft8: false
    }),
    require('postcss-cssnext'),
    require('postcss-px-to-viewport')({
      viewportWidth: 1920, // 视窗的宽度，对应的是我们设计稿的宽度，一般是750
      viewportHeight: 1080, // 视窗的高度，根据750设备的宽度来指定，一般指定1334，也可以不配置
      unitPrecision: 3, // 指定`px`转换为视窗单位值的小数位数（很多时候无法整除）
      viewportUnit: 'vw', // 指定需要转换成的视窗单位，建议使用vw
      selectorBlackList: ['.ignore', '.hairlines'], // 指定不转换为视窗单位的类，可以自定义，可以无限添加,建议定义一至两个通用的类名
      minPixelValue: 1, // 小于或等于`1px`不转换为视窗单位，你也可以设置为你想要的值
      mediaQuery: false // 允许在媒体查询中转换`px`
    }),
    require('postcss-viewport-units'),
    require('cssnano')({
      autoprefixer: true, // 和cssnext同样具有autoprefixer，保留一个
      'postcss-zindex': false
    }),
  ] 
}
```

插件介绍
`postcss-cssnext`：其实就是cssnext。该插件可以让我们使用CSS未来的特性，其会对这些特性做相关的兼容性处理。
`cssnano`：主要用来压缩和清理CSS代码。
`postcss-px-to-viewport`：要用来把px单位转换为vw、vh、vmin或者vmax这样的视窗单位，也是vw适配方案的核心插件之一。
`postcss-write-svg`：插件主要用来处理移动端1px的解决方案。该插件主要使用的是border-image和background来做1px的相关处理。

## 参考文档
https://www.cnblogs.com/kdcg/p/9106463.html



