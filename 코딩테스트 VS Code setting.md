 
1.
ctrl + shift + p를 눌러서 설정
"preferences: open user settings (JSON)" 안에서

이거 확인

````JSON


  "editor.quickSuggestions": {
    "other": false,
    "comments": false,
    "strings": false
  },
  "editor.suggest.showWords": false,        // disables word-based suggestions
  "editor.suggest.showFunctions": false,    // disables function suggestions
  "editor.suggest.showMethods": false,      // disables method suggestions
  "editor.suggest.showModules": false,      // disables module suggestions like sys.*
  "editor.parameterHints.enabled": false,   // disable parameter hints
  "editor.hover.enabled": false             // disable hover info


````

2.
Extension

````JSON
// please set this enabled
Pylance = disable
Pylint = disable
Python = disable
````
