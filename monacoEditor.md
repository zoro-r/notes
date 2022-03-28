# monaco 编辑器的使用经验

简介: monaco 是vscode的代码编辑器，由于官方文档过于粗糙，顾写次文档进行记录遇到的问题以及解决方案

官方文档：https://microsoft.github.io/monaco-editor/

## 问题1: 如何创建编辑器？

```javaScript
const editor.current = editor.create(monacoEleRef?.current, {
    model: modelRef.current,
    // tabSize: 2,
    theme,
    minimap: {
      enabled: enabledMinimap,
    },
    selectOnLineNumbers: true,
    roundedSelection: false,
    formatOnType: true,
    automaticLayout: true,
    readOnly,
    contextmenu: false,
    ....
  });
```

## 问题2：如何添加语言提示功能？

```javaScript
languages.registerCompletionItemProvider(language, {
    triggerCharacters: ['.'], // 提示器的触发条件
    suggestions: [ // 提示内容对象
        {
          range,
          label: suggest,
          kind: molanguages.CompletionItemKind.Snippet, // 这里Function也可以是别的值，主要用来显示不同的图标
          insertTextRules: molanguages.CompletionItemInsertTextRule.InsertAsSnippet,
          insertText: suggest, // 我试了一下，如果没有此项，则无法插入
          detail: suggest,
          documentation: '文档',
        }
    ]
})
```

## 问题3: 如何设置某段区域的背景色？

```javaScript
// create 返回的对象
editor.current.deltaDecorations(
  [],
  [
    {
      range: new Range(3, 1, 3, 1),
      options: {
        isWholeLine: true,
        className: 'myContentClass',
        glyphMarginClassName: 'myGlyphMarginClass',
      },
    },
  ],
);
```

## 问题4: 如何进行报错等提示
```javaScript
editor.setModelMarkers(model, 'eslint', [
  {
    startLineNumber: 1,
    endLineNumber: 1,
    startColumn: 0,
    endColumn: 50,
    message: '代码',
    severity: 2, // 2 蓝色 3 红色 4 黄色 ～～波浪线 分别为报错，警告 提示～～～ 默认为红色 可以参考源代码
    source: monacoRef.current?.getValue(),
    code: '',
  },
]);
```
