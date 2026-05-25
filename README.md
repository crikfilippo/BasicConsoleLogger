# BasicConsoleLogger.js

A simple JS class to log messages to the browser console.

**Notes:**
- Single file class, no dependencies needed.
- Supports three log levels: standard, warning, and error.
- Errors can optionally be re-thrown as custom `Error` objects.
- Log output can be globally enabled or disabled via constructor parameter.

---

## Usage

Include the class in your project and instantiate it with your preferred options.

```js
let logger = new BasicConsoleLogger({ instanceName: 'MyApp', isLogEnabled: true });
```

- Use `logger.log('message')` to output a standard `[LOG]` message to the console.
- Use `logger.warning('message')` to output a `[WARNING]` message via `console.warn`.
- Use `logger.error('message')` to output an `[ERROR]` message via `console.error`.

---

## Advanced usage

Each method accepts an array of message trunks, an optional caller function name, and additional options.

```js
// Standard log with trunks and caller name
logger.log(['main message', 'detail 1', 'detail 2'], 'myFunction');

// Warning log
logger.log(['main message', 'detail 1'], 'myFunction', 1);

// Error log
logger.log(['main message', 'detail 1'], 'myFunction', 2);

// Error log re-throwing the error
try {
    logger.log(['main message', 'detail 1'], 'myFunction', 2, true);
} catch(e) {
    console.log(e);
}
```

The `log` method signature is:

```js
log(trunks = ['hey'], fName = '', level = 0, throwError = false)
```

| Parameter    | Type             | Default  | Description                                        |
|--------------|------------------|----------|----------------------------------------------------|
| `trunks`     | `string\|Array`  | `['hey']`| Message or array of message parts to log           |
| `fName`      | `string`         | `''`     | Caller function name, prepended to the output      |
| `level`      | `number`         | `0`      | `0` = log, `1` = warning, `2` = error              |
| `throwError` | `boolean`        | `false`  | If `true`, throws the last trunk as an `Error`     |

---

## Constructor options

```js
new BasicConsoleLogger({
    instanceName  : 'MyApp',  // string prefix shown in every log line
    isLogEnabled  : true      // set to false to silence all non-throwing logs
});
```

---

## Shorthand methods

```js
logger.warning('something looks off', 'myFunction');
logger.error('something went wrong',  'myFunction');
logger.error('critical failure',      'myFunction', true); // throws
```

---

## Output format

```
[LOG]     MyApp myFunction : main message; detail 1; detail 2;
[WARNING] MyApp myFunction : something looks off;
[ERROR]   MyApp myFunction : something went wrong;
```

---

*@author Filippo Maria Grilli — [@crikfilippo](https://github.com/crikfilippo)*  
*@license MIT*  
*@version 1.0.0*
