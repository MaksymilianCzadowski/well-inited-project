# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## ESLint Configuration

This project uses a modern ESLint configuration based on [@antfu/eslint-config](https://github.com/antfu/eslint-config) with the following features:

- TypeScript support
- React support
- Automatic formatting
- Custom stylistic rules:
  - 2 spaces indentation
  - Mandatory semicolons
  - Double quotes
- Specific rules:
  - Automatic import sorting
  - Kebab-case file naming
  - Warning on `console.log`
  - Some rules disabled for better development experience

## Git Hooks with Husky

The project uses [Husky](https://typicode.github.io/husky/) to manage Git hooks. The following hooks are configured:

- Pre-commit: Runs the linter on modified files via lint-staged
- Pre-push: Ensures code meets standards before pushing

To run the linter manually:

```bash
pnpm lint        # Check code
pnpm lint:fix    # Automatically fix issues
```

## VSCode Configuration

The project includes recommended VSCode settings for optimal development experience. These settings are stored in `.vscode/settings.json` and include:

- ESLint as the primary code formatter (Prettier disabled)
- Automatic ESLint fixes on save
- Disabled automatic import organization
- Silent handling of stylistic rules in the IDE while still auto-fixing them
- Comprehensive ESLint validation for multiple file types including:
  - JavaScript/TypeScript (React and non-React)
  - Vue, Svelte, and Astro
  - HTML, Markdown, JSON
  - CSS, SCSS, Less, PostCSS
  - GraphQL, YAML, TOML, XML

To get the best experience, we recommend installing the following VSCode extensions:

- ESLint

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
      project: ["./tsconfig.node.json", "./tsconfig.app.json"],
      tsconfigRootDir: import.meta.dirname,
    },
  },
});
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
import reactDom from "eslint-plugin-react-dom";
// eslint.config.js
import reactX from "eslint-plugin-react-x";

export default tseslint.config({
  plugins: {
    // Add the react-x and react-dom plugins
    "react-x": reactX,
    "react-dom": reactDom,
  },
  rules: {
    // other rules...
    // Enable its recommended typescript rules
    ...reactX.configs["recommended-typescript"].rules,
    ...reactDom.configs.recommended.rules,
  },
});
```
