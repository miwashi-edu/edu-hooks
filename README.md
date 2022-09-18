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
# Git hooks

cd ws
mkdir git-hooks
cd git-hooks

git init
npm init -y

mkdir __tests__
touch ./__tests__/unittest.js

npm pkg set scripts.prepare="husky install"

npm install husky -D

npm pkg set scripts.dev="nodemon server.js" #Inget mellanslag runt =
npm pkg set scripts.test="jest  --group=-component --group=-integration"
npm pkg set scripts.componenttest="jest  --group=component"
npm pkg set scripts.integrationtest="jest  --group=integration"
    
npm run prepare #Samma som "npx husky install"

# Lägg till en pre-commit hook
npx husky add .husky/pre-commit "npm test"

# Lägg till hooken till git
git add .husky/pre-commit


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


## Använd NVM för att se hämta senaste node

```bash

# Linux, Mac
https://github.com/nvm-sh/nvm

## Windows
https://community.chocolatey.org/packages?q=nvm
```

ren C:\ProgramData\chocolatey C:\ProgramData\chocolatey_old
