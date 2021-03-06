---
title: Development guidelines
---

### Principles

1. **Failure is a mandatory component of success**. As people, learning and failure go hand in hand.

1. **Learn and adapt from prior learnings**. Adopt the learnings of continuous improvement: when failure occurs, immediately determine what needs to be done to prevent recurrence and focus on those tasks (e.g. [Kaizen](https://en.wikipedia.org/wiki/Kaizen) and [Antifragile](https://en.wikipedia.org/wiki/Antifragile)).

1. **Focus on software and architecture that continually reduces the risk of changes.** These practices focus on:

   1. _isolation_ - truly ensuring that one change cannot impact another. For example, our focus on API design and micro service architecture on the backend is one technique we use to create isolation.

   1. _continuous delivery_ - by releasing small changes continuously to our production environment, we minimize the impact of any one change and significantly decrease time to resolution.

   1. _automation_ - by writing software to manage and implement our processes - including testing, patching and deployment - we focus on capturing our assumptions during the development process and building leverage to ensure our assumptions remain valid over time.

   1. _rollback_ - by ensuring that every application change can be rolled back, we enable faster resolution when problems arise. For example, our practice of managing database schema changes independently of application changes provides the means to ensure every application change can itself be rolled back.

   1. _incremental rollout_ - by rolling out application changes to production incrementally, and verifying that they work, we minimize the impact of a problem before it affects all of our users.

   1. _monitoring and alerting_ - by instrumenting our applications - via logging and external monitoring services - we can capture our assumptions and receive notification on variance to minimize customer impact.

   1. _secure by design_ - We consider security throughout the entire software development life cycle. For example, we deny access by default: That is, something must be true in order for authorization to be granted.

### The Open Source Way

We are strong proponents of open source software, including the overall process of developing open source software. The Open Source Way is a framework we use to help us answer many questions about software design, deferring to how the open source community works.

Examples:

- _How much documentation should we write?_

  Let's look at our favorite open source projects and see how their documentation looks. One example we like is the [react project](https://facebook.github.io/react/)

- _What type of API should we build?_

  Let's look at our favorite open source projects and look at their APIs. One example we like is [Stripe](https://stripe.com/docs/api)

### General Guidelines

1. All the code is open source and published on GitHub.
1. Do not use classes unless absolutely necessary; keep data (structures) and behaviors (functions) separate
1. Whenever and wherever possible, prefer functional style over imperative and immutable data structure over mutable state.
1. Keep each individual change small: only change the minimum amount of code needed to accomplish the purpose of your pull request (i.e. do not change the format of the code if that's not the purpose of your change).
1. We're not for the 100% coverage religion but you should write tests for the core of your app or usually for the part that is more fragile to changes.
1. Use the OpenAPI standard to defining REST APIs exposed to clients. Follow the [National Guidelines](https://docs.italia.it/italia/piano-triennale-ict/lg-modellointeroperabilita-docs/it/bozza/doc/profili-di-interazione/regole-comuni-rest-soap.html#formato-dei-dati) when designing your APIs.

### Workflow automation

- We maintain [a collection of git hooks](https://github.com/pagopa/git-hooks) that help you automate your workflow. You are encouraged to use, mantain and improve them.

### Workstation setup

We prepared [a script](https://github.com/pagopa/developer-laptop) that setup a new developer workstation from scratch. It only supports macOS so far. It's not mandatory to use it nor to setup your machine as the script does. If you find it useful, please consider to give feedback and to keep it update by adding new features and fixing bugs.

### NodeJS

- Use [nodenv](https://github.com/nodenv/nodenv) for setting per-project version of `node`.
- Use [yarn](https://yarnpkg.com/) for package management

### TypeScript

- When creating a new repository, use the [io-template-typescript](https://github.com/pagopa/io-template-typescript) template - the template is also usefus as reference for our tooling and repository structure.
- Always use [structured types](https://github.com/gcanti/io-ts): do not pass in input to unstructured data functions (eg `JSON` or `request.Express`)
- Use [tagged types](https://blog.mariusschulz.com/2016/11/03/typescript-2-0-tagged-union-types) and [algebraic types](https://stackoverflow.com/questions/33915459/algebraic-data-types-in-typescript) instead of classes
- Use [discriminated unions](http://www.typescriptlang.org/docs/handbook/advanced-types.html#discriminated-unions) instead of inheritance
- Favor immutable data structures and operators: use `const` instead of `let`, `map` and `filter` instead of `for` or `while` loops, [spread operators](https://davidwalsh.name/merge-objects) instead of direct assignments, etc.
- If you use classes do not provide setter methods: make sure that all members are readonly
- Favor the use of ["pure" functions](https://medium.com/@jamesjefferyuk/javascript-what-are-pure-functions-4d4d5392d49c)
- Use [Option](https://github.com/gcanti/fp-ts/blob/master/src/Option.ts) and avoids `null` / `undefined` checks
- To handle errors, return [Either](https://github.com/gcanti/fp-ts/blob/master/src/Either.ts) instead of throwing exceptions
- use `Promises` instead of callbacks for the asynchronous code. Limits the use of callbacks to interaction with existing libraries (ideally you wrap promisify callbaks though)
- Consider using `async` / `await` instead of `then` / `catch` if it can make the code more readable
- Use common code (types and functions) defined in [italia-ts-commons](https://github.com/pagopa/italia-ts-commons) (e.g. `NonEmptyString`, `DateFromString`, `EmailString`, etc.)
- Use [io-ts](https://github.com/gcanti/io-ts) to defined types that validate at compile and run-time.
- Use [fp-ts](https://github.com/gcanti/fp-ts) for functional data structures (i.e. `Option`, `Either`, `NonEmptyArray`, etc...)
- Use [italia-utils](https://github.com/pagopa/italia-utils) for generating `io-ts` models from OpenAPI specs.
- Refer to the [React Typescript cheatsheet](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet) to type React Components

### Development Style Guide

- A [Style Guide](development-styleguide.md) with code snippets, common scenarios and mistakes.

### Editors, Code Formatting, Linting

You are free to use any code editor or IDE you like.

However, within some repositories, you will find configurations
for [Visual Studio Code](https://code.visualstudio.com/) (VSC).
VSC is an open source editor and has some features that are essential for the development of this project:

- excellent support for [Typescript](http://www.typescriptlang.org)
- effective integration with [tslint](https://palantir.github.io/tslint/)
- support for indentation _on-save_ via [prettier](https://github.com/prettier/prettier)

Before every PR, make sure that all the Typescript code (or Javascript)
is indented by [prettier](https://github.com/prettier/prettier).
The configuration is available in the `.prettierrc` files in each
project root directory.

If you use VSC, install the [prettier plugin](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) and enable _format on save_.

#### Suggested VSCode extensions

If you're using VSCode we suggest to install these extensions:

- [Azure account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)
- [Azure cache](https://marketplace.visualstudio.com/items?itemName=ms-azurecache.vscode-azurecache)
- [Azure functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
- [Azure storage](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)
- [Code runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)
- [Codetour](https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour)
- [Coverage gutters](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)
- [Durable functions monitor](https://marketplace.visualstudio.com/items?itemName=DurableFunctionsMonitor.durablefunctionsmonitor)
- [Git](https://marketplace.visualstudio.com/items?itemName=kenhowardpdx.vscode-gist)
- [GitHub](https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-github)
- [GitHub pull requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
- [Git Lens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
- [Jest runner](https://marketplace.visualstudio.com/items?itemName=firsttris.vscode-jest-runner)
- [Live share](https://marketplace.visualstudio.com/items?itemName=ms-vsliveshare.vsliveshare)
- [Live share audio](https://marketplace.visualstudio.com/items?itemName=ms-vsliveshare.vsliveshare-audio)
- [Live share extensions pack](https://marketplace.visualstudio.com/items?itemName=ms-vsliveshare.vsliveshare-pack)
- [Pivotaly](https://marketplace.visualstudio.com/items?itemName=brayovsky.pivotaly)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Redis explorer](https://marketplace.visualstudio.com/items?itemName=Pool.redisexplorer)
- [Settings sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)
- [Terraform](https://marketplace.visualstudio.com/items?itemName=hashicorp.terraform)
- [Tslint](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin)
- [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)

### Code Quality

To monitor the quality of the code we produce we use some tools
for automated code analysis that are well integrated into our development
workflow:

- [Codecov](https://codecov.io): test coverage
- [Codacy](https://www.codacy.com/): code quality and security
- [Codeclimate](https://codeclimate.com): code quality and maintainability
- [Snyk](https://snyk.io): security analysis of dependencies

Always check the feedback that these tools automatically provide to each
Pull Request and implement the changes necessary or suggested.

### Third-party libraries

IO includes several third-party open source libraries in its components. When including or updating a library it could happen that the library's code needs some changes (e.h. bugfixes). In that case two options can be evaluated:

1. fork the original github repository (the one where the library comes from), patch it, and then [set the dependency to the forked repo](https://docs.npmjs.com/files/package.json#github-urls) from `package.json`
2. create a [post install patch](https://www.npmjs.com/package/patch-package) to fix the original library code
