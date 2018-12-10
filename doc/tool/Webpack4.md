## Webpack4

[原文](https://webpack.js.org)

* **Entry Points：入口**
```js
//单一条目（速记）语法: entry: string|Array<string>
module.exports = {
  entry: './path/to/my/entry/file.js'
};
//对象语法: entry: {[entryChunkName: string]: string|Array<string>}
module.exports = {
  entry: {
    app: './src/app.js',
    adminApp: './src/adminApp.js'
  }
};
```

* **Output：输出**
```js
//用法
module.exports = {
  output: {
    filename: 'bundle.js',
  }
};
//多个入口点
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
};
//哈希
module.exports = {
  //...
  output: {
    path: '/home/proj/cdn/assets/[hash]',
    publicPath: 'http://cdn.example.com/assets/[hash]/'
  }
};
```

* **Mode：模式**
```js
/*
production:生产
development:开发
none:选择退出任何默认优化选项
*/
//用法:配置
module.exports = {
  mode: 'production'
};
//用法:CLI
webpack --mode=production
```

* **Loaders：加载器**
```js
//用法：配置
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
//组合
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          },
          { loader: 'sass-loader' }
        ]
      }
    ]
  }
};
//用法：内联
import Styles from 'style-loader!css-loader?modules!./styles.css';
//用法：CLI
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```

* **Plugins：插件**
```js
//用法
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins
const path = require('path');
module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

* **建立项目**
```js
//初始化
mkdir webpack-demo && cd webpack-demo
npm init -y //package.json
npm install webpack webpack-cli --save-dev
//配置：新建webpack.config.js
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
};
//创建dist/index.html文件
<script src="main.js"></script>
//修改package.json
"build": "webpack"
```

* **加载**
```js
/*
include：仅应用实际需要由其转换的加载程序模块
exclude：排除不需要由其转换的加载程序模块
*/
//加载css
1、npm install --save-dev style-loader css-loader
2、{
      test: /\.css$/,
      use: [
          "style-loader",
          "css-loader"
      ]
    }
3、import './style.css';
//加载图片
1、npm install --save-dev file-loader
2、{
        test: /\.(png|svg|jpg|gif)$/,
        use: [
            "file-loader"
        ]
    }
3、css：url('./my-image.png')
4、html：<img src="./my-image.png" />
//加载字体：[字体兼容性](https://juejin.im/post/5aefebb6f265da0ba60fb714)
1、npm install --save-dev file-loader
2、{
        test: /\.(woff|woff2|eot|ttf|otf)$/,
        use: [
            "file-loader"
        ]
    }
3、css：@font-face {
             font-family: 'MyFont';
             src:  url('./MoMoYueYaTi-2.woff') format('woff');
             font-weight: 600;
             font-style: normal;
         }
         .hello {
             font-family: 'MyFont';
         }
//加载数据格式：转换成默认支持的json格式
1、npm install --save-dev csv-loader xml-loader
2、{
        test: /\.(csv|tsv)$/,
        use: [
            "csv-loader"
        ]
    },
    {
        test: /\.xml$/,
        use: [
            "xml-loader"
        ]
    }
3、import Data from './data.xml';
//使用es6
1、npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
2、{
        test: /\.js$/,
             exclude: /node_modules/,
             use: {
                 loader: 'babel-loader',
                 options: {
                     presets: ['@babel/preset-env'],
                     plugins: ['@babel/plugin-transform-runtime']
                 }
             }
         }
//使用TypeScript
1、npm install --save-dev typescript ts-loader
2、创建tsconfig.json
    {
      "compilerOptions": {
        "outDir": "./dist/",
        "sourceMap": true,
        "noImplicitAny": true,
        "module": "es6",
        "target": "es5",
        "jsx": "react",
        "allowJs": true
      }
    }
3、{
      test: /\.tsx?$/,
      use: [
          {
            loader: 'ts-loader',
            options: {
              transpileOnly: true, //获得更快的增量构建
              experimentalWatchApi: true,
            },
          },
        ],
      exclude: /node_modules/
    }
    resolve: {
      extensions: [ '.tsx', '.ts', '.js' ]
    }
