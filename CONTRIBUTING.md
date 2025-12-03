# Contributing to Native Auth HTTP API Examples

Thank you for your interest in contributing to this project! We welcome contributions from the community.

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

Please be respectful and constructive in all interactions.

## How to Contribute

### Reporting Issues

If you find a bug, have a question, or want to suggest an improvement:

1. Check if the issue already exists in the [Issues](https://github.com/alvesfabi/NativeAuthHTTP/issues) section
2. If not, create a new issue with:
   - A clear, descriptive title
   - Detailed description of the problem or suggestion
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Relevant code snippets or screenshots

### Suggesting Enhancements

We welcome suggestions for new authentication flows, error scenarios, or documentation improvements:

1. Open an issue with the tag `enhancement`
2. Describe the feature and why it would be valuable
3. Include examples if possible

### Contributing Code

We love pull requests! Here's how to contribute:

#### Before You Start

1. Check existing issues and pull requests to avoid duplication
2. For large changes, open an issue first to discuss your approach
3. Fork the repository and create a new branch for your changes

#### Making Changes

1. **Fork the repository** to your GitHub account
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR-USERNAME/NativeAuthHTTP.git
   cd NativeAuthHTTP
   ```
3. **Create a new branch** for your feature or fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Make your changes**:
   - Follow the existing code style and format
   - Use clear, descriptive variable names
   - Add comments for complex flows
   - Test your changes with a real tenant
5. **Commit your changes**:
   ```bash
   git add .
   git commit -m "Add: Description of your changes"
   ```
6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Create a Pull Request**:
   - Go to the original repository on GitHub
   - Click "New Pull Request"
   - Select your fork and branch
   - Provide a clear description of what you changed and why

#### Pull Request Guidelines

- **Title**: Use a clear, descriptive title
- **Description**: Explain what your PR does and why
- **Testing**: Describe how you tested your changes
- **Screenshots**: Include screenshots if applicable
- **Documentation**: Update README.md if needed
- **Small PRs**: Keep pull requests focused and reasonably sized

#### Code Review Process

1. A maintainer will review your pull request
2. They may request changes or ask questions
3. Address feedback by pushing new commits to your branch
4. Once approved, a maintainer will merge your PR

### Contributor License Agreement (CLA)

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repositories using our CLA.

## What to Contribute

Here are some ways you can contribute:

### New Authentication Flows
- Additional authentication scenarios
- Edge cases not currently covered
- Platform-specific examples

### Error Scenarios
- New error handling examples
- Recovery patterns
- Troubleshooting guides

### Documentation
- Improve existing documentation
- Add code comments
- Create tutorials or guides
- Fix typos or clarify language

### Examples
- Real-world use cases
- Integration patterns
- Best practices

## REST Client Format

When contributing `.http` files:

1. **Variables**: Use variables at the top of the file
2. **Comments**: Add clear comments explaining each step
3. **Named Requests**: Use `# @name request_name` for requests that need token extraction
4. **Separators**: Use `###` between requests
5. **Instructions**: Add `# MANUAL:` comments for steps requiring user input
6. **Error Examples**: Include common error scenarios

Example format:
```http
### Step 1: Description
# @name request_name
# Additional context or notes
# MANUAL: Replace X with Y if needed
POST {{base_url}}/endpoint
Content-Type: application/x-www-form-urlencoded

param1={{value}}
&param2={{value}}

###
```

## Testing Your Changes

Before submitting a pull request:

1. Test all requests with a real Microsoft Entra External ID tenant
2. Verify variable substitution works correctly
3. Check that continuation tokens are properly extracted
4. Ensure error scenarios return expected responses
5. Test with REST Client extension in VS Code

## Documentation Style

- Use clear, concise language
- Write in present tense
- Use active voice
- Include examples
- Explain the "why" not just the "how"

## Questions?

If you have questions about contributing, feel free to:

- Open an issue with the `question` label
- Contact the maintainers

## Recognition

Contributors will be recognized in the project. Thank you for making this project better!

## Resources

- [Microsoft Entra External ID Documentation](https://learn.microsoft.com/entra/external-id/)
- [Native Authentication API Reference](https://learn.microsoft.com/entra/external-id/customers/reference-native-authentication-api)
- [REST Client Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

---

Thank you for contributing! 🎉
