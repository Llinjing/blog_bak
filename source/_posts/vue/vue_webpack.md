---
title: vue webpack project 介绍
---
<div align=left>
    <img src="/img/vue/20170927151927.jpg" width="" height="" alt=""/>
</div>
这里介绍如何使用vue webpack 进行项目的创建。

+ <!-- more -->


## 使用webpack simple

### 创建simple 项目
```
vue init webpack-simple vue-simple
```

### 目录结构

```
├─.babelrc		// babel配置文件
├─.gitignore	
├─index.html		// 主页
├─package.json		// 项目配置文件
├─README.md  
├─webpack.config.js	// webpack配置文件
├─dist			// 发布目录
│   ├─.gitkeep       
├─src			// 开发目录	
│   ├─App.vue		// App.vue组件
│   ├─main.js		// 预编译入口
```

### webpack.config.js
```
var path = require('path')
var webpack = require('webpack')

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'build.js'
  },
  resolveLoader: {
    root: path.join(__dirname, 'node_modules'),
  },
  module: {
    loaders: [
      {
        test: /\.vue$/,
        loader: 'vue'
      },
      {
        test: /\.js$/,
        loader: 'babel',
        exclude: /node_modules/
      },
      {
        test: /\.json$/,
        loader: 'json'
      },
      {
        test: /\.html$/,
        loader: 'vue-html'
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'url',
        query: {
          limit: 10000,
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  devServer: {
    historyApiFallback: true,
    noInfo: true
  },
  devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    }),
    new webpack.optimize.OccurenceOrderPlugin()
  ])
}
```
webpack.config.js内容还是比较好理解的，它采用了CommonJS的写法，entry节点配置了编译入口，output节点配置了输出。
这段entry和output配置的含义是：编译src/main.js文件，然后输出到dist/build.js文件

### 安装依赖
```
cd my-webpack-simple-demo
npm install
```
安装完成后，目录下会产生一个node_modules文件夹。

### 运行
```
npm run dev
```
执行npm run dev命令后并不会在dist目录下生成build.js文件，开发环境下build.js是在运行内存中的

### 发布
```
npm run build
```
执行该命令会生成发布时的build.js，并且是经过压缩的


## 使用vue-webpack模板
### 创建项目
```
vue init webpack vue-webpack-demo
```

### vue webpack project 目录结构

```
├── build/                      # webpack config files
│   └── ...
├── config/                     
│   ├── index.js                # main project config
│   └── ...
├── src/
│   ├── main.js                 # app entry file
│   ├── App.vue                 # main app component
│   ├── components/             # ui components
│   │   └── ...
│   └── assets/                 # module assets (processed by webpack)
│       └── ...
├── static/                     # pure static assets (directly copied)
├── test/
│   └── unit/                   # unit tests
│   │   ├── specs/              # test spec files
│   │   ├── index.js            # test build entry file
│   │   └── karma.conf.js       # test runner config file
│   └── e2e/                    # e2e tests
│   │   ├── specs/              # test spec files
│   │   ├── custom-assertions/  # custom assertions for e2e tests
│   │   ├── runner.js           # test runner script
│   │   └── nightwatch.conf.js  # test runner config file
├── .babelrc                    # babel config
├── .editorconfig.js            # editor config
├── .eslintrc.js                # eslint config
├── index.html                  # index.html template
└── package.json                # build scripts and dependencies
```

### 安装依赖
```
cd my-webpack-demo
npm install
```

### 运行
```
npm run dev

```

### 发布
```
npm run build

```
和vue-simple-webpack模板不同的是，所有的静态资源，包括index.html都生成到dist目录下了。这意味着你可以直接拿着dist目录去发布应用，例如在IIS下将dist目录发布为一个网站。





