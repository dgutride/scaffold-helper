# scaffold-helper

> Copies files and folders from source directory to destination directory (all directories recursively or just files from the source directory) with template style from [template-file](https://github.com/gsandf/template-file#readme)

[![Build Status](https://travis-ci.org/cliffpyles/scaffold-helper.svg?branch=master)](https://travis-ci.org/cliffpyles/scaffold-helper)
[![Build status](https://ci.appveyor.com/api/projects/status/6xmc4f007uoacpcl?svg=true)](https://ci.appveyor.com/project/cliffpyles/scaffold-helper)
[![Coverage Status](https://coveralls.io/repos/github/cliffpyles/scaffold-helper/badge.svg?branch=master)](https://coveralls.io/github/cliffpyles/scaffold-helper?branch=master)

## Installation

```sh
$ npm i scaffold-helper --save
```

or

```sh
$ yarn add scaffold-helper
```

## Usage

In this section you will see two example usages. [One example](#example-one) copies the complete source directory tree to the destination and replaces all variables within the templates. [The other example](#example-two) will only copy files within the source directory to the destination directory and replaces all variables within the templates.

The given source directory tree:

```
.
+-- source/directory/
    |
    +-- dir-1
    |   |
    |   +-- file-2
    |
    +-- dir-2
    |   |
    |   +-- file-3
    |
    +-- template-1
```

The given `template-1`:

```txt
My name is {{name}} and I am {{age}} years old.
```

### example one

The `scaffold-helper` module example **WITH** copying recursive all files and directories:

```js
const scaffold = require('scaffold-helper'); // import scaffold from 'scaffold-helper';

// if we set onlyFiles to false it copies the complete directory tree
// from 'source/directory' to 'destination/directory'
// excluding 'dir-1'
scaffold(
  {
    source: 'source/directory',
    destination: 'destination/directory',
    onlyFiles: false,
    exclude: ['dir-1'], // add as many directories as you want to the array
  },
  {
    name: 'Cliff',
    age: '25',
  },
);
```

The example above will copy the source directory tree to the 'destination/directory' and replace all variables within all files

The destination directory tree:

```
.
+-- destination/directory/
    |
    +-- dir-2
    |   |
    |   +-- file-3
    |
    +-- template-1
```

The template-1 with filled variables:

```txt
My name is Cliff and I am 25 years old.
```

### example two

The `scaffold-helper` module example **WITHOUT** copying recursive all files and directories:

```js
const scaffold = require('scaffold-helper'); // import scaffold from 'scaffold-helper';

// if we set onlyFiles to true it copies only the files
// within 'source/directory' to 'destination/directory'
scaffold(
  {
    source: 'source/directory',
    destination: 'destination/directory',
    onlyFiles: true
  },
  {
    name: 'Cliff',
    age: '25',
  },
);
```

The example above will only copy the files within the source directory and will not recursively copy all directories and files.

The destination directory tree:

```
.
+-- destination/directory/
    |
    +-- template-1
```

The template-1 with filled variables:

```txt
My name is Cliff and I am 25 years old.
```

## LICENSE

MIT © Cliff Pyles
