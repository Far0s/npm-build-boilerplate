# npm-boilerplate

This is a simple front-end boilerplate forked from Damon Bauer's own [npm-build-boilerplate](https://github.com/damonbauer/npm-build-boilerplate).

## Install
1. Clone this repo — or copy the contents `"devDependencies"` into your `package.json` + copy any tasks you want from the `"scripts"` object into your `package.json` `"scripts"` object.
2. Run `sudo npm install`
3. Run any taks with `npm run task` where `task` is the name of the task from the `"scripts"` object.
4. Quickstart: `npm run postinstall` -> NPM will build the project in the `/dist` folder and start a live-reloading server after.
5.

## List of available tasks
### `clean`
  `rm -f dist/{index.html,css/*,js/*,images/*}`

  Delete existing dist files

### `autoprefixer`
  `postcss -u autoprefixer -r dist/css/*`

  Add vendor prefixes to your CSS automatically

### `scss`
  `node-sass --output-style compressed -o dist/css src/scss`

  Compile Scss to CSS

### `lint`
  `eslint src/js`

  "Lint" your JavaScript to enforce a uniform style and find errors

### `uglify`
  `mkdir -p dist/js && uglifyjs src/js/*.js -m -o dist/js/app.js && uglifyjs src/js/*.js -m -c -o dist/js/app.min.js`

  Uglify (minify) a production ready bundle of JavaScript

### `imagemin`
  `imagemin src/images/* -o dist/images`

  Compress all types of images

### `icons`
  `svgo -f src/images/icons && mkdir -p dist/images && svg-sprite-generate -d src/images/icons -o dist/images/icons.svg`

  Compress separate SVG files and combine them into one SVG "sprite"

### `serve`
  `browser-sync start --server --files 'dist/css/*.css, dist/js/*.js, **/*.html, !node_modules/**/*.html'`

  Start a new server and watch for CSS & JS file changes in the `dist` folder

### `build:pug`
  `pug --output-style compressed -o dist/ src/pug/*.pug`

  Compiles index.pug into dist/index.html

### `build:css`
  `npm run scss && npm run autoprefixer`

  Alias to run the `scss` and `autoprefixer` tasks. Compiles Scss to CSS & add vendor prefixes

### `build:js`
  `npm run lint && npm run concat && npm run uglify`

  Alias to run the `lint`, `concat` and `uglify` tasks. Lints JS, combines `src` JS files & uglifies the output

### `build:images`
  `npm run imagemin && npm run icons`

  Alias to run the `imagemin` and `icons` tasks. Compresses images, generates an SVG sprite from a folder of separate SVGs

### `build:all`
  `npm run build:css && npm run build:js && npm run build:images`

  Alias to run all of the `build` commands

### `watch:pug`
  `onchange \"src/pug\" -- npm run build:pug`

  Watches for any .pug file in `src` to change, then run the `build:pug` task

### `watch:css`
  `onchange 'src/**/*.scss' -- npm run build:css`

  Watches for any .scss file in `src` to change, then runs the `build:css` task

### `watch:js`
  `onchange 'src/**/*.js' -- npm run build:js`

  Watches for any .js file in `src` to change, then runs the `build:js` task

### `watch:images`
  `onchange 'src/images/**/*' -- npm run build:images`

  Watches for any images in `src` to change, then runs the `build:images` task

### `watch:all`
  `npm-run-all -p serve watch:pug watch:css watch:js watch:images`

  Run the following tasks simultaneously: `serve`, `watch:pug`, `watch:css`, `watch:js` & `watch:images`. When a .pug, .scss or .js file changes in `src` or an image changes in `src/images`, the task will compile the changes to `dist`, and the server will be notified of the change. Any browser connected to the server will then inject the new file from `dist`

### `postinstall`
  `npm run build:all && npm run watch:all`

  Runs `watch:all` after `npm install` is finished
