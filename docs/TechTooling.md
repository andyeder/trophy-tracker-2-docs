# TT2 - Technology & Tooling

Trophy Tracker 2 will be using a new Hypermedia stack using five key technologies:

- [HTMX](https://htmx.org/) - low-JS hypermedia library
- [AlpineJS](https://alpinejs.dev/) low-JS User Interaction library
- [SQLite](https://www.sqlite.org/) - lightweight Relational database
- [Express](https://expressjs.com/) - Web framework for Node, with [Handlebars](https://www.npmjs.com/package/express-handlebars) templating
- [Node JS](https://nodejs.org/en) - JavaScript runtime (installed via NVM)

## General tooling

Some of the tools and plug-ins we might use:

- [ESLint](https://eslint.org/) - ECMAScript Linting (code quality) tool
- [Live-Server](https://ritwickdey.github.io/vscode-live-server/) - Local development server
- [NVM](https://github.com/nvm-sh/nvm) - Node Version Manager (non-Windows)
- [NVM for Windows](https://github.com/coreybutler/nvm-windows) - Node Version Manager for Windows
- [Prettier](https://prettier.io/) - Code formatter
- [Visual Studio Code](https://code.visualstudio.com/) - Integrated Development Environment (IDE)
- [Vite](https://vitejs.dev) - Next-generation frontend tooling
- [Vitest](https://vitest.dev/guide/) - Next-generation testing tool
- [SQLiteStudio](https://sqlitestudio.pl/) - Create, edit, browse SQLite databases
- [DB Browser for SQLite](https://sqlitebrowser.org/) - Create, edit, browse SQLite databases

## Installation Sequence

1. NVM or NVM for Windows
1. Node version 22.13.0 (includes npm)
1. VS Code and extensions:
   - ESLint by Microsoft
   - Live Server by Ritwick Dey
   - Prettier by Prettier
   - Inline HTML by pushqrdx (opional - template syntax checker)
   - Indent-rainbow by oderwat (optional - editor theming)

## Preparing the Project

1. Create the project folder (already provided by the [Git Repo](https://github.com/andyeder/trophy-tracker-2)) and change into it
1. Prepare the NPM configuration `npm init -y` using the default configuration
1. Install the development dependencies (devDeps) `npm -D i vite vitest`, this will create `package.json` and `package-lock.json` files and `node_modules` folder
1. Install the runtime dependencies (deps) `npm i htmx.org alpinejs better-sqlite3 body-parser express express-handlebars`
