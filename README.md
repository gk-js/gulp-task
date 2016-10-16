# gulp-task

var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var sass        = require('gulp-sass');
var autoprefixer = require('gulp-autoprefixer')

// Static Server + watching scss/html files
gulp.task('serve', function() {

    browserSync.init({
        server: "./app"
    });

    gulp.watch("app/style/*.scss", ['sass']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
    gulp.watch("app/style/*.css").on('change', browserSync.reload);

});

// Compile sass into CSS & auto-inject into browsers
gulp.task('sass', function() {
    return gulp.src("app/style/*.scss")
        .pipe(sass({ style: 'expanded' }))
        .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
        // .pipe(autoprefixer('last 2 version'))
        .pipe(gulp.dest("app/style"))
        .pipe(browserSync.stream());
});

gulp.task('default', ['serve']);

http://www.techug.com/gulp
