## git
```bash
git clone
# .gitignore
echo -e "node_modules\n" > .gitignore
```
## package.json
```bash
npm init -y
```
## nodemon
```bash
npm install --save-dev nodemon
# nodemon.json
echo -e '{\n\t"ignore": [\n\t]\n}' > .nodemon
```
## eslint
```bash
# How would you like to use ESLint? To check syntax and find problems
# What type of modules does your project use? JavaScript modules (import/export)
# Which framework does your project use? Vue
# Does your project use TypeScript? No
# Where does your code run? Browser, Node
# What format do you want your config file to be in? JSON
npx eslint --init
npm install -- dave-dev @babel/eslint-parser
# .eslintrc
echo -e '{\n\t"env": {\n\t\t"browser": true,\n\t\t"es2021": true,\n\t\t"node": true\n\t},\n\t"extends": [\n\t\t"eslint-config-airbnb-base",\n\t\t"plugin:vue/vue3-recommended",\n\t\t"prettier"\n\t],\n\t"parserOptions": {\n\t\t"ecmaVersion": 12,\n\t\t"sourceType": "module"\n\t},\n\t"plugins": [\n\t\t"vue"\n\t],\n\t"rules": {\n\t}\n}' > .eslintrc
# .eslintignore
echo -e "/.git\n/.vscode\nnode_modules\n" > .eslintignore
```
## [prettier](ttps://prettier.io)
```bash
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
npm install --save-dev --save-exact prettier
# [.prettierrc](https://prettier.io/docs/en/options.html)
echo -e '{\n\t"singleQuote": true,\n\t"jsxSingleQuote": true,\n\t"arrowParens": "avoid",\n\t"max-len": ["error", 140, 2],\n\t"tabWidth": 2,\n\t"useTabs": false\n}' > .prettierrc
# .prettierignore
echo -e "node_modules\n" > .prettierignore
```
## airbnb
```bash
npx install-peerdeps --dev eslint-config-airbnb-base
```
## mocha
```bash
mkdir tests
```
## docker
```bash
# .dockerignore
echo -e "node_modules\n" > .dockerignore
```
## .vscode workspace exclude
```bash
mkdir .vscode
echo -e '{\n\t"files.exclude": {\n\t\t"node_modules":true,\n\t\t".vscode":true,\n\t\t"package-lock.json":true,\n\t\t".prettierrc": true,\n\t\t".prettierignore": true,\n\t\t".eslintrc":true,\n\t\t".gitignore":true,\n\t\t".eslintignore":true,\n\t\t".nodemon":true\n\t}\n}\n' > ./.vscode/settings.json
```
## workspace
```bash
## folders
mkdir browser node test log
```
## readme
```bash
## shields
### rating: [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)"
test success
```