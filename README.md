# gruntjs task runner

Менеджер задач (?)

javascript, nodejs, npm

Инструмент для запуска задач (task).

Каждая задача в виде внешнего модуля с описанием параметров в json

npm (nodejs package manager) менеджер nodejs модулей

package.json - описание модулей и зависимостей для npm, а так же информация о модуле

https://www.npmjs.org/doc/json.html

## Установка

### nodejs, npm

Установить nodejs (http://nodejs.org/) (под windows убедиться, что путь с установленной программой прописан в переменную окружения ``path`` и вызывается ``npm``)

### gruntjs

Командный интерфейс Grunt необходимо установить глобальным модулем:
```
npm install -g grunt-cli
```

###  package.json

В корневой папке рабочего проекта создать ``package.json`` со списком используемых модулей (включая модуль gruntjs):

```
{
	"name": "project-name",
	"author": "Dmitry Shvalyov <dshvalyov@igsystems.ru>",
	"devDependencies": {
		"grunt": "~0.4.0",
		"grunt-contrib-cssmin": "latest",
		"grunt-contrib-concat": "0.4.0",
		"grunt-contrib-watch": "~0.6.0"
	}
}
```

где для каждого модуля указана точная, примерная и последняя (latest) версия.

Установка модулей в папку проекта:
```
npm install
```

если используется СКВ git, то созданную при установке модулей папку ``node_modules`` необходимо добавить в ``.gitignore``

### Gruntfile.js

###### Обертка (wrapper function)
```
module.exports = function(grunt) {
	"use strict";

};
```

###### Загрузка модулей
```
grunt.loadNpmTasks('grunt-contrib-cssmin');
grunt.loadNpmTasks('grunt-contrib-concat');
grunt.loadNpmTasks('grunt-contrib-watch');
```

###### Задача по-умолчанию (без задач)

запускается при вызове grunt без передачи параметров

```
grunt.registerTask('default', []);
```

###### Конфигурация проекта
с загрузкой данных о проекте из файла ``package.json``
```
grunt.initConfig({
	pkg: grunt.file.readJSON('package.json'),
});
```

###### Конфигурация модулей

**cssmin**

```
cssmin: {
    production: {
        options: {
            banner: "/* minified css file */",
            report: "gzip"
        },
        files: {
            "styles.min.css": ["style-one.css", "style-two.css"]
        }
    }
}
```

# Ссылки

* http://nodejs.org/
* https://github.com/gruntjs
* http://gruntjs.com/getting-started
* https://www.npmjs.org/doc/json.html