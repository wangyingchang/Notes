##### 1.webpack4 概念

webpack是javascript应用程序的静态模块打包器(module bundler);它会递归地构建依赖关系图(dependency graph)



##### 2.webpack4 entry

webpack.config.js

~~~javascript
const config={
    entry:'./index.js'
};
module.exports=config;
~~~



##### 3.webpack4 output

webpack.config.js

~~~javascript
const path=require('path');
module.exports={
    entry:'./index.js',
    output:{
    	path:path.resovle(_dirname,'dist'),
    	filename:'bundle.js'
	}
}
~~~



##### 4.webpack4 loader

*loader* 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效[模块](https://www.webpackjs.com/concepts/modules)，然后你就可以利用 webpack 的打包能力，对它们进行处理。

webpack.config.js

~~~javascript
const path=require('path');
module.exports={
    entry:'./index.js',
    output:{
    	path:path.resovle(_dirname,'dist'),
    	filename:'bundle.js'
	},
    moudle:{
        rules:[
            {
                test:/\.txt$/,
                use:'raw-loader'
            }
        ]
    }
}
~~~



##### 5.webpack4 plugins

webpack.config.js

~~~javascript
const path=require('path');
const HtmlWebpackPlugin=require('html-webpack-plugin');// 通过 npm 安装
const webpack=require('webpack');//用户访问内置插件
module.exports={
    entry:'./index.js',
    output:{
    	path:path.resovle(_dirname,'dist'),
    	filename:'bundle.js'
	},
    moudle:{
        rules:[
            {
                test:/\.txt$/,
                use:'raw-loader'
            }
        ]
    },
    plugins:[
        new HtmlWebpackPlugin({
            template: './src/index.html'
        })
    ]
}
~~~



##### 6.webpack4 mode

通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，你可以启用相应模式下的 webpack 内置的优化

webpack.config.js

~~~javascript
const path=require('path');
const HtmlWebpackPlugin=require('html-webpack-plugin');// 通过 npm 安装
const webpack=require('webpack');//用户访问内置插件
module.exports={
    entry:'./index.js',
    output:{
    	path:path.resovle(_dirname,'dist'),
    	filename:'bundle.js'
	},
    moudle:{
        rules:[
            {
                test:/\.txt$/,
                use:'raw-loader'
            }
        ]
    },
    plugins:[
        new HtmlWebpackPlugin({
            template: './src/index.html'
        })
    ],
    mode:'production'
}
~~~

