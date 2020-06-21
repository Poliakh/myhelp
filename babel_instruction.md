# Инструкция Babel
1. Создание папки проекта
	>__mkdir [name project]__
2. Войти  в папку проекта
	>__cd [name project]__
3. Инициализация добавить флаг  "-y" для согласия на все вопросы.
	>__npm init__
4. __npm install --save-dev @babel/core @babel/cli__ - установка  babel
5. Запуск  babel, 'src' - источник, 'build' имя папки для переноса файлов

	>__npx babel src --out-dir build__

6.Установка плагинов:
- Утановка плагина babel.
	>__npm install --save-dev @babel/plugin-transform-template-literals__ 

	* Запуск установленного плагина
		>__npx babel *src* --out-dir *build* --plugins @babel/plugin-transform-template-literals__
- Устновка плагина трансформации классов и 
	>__npm install --save-dev @babel/plugin-transform-classes @babel/plugin-transform-block-scoping__
	* Запуск плагинов с указанием входящхи и исходящих папок
		>__npx babel *src* --out-dir *build* --plugins @babel/plugin-transform-template-literals,@babel/plugin-transform-classes,@babel/plugin-transform-block-scoping__
7. Создаем файл конфигурации  babel - ".babelrс". В формате json прописываем конфиругацию
8. Далее плагин запускаются командой 

		npx babel src --out-dir build
## Установка всех плагинов
__babel-preset-env__ - пресет содержащий все плагинамы babel

9. Установка пресета
	>__npm install --save-dev @babel/preset-env__
10. В файле конфигурации ".babelrs" оставляем 

		{
		  "presets":["@babel/preset-env"]
		}
	и снова запускаем babel __npx babel *src* --out-dir *build*__
11. Устанавливаем и добавляем обавляем плагин для обработки не вошедших в стандарт, например поля классов ( в _.babelrc_)
	>__npm install --save-dev @babel/plugin-proposal-class-properties__

		{
			"presets":["@babel/preset-env"],
			"plugins":[
				"@babel/plugin-proposal-class-properties"
			]
		}

		одно и тоже ->

		{
			"presets":["@babel/env"],
			"plugins":[
				"@babel/proposal-class-properties"
			]
		}
12. Babel можно оптимизировать строго для определенных версий файлов, для этого в конфигурации необходимо плагин задать как новый массив вместе с объектом свойств для этого плагина. т.е.

		{
			"presets":[[
			"@babel/preset-env",
			{
				"tergets":{
					"edge:"18",
					"chrome":"74"
				}
			}
			]],
			"plugins":[
				"@babel/plugin-proposal-class-properties"
			]
		}

	Динамическая поддержка браузеров

			{
				"presets":[[
					"@babel/env",
					{
						"debug":true,
						"targets":[
							"last 2 chrome versions",
							"last 2 firefox versions",
							"last 2 ios versions"
						]
					}]],
				"plugins":[
					"@babel/proposal-class-properties"
				]
			}
	__"debug":true__ - отобразит поддерживаемы браузеры в терминале и список примененных плагинов для адаптации

	[**browserslist**](https://github.com/browserslist/browserslist) - опенсерс проект, можно посмотреть как задать другие выражения для выбора комбинаций браузеров
	например:

			"targets":[
				">0.3%",
				"not ie > 0"
			]

	Такое вырожение говорит, выбрать браузеры используемые более 30% польщователей, кроме всех версий IE.

13.
			"targets":[
					"last 2 chrome versions",
					"last 2 firefox versions",
					"last 2 ios versions"
				]
	Эту часть конфигурации .babelrс бывает удобнее перенести в файл конфигурации package.json и добавтиь там аналагичное свойство:

			"browserslist":[
				"last 2 chrome versions",
				"last 2 firefox versions",
				"last 2 ios versions"
			]

	и еще вариант:
	* можно создать дополнительный файл конфигурации __.browserslistrc__ и в этом файле прописать конфигурацию уже следующим образом

			last 2 chrome versions
			last 2 firefox versions
			last 2 ios versions
			
	т.е. просто список без кавычек
	
	Можно посмотреть в терминале версии билдов командой
	>npx browserslist

14. Polyfills
Для подключения библиотеки полифилов необходимо установить соостветсвующий плагин.

	>npm install core-js

	затем добавляем несколько параметров конфигурации в пресет /env

			"corejs":3,
			"useBuiltIns":"usage"

	3 - версия  corejs
	* __"useBuiltIns":"usage"__ - (рекомендуется)подключит только те полифилы в нашем коде которые необходимы для поддержки указанных нами версий бразуеров.
	* __"useBuiltIns":"etnry"__ - добавит обсолютно все полифилы для требуемых браузеров в начале главного файла js на месте строки "import "core-js;" которую необходимо предварительно туда поместить.

	В итоге получим следующую конфигурацию:

			{
				"presets":[[
					"@babel/env",
					{
						"corejs":3,
						"useBuiltIns":"usage",
						"debug":true
						// "targets":[
						// 	"last 2 chrome versions",
						// 	"last 2 firefox versions",
						// 	"last 2 ios versions"
						// ]
					}]],
				"plugins":[
					"@babel/proposal-class-properties"
				]
			}

	__"modules":false__ в файле .babelrс скажет бабелю не добавлять полифил модулей файлов  js  таккак веб-пак сам умеет работать с модулями.

15. Для транспиляции JSX  необходимо установить следующие библиотеки:
	>__npm install react react-dom__\
	>__npm install --save-dev @babel/preset-react__
	Далее необходимо добавить конфигурацию _.babelrc_ -> presets следующее

		"@babel/react"
	получим в _.babelrc_:

		{
			"presets":[[
				"@babel/env",
				{
					"corejs":3,
					"useBuiltIns":"usage",
					"debug":true,
					"modules":false
				}],
			"@babel/react"],
			"plugins":[
				"@babel/proposal-class-properties"
			]
		}

