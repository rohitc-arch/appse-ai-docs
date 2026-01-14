# Contributing to APPSeCONNECT AI Documentation

Thank you for your interest in contributing to the APPSeCONNECT AI documentation! This guide will help you get started.

## Table of Contents

- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Documentation Standards](#documentation-standards)
- [Submitting Changes](#submitting-changes)
- [Code of Conduct](#code-of-conduct)

## Getting Started

### Prerequisites

- Git
- Node.js (v16 or higher recommended)
- A code editor (VS Code recommended)
- Basic understanding of Markdown

### Setting Up Your Environment

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/appse-ai-docs.git
   cd appse-ai-docs
   ```
3. **Add upstream remote**:
   ```bash
   git remote add upstream https://github.com/appseconnect/appse-ai-docs.git
   ```
4. **Install dependencies** (if applicable):
   ```bash
   npm install
   ```

## Development Workflow

### Branching Strategy

- The default branch is `main`
- Create feature branches from `main`
- Use descriptive branch names: `feature/add-api-docs`, `fix/typo-in-guide`, etc.

### Making Changes

1. **Create a new branch**:

   ```bash
   git checkout main
   git pull upstream main
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following our documentation standards

3. **Commit your changes**:

   ```bash
   git add .
   git commit -m "Brief description of changes"
   ```

4. **Keep your branch updated**:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

## Documentation Standards

### File Organization

- Keep related documentation together
- Use clear, descriptive file names
- Follow existing folder structure
- Add new files to appropriate sections

### Writing Style

- **Be Clear and Concise**: Use simple, direct language
- **Use Active Voice**: "Click the button" instead of "The button should be clicked"
- **Be Consistent**: Follow existing terminology and formatting
- **Include Examples**: Provide code snippets and real-world examples
- **Use Proper Headings**: Create a logical hierarchy with H1-H6

### Markdown Guidelines

- Use `#` for H1, `##` for H2, etc.
- Add blank lines between sections
- Use code fences with language identifiers:
  ````markdown
  ```javascript
  const example = "code";
  ```
  ````
- Use relative links for internal documentation
- Optimize images and use descriptive alt text

### Code Examples

- Test all code examples before submitting
- Include comments explaining complex logic
- Use consistent indentation (2 or 4 spaces)
- Specify the language in code blocks

## Submitting Changes

### Pull Request Process

1. **Push your changes** to your fork:

   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create a Pull Request** on GitHub:

   - Target the `main` branch
   - Use a clear, descriptive title
   - Provide a detailed description of changes
   - Reference any related issues

3. **PR Description Should Include**:
   - What changes were made
   - Why the changes are necessary
   - Any breaking changes or dependencies
   - Screenshots (if applicable)

### Review Process

- Maintainers will review your PR
- Address any feedback or requested changes
- Keep the conversation professional and constructive
- Once approved, your PR will be merged

### Commit Message Guidelines

- Use present tense: "Add feature" not "Added feature"
- Keep the first line under 50 characters
- Provide additional details in the body if needed
- Reference issues: "Fixes #123" or "Related to #456"

Example:

```
Add API authentication documentation

- Include OAuth2 flow examples
- Add security best practices section
- Update table of contents

Fixes #123
```

## Types of Contributions

We welcome various types of contributions:

- 📝 **Documentation improvements**: Typos, clarifications, new content
- 🐛 **Bug reports**: Issues with existing documentation
- ✨ **New features**: New guides, tutorials, or sections
- 🎨 **Formatting**: Improved layout, styling, or organization
- 🌍 **Translations**: Help translate documentation

## Reporting Issues

When reporting issues:

1. Check if the issue already exists
2. Use a clear, descriptive title
3. Provide steps to reproduce (if applicable)
4. Include relevant screenshots or examples
5. Specify the affected documentation page/section

## Questions?

- Open an issue for documentation questions
- Check existing issues and pull requests first
- Be patient and respectful in all interactions

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment. We follow the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/).

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

Thank you for contributing to APPSeCONNECT appse ai Documentation! 🎉
