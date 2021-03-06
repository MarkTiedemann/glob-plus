
# glob+

**A glob that learned to read.**

Same as [glob](https://github.com/isaacs/node-glob) but also returns the content and stats of the file.

![](https://github.com/isaacs/node-glob/raw/master/oh-my-glob.gif)

## Installation

```
npm install --save glob-plus
```

## Quickstart

```javascript
const glob = require('glob-plus')

const plus = glob.plus('**', { ignore: 'node_modules/**' })

plus.on('file', ({ name, stats, data }) => {
    console.log(`Found file '${name}' with size ${stats.size}`)
})

plus.on('error', err => {
    console.error(err)
})

plus.on('end', () => {
    console.log('Done!')
})
```

## API

### glob.plus([pattern][, options])

- `pattern` `<String>`: *optional*; the [pattern](https://github.com/isaacs/node-glob#glob-primer) to be matched; *default*: `'**'`
- `options` `<Object>`: *optional*; the [glob](https://github.com/isaacs/node-glob) [options](https://github.com/isaacs/node-glob#options); *default*: `{ nodir: true }`
- returns an `<EventEmitter>` with the following events:
  - `file` `<Object>`: when a file was matched, statted, and read
    - `name` `<String>`: the file name
    - `stats` `<Stats>`: the file [stats](https://nodejs.org/api/fs.html#fs_class_fs_stats)
    - `data` `<Buffer>`: the file content
  - `error` `<Error>`: when an error occcured while matching, statting, or reading
  - `end` `<>`: when matching, statting, and reading has finished

### glob.read([pattern][, options])

Same as `glob.plus(..)` but does not return file `stats`.

### glob.stats([pattern][, options])

Same as `glob.plus(..)` but does not return file `data`.

## License

[WTFPL](http://www.wtfpl.net/) – Do What the F*ck You Want to Public License.

Made with :heart: by [@MarkTiedemann](https://twitter.com/MarkTiedemannDE).
