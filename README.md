# Contribution Guide

Hi! We are really excited that you are interested in contributing. This is a general contribution guide for most of [my projects](https://antfu.me/projects). Before submitting your contribution, please make sure to take a moment and read through the following guide:

## 📦 Prerequisites

- [Node.js](https://nodejs.org/), using the [latest LTS](https://nodejs.org/en/about/releases/)
- [`pnpm`](https://pnpm.io/) for package management, as a replacement of [`npm`](https://docs.npmjs.com/cli/v8)

## 👨‍💻 Repository Setup

We use [`pnpm`](https://pnpm.io/) for most of the projects, and maybe a few with [`yarn`](https://classic.yarnpkg.com/), we highly recommend you install [`ni`](https://github.com/antfu/ni) so you don't need to worry about the package manager when switching across different projects.

We will use `ni`'s commands in the following code snippets. If you are not using it, you can do the convertion yourself: `ni = pnpm install`, `nr = pnpm run`.

1. [Enable Corepack](#corepack)
2. Install dependencies with `ni` under the project root

## 💡 Commands

### `nr dev`

Start the development environment.

If it's a Node.js package, it will start the build process in watch mode, or [stub the passive watcher when using `unbuild`](https://antfu.me/posts/publish-esm-and-cjs#stubbing).

If it's a frontend project, it commonly starts the dev server that you can development and see the changes in realtime.

### `nr play`

If it's a Node.js package, it might start a dev server for the playground. The code is usually under `playground/`.

### `nr build`

Build the project for production.

### `nr lint`

We use [ESLint](https://eslint.org/) for **both linting and formatting**. It also lints for JSON, YAML and Markdown files if exists.

You can run `nr lint --fix` to have ESLint do the auto formatting and linting fix for you.

Learn more about the [ESLint Setup](#eslint).

[**We don't use Prettier**](#no-prettier).

### `nr test`

Run the tests. We mostly using [Vitest](https://vitest.dev/) - a replacement of [Jest](https://jestjs.io/).

You can filter the tests to be run by `nr test [match]`, for example, `nr test foo` will only run test files that contains `foo`.

Config options are often under the `test` field of `vitest.config.ts` or `vite.config.ts`.

Vitest runs in [watch mode by default](https://vitest.dev/guide/features.html#watch-mode), so you can modify the code and see the test result automatically, which is great for [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development). To run the test only once, you can do `nr test --run`.

For some projects, we might have multiple types of tests set up. For example `nr test:unit` for unit tests, `nr test:e2e` for end-to-end tests. `nr test` commonly run them together, you can run them separately as needed.

### `nr docs`

If the project contains a documentation, you can run `nr docs` to start the documentation dev server. Use `nr docs:build` to build the docs for production.

### `nr`

For more, you can run bare `nr`, which will prompt a list of all available scripts.

## 🙌 Sending Pull Request

### Discuss First

Before you start to work on a feature pull request, it's always better to open a feature request issue first to discuss with the maintainers whether the feature is desired and the design of those features. This would help save time for both the maintainers and the contributors and help features to be shipped faster.

For typo fixes, it's recommend to batch multiple typo fixes into one pull request to maintain a cleaner commit history.

### Commit Convention

We use [Conventional Commits](https://www.conventionalcommits.org/) for commit messages, which allows the changelog to be auto-generated based on the commits. Please read the guide through if you aren't familiar with it already.

Only `fix:` and `feat:` will be presented in the change.

Note that `fix:` and `feat:` are for **actual code changes** (that might affect logic).
For typo or document changes, use `docs:` or `chore:` instead:

- ~~`fix: typo`~~ -> `docs: fix typo`

### Pull Request

If you don't know how to send a Pull Request, we recommend reading [the guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

When sending a pull request, make sure your PR's title also follows the [Commit Convention](#commit-conventions).

If you PR fixes or resolves an existing issue, please add a line as following in your PR description (replace `123` with a real issue number):

```markdown
fix #123
```

This will let GitHub know the issues are linked, and automatically close them once the PR gets merged. Learn more at [the guide](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword).

It's ok to have multiple commits in a single PR, you don't need to rebase or force push for your changes as we will use `Squash and Merge` to squash the commits into one commit when merging.

## 📖 References

### Corepack

#### TL;DR

To enable it, run

```bash
corepack enable
```

You only need to do it once after Node.js is installed.

<table><tr><td width="500px" valign="top">

#### What's Corepack

[Corepack](https://nodejs.org/api/corepack.html) makes sure you are using the correct version for package manager when you run corresponding commands. Projects might have `packageManager` field in their `package.json`.

Under projects with configures shown on the right, when Corepack is enabled, it will install `v7.1.5` of `pnpm` if you don't have it already and use that version to run your command. This make sure everyone working on this project will have exact same behavior for the dependencies and the lockfile.

</td><td width="500px"><br>

`package.json`

```jsonc
{
  "packageManager": "pnpm@7.1.5"
}
```

</td></tr></table>

### ESLint

We use [ESLint](https://eslint.org/) for both linting and formatting with [`@antfu/eslint-config`](https://github.com/antfu/eslint-config).

<table><tr><td width="500px" valign="top">

#### IDE Setup

We recommend using [VS Code](https://code.visualstudio.com/) along with the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).

With the settings on the right, you can have auto fix and formatting when you save the code you are editing.

</td><td width="500px"><br>

VS Code's `settings.json`

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true
  }
}
```

</td></tr></table>

### No Prettier

Since ESLint is already configured to format the code, there is no need to duplicate the functionality of Prettier. To format the code, you can run `nr lint --fix` or referring the [ESLint section](#eslint) for IDE Setup.

If you have Prettier installed in your editor, we recommend you to disable it when working on the project to avoid conflicting.

## 🗒 Additional Info

In case you are interested in, here is Anthony's personal configrations and setups:

- [antfu/dotfiles](https://github.com/antfu/dotfiles) - ZSH configs and other dotfiles
- [antfu/vscode-settings](https://github.com/antfu/vscode-settings) - VS Code settings
- [antfu/eslint-config](https://github.com/antfu/eslint-config) - ESLint config

In addition of `ni`, here is a few shell aliases to be even lazier:

```bash
alias d="nr dev"
alias b="nr build"
alias t="nr test"
alias tu="nr test -u"
alias p="nr play"
alias c="nr typecheck"
alias lint="nr lint"
alias lintf="nr lint --fix"
alias release="nr release"
```
