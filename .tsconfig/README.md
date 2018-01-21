# Riotz Configs :: Project :: TypeScript

This is a TypeScript configuration commonly used in the Riots Works projects.


## Overview
This is a project-specific configuration for TypeScript project.  
Users of this repository are assumed to be engineers of Riotz Works.  

Though we intend to utilize this repository as an internal use of Riotz Works, there is no restriction on using this if it's useful to you.  


*Why is this repository necessary?*  
In the development project, the compiler settings and lint configuration of each repository are often the same.  
When these configurations are maintained for each repository, gaps will gradually occur. And sometimes it could be a serious situation that it cannot be properly managed anymore.  
We believe that this problem can be solved by utilizing general knowledge and inheritance.  
Fortunately TypeScript and TSLint can do that.


## Requirements
Requires the following to use:
- [Git](https://git-scm.com/) 2.14+
- [TypeScript](https://www.typescriptlang.org/) 2.5+
- [TSLint](https://palantir.github.io/tslint/) 5.7+


## Usage
### Getting Started
In the directory of the project to be developed with TypeScript, follow the steps below to add common settings.
- Add this repository as a remote repository to the project
- Add the tree as `git subtree add --prefix=.tsconfig` in the project
- Create `tsconfig.json` and` tslint.json` to refer to common settings

For example, the following command:
```console
git remote add -f typescript git@github.com:riotz-works/riotz-configs-project-typescript.git
git subtree add --squash --prefix=.tsconfig typescript master
git push

echo { "extends": "./tsconfig/tsconfig-base.json" }> tsconfig.json
echo { "extends": "./tsconfig/tslint-base.json" }> tslint.json
```

This change is pushed to the repository and the source code is shared to other engineers.  
However, the configuration file added with the `git remote add` command is a local repository setting and is not shared to other engineers.  
If another engineers receives an update or updates the sub tree, it is necessary to make `git remote add` for each engineers.  


### Upgrade
To receive this repository upgrade, update the subtree in the project's directory with the `--squash` option.
For example, the following command:
```console
git subtree pull --squash --prefix=.tsconfig typescript master
git push
```


## Notes
### In TSC, the following options have been added
- `noUnusedLocals` : *unset*  
Instead of using TSLint `no-unused-variable`  

- `noUnusedParameters` : *unset*  
Instead of using TSLint `no-unused-variable`  

* When TSC and TSLint have the same type of check and warning is displayed, use of TSLint is prioritized.  
Because the TSC is checked at compile time, while the editor can check with TSLint  
TSC is checked at compile time, however TSLint can be checked with editor  


### In TSLint, the following options have been added  
- `no-require-imports` : `false`  
Because Claudia API(which we often use) Builder is an ES5-Style export.  
If Claudia API Builder supports ES6-style or we use other products, set it to `true`.  

- `no-magic-numbers` : *unset*  
Because considered that it is not appropriate for coding and readability to constantize numerical values that are used only once.  
It will be evaluated in reviews instead of Lint.  

- `typedef` / `variable-declaration` : *unset*  
Because the type definition of the function becomes redundant and the line breakage is forced, the readability drops.  
Even without typing, we think that users of functions can understand types by type inference, so there is no problem.  
However, if evils arise due to not performing type definition, this item will be set.  


## Contribution
This repository is assumed to be used by engineers of Riotz Works.  
However, feedbacks are welcome for improvement of this repository. For more information please see [CONTRIBUTING](/.github/CONTRIBUTING.md).  


## Licence
This repository and deliverables are published under the MIT license. For the full license text please see [LICENSE](/LICENSE).  
© Riots Works  
