## Debugging custom tslint rules in Visual Studio Code

1. Create rule following: https://palantir.github.io/tslint/develop/custom-rules/


2. Place rules in root of your app, inside tslint-rules (or however you want to name your rules folder)

3. Modify tslint.json in root of your app to include:
```
{
  "rulesDirectory": [
    "./tslint-rules"
  ],
  "rules": {
    "no-imports": true
  }
}
```

4. Compile your rule: tsc tslint-rules/noImportsRule.ts

5. Previous step generated 'noImportsRule.js' file inside tslint-rules folder.
Open this JS file and add breakpoint anywhere in the file (NOTE: adding breakpoint is TS file will not work!)

6. Add VSC debug config (in launch.json):

```
{
  "name": "lint",
  "cwd": "${workspaceFolder}",
  "type": "node",
  "request": "launch",
  "program": "${workspaceRoot}\\node_modules\\tslint\\bin\\tslint",
  "protocol": "inspector",
  "args": ["--project", "tsconfig.json"]
},
```

7. Run debugger for added config - it will hit breakpoint added in previous steps
