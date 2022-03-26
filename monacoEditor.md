# monaco 编辑器的使用经验

简介: monaco 是vscode的代码编辑器，由于官方文档过于粗糙，顾写次文档进行记录遇到的问题以及解决方案

官方文档：https://microsoft.github.io/monaco-editor/

## 第一步 创建编辑器

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


