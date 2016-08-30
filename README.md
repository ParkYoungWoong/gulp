# gulp
Learn Gulp!

- `npm init` 명령어는 인터렉티브 프롬프트가 동작하면서 프로젝트에 대한 여러가지 정보를 입력할 수 있게 되고 그 정보를 기반으로 기본적인 `package.json` 파일을 생성
```shell
npm init
```

- Gulp 를 전역으로 설치
```shell
npm install -g gulp
```

- `--save-dev` 플래그를 추가하여 devDependency로 설치
- Gulp 의 플러그인들도 `--save-dev` 플래그를 추가하여 설치
```shell
npm install --save-dev gulp
npm install --save-dev gulp-[plugin name]
```

- gulpfile.js 생성
```shell
# windows
echo > gulpfile.js
# mac
touch gulpfile.js
```

- Gulp 플러그인 설치
```shell
npm install --save-dev gulp-webserver gulp-concat gulp-uglify gulp-minify-html gulp-sass gulp-livereload
```

- gulpfile.js 수정
```js
var gulp = require('gulp');  // Gulp
var webserver = require('gulp-webserver');  // 웹서버처럼 동작하게 하는 플러그인
var concat = require('gulp-concat');  // js 파일 병합을 위한 플러그인
var uglify = require('gulp-uglify');  // js 파일 압축을 위한 플러그인
var minifyhtml = require('gulp-minify-html');  // html 파일 압축을 위한 플러그인
var sass = require('gulp-sass');  // sass 파일을 컴파일하기 위한 플러그인
var livereload = require('gulp-livereload');  // 웹 브라우저를 리로드하기 위한 플러그인
```




