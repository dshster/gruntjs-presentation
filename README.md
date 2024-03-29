# gruntjs task runner

Менеджер задач (?)

javascript, nodejs, npm

Инструмент для запуска задач (task).

Каждая задача в виде внешнего модуля с описанием параметров в json

npm (nodejs package manager) менеджер nodejs модулей

package.json - описание модулей и зависимостей для npm, а так же информация о модуле

https://www.npmjs.org/doc/json.html

## Установка и настройка

### nodejs, npm

Установить nodejs (http://nodejs.org/) (под windows убедиться, что путь с установленной программой прописан в переменную окружения ``path`` и вызывается ``npm``)

### gruntjs

Командный интерфейс Grunt необходимо установить глобальным модулем:
```
npm install -g grunt-cli
```

###  package.json

В корневой папке рабочего проекта создать ``package.json`` со списком используемых модулей (включая модуль grunt):

```
{
	"name": "project-name",
	"author": "Dmitry Shvalyov <*@*>",
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

###### Конфигурация модуля

**cssmin**

```
cssmin: {
    options: {
        banner: "/* minified css file */",
        report: "gzip"
    },
    files: {
        "styles.min.css": ["style-one.css", "style-two.css"]
    }
}
```
Если необходимо добавить несколько вариантов параметров модуля, например ``production``, ``development``, ``testing``, то добавляем дополнительные секции:

```
cssmin: {
    production: {
        options: {
            banner: "/* production css file */",
            report: "gzip"
        },
        files: {
            "styles.min.css": ["style-one.css", "style-two.css"]
        }
    },
    development: {
        options: {
            banner: "/* development css file */",
            report: "gzip"
        },
        files: {
            "styles.min.css": ["style-one.css", "style-two.css"]
        }
    }
}
```
Вызов конкретной секции - ``cssmin:production`` или ``cssmin:development``, если при вызове задачи секция не указана вызывается первая секция:

```
grunt.registerTask('default', ['cssmin:production']);
```

###  file mappings

**static mappings**

``'lib/source.js'``, ``'lib/module/engine.js'``

**dynamic mappings**

``'lib/*.js'``, ``'lib/*/*.js'``, ``'lib/**/engine.js'``

###  templates

Подстановка значений в текстовые переменные ``<% %>``, например: ``<%= grunt.template.today('yyyy-mm-dd') %>``. Значения подставляемые через шаблоны так же могут быть и массивами и объектами.

Например подстановка значения ``name`` из загруженного файла ``package.json``

```
options: {
  banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
},
dist: {
  src: 'src/<%= pkg.name %>.js',
  dest: 'dist/<%= pkg.name %>.min.js'
}
```

# Ссылки

* http://nodejs.org/
* https://github.com/gruntjs
* http://gruntjs.com/getting-started
* https://www.npmjs.org/doc/json.html