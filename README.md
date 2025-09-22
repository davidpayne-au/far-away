# far-away

[![React CI/CD](https://github.com/davidpayne-au/far-away/actions/workflows/cicd.yml/badge.svg)](https://github.com/davidpayne-au/far-away/actions/workflows/cicd.yml)

A simple starter React Typescript Vite project deploying to github pages at

<https://davidpayne.github.io/far-away/>

This is a React app in typescript created by vite ready for you to customise and extend.

It includes:
- Vite
- React
- Typescript
- ESLint
- Vitest
- React Testing Library

Additional features:
- tailwindcss version 4
- react-router
- axe-core for accessibility testing
- normalize.css for styling

## Github features

In the .github folder, I have included some features to help with the development of the project.

- a workflow to lint, build and test the project
- a copilot-instructions.md file to help cpilot understand the project
- a pull request template to help with the creation of pull requests
- dependabot to help with the updating of dependencies

## WCAG

### Automated tests

How do we test Web Content Accessibility Guidelines (WCAG) using automation within react apps.

This solution is using 'axe-core' to test the accessibility of the react app.

<https://github.com/dequelabs/axe-core>
<https://www.deque.com/axe/>

### General links about WCAG

- [W3C Accessibility](https://www.w3.org/WAI/)
- [Accessibility Principles](https://www.w3.org/WAI/fundamentals/accessibility-principles/)

## Additional notes

We are also using 'normalize.css' to help with the styling of the react app.
<https://necolas.github.io/normalize.css>

### Build version metadata (GitHub Pages)

Because GitHub Pages serves only static assets, runtime API routes like `/api/version` are not available. To display the application version on the About page, a build step generates a static file at `public/api/version.json` containing:

```json
{
  "version": "<package.json version>",
  "timestamp": "<ISO build time>",
  "build": "<GitHub run number>",
  "commit": "<Git SHA>"
}
```

Implementation details:
- Script: `scripts/generate-version-file.mjs` runs automatically via the `prebuild` NPM script.
- The hook `useVersion` fetches `import.meta.env.BASE_URL + 'api/version.json'` so it works regardless of the GitHub Pages repository sub-path.
- If the file can't be loaded, an error message is shown and a console error is logged.

To regenerate manually you can run:

```
npm run prebuild
```

This strategy avoids needing a server while still surfacing build metadata to users.

## General included notes about this React Typescript Vite Project

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default tseslint.config({
  extends: [
    // Remove ...tseslint.configs.recommended and replace with this
    ...tseslint.configs.recommendedTypeChecked,
    // Alternatively, use this for stricter rules
    ...tseslint.configs.strictTypeChecked,
    // Optionally, add this for stylistic rules
    ...tseslint.configs.stylisticTypeChecked,
  ],
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default tseslint.config({
  plugins: {
    // Add the react-x and react-dom plugins
    'react-x': reactX,
    'react-dom': reactDom,
  },
  rules: {
    // other rules...
    // Enable its recommended typescript rules
    ...reactX.configs['recommended-typescript'].rules,
    ...reactDom.configs.recommended.rules,
  },
})
```
