## Инструкция WebPack
* Установка 
	>npm install --save-dev webpack webpack-cli
* запуск  _webpack_ 
	>npx webpack

	в таком режиме вебпак запустит сборку по умолчанию (продакшн) если найдет папку _'src'_ и в ней _'index.js'_.
	Для запуска мода разработчика :
	>npx webpack --mode development
* Создаем файл конфигурации  _webpack.config.js_
	первая конфигурация

		module.exports = {
			mode: "development"
		}
	
* в файле _package.json_ в разделе _script_  добавляем конфигурацию
			
		"sctipt":{
			"start": "webpack"
		}
	После этого запускаем нашу  конфигурацию  webpack командой 
	>npm start
* Установка лодаеров для обработки других файлов
	>npm install --save-dev file-loader
* добавялем в конфиг новую конфигурацию  _"model"_ и правила  _"role"_

```
	module.exports = {
		mode: "development",

		module: {
			rules:[
			  {
			    test:/\.png$/,
			    use:[{ loader: 'file-loader' }]
			  }
			]
		}
	};

	...
```

* Установка babel-loader:
	>npm install --save-dev babel-loader
	конфигурация babel добавляем в раздел _module -> rule_ 

			// Loading javascript-files
			{
				test: /\.js$/,
				exclude: /node_modules/, // - исключаем файды с таким названием
				use:[
					{loader: 'babel-loader'}
				]
			}

* Установка css-loader:
	>npm install --save-dev css-loader

			// Loading style css
			{
				test: /\.(css)$/,
				use:[
					{loader: 'css-loader'}
				]
			}
	+ Устанавливаем style-loader для (не понял зачем этот модуль...)
		>npm install --save-dev style-loader

		И добавим в ту же конфигурацию

			// Loading style css
			{
				test: /\.(css)$/,
				use:[
					{loader: 'style-loader'},
					{loader: 'css-loader'}
				]
			}

		тут первым будет обработан _'css-loader'_, затем _'style-loader'_

* Поддержка SASS
	устанавливаем два лоудера:
	> npm install --save-dev node-sass sass-loader

	Добавляем конфигурацию 

		{
			test: /\.(s[ac]ss)$/,
			use:[
				{loader: 'style-loader'},
				{loader: 'css-loader'},
				{loader: 'sass-loader'}
			]
		}

* можно упростить синтаксис

		{
			test: /\.(s[ac]ss)$/,
			use:[
				{'style-loader', loader: 'css-loader', 'sass-loader'}
			]
		}

	А если у одного из лоадеров есть опции то их можно дописать в виде:

			{
				test: /\.(s[ac]ss)$/,
				use:[
					{'style-loader', loader: 'css-loader'},
					{
						loader: 'sass-loader',
						options: {
							outputPath: 'style',
							name: '[name].[ext]'
						}
					}
				]
			}
* Плагины
	Установим плагин
	>npm install --save-dev html-webpack-plugin
	
	В отличии от лоадеров, плагины необходимо импортировать файле конфигурации:

			const HtmlWebpackPlugin = require('html-webpack-plugin');

	+ Создаем в папке проекта папку _public_, переносим в неё наш  _index.html_ удаляем в нем строку с тегом _script_, плагин добавит её самостоятельно, и добавляем в файл конфигурации в корневые свойства новую конфигурацию в консруктор корого мы передаем настройки этой конфигурации в виде объекта

				plugins:[
					new HtmlWebpackPlugin({
						template: 'public/index.html'
					})
				]

* Готовим в продакшену

	Устанаваливаем плагин
	> npm install --save-dev mini-css-extract-plugin

	Так как это плагин, его необходимо также импортировать в файле конфигурации:

		const MiniCssExtractPlugin = require('mini-css-extract-plugin');

	И добавить конфигурацию

		plugins:[
			new HtmlWebpackPlugin({
				template: 'public/index.html'
			}),
			new MiniCssExtractPlugin({
				filename:'main-[hash:8].css'
			})
		]

	строка __filename:'main-[hash:8].css'__ необходиом для того, что все файлы стилей были уникальными и не было пролема в браузерах при загрузке новых файлов с таким же именем. 

	также необходимо заменить лоадер _'{loader: 'style-loader'}'_ на _'MiniCssExtractPlugin.loader'_

	> -для dev версии лучше использовать _{loader: 'style-loader'}_\
	 -для production  _MiniCssExtractPlugin.loader_

	* Server
	Устанавливаем утилиту _webpack-dev-server_
		Это не лоадер и не плагин, это отдельная утилита.
		Так как это главная утилита, и именно она запускает сборщик вебпак, необходимо внести изменения  в параметры запуска сборщика в файле _package.json_

			"scripts": {
				"start": "webpack-dev-server",
				"build":"webpack",
			},

	В это случае при запуске команды __npm start__  мы запустим сервер  который в свою очередь запустит сборщик webpack , но для запуска самого сборщика теперь необходимо запускать команду __npm run build__ __ЧАСТАЯ ОШИБКА!!!__ 

	конфигурация сервера

			devServer: {
				open: true //автоматически откроет браузер
			}

* Конфигурация для production.

	
