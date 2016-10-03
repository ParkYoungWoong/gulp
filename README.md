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
var concat = require('gulp-concat');  // js 파일 [병합]을 위한 플러그인
var uglify = require('gulp-uglify');  // js 파일 [압축]을 위한 플러그인
var minifyhtml = require('gulp-minify-html');  // html 파일 [압축]을 위한 플러그인
var sass = require('gulp-sass');  // sass 파일을 컴파일하기 위한 플러그인
var livereload = require('gulp-livereload');  // 웹 브라우저를 리로드하기 위한 플러그인

// 원본
var src = 'public/src';

// 배포용
var dist = 'public/dist';

// 모든 경로를 paths 경로에 담아 사용하기 편리하게 정리
var paths = {
    js: src + '/js/*.js',
    scss: src + '/scss/*.scss',
    html: src + '/**/*.html'
};

// 웹서버를 localhost:8000 로 실행한다.
gulp.task('server', function () {
    return gulp.src(dist + '/')
        .pipe(webserver());
});

// 모든 자바스크립트 파일을 하나로 합치고 압축한다.
gulp.task('combine-js', function () {
    return gulp.src(paths.js)
        .pipe(concat('common.js'))
        .pipe(uglify())
        .pipe(gulp.dest(dist + '/js'));
});

// sass 파일을 css로 컴파일한다.
gulp.task('compile-sass', function () {
    return gulp.src(paths.scss)
        .pipe(sass())
        .pipe(gulp.dest(dist + '/css'));
});

// HTML 파일을 압축한다.
gulp.task('compress-html', function () {
    return gulp.src(paths.html)
        .pipe(minifyhtml())
        .pipe(gulp.dest(dist + '/'));
});

// 파일 변경 감지 및 브라우저 재시작
gulp.task('watch', function () {
    livereload.listen();
    gulp.watch(paths.js, ['combine-js']);
    gulp.watch(paths.scss, ['compile-sass']);
    gulp.watch(paths.html, ['compress-html']);
    gulp.watch(dist + '/**').on('change', livereload.changed);
});

// 기본 task 설정
gulp.task('default', [
    'server',
    'combine-js',
    'compile-sass',
    'compress-html',
    'watch'
]);
```

## gulp API

### gulp.src()

### gulp.dest()

### gulp.task(name[, deps][, 실행함수])

`Gulp`가 수행할 작업을 설정한다.

#### name
type: `String`

수행할 작업의 이름을 설정

#### deps
type: `Array`

해당 작업이 실행되기 전에 실행될 다른 작업들의 배열 (dependency)

#### fn
type: `Function`

해당 작업의 동작을 설정

### gulp.watch()
