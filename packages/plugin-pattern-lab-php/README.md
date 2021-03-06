# Pattern Lab Plugin for Theme Tools

> Theme core plugins let you easily pass in configuration and get a set of Gulp-ready task functions back that have sensible defaults and work well together.

# Getting Started

## Requirements

- Gulp 4 installed with `npm install --save gulpjs/gulp#4.0`

## Install

```bash
npm install @theme-tools/plugin-pattern-lab-php --save
```

## Configure

The config that is passed in is merged with [`config.default.js`](config.default.js).

```bash
cp node_modules/@theme-tools/plugin-pattern-lab-php/config.default.js config.pattern-lab.js
```

## Setup

Add this to your `gulpfile.js`:

```js
const gulp = require('gulp');
const config = {};
config.pl = require('./config.pattern-lab.js');
const plTasks = require('@theme-tools/plugin-pattern-lab-php')(config.pl);

gulp.task('pl', plTasks.compile);
gulp.task('watch:pl', plTasks.watch);
```

# Details

## Tasks

These tasks are methods inside `plTasks` from the above code example. You can run them anyway you can run a function, though they are often ran via Gulp. All tasks take a callback function as the first and only parameter that will run when the task is done - exactly how `gulp.task()`, `gulp.parallel()`, and `gulp.series()` want.

### `plTasks.compile()` - Compile Pattern Lab

Compiles Pattern Lab. Basically runs `php pattern-lab/core/console --generate` for you and notifies you of errors using a OS Native Notification.

### `plTasks.watch()` - Watch Pattern Lab

Watch and Compile Pattern Lab.

## Configuration

**All configuration is deep merged with [`config.default.js`](config.default.js).**

### `configFile`

Type: `String` Default: `pattern-lab/config/config.yml`

The configuration lifted from this file is where the plugin gets most of it's information such as: the `sourceDir` to determine which folder to watch, the path to `core/console`, and a few other options.

### `watchedExtensions`

Type: `Array<String>`

Default:

```js
[
  'twig',
  'json',
  'yaml',
  'yml',
  'md',
  'jpg',
  'jpeg',
  'png'
]
```

These file extensions are watched inside the `sourceDir` found in `configFile` and trigger the compile afterwards.

### `extraWatches`

Type: `Array<String>` Default: `[]`

Extra paths to watch that would trigger a compile.

## Theme Core Events

This is only info for other Theme Core plugin developers.

### emit `'reload'`

This event is emmited when files are done compiling.
