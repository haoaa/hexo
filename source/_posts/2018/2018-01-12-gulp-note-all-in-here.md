---
title: gulp-note-all-in-here
date: 2018-01-12 10:39:54
categories: gulp
tags: gulp
---

## This post is all about issues come up when I use gulpjs.

### Multiple gulp process flow working with runing tasks in sequence demand.
- 
```js
gulp.task('someTask', function(){
    if (gulpConfig.multi-dist){
        const stream = merge();
        _.forEach(gulpConfig.branches, function (name) {
            stream.add(
            gulp.src('biz/*.html')
                .pipe(gulp-plumber(errorHandler))
                .pipe(gulp-newer('./dest/' + name))
                .pipe(gulp.dest('./dest/' + name))
            );
        })
        return stream;
    }
});
```
- By doing this, now can run this multiple working flow with other tasks in sequence.

### alter gulp dest path through gulp-rename
```js
    srcPath = path.join(component, '*', 'lib/**/*')
```
```js
function getJsStream(srcPath, distPath){
	return gulp.src(srcPath)
		.pipe(gulp-plumber(errorHandler))
		// .pipe(gulp-logger({showChange: true}))
		.pipe(rename(function(file) {
			var pathArr = file.dirname.split(path.sep);
			pathArr.splice(1,1); //切掉lib
			file.dirname = pathArr.join(path.sep);
		}))
		.pipe(gulp-newer(distPath))
		.pipe(gulp.dest(distPath));
}

```