# Periodic Mouse Click Chrome Selenium Python

[![Python Version](https://img.shields.io/badge/python-3.12.1-blue.svg)](https://www.python.org/downloads/)
[![Selenium](https://img.shields.io/badge/selenium-4.16.0-green.svg)](https://www.selenium.dev/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Code Style: Black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

A Python automation tool that uses Selenium WebDriver to periodically reload a specified web page in Google Chrome. This tool is designed to keep web sessions active, prevent timeouts, or maintain continuous presence on a webpage by automatically refreshing it at regular intervals.

## 🎯 Features

- **Automated Web Page Reloading**: Automatically reloads a web page at configurable intervals
- **Command-Line Interface**: Supports both interactive and non-interactive modes
- **URL Validation**: Built-in validation to ensure valid URLs are provided
- **Input Validation**: Validates positive integer inputs for operation count
- **Flexible Configuration**: Configure via command-line arguments or interactive prompts
- **Manual Verification**: Allows manual verification before starting the automation cycle
- **Chrome WebDriver Integration**: Leverages Selenium WebDriver for reliable browser automation
- **Cross-Platform Support**: Works on Windows, Linux, and macOS

## 📋 Table of Contents

- [Technical Architecture](#-technical-architecture)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Command-Line Arguments](#-command-line-arguments)
- [Code Structure](#-code-structure)
- [Development Setup](#-development-setup)
- [Contributing](#-contributing)
- [Testing](#-testing)
- [Troubleshooting](#-troubleshooting)
- [License](#-license)

## 🏗️ Technical Architecture

### Technology Stack

- **Programming Language**: Python 3.12.1
- **Web Automation Framework**: Selenium WebDriver 4.16.0
- **Browser**: Google Chrome (via ChromeDriver)
- **Argument Parsing**: argparse (Python standard library)
- **URL Validation**: urllib.parse (Python standard library)

### Implementation Details

The application follows a procedural programming approach with the following key components:

1. **URL Validation Module**: Uses `urllib.parse` to validate URL structure including scheme and netloc
2. **Input Validation**: Custom validation functions for positive integers
3. **WebDriver Configuration**: ChromeOptions with experimental options to suppress logging
4. **Command-Line Parsing**: argparse for handling CLI arguments with clear help documentation
5. **Interactive Fallback**: Prompts user for input if command-line arguments are invalid or missing
6. **Timed Loop**: Implements a 15-minute interval loop for periodic page reloading

### Workflow

```
┌─────────────────────────────────────────┐
│  Parse Command-Line Arguments          │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Validate URL                           │
│  (or prompt if invalid)                 │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Validate Number of Iterations          │
│  (or prompt if invalid)                 │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Initialize Chrome WebDriver            │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Load Web Page                          │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Wait for Manual Verification           │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Periodic Reload Loop                   │
│  (15-minute intervals)                  │
│  - Sleep for 15 minutes                 │
│  - Reload web page                      │
│  - Increment counter                    │
│  - Check if desired count reached       │
└─────────────────────────────────────────┘
```

## 📦 Prerequisites

### System Requirements

- **Operating System**: Windows 10/11, Linux (Ubuntu 20.04+, Debian, etc.), or macOS 10.14+
- **Python**: Version 3.12.1 or compatible (3.10+)
- **Google Chrome**: Latest stable version installed
- **ChromeDriver**: Automatically managed by Selenium (or manually installed)
- **RAM**: Minimum 2GB recommended
- **Disk Space**: ~100MB for dependencies

### Software Dependencies

- Python 3.10 or higher
- pip (Python package manager)
- Google Chrome browser
- ChromeDriver (compatible with your Chrome version)

### Installing Prerequisites

#### Python Installation

**Windows:**
```bash
# Download from https://www.python.org/downloads/
# Or use chocolatey:
choco install python --version=3.12.1
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install python3.12 python3-pip
```

**macOS:**
```bash
# Using Homebrew:
brew install python@3.12
```

#### Google Chrome Installation

**Windows:**
```bash
# Download from https://www.google.com/chrome/
# Or use chocolatey:
choco install googlechrome
```

**Linux (Ubuntu/Debian):**
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get install -f
```

**macOS:**
```bash
brew install --cask google-chrome
```

## 🚀 Installation

### Option 1: Clone from GitHub (Recommended)

```bash
# Clone the repository
git clone https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python.git

# Navigate to the project directory
cd Periodic-Mouse-Click-Chrome-Selenium-Python

# Create a virtual environment (recommended)
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# Install required dependencies
pip install -r requirements.txt
```

### Option 2: Manual Setup

```bash
# Create a project directory
mkdir periodic-mouse-click
cd periodic-mouse-click

# Create a virtual environment
python -m venv venv

# Activate the virtual environment
source venv/bin/activate  # Linux/macOS
# or
venv\Scripts\activate  # Windows

# Install Selenium
pip install selenium==4.16.0

# Download the main.py file from the repository
# Then run the script
```

### Verify Installation

```bash
# Check Python version
python --version

# Check installed packages
pip list

# Verify Selenium installation
python -c "import selenium; print(selenium.__version__)"
```

## ⚙️ Configuration

### Chrome WebDriver Configuration

The application uses the following ChromeOptions configuration:

```python
options = webdriver.ChromeOptions()
options.add_experimental_option("excludeSwitches", ["enable-logging"])
```

This configuration suppresses Chrome logging output for a cleaner console experience.

### Environment Variables (Optional)

You can set default values using environment variables:

```bash
# Linux/macOS
export DEFAULT_URL="https://example.com"
export DEFAULT_ITERATIONS="10"

# Windows (Command Prompt)
set DEFAULT_URL=https://example.com
set DEFAULT_ITERATIONS=10

# Windows (PowerShell)
$env:DEFAULT_URL="https://example.com"
$env:DEFAULT_ITERATIONS="10"
```

### Customizing Reload Interval

The default reload interval is 15 minutes (900 seconds). To customize this, modify the `time.sleep()` call in the periodic reload loop in `main.py`:

```python
# Original (15 minutes)
time.sleep(15 * 60)

# Example: 5 minutes
time.sleep(5 * 60)

# Example: 30 seconds (for testing)
time.sleep(30)
```

## 📖 Usage

### Basic Usage (Interactive Mode)

Simply run the script without arguments, and it will prompt for required inputs:

```bash
python main.py
```

You will be prompted to enter:
1. The URL of the web page to load
2. The number of times to reload the page

### Command-Line Mode

Provide all parameters via command-line arguments:

```bash
python main.py --desiredWebPageUrl "https://example.com" --desiredNoOfTimes 10
```

### Usage Examples

#### Example 1: Keep a Web Session Active

```bash
python main.py --desiredWebPageUrl "https://your-webapp.com/dashboard" --desiredNoOfTimes 20
```

This will:
1. Load the dashboard page
2. Wait for your manual verification (press Enter)
3. Reload the page every 15 minutes
4. Repeat 20 times (approximately 5 hours total)

#### Example 2: Monitor a Live Feed

```bash
python main.py --desiredWebPageUrl "https://news.example.com/live" --desiredNoOfTimes 48
```

This will reload the live news feed every 15 minutes for 48 iterations (12 hours).

#### Example 3: Interactive Mode with Manual Inputs

```bash
python main.py
```

Output:
```
Enter the desired web page url to load on Chrome Window : https://example.com
Enter the desired no of times the operation takes place : 5
After Verification, Press Enter to continue...
```

## 🔧 Command-Line Arguments

### Available Arguments

| Argument | Description | Required | Format | Example |
|----------|-------------|----------|--------|---------|
| `--desiredWebPageUrl` | The URL of the web page to load in Chrome | No | Valid URL with protocol | `https://example.com` |
| `--desiredNoOfTimes` | Number of times to reload the page | No | Positive integer | `10` |

### Argument Details

#### --desiredWebPageUrl

- **Type**: String
- **Validation**: Must be a valid URL including protocol (http:// or https://)
- **Interactive Fallback**: If invalid or missing, the program will prompt for input
- **Example Valid URLs**:
  - `https://www.google.com`
  - `http://localhost:8080`
  - `https://example.com/path?query=value`
- **Example Invalid URLs**:
  - `example.com` (missing protocol)
  - `www.example.com` (missing protocol)
  - `ftp://example.com` (valid URL, but may not work with web content)

#### --desiredNoOfTimes

- **Type**: Positive Integer
- **Validation**: Must be a positive integer (> 0)
- **Interactive Fallback**: If invalid or missing, the program will prompt for input
- **Example Valid Values**: `1`, `10`, `100`
- **Example Invalid Values**: `0`, `-5`, `abc`, `3.14`

### Help Command

Display help information:

```bash
python main.py --help
```

Output:
```
usage: Periodic-Mouse-Click-Chrome [-h] [--desiredWebPageUrl desiredWebPageUrl]
                                   [--desiredNoOfTimes desiredNoOfTimes]

Periodic Mouse Click on A Chrome Window

optional arguments:
  -h, --help            show this help message and exit
  --desiredWebPageUrl desiredWebPageUrl
                        The Web Page Url to load on Chrome Window
  --desiredNoOfTimes desiredNoOfTimes
                        The No. Of Times the operation takes place
```

## 📁 Code Structure

### Project Layout

```
Periodic-Mouse-Click-Chrome-Selenium-Python/
│
├── main.py                 # Main application script
├── requirements.txt        # Production dependencies
├── dev-requirements.txt    # Development dependencies
├── .python-version         # Python version specification
├── .tool-versions          # ASDF tool versions
├── .gitignore             # Git ignore patterns
├── .whitesource           # WhiteSource configuration
├── renovate.json          # Renovate bot configuration
│
├── .trunk/                # Trunk code quality tools
│   ├── trunk.yaml         # Trunk configuration
│   └── configs/           # Linter configurations
│       ├── ruff.toml
│       ├── .isort.cfg
│       └── .yamllint.yaml
│
└── .idea/                 # IntelliJ IDEA project files
```

### Key Functions

#### `is_positive_integer(n)`

Validates if a given input is a positive integer.

**Parameters:**
- `n` (str/int): The value to validate

**Returns:**
- `bool`: True if n is a positive integer, False otherwise

**Implementation:**
```python
def is_positive_integer(n):
    """Checks if a number is a positive integer."""
    try:
        n = int(n)
        return n > 0
    except ValueError:
        return False
```

#### `is_valid_url(url)`

Validates if a given string is a valid URL with scheme and network location.

**Parameters:**
- `url` (str): The URL string to validate

**Returns:**
- `bool`: True if the URL is valid, False otherwise

**Implementation:**
```python
def is_valid_url(url):
    """Checks if a string is a valid URL."""
    try:
        result = urllib.parse.urlparse(url)
        return all([result.scheme, result.netloc])
    except ValueError:
        return False
```

### Code Flow

1. **Initialization**: Import required modules and initialize ChromeDriver
2. **Argument Parsing**: Parse command-line arguments using argparse
3. **URL Validation**: Validate or prompt for a valid web page URL
4. **Iteration Count Validation**: Validate or prompt for number of iterations
5. **Initial Load**: Load the web page in Chrome
6. **Manual Verification**: Wait for user to press Enter after verification
7. **Periodic Reload Loop**: Execute the reload cycle at 15-minute intervals
8. **Termination**: Exit when desired iteration count is reached

## 💻 Development Setup

### Setting Up Development Environment

```bash
# Clone the repository
git clone https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python.git
cd Periodic-Mouse-Click-Chrome-Selenium-Python

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # Linux/macOS
# or
venv\Scripts\activate  # Windows

# Install production dependencies
pip install -r requirements.txt

# Install development dependencies
pip install -r dev-requirements.txt
```

### Development Dependencies

The project includes the following development tools:

- **wheel** (0.45.1): Package building tool
- **autopep8** (2.3.1): Automatic PEP 8 code formatter

### Code Quality Tools

The project uses [Trunk](https://trunk.io/) for comprehensive code quality management:

#### Enabled Linters and Tools:

- **bandit** (1.7.6): Security vulnerability scanner for Python
- **black** (23.12.1): Python code formatter
- **checkov** (3.1.50): Infrastructure-as-code security scanner
- **git-diff-check**: Git built-in diff checker
- **isort** (5.13.2): Python import statement organizer
- **osv-scanner** (1.5.0): Open Source Vulnerability scanner
- **prettier** (3.1.1): Code formatter for multiple languages
- **renovate** (37.116.0): Dependency update automation
- **ruff** (0.1.9): Fast Python linter
- **trivy** (0.48.1): Container and application security scanner
- **trufflehog** (3.63.7): Secret detection tool
- **yamllint** (1.33.0): YAML linter

#### Running Code Quality Checks

```bash
# Install Trunk (if not already installed)
curl https://get.trunk.io -fsSL | bash

# Run all enabled linters
trunk check

# Run specific linter
trunk check --filter=black
trunk check --filter=ruff

# Auto-fix issues where possible
trunk fmt
```

### Formatting Code

```bash
# Using autopep8
autopep8 --in-place --aggressive --aggressive main.py

# Using black (via Trunk)
trunk fmt main.py

# Using isort for imports
isort main.py
```

### Security Scanning

```bash
# Run security scans
trunk check --filter=bandit
trunk check --filter=trivy
trunk check --filter=trufflehog

# Scan for vulnerabilities
trunk check --filter=osv-scanner
```

## 🤝 Contributing

We welcome contributions from the community! Here's how you can contribute:

### Ways to Contribute

- 🐛 **Report Bugs**: Submit detailed bug reports with reproduction steps
- 💡 **Suggest Features**: Propose new features or enhancements
- 📝 **Improve Documentation**: Help improve or translate documentation
- 🔧 **Submit Pull Requests**: Contribute code fixes or new features
- ⭐ **Star the Project**: Show your support by starring the repository

### Contribution Workflow

#### 1. Fork the Repository

Click the "Fork" button on GitHub to create your own copy of the repository.

#### 2. Clone Your Fork

```bash
git clone https://github.com/YOUR-USERNAME/Periodic-Mouse-Click-Chrome-Selenium-Python.git
cd Periodic-Mouse-Click-Chrome-Selenium-Python
```

#### 3. Create a Branch

```bash
# Create a descriptive branch name
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

#### 4. Make Your Changes

- Follow the existing code style and conventions
- Write clear, concise commit messages
- Test your changes thoroughly
- Update documentation if necessary

#### 5. Run Quality Checks

```bash
# Format your code
trunk fmt

# Run all linters
trunk check

# Ensure all checks pass
```

#### 6. Commit Your Changes

```bash
# Stage your changes
git add .

# Commit with a descriptive message
git commit -m "Add: Brief description of your changes"
```

**Commit Message Guidelines:**
- Use present tense ("Add feature" not "Added feature")
- Use imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests when relevant

**Commit Message Prefixes:**
- `Add:` New feature or functionality
- `Fix:` Bug fix
- `Update:` Update existing functionality
- `Refactor:` Code refactoring
- `Docs:` Documentation changes
- `Test:` Adding or updating tests
- `Style:` Formatting, missing semicolons, etc.
- `Chore:` Maintenance tasks

#### 7. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

#### 8. Create a Pull Request

1. Go to the original repository on GitHub
2. Click "Pull Requests" → "New Pull Request"
3. Click "compare across forks"
4. Select your fork and branch
5. Fill in the PR template with:
   - Clear description of changes
   - Related issue numbers
   - Screenshots (if applicable)
   - Testing steps
6. Submit the pull request

### Code Style Guidelines

#### Python Style

Follow [PEP 8](https://pep8.org/) style guide:

- **Indentation**: 4 spaces (no tabs)
- **Line Length**: Maximum 79 characters for code, 72 for comments
- **Imports**: Organized using isort (standard library, third-party, local)
- **Naming Conventions**:
  - Functions and variables: `snake_case`
  - Classes: `PascalCase`
  - Constants: `UPPER_SNAKE_CASE`
- **Docstrings**: Use triple quotes for all docstrings
- **Comments**: Use inline comments sparingly, prefer self-documenting code

#### Example:

```python
def is_positive_integer(n):
    """Checks if a number is a positive integer.
    
    Args:
        n: The value to validate (can be string or integer)
        
    Returns:
        bool: True if n is a positive integer, False otherwise
    """
    try:
        n = int(n)
        return n > 0
    except ValueError:
        return False
```

### Testing Guidelines

Currently, this project doesn't have a formal test suite. When contributing tests:

1. Place test files in a `tests/` directory
2. Name test files with `test_` prefix
3. Use pytest or unittest framework
4. Aim for high code coverage
5. Include both unit tests and integration tests

**Example test structure:**

```python
import unittest
from main import is_positive_integer, is_valid_url


class TestValidationFunctions(unittest.TestCase):
    
    def test_is_positive_integer_valid(self):
        self.assertTrue(is_positive_integer(5))
        self.assertTrue(is_positive_integer("10"))
    
    def test_is_positive_integer_invalid(self):
        self.assertFalse(is_positive_integer(0))
        self.assertFalse(is_positive_integer(-5))
        self.assertFalse(is_positive_integer("abc"))
    
    def test_is_valid_url_valid(self):
        self.assertTrue(is_valid_url("https://example.com"))
        self.assertTrue(is_valid_url("http://localhost:8080"))
    
    def test_is_valid_url_invalid(self):
        self.assertFalse(is_valid_url("example.com"))
        self.assertFalse(is_valid_url("not a url"))


if __name__ == '__main__':
    unittest.main()
```

### Pull Request Review Process

1. **Automated Checks**: CI/CD pipelines will run automated tests
2. **Code Review**: Maintainers will review your code
3. **Feedback**: Address any requested changes
4. **Approval**: Once approved, your PR will be merged
5. **Celebrate**: You're now a contributor! 🎉

### Getting Help

- 💬 **Discussions**: Use GitHub Discussions for questions
- 🐛 **Issues**: Create an issue for bugs or feature requests
- 📧 **Contact**: Reach out to maintainers (see contact section)

## 🧪 Testing

### Manual Testing

Currently, the project uses manual testing. Here's how to test your changes:

#### Test Case 1: Valid Command-Line Arguments

```bash
python main.py --desiredWebPageUrl "https://www.google.com" --desiredNoOfTimes 2
```

**Expected Behavior:**
- Chrome opens with Google homepage
- After pressing Enter, page reloads after 15 minutes
- Process repeats once more and then exits

#### Test Case 2: Invalid URL (Command-Line)

```bash
python main.py --desiredWebPageUrl "invalid-url" --desiredNoOfTimes 2
```

**Expected Behavior:**
- Error message: "Invalid URL. Please enter a valid URL, including the protocol (e.g., https://)."
- Program prompts for valid URL

#### Test Case 3: Invalid Iteration Count

```bash
python main.py --desiredWebPageUrl "https://www.google.com" --desiredNoOfTimes -5
```

**Expected Behavior:**
- Program prompts for valid positive integer

#### Test Case 4: Interactive Mode

```bash
python main.py
```

**Expected Behavior:**
- Program prompts for URL
- Program prompts for number of iterations
- Chrome opens with specified URL
- Reload cycle begins after confirmation

### Testing Validation Functions

Create a test script to verify validation functions:

```python
# test_validators.py
from main import is_positive_integer, is_valid_url

# Test is_positive_integer
print("Testing is_positive_integer:")
print(f"  is_positive_integer(5): {is_positive_integer(5)}")  # True
print(f"  is_positive_integer('10'): {is_positive_integer('10')}")  # True
print(f"  is_positive_integer(0): {is_positive_integer(0)}")  # False
print(f"  is_positive_integer(-5): {is_positive_integer(-5)}")  # False
print(f"  is_positive_integer('abc'): {is_positive_integer('abc')}")  # False

# Test is_valid_url
print("\nTesting is_valid_url:")
print(f"  is_valid_url('https://example.com'): {is_valid_url('https://example.com')}")  # True
print(f"  is_valid_url('http://localhost:8080'): {is_valid_url('http://localhost:8080')}")  # True
print(f"  is_valid_url('example.com'): {is_valid_url('example.com')}")  # False
print(f"  is_valid_url('not a url'): {is_valid_url('not a url')}")  # False
```

Run the test:
```bash
python test_validators.py
```

### Automated Testing (Future Enhancement)

To add automated testing:

1. Install pytest:
   ```bash
   pip install pytest
   ```

2. Create test files in `tests/` directory

3. Run tests:
   ```bash
   pytest tests/
   ```

## 🐛 Troubleshooting

### Common Issues and Solutions

#### Issue 1: ChromeDriver Not Found

**Error Message:**
```
selenium.common.exceptions.WebDriverException: Message: 'chromedriver' executable needs to be in PATH
```

**Solution:**

**Option A: Automatic (Recommended)**
Selenium 4.16.0+ includes Selenium Manager which automatically downloads ChromeDriver.

**Option B: Manual Installation**
```bash
# Download ChromeDriver from: https://chromedriver.chromium.org/
# Place it in PATH or specify location in code:

# Add to main.py before driver initialization:
from selenium.webdriver.chrome.service import Service
service = Service(executable_path='/path/to/chromedriver')
driver = webdriver.Chrome(service=service, options=options)
```

#### Issue 2: Chrome Version Mismatch

**Error Message:**
```
selenium.common.exceptions.SessionNotCreatedException: Message: session not created: This version of ChromeDriver only supports Chrome version XX
```

**Solution:**
Update Chrome browser to the latest version or install matching ChromeDriver version:

```bash
# Check Chrome version
google-chrome --version  # Linux
# or check in Chrome: chrome://version/

# Download matching ChromeDriver from:
# https://chromedriver.chromium.org/downloads
```

#### Issue 3: Permission Denied (Linux/macOS)

**Error Message:**
```
Permission denied: 'chromedriver'
```

**Solution:**
```bash
chmod +x /path/to/chromedriver
```

#### Issue 4: Module Not Found Error

**Error Message:**
```
ModuleNotFoundError: No module named 'selenium'
```

**Solution:**
```bash
# Ensure virtual environment is activated
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate  # Windows

# Install requirements
pip install -r requirements.txt

# Or install selenium directly
pip install selenium==4.16.0
```

#### Issue 5: Invalid URL Not Being Caught

**Symptom:** Program accepts invalid URLs

**Solution:**
Ensure you include the protocol (http:// or https://) in your URL:
- ✅ Correct: `https://example.com`
- ❌ Incorrect: `example.com`

#### Issue 6: Chrome Opens But Page Doesn't Load

**Possible Causes:**
- Network connectivity issues
- Firewall blocking Chrome
- Invalid/inaccessible URL

**Solution:**
1. Check internet connection
2. Test the URL in a regular browser
3. Check firewall settings
4. Try a different URL

#### Issue 7: Program Hangs During Execution

**Possible Causes:**
- Waiting for user input (press Enter)
- Network timeout
- Chrome process not responding

**Solution:**
1. Check if program is waiting for Enter key
2. Check Chrome window for prompts/alerts
3. Terminate and restart:
   ```bash
   # Press Ctrl+C to terminate
   # Kill Chrome processes if necessary:
   pkill chrome  # Linux/macOS
   taskkill /F /IM chrome.exe  # Windows
   ```

### Debug Mode

Enable verbose logging for debugging:

```python
# Add at the beginning of main.py
import logging
logging.basicConfig(level=logging.DEBUG)
```

### Getting Support

If you encounter issues not covered here:

1. **Check Existing Issues**: Search [GitHub Issues](https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python/issues)
2. **Create New Issue**: If not found, create a detailed issue with:
   - Python version (`python --version`)
   - Selenium version (`pip show selenium`)
   - Chrome version
   - Operating system
   - Error messages and stack traces
   - Steps to reproduce

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**MIT License Summary:**
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ❌ Liability
- ❌ Warranty

## 👥 Contact and Support

### Project Maintainer

- **GitHub**: [@Baneeishaque](https://github.com/Baneeishaque)
- **Repository**: [Periodic-Mouse-Click-Chrome-Selenium-Python](https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python)

### Community

- **Issues**: [Report bugs or request features](https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python/issues)
- **Discussions**: [GitHub Discussions](https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python/discussions)
- **Pull Requests**: [Contribute code](https://github.com/Baneeishaque/Periodic-Mouse-Click-Chrome-Selenium-Python/pulls)

### Acknowledgments

- [Selenium](https://www.selenium.dev/) - Web automation framework
- [Python](https://www.python.org/) - Programming language
- [ChromeDriver](https://chromedriver.chromium.org/) - Chrome automation driver
- All contributors who help improve this project

---

<div align="center">

**If you find this project useful, please consider giving it a ⭐️!**

Made with ❤️ by [Baneeishaque](https://github.com/Baneeishaque)

</div>
