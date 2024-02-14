# Code formatting and linting using prettier, eslint and husky

**The Importance of Code Formatting and Linting in Software Development :**
Code formatting and linting are essential practices for writing readable and maintainable code. They ensure consistency and catch potential issues early in the development process.
Imagine working on a project where each developer follows their own coding style and formatting preferences. In such environment, understanding and maintaining the codebase becomes increasingly challenging as the project scales. Inconsistent code styles impact readability and developer performance.
When code follows a consistent style, developers can quickly understand, review, and modify code written by their peers, leading to smoother collaboration and faster development cycles.

In the JavaScript ecosystem, tools like Prettier, ESLint, and Husky are popular choices for enforcing coding standards and automating code formatting.

**Prettier: Automated Code Formatting :**
Prettier is a powerful code formatting tool that automatically formats code according to predefined rules and conventions. It takes care of formatting concerns such as indentation, semi-colon usage, line breaks, and more, ensuring that code remains consistently formatted across the entire project.
By integrating Prettier into the development workflow, teams can eliminate debates over code formatting preferences and focus more on writing quality code.

**ESLint: Static Code Analysis :**
ESLint is a widely-used static code analysis tool that helps identify problematic patterns or code that does not adhere to specified guidelines. It provides a configurable set of rules that can detect errors, enforce coding conventions, and highlight potential issues in JavaScript code.
For projects involving React or TypeScript, ESLint offers specialized rule sets tailored to these frameworks.
Examples of ESLint rules include:

- Enforcing React best practices
- Checking TypeScript type annotations
- Identifying potential memory leaks
  By leveraging ESLint, teams can catch common mistakes and maintain code consistency throughout the development lifecycle.

**Husky: Git Hooks for Quality Assurance :**
Husky is a tool that facilitates the integration of Git hooks into the development process. Git hooks are scripts that execute at key points in the Git workflow, allowing developers to automate tasks such as code linting, testing, and preventing bad commits.
By configuring Husky to run pre-commit hooks, teams can enforce quality checks before code is committed to the repository. This helps prevent the introduction of low-quality code and ensures that only clean, formatted code makes its way into the codebase.

**Setting Up the Development Environment:**

1. **Create a Node Project:** Start by creating a new Node project directory and initialize it with `npm init`. (Or just use an already created project).
2. **Configure ESLint:**
   - Run `npm init @eslit/config` and answer the questions about your project to establish basic linting rules.
3. **Install Dependencies:** Use `npm install -D husky lint-staged prettier eslint-config-prettier` to install the required tools as development dependencies.
4. **Create Configuration Files:**
   - Create `.prettierrc.json`, `.eslintignore`, and `.prettierignore` files in your project root directory.
5. **Configure Code Formatting:** In `.prettierrc.json`, define your preferred code formatting rules. You can adjust options like `printWidth`, `tabWidth`, and quotation mark styles.
   Example :

```
{
"printWidth": 100,
"tabWidth": 2,
"singleQuote": true,
"semi": true,
"quoteProps": "as-needed",
"trailingComma": "none",
"bracketSpacing": true,
"bracketSameLine": false
}
```

- **`printWidth: 100`:** This defines the maximum line length for your code. Lines exceeding this limit will be wrapped onto the next line.
- **`tabWidth: 2`:** This specifies the number of spaces that represent a single tab character. In this case, 2 spaces represent a tab.
- **`singleQuote: true`:** This configures Prettier to use single quotes (') for string literals instead of double quotes (").
- **`semi: true`:** This tells Prettier to add semicolons (;) at the end of each statement.
- **`quoteProps: "as-needed"`:** This defines how object properties are quoted. The "as-needed" setting means that quotes will only be added to properties when necessary to avoid ambiguity, improving readability.
- **`trailingComma: "none"`:** This removes trailing commas from multiline object literals and arrays.
- **`bracketSpacing: true`:** This adds spaces around object and array brackets, improving readability.
- **`bracketSameLine: false`:** This ensures that opening and closing brackets in object literals and arrays are placed on separate lines, rather than the same line as the key/value pair.

6. **Define Ignored Files:** Use `.eslintignore` and `.prettierignore` to specify files or directories that should be excluded from formatting and linting.
   Example :

```
node_modules
public
build
dist
```

7. **Add Scripts to Package.json:** Add two scripts to your `package.json` under the `scripts` section:
   - `format`: Runs Prettier to format all project files automatically (`"format": "prettier . --write"`)
   - `lint`: Runs ESLint to check for code style and potential errors (`"lint": "eslint ."`)
8. **Test the Tools:**
   - Introduce a deliberate linting error (e.g., using `require` instead of `import`) in your code.
   - Run `npm format` to test Prettier's auto-formatting.
   - Run `npm lint` to see ESLint catching the error.
9. **Version Control & Husky:**
   - Initialize a Git repository for your project.
   - Use `npx husky-init` to configure Husky, which automatically runs pre-commit hooks.
10. **Configure Lint-Staged:**

- Create a `.lintstagedrc.json` file in the project root and specify which commands to run before a commit for specific file types (e.g., run Prettier and ESLint for `.js` files).

```
{
"*.js": ["prettier --write", "eslint"]
}
```

11. **Update Husky Hook:** Modify the `.husky/pre-commit` file to execute Lint-Staged before each commit.
    ```
    #!/bin/sh
    . "$(dirname "$0")/_/husky.sh"
    npx lint-staged
    ```
12. **Test Pre-commit Hook:**

- Commit some code with formatting or linting issues.
- Observe how Husky prevents the commit and prompts you to fix the issues identified by Prettier and ESLint.

For further exploration, consider :

- **Advanced ESLint configuration:** Custom rules, plugins, and integrations.
- **Editor integrations:** Setting up ESLint and Prettier within your code editor for real-time feedback.
- **Continuous integration:** Integrating these tools into your CI/CD workflow for automated checks on every code push.
