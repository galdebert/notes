# how-to-build-node-from-source

- download node-v12.7.0.tar.gz
- extract to node-v12.7.0

# to build on windows

# release

- build release: `vcbuild openssl-no-asm`
- quick test:  `Release\node -e "console.log('Hello from Node.js', process.version)"`
- run all tests: `vcbuild test` <- not tested

## debug

- build debug: `vcbuild debug openssl-no-asm`
- quick test: `Debug\node -e "console.log('Hello from Node.js', process.version)"`

# run

`D:\dev\nodejs-source\node-v10.16.0\Debug\node --allow-natives-syntax src/javascript-vanilla/array-dense-vs-sparse.js`
but MIND THE with `;`, either you puputse `;` at the end of every line, or put `;` before the `%`
```
;%DebugPrint(sparseArray)
```

# how to avoid syntax errors

- `%DebugPrint(sparseArray)` is not valid javascript, even if we use `node --allow-natives-syntax`, this still triggers erros in vscode and typescript
- `node --expose-natives-as="builtins"` does not work
- let's use `v8-natives`, but note your still need to run node with `--allow-natives-syntax`



