# node-sass-importer
Simple implementation of custom importer of SCSS files for node-sass. May be useful in a case if your SASS styles includes some third-party libraries and you don't want to hard link paths to them into your code. 

Also it mimics [compass-import-once](https://github.com/Compass/compass/tree/stable/import-once) functionaliy and avoid repetitive loading of SCSS files that are included multiple times into project. 

## Usage
Example usage in Gulp task
```js
gulp.src('*.scss')
    .pipe(sass({
        importer: require('node-sass-importer')
    })
```

## Options
Since importer signature is defined by node-sass itself - additional options are stored into ```importerOptions``` entry within node-sass options set.
Importer tries to locate SCSS files by constructing their paths from given parts. They are:

### roots
Array of additional root paths to search for SCSS files in. Should be defined as relative paths against current directory, main Node process is running from.      
Default: ```['']```     

### paths
Array of additional path components within any of root paths to search SCSS files in. Can contain ```{url}``` placeholder, it will be replaced with value of ```url``` argument that is passed to importer.   
Default: ```['', '{url}']```    

### filePrefixes
Array of prefixes to set before SCSS file name. Normally is not need to be overridden.   
Default: ```['_', '']```


### fileExtensions
Array of file extension to set after SCSS file name. Normally is not need to be overridden.   
Default: ```['.scss', '/_index.scss']```

## Importing of third-party libraries

Since v2.0 in a case if you're importing third-party library from `node_modules` - you can do it by use `~` as a prefix. 

For example: `@import "~bootstrap/scss/bootstrap"`. 

## Import of directory index files

Since v2.0 you can load `some-dir/_index.scss` by simply referencing directory itself: `@import "some-dir"` 
