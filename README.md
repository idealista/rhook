# rhook - Realm Git Hook
A git hook to work with [Realm](https://realm.io/)

## Introduction
This repo contains a git commit-hook which can be used to check if Realm data model in your project has accidentally been modified without a migration. This way a commit shouldn't be made in the Realm data model without the related migration, avoid unexpected runtime crashes in your app! 

## How it works
This is based on a git pre-commit hook, which will be executed after a 'git commit' is typed and before the commit itself. Inside the hook script, we check if there is a file in the Realm data model of your project which has changes and if the
migration file hasn't, in that case the hook script will exit non-zero and abort the commit.

This script is meant to be added as a "pre-commit"-hook. See this page
for further information:

[Customizing git - git hooks](https://git-scm.com/book/uz/v2/Customizing-Git-Git-Hooks)

## Usage
Repo contains two files: 'pre-commit' which is the hook itself and a 'paths.json' file, which contains the paths needed by the hook script.

* Copy the script in your '.git/hooks' folder (be sure that it has execution perms). Note: You can also make a symbolic link in your '.git/hooks' folder of your project to the file in this repo (recommended way, as it would be easier for you to update it)

* Copy the 'paths.json' file in the root of your project and fill it with the needed paths (one for the Realm data model and other for the path of the file where you make your Realm migrations)


```json
{
    "realmDataModelPath": Your Realm data model path,
    "realmMigrationPath": Your Realm Migration file path
}
```
Example:
```json
{
    "realmDataModelPath": "app/src/main/java/com/idealista/android/realm/entity/",
    "realmMigrationPath": "app/src/main/java/com/idealista/android/realm/Migration.java"
}
```

## TODO
- Improve hook logic related to migration checks in order to know if a migration for the Realm data model changed has been provided (now we only checks if Migration file has any changes).
- Create a task for gradle to work with this.

## License
![Apache 2.0 Licence](https://img.shields.io/hexpm/l/plug.svg)

This project is licensed under the [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) license - see the [LICENSE.txt](LICENSE.txt) file for details.