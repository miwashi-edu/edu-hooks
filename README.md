# Skydda din kod


## Hooks

[GIT-Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)  

> Hooks är en inbbyggd del i git. Normalt lagras de i katalogen .git/hooks. 
> Vill du lägga till en hook, lägger du bara ett bash script med namnet på den händelse du vill git ska reagera på


## Husky

[Husky](https://typicode.github.io/husky/)

> Husky är ett scriptbibliotek som tillåter att man skriver hooks i andra språk än bash.  

> När Husky installeras lägger den till git config **core.hookspath=.husky** som tillåter att man lagrar git hooks i *.husky* istället för *.git/hooks*. De "krokar" man skapar läggs sedan till i git med "git add ." för att alla ska få samma beteende i git.



```mermaid

```
```bash
ls .git/hooks
applypatch-msg.sample     
fsmonitor-watchman.sample 
pre-applypatch.sample     
pre-commit.sample         
pre-push.sample           
pre-receive.sample        
push-to-checkout.sample
commit-msg.sample         
post-update.sample                        
pre-merge-commit.sample   
pre-rebase.sample         
prepare-commit-msg.sample 
update.sample
```


## Description

```bash
cd ws
mkdir git-hooks
cd git-hooks

git init
npm init -y
mkdir __tests__
curl -L https://gist.github.com/miwashiab/7ea5be9d7a645f197440f5746fd340bc/raw/unit-test.js -o ./__tests__/unit-test.js
curl -L https://gist.github.com/miwashiab/5000a9ba2f8eec98fb61b99ec041ed04/raw/component-test.js -o ./__tests__/component-test.js
curl -L https://gist.github.com/miwashiab/352322c4aa4ca4ecd839d63b0e95c8bd/raw/integration-test.js -o ./__tests__/integration-test.js
curl -L  https://gist.github.com/miwashiab/642d5f51c7c93e6793356ad666f6be03/raw/server.js -o server.js
npm pkg set main="server.js"
npm pkg set description="Simple application to test commit hooks"
npm pkg set scripts.start="node server.js" 
npm pkg set scripts.dev="nodemon server.js"
npm pkg set scripts.test="jest  --group=-component --group=-integration"
npm pkg set scripts.componenttest="jest  --group=component"
npm pkg set scripts.integrationtest="jest  --group=integration"
npm pkg set scripts.prepare="husky install"

npm install husky -D
npm install nodemon -D
npm install jest -D
npm install jest-runner-groups -D
npm install express

npm run prepare #Samma som "npx husky install"

# Lägg till en pre-commit hook
npx husky add .husky/pre-commit "npm test"

echo "node_modules" > .gitignore
echo "logs" >> .gitignore
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
echo ".env.test" >> .gitignore
git add .
git commit -m "First commit with pre-commit unittesting"

```

## Kontrollera att hooks katalog är .husky
```bash
git config --list | grep hookspath
```

## ./__tests__/unit-test.js

```js
describe('When testing jest', () => {
	describe('given i have a non failing test', () => {
		it('should be one', () => {
			expect(1).toBe(1)
		})
	})
})
```

## ./__tests__/component-test.js

```js
describe('When testing jest', () => {
	describe('given i have a non failing test', () => {
		it('should be one', () => {
			expect(1).toBe(1)
		})
	})
})
```

## ./__tests__/api-test.js

```js
describe('When testing jest', () => {
	describe('given i have a non failing test', () => {
		it('should be one', () => {
			expect(1).toBe(1)
		})
	})
})
```

## server.js

```js
const express = require('express')
const app = express()

const PORT = process.env.PORT || 3000

app.use('/', (req, res) => {
  res.status(200).json({"status":"success"})
})

app.listen(PORT, console.log(`Server is listening at port ${PORT}`))
```

## Använd NVM för att se hämta senaste node

```bash

# Linux, Mac
https://github.com/nvm-sh/nvm

## Windows
https://community.chocolatey.org/packages?q=nvm
```
