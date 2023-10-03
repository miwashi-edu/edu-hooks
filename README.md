# Skydda din kod

> Vi lägger till lint.
> Här är det viktigt att besluta om koden skall lintas automatiskt, eller bara kontrolleras.
> Ofta är det bra att låta utvecklaren själv linta, emedan hooken bara kontrollerar.


## instruktioner

```bash
npm init @eslint/config -y

#✔ How would you like to use ESLint? · style
#✔ What type of modules does your project use? · commonjs
#✔ Which framework does your project use? · none
#✔ Does your project use TypeScript? · No / Yes
#✔ Where does your code run? · node
#✔ How would you like to define a style for your project? · guide
#✔ Which style guide do you want to follow? · standard
#✔ What format do you want your config file to be in? · JSON

npm pkg set scripts.lint="eslint ."
npm pkg set scripts.lint-fix="eslint --fix ."
npx husky add .husky/pre-commit "npm run lint"
```

## Lär eslint att läsa jest

```bash
npm install --save-dev eslint-plugin-jest
echo '{
    "env": {
        "browser": true,
        "commonjs": true,
        "es2021": true,
        "jest": true
    },
    "extends": [
        "standard",
        "plugin:jest/recommended"
    ],
    "parserOptions": {
        "ecmaVersion": "latest"
    },
    "rules": {
    },
    "plugins": ["jest"]
}' > .eslintrc.json
```

## ändra .eslint.json med jq (choco install jq / brew install jq)

```bash
jq '.env.jest = true | .extends = [.extends] + ["plugin:jest/recommended"] | .plugins += ["jest"]' .eslintrc.json
```
