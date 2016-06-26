# Confabulous HTTP Loader
Confabulous-HTTP-Loader is an HTTP Loader for [Confabulous](https://github.com/guidesmiths/confabulous) - a hierarchical, asynchronous config loader and post processor.

## TL;DR
```
const confabulous = require('confabulous')
const Confabulous = confabulous.Confabulous
const http = require('confabulous-http-loader')
const processors = confabulous.processors

new Confabulous()
    .add((config) => http({ url: config.server.url, mandatory: false, watch: { interval: '5m' } }))
    .on('loaded', (config) => console.log('Loaded', JSON.stringify(config, null, 2)))
    .on('reloaded', (config) => console.log('Reloaded', JSON.stringify(config, null, 2)))
    .on('error', (err) => console.error('Error', err))
    .on('reload_error', (err) => console.error('Reload Error', err))
    .end()
```

### Options
|  Option  |  Type  |  Default  |  Notes  |
|----------|--------|-----------|---------|
| mandatory | boolean | true       | Causes an error/reload_error to be emitted if the configuration does not exist |
| watch     | object  |            | Watching is implemented by issuing HEAD requests and comparing the Etag and Last-Modified headers. You need to specify and interval in the configuration, e.g. ```{ watch: { interval: '5m' } }``` |
| request   | object  | [see here](https://github.com/guidesmiths/confabulous/blob/master/lib/loaders/http.js#L14) | options that will be passed to [the underlying http client](https://github.com/request/request).