```

* **插件**
```js
//输出html文件
1、npm install --save-dev html-webpack-plugin
2、const HtmlWebpackPlugin = require('html-webpack-plugin');
    new HtmlWebpackPlugin({
        title: 'Output Management'
    })
//清理/dist文件夹
1、npm install --save-dev clean-webpack-plugin
2、const CleanWebpackPlugin = require('clean-webpack-plugin');
    new CleanWebpackPlugin(['dist'])
```

* **development：开发模式**
```js
//源映射：准确定位错误
devtool: 'inline-source-map'
//更新自动编译
1、观察模式：必须刷新浏览器才能看到更改
"watch": "webpack --watch"
2、webpack-dev-server：浏览器自动刷新
    1、npm install --save-dev webpack-dev-server
    2、devServer: {
            contentBase: './dist'
          }
    3、"start": "webpack-dev-server --open" //启动localhost:8080
3、webpack-dev-middleware：包装器
    1、npm install --save-dev express webpack-dev-middleware
    2、output: {
            ...
            publicPath: '/'
        }
    3、新建server.js
        const express = require('express');
        const webpack = require('webpack');
        const webpackDevMiddleware = require('webpack-dev-middleware');

        const app = express();
        const config = require('./webpack.config.js');
        const compiler = webpack(config);

        // Tell express to use the webpack-dev-middleware and use the webpack.config.js
        // configuration file as a base.
        app.use(webpackDevMiddleware(compiler, {
          publicPath: config.output.publicPath
        }));

        // Serve the files on port 3000.
        app.listen(3000, function () {
          console.log('Example app listening on port 3000!\n');
        });
    4、"server": "node server.js" //启动localhost:3000
//热模块更新：webpack-dev-server（更新print.js、更新css文件 浏览器局部刷新页面）
1、const webpack = require('webpack');
    entry：去掉 print: './src/print.js'
    devServer: {
          ...
          hot: true
    }
    plugins: [
          ...
          new webpack.HotModuleReplacementPlugin()
    ]
2、index.js
if (module.hot) {
    module.hot.accept('./print.js', function() {
      console.log("print文件更新");
    })
}
//nginx代理：webpack-dev-server（模仿生产环境）
1、nginx配置文件添加
    server {
      location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        error_page 502 @start-webpack-dev-server;
      }

      location @start-webpack-dev-server {
        default_type text/plain;
        return 502 "Please start the webpack-dev-server first.";
      }
    }
2、启动：webpack-dev-server --public 10.10.10.本机ip --watch-poll
```

* **production：生产模式**
```js
//配置不同模式
1、npm install --save-dev webpack-merge
2、删除webpack.config.js
    1、webpack.common.js
        const path = require('path');
        const CleanWebpackPlugin = require('clean-webpack-plugin');
        const HtmlWebpackPlugin = require('html-webpack-plugin');
        module.exports = {
            entry: {
                app: './src/index.js'
            },
            output: {
                filename: '[name].bundle.js',
                path: path.resolve(__dirname, 'dist')
            },
            plugins: [
                new CleanWebpackPlugin(['dist']),
                new HtmlWebpackPlugin({
                      title: 'Production'
                })
            ]
        };
    2、webpack.dev.js
        const merge = require('webpack-merge');
        const common = require('./webpack.common.js');
        module.exports = merge(common, {
            mode: 'development',
            devtool: 'inline-source-map',
            devServer: {
                contentBase: './dist'
            }
        });
    3、webpack.prod.js
        const merge = require('webpack-merge');
        const common = require('./webpack.common.js');
        module.exports = merge(common, {
            mode: 'production'
        });
3、"start": "webpack-dev-server --open --config webpack.dev.js"
    "build": "webpack --config webpack.prod.js"
4、index.js：process.env.NODE_ENV === 'production'|'development'
//源映射：准确定位错误
devtool: 'source-map'
```