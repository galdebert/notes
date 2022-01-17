# npm-yarn-cheat-sheet

- `yarn outdated`: lists available updates, install them 
- `yarn why mypackage`: tells what package has mypackage as a dependency
- `yarn upgrade`: changes your `yarn-lock.json`, but **does NOT change** `package.json`
- `yarn upgrade --latest`: same as the upgrade command, but ignores the version range specified in package.json. Instead, the version specified by the latest tag will be used (potentially upgrading the packages across major versions). `package.json` **is updated**.
- `yarn upgrade-interactive --latest`: interactive version of `yarn upgrade --latest`
- `yarn check`: checks dependencies
- `yarn info mypackage versions`: views mypackage available versions online
- `yarn info mypackage version`: views mypackage latest version online
- `yarn list mypackage`: views mypackage version installed locally
- `yarn list --depth=0`: lists packages installed locally
- `yarn global list --depth=0`: lists packages installed globally

### Where does yarn store global packages

https://github.com/yarnpkg/yarn/issues/2049
- `%LOCALAPPDATA%/Yarn/config/global` on Windows
- `~/.config/yarn/global` on OSX and non-root Linux
- `/usr/local/share/.config/yarn/global` on Linux if logged in as root


### mind the ^ on windows

- on windows: `yarn add react-dnd@^3.0.2` results in "react-dnd": "3.0.2" in the package.json
- use instead: `yarn add "react-dnd@^3.0.2"` results in "react-dnd": "^3.0.2" in the package.json

### yarn install, NODE_ENV, devDependencies

- `yarn install` if NODE_ENV = production, yarn will NOT install devDependencies
- `yarn install --production=true` ignore NODE_ENV, yarn will NOT install devDependencies
- `yarn install --production=false` ignore NODE_ENV, yarn WILL install devDependencies

### yarn run

- `yarn run env`: lists environment variables available to the scripts at runtime
- `yarn run [script] [<arg>]`: passes additional argumentsarguments
- [script] can also be any locally installed executable that is inside `node_modules/.bin/`

```json
"scripts": {
  "server": "node server.js"
}
```
`yarn run server --port=1337` runs `server.js --port=1337`

### use a locally modified version of a package

in `my-app/package.json`:
```
"dependencies": {
   "mobx": "link:../my-mobx/dist/v5",
}
```

yarn install will create a symlink
`dev/my-app/node_modules/mobx` pointing to target `dev/my-mobx/dist/v5`


### yarn link

`yarn link` registers some linkable packages **globally**. This is sounds awful. Don't use it

https://yarnpkg.com/lang/en/docs/cli/link/

link
- in `dev/my-mobx/dist/v5`, run `yarn link`
  - creates the symlink `%LOCALAPPDATA%\Yarn\Data\link\mobx` pointing to target `dev/my-mobx/dist/v5`
- in `dev/my-app`, run `yarn link mobx`
  - creates the symlink `dev/my-app/node_modules/mobx` pointing to target `%LOCALAPPDATA%\Yarn\Data\link\mobx`
 
unlink
- in `dev/my-app`, run
  - `yarn unlink mobx`
  - `yarn install`
- in `dev/my-mobx/dist/v5`, run
  - `yarn link`

### where to find the what has been yarn linked

- linux: ~/.config/yarn/link
- windows: `explorer C:\Users\%USERNAME%\AppData\Local\Yarn\Data\link`

# package.json "resolutions" specification

https://github.com/yarnpkg/rfcs/blob/master/implemented/0000-selective-versions-resolutions.md

