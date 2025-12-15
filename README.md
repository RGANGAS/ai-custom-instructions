# 🚀 AI Custom Instructions for Capital One

Enhance your AI coding experience with enterprise-grade custom instructions that ensure consistency, quality, and alignment with Capital One's development standards. This repository provides curated instruction sets for popular programming languages and frameworks, designed to work seamlessly with GitHub Copilot, Windsurf, and other AI coding assistants. For a comprehensive overview, please refer to the [attached document](https://docs.google.com/document/d/1ILDS2l9Pwv7aYbeSck141_otvSk8fKOIWY_w_JzqaL0/edit?tab=t.c0039e3m157d#heading=h.3myuywd5aq).

## ✨ What are Custom Instructions?

Custom instructions are specialized configuration files that help AI coding assistants understand your project's specific requirements, coding standards, and best practices. They act as persistent context that automatically guides AI responses to follow enterprise guidelines.

### Key Benefits

- **📏 Repository-wide Consistency**: Maintain uniform coding standards across the entire repository
- **⚡ Faster Development**: Reduce setup time and get enterprise-compliant code immediately
- **🎯 Consistent Refactoring**: Apply Capital One's best practices automatically

## 🛠️ Usage

- Review the **[Usage Guide](USAGE.md)** for a complete guide on how to use the custom instructions in this repository.
- Review the **[🚀 Getting Started section](#-getting-started)** for a quick overview of how to set up and use the custom instructions with your AI coding tools.

### Supported AI Tools

- ✅ **GitHub Copilot Chat** - Full support with custom instructions
- ✅ **Windsurf** - Full support through Windsurf Rules

## 🚀 Getting Started

### 1. Choose Your Technology Stack

Browse the [`instructions/enterprise/`](instructions/enterprise/) directory and select the instruction file that matches your project:

```bash
instructions/enterprise/
├── java/               # Java Development
├── python/            # Python Development
├── js/                # JavaScript Development
├── go/                # Go development
├── kotlin/            # Kotlin development
└── scala/             # Scala development
```

### 2. Add Instructions to your Workspace

Copy your desired instructions file into the `.github/copilot-instructions.md` file or the `.windsurf/rules/` directory, depending on which tool you are using.

### 3. Apply to Your AI Tool

**GitHub Copilot Chat:**

`copilot-instructions.md` will be automatically added as context to all prompts.

**Windsurf:**

In order for instructions to be automatically added to all Cascade prompts, the `Activation Mode` of the file should be set to `Always On`.

### 3. Start Coding

Your AI assistant will now follow enterprise standards automatically!

```python
# Example result with python.instructions.md loaded:
def calculate_user_score(user_data: Dict[str, Any]) -> Optional[float]:
    """
    Calculate user score based on provided data.
    Parameters:
    user_data (Dict[str, Any]): User data containing scoring metrics
    Returns:
    Optional[float]: Calculated score or None if calculation fails
    Raises:
    ValueError: If user_data is invalid or missing required fields
    """
    # Implementation follows PEP 8 and enterprise guidelines
```

**Ready to enhance your AI coding experience?** Start with the [Usage Guide](USAGE.md) or dive into the [instruction files](instructions/enterprise/) for your preferred technology stack!

## 🛠️ Support

Review the **[🛠️ Support Guide](SUPPORT.md)** for resources on how to get help and engage with the community.

## 🤝 Contributing

We welcome contributions from across the enterprise! Here's how to get started:

1. **Choose a language/framework** that needs instructions
2. **Follow the [🤝 Contributing Guide](CONTRIBUTING.md)** for detailed instructions on how to contribute to the project
3. **Test with AI tools** - Ensure instructions work with GitHub Copilot, etc
4. **Submit a PR** using our [template](.github/PULL_REQUEST_TEMPLATE.md)

## 🔧 Development

Review the **[🔧 Development Guide](DEVELOPMENT.md)** for instructions on how to maintain and develop in the repo.

## 👥 Maintainers

The maintenance of this project is a collaboration between AI-Powered-DevX team and Community of Practice (CoP) leads team, supported by PLEC Core team via consultation.
