
当创建一个新的 [`repl.REPLServer`] 时，可以提供一个自定义的解释函数。
这可以用于实现完全定制化的 REPL 应用。

以下是 REPL 的一个假设的示例，执行从一种语言到另一种语言的文本转换：

```js
const repl = require('repl');
const { Translator } = require('translator');

const myTranslator = new Translator('en', 'fr');

function myEval(cmd, context, filename, callback) {
  callback(null, myTranslator.translate(cmd));
}

repl.start({ prompt: '> ', eval: myEval });
```

