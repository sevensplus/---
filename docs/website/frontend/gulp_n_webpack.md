## Gulp & Webpack 比較
通常都說 gulp 是 task runner，Webpack 是 module bundler。從運作方式來看，gulp 讓使用者自訂一系列的任務，對於所需要的檔案進行轉化處理，並且使用 series(有先後順序) 或 parallel(平行) 方式做任務間的串接。而 webpack 則將所有資源看做 module，目的是將所有物件打包在一起，使用時不像 gulp 批次處理 css、js 檔，而是從 index 當中去找其他用到過的資源，再從其他資源擴展出去，最後將所有用過的東西整合。
這兩個工具就像 CSS Prepocessor，目的是為了簡化工作流程、減少重複性高的工作。因此，如果不使用這兩個工具當然是沒問題的，只是自己必須手動處理而已。

-----

## Gulp
> 為什麼需要 gulp：將工作流程自動化。讓電腦自動執行 scss -> css 的轉換、css 的壓縮、javascript 的版本轉換等動作。通常會有原始資料夾(file），依需求看要不要建 css、js 專門的資料夾，然後建好後放在新資料夾（build）裡面

### gulp 指令
- gulp-concat：合併檔案
- gulp-minify-css：壓縮 CSS
- gulp-uglify：混淆並壓縮 JS
- gulp-rename：重新命名檔案

### 範例
```javascript
const gulp = require('gulp');
const sass = require('gulp-sass'); // 將 scss 轉譯成 css
const minifyCss = require('gulp-minify-css'); // 壓縮 css
const rename = require('gulp-rename'); // 重新命名檔案
const babel = require('gulp-babel'); // 用 babel 將 js 轉成 ES5
const uglify = require('gulp-uglify'); // 壓縮js
const minify = require('gulp-minifier'); // 一次壓縮所有類型(html, css, js)的檔案

// 將 scss 轉譯成 css 並壓縮
function css() {
  return gulp
    .src('./file/*.scss')
    .pipe(sass({ outputStyle: 'expanded' }))
    .pipe(minifyCss({ keepBreaks: true })) // 也可以之後再一起壓縮
    .pipe(rename({ suffix: 'min' }))
    .pipe(gulp.dest('./build/'));
}

// 將 js 轉成 ES5 並壓縮
function script() {
  return gulp
    .src('./file/*.js')
    .pipe(babel({ presets: ['@babel/env'] }))
    .pipe(uglify()) // 也可以之後再一起壓縮
    .pipe(rename({ duffix: 'min' }))
    .pipe(gulp.dest('./build/'));
}

// 壓縮全部檔案
function minifier() {
  return gulp
    .src('./build/*')
    .pipe(minify({
      minify: true,
      minifyJS: {
        sourceMap: true,
      },
      minifyCSS: true,
    }))
    .pipe(gulp.dest('./build/min_document/'));
}

// 輸出
// 方法一：用 gulp.css, gulp.script 分別呼叫函式、執行不同動作
exports.css = css;
exports.script = script;
exports.minifier = minifier;

// 方法二：全部裝進 default 然後用 gulp 一次輸出
const build = gulp.series(css, script, minifier);
exports.default = build;

```
#### 參考資源
- [升级到 gulp 4.0](https://blog.skk.moe/post/update-gulp-to-4/)   
- [[译] Gulp 4 入门指南](https://github.com/cssmagic/blog/issues/62)

---

## webpack
> 為什麼需要 webpack：在前端（瀏覽器）用 node.js 的模組化開發，就可以用 import 的方式加載資源。一般有原始資料夾（src）和編譯後資料夾（dist）
### 範例
```javascript
// webpack.config.js
const path = require('path');
module.exports = {
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

