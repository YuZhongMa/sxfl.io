---
layout: post
title: webpack
category: 资源
tags: webpack
keywords: webpack
description: 
---
## webpack+babel
直接看配置代码
``` js
const webpack = require('webpack');
const path = require('path');
module.exports = {
	entry: {
		index: './src/app.js'
	},
	output: {
		path: __dirname+'/build',
		filename: 'app.js'
	},
	module: {
		loaders: [{
			test: /\.js$/,
			exclude: /node_modules/,
			use: [
				"babel-loader"//引用loader
			]
		}]
	},
	devtool: 'eval-source-map'//将报错信息指向源文件，而不是build文件
}
、、、
#### 目前只是实现了兼容es6