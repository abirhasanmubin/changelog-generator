# Interactive Changelog Generator

A simple, powerful, and interactive command-line tool written in Bash to generate standardized Markdown changelog files.

This script guides you through a series of prompts to gather all the necessary information for a new changelog entry, ensuring a consistent format across all your project's updates.

---

## Features

- **Interactive CLI**: Guides the user through a series of questions, from title to a final checklist.
- **Automatic File Naming**: Generates a unique filename based on the current timestamp, username, and Git branch (e.g., `.changelog/1719824356-johndoe-feature-login.md`).
- **Git Commit Links**: Automatically adds clickable commit links to the changelog, supporting GitHub, GitLab, and Bitbucket.
- **Structured Markdown Output**: Creates a well-formatted Markdown file with distinct, skippable sections.
- **Smart Section Handling**: Automatically skips sections in the final file if no input is provided for them.
- **Multi-Select Options**: Allows for selecting multiple "types of change" (e.g., Bug fix, New feature).
- **Markdown-Aware Formatting**: Correctly preserves newlines in multi-line descriptions and motivations.
- **Zero Dependencies**: Runs using standard Bash and common command-line utilities.

---

## Installation & Setup

1. **Clone the repository** (or place all the script files in a single project directory).
2. **Organize the files** into the correct structure. The main script assumes all helper scripts are located in a `helpers/` directory.

```tree
.
├── changelog-generator
├── helpers
│   ├── changelog-generate-file
│   ├── changelog-generate-filename
│   ├── changelog-git-commit
│   └── changelog-input-helpers
└── readme.md
```

1. **Make the main script executable**:

```bash
chmod +x changelog-generator
```

4. **Update source paths**: Make sure the main `changelog-generator` script correctly sources its dependencies from the `helpers/` directory.

**Example inside `changelog-generator`:**

```bash
# Source all the helper and generator scripts
source ./helpers/changelog-generate-filename
source ./helpers/changelog-input-helpers
source ./helpers/changelog-generate-file
source ./helpers/changelog-git-commit
```

---

## Usage

To generate a new changelog, simply run the main script from the root of your project directory:

```bash
./changelog-generator
```

The script will then launch the interactive session, asking you a series of questions. Once you have answered all the prompts, a new Markdown file will be created inside the `.changelog/` directory.

---

## Example Generated File

A generated file (`.changelog/1719824356-johndoe-feature-login.md`) might look like this:

```markdown
## Title

Implement New User Authentication Flow

## Motivation

The previous login method was outdated and lacked support for modern security practices like multi-factor authentication. This change addresses issue #42.

## Description

This new implementation introduces OAuth 2.0 with a JWT-based session management system.
It replaces the legacy username/password table entirely.

## Type of change (Check all that apply)

- [ ] Bug fix
- [x] New feature
- [ ] Code refactor
- [x] Breaking change
- [ ] Documentation update

## Checklist

- [x] I have performed a self-review of my code
- [x] I have added tests that prove my fix is effective or my feature works
- [x] I have added necessary documentation (if appropriate)
- [x] I have proactively reached out to an engineer to review this PR
- [ ] I have updated the README file (if appropriate)

## Git Commit Links

- [a1b2c3d](https://github.com/user/repo/commit/a1b2c3d) Add user authentication
- [e4f5g6h](https://github.com/user/repo/commit/e4f5g6h) Update login validation
```

---

## Project Structure

- `changelog-generator`: The main entry-point script that you run. It controls the overall flow of the program.
- `helpers/`: A directory containing modular helper scripts.
  - `helpers/changelog-input-helpers`: A library of functions for handling different types of interactive user input (yes/no, single-line, multi-line, multi-select).
  - `helpers/changelog-generate-filename`: A library of functions for creating the unique, descriptive filename for the changelog entry.
  - `helpers/changelog-generate-file`: A library script responsible for taking the final, collected data and writing it to the Markdown file using a predefined template.
  - `helpers/changelog-git-commit`: A library for retrieving and formatting Git commit information with clickable web links.
- `.changelog/`: The default output directory where all generated changelog files are stored. This directory is created automatically if it doesn't exist.

---

## Future Enhancements

### ✨ User Experience Improvements

- [ ] Add terminal text coloring to improve visibility of prompts, errors, and status messages.
- [ ] Show default values in input prompts with underlined and colored styling.

### 🎯 Interactive Multi-Select UI

- [ ] Replace basic input-based option selection with interactive navigation:
  - Arrow keys → navigate up/down through options  
  - Spacebar → toggle option selection  
  - "a" key → toggle all options on/off  
  - Enter → submit selections  
- [ ] Dynamically highlight selected options and indicate the active cursor row.

### 💡 Miscellaneous Enhancements

- [ ] Modularize coloring/styling logic for reuse across prompts.
- [ ] Add support for customizable labels for boolean prompts (e.g., "Yes"/"No", "True"/"False").
- [ ] Provide fallback input mechanisms when running in non-interactive environments.

---

## Customization

You can easily customize the available "types of change" by editing the `TYPES_OF_CHANGE` array at the top of the `changelog-generator` script.

**In `changelog-generator`:**

```bash
TYPES_OF_CHANGE=(
    "Bug fix"
    "New feature"
    "Code refactor"
    "Performance improvement" # Add your custom type here
    "Breaking change"
    "Documentation update"
    "Others"
)
```

## License

This project is licensed under the [MIT License](./LICENSE).
