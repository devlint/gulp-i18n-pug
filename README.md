# gulp-pug-i18n

[![Build Status](https://travis-ci.org/felixzapata/gulp-pug-i18n.png)](https://travis-ci.org/felixzapata/gulp-pug-i18n)

[![Package Quality](http://npm.packagequality.com/badge/gulp-pug-i18n.png)](http://npm.packagequality.com/badge/gulp-pug-i18n.png)

> Gulp plugin to compile Pug templates with internationalization support based on JS/JSON/YAML files

Inspired by [grunt-pug-i18n](https://github.com/AdesisNetlife/grunt-pug-i18n).

It adds high level support for Pug template internationalization based on JSON/YAML/JS files.

### Usage

#### Example JSON locale file (es_ES.json)
```json
{
  "hello": {
    "world": "Hola Mundo"
  }
}
```

##### Example Pug template
```pug
body
  h1 #{$i18n.hello.world}!
  p Using locale #{$localeName}
```

```javascript
gulp.task('pugI18n', function () {
  var options = {
    i18n: {
      dest: 'dist',
      locales: 'test/locales/*.*'
    },
    pretty: true
  };
  return gulp.src('myPugTemplates/directory/*.pug')
    .pipe(pugI18n(options))
    .pipe(gulp.dest(options.i18n.dest));
});
```

```javascript
gulp.task('pugI18n', function () {
  var options = {
    i18n: {
      locales: 'test/locales/*',
      namespace: '$t',
      localeExtension: true
    },
    client: false,
    pretty: true
  };
  return gulp.src('myPugTemplates/directory/*.pug')
    .pipe(pugI18n(options))
    .pipe(gulp.dest(options.i18n.dest));
});
```

```javascript
gulp.task('pugI18n', function () {
  var options = {
    i18n: {
      dest: '.tmp'
    },
    data: {
      $i18n: {
        message: 'Hello world!',
        nested: {
          msg: 'and hello to you'
        }
      }
    },
    pretty: true
  };
  return gulp.src('myPugTemplates/directory/*.pug')
    .pipe(pugI18n(options))
    .pipe(gulp.dest(options.i18n.dest));
});
```

### Options

Only `i18n` specific options are listed below


#### locales
Type: `string|array`

Path to localization files. Please check the examples in tests. Glob patterns can be used

`JSON`, `YAML` and `JS` formats are supported for the translation templates

#### namespace
Type: `string`
Default: `$i18n`

Namespace to expose translation keys in Pug template

#### localeExtension
Type: `boolean`
Default: `false`

Generate the HTML output files with the extension prefix with the current language.
By default it will create different folders for each language

Setting this option into `true`, the generated HTML files will look like this:
```
html/
├── view.en-en.html
└── view.es-es.html
```
... instead of:
```
html/
├── en-EN/
│   └── view.html
└── es-ES/
    └── view.html
```

## License

MIT © [Felix Zapata](http://github.com/felixzapata)