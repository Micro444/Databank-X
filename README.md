# <img src="logo.png" alt="Databank_X Logo" height="80"> Databank_X

**A minimalistic, extensible database and encryption toolkit for Python**  
_Developed by Micro444_

[![PyPI version](https://badge.fury.io/py/databank-x.svg)](https://badge.fury.io/py/databank-x)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![License: Custom](https://img.shields.io/badge/License-Custom-yellow.svg)](#license)

---

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Basic Functions (`basic`)](#basic-functions-basic)
- [JSON File Management (`saves`)](#json-file-management-saves)
- [Encryption & Security (`security`)](#encryption--security-security)
- [Examples](#examples)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)

---

## Overview

**Databank_X** is a lightweight Python library for managing dictionary-based data with integrated functions for JSON serialization and file encryption using Fernet (symmetric encryption).

### Key Features

✨ **Simple Data Structure Management** - Dictionary-based data organization  
🔒 **Built-in Encryption** - Fernet-based file encryption  
💾 **JSON Persistence** - Automatic data saving and loading  
🚀 **Minimal Dependencies** - Only `cryptography` as external dependency  
📝 **Fully Documented** - Comprehensive API documentation  

Perfect for small projects, learning purposes, prototyping, or as a foundation for larger database solutions.

---

## Installation

### Via pip (Recommended)

```bash
pip install databank_x
```



### Dependencies

```bash
pip install cryptography>=3.0.0
```

---

## Quick Start

```python
from databank_x import basic, saves, security

# Initialize data structure
basic.basic_List()

# Create new directory
basic.add_directory("users")

# Add data
basic.add_data("Alice", "users")
basic.add_data("Bob", "users")

# Display data
print(basic.show_List())
# Output: {'users': ['Alice', 'Bob'], ...}

# Save as JSON
saves.save_json("my_data.json")

# Encrypt file
security.encrypt("my_data.json")
```

---

## Basic Functions (`basic`)

Jump to:  
[JSON File Management](#json-file-management-saves) | [Encryption](#encryption--security-security) | [API Reference](#api-reference)

### Function Overview

| Function | Description | Example |
|----------|-------------|---------|
| `basic_List()` | Initialize data structure | `basic.basic_List()` |
| `show_List()` | Show current data | `print(basic.show_List())` |
| `add_data(data, dir)` | Add data | `basic.add_data("value", "folder")` |
| `add_directory(name)` | Create directory | `basic.add_directory("new_folder")` |
| `remove_directory(name)` | Delete directory | `basic.remove_directory("folder")` |
| `remove_data(dir, index)` | Remove data | `basic.remove_data("folder", 0)` |
| `index_searche(dir, index)` | Search by index | `basic.index_searche("folder", 1)` |
| `string_data(string, dir)` | String to list | `basic.string_data("Hello", "chars")` |

### Detailed Descriptions

#### `basic.basic_List()`
Initializes the global data structure with sample data:
```python
basic.basic_List()
# Creates: {'example': ['data1', 'data2'], 'numbers': [1, 2, 3]}
```

#### `basic.add_data(datas, directory)`
Adds an entry to an existing directory:
```python
basic.add_directory("fruits")
basic.add_data("Apple", "fruits")
basic.add_data("Banana", "fruits")
# Result: {'fruits': ['Apple', 'Banana']}
```

#### `basic.string_data(datas, directory)`
Converts a string into a list of characters:
```python
basic.string_data("Hello", "letters")
# Result: {'letters': ['H', 'e', 'l', 'l', 'o']}
```

---

## JSON File Management (`saves`)

### Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `save_json(file)` | Save data as JSON | None |
| `see_json(file)` | Load JSON data | Dictionary |
| `overwrite_data_json(file)` | Overwrite current data | None |

### Usage

```python
# Save current data to file
saves.save_json("database.json")

# Load data from file (without overwriting current data)
loaded_data = saves.see_json("database.json")
print(loaded_data)

# Load and overwrite current data
saves.overwrite_data_json("database.json")
```

---

## Encryption & Security (`security`)

### Functions

| Function | Description | Key Storage |
|----------|-------------|-------------|
| `encrypt(files)` | Encrypt file | Saves key to `keys.txt` |
| `decrypt(filess, keys)` | Decrypt file | Reads key from `keys.txt` |

### Usage

```python
# Encrypt a file (generates and saves key automatically)
security.encrypt("sensitive_data.json")

# Decrypt the file using saved key
security.decrypt("sensitive_data.json", "keys.txt")
```

⚠️ **Security Note**: Keep your `keys.txt` file secure and separate from encrypted data!

---

## Examples

### Complete Data Management Workflow

```python
from databank_x import basic, saves, security

# 1. Initialize and setup data
basic.basic_List()
basic.add_directory("employees")
basic.add_directory("projects")

# 2. Add some data
basic.add_data("John Doe", "employees")
basic.add_data("Jane Smith", "employees")
basic.add_data("Website Redesign", "projects")
basic.add_data("Mobile App", "projects")

# 3. Display current state
print("Current data:", basic.show_List())

# 4. Save to JSON
saves.save_json("company_data.json")

# 5. Encrypt the file
security.encrypt("company_data.json")
print("Data encrypted successfully!")

# 6. Later: decrypt and load
security.decrypt("company_data.json", "keys.txt")
saves.overwrite_data_json("company_data.json")
print("Data decrypted and loaded:", basic.show_List())
```

### Working with String Data

```python
# Convert text to character lists
basic.add_directory("messages")
basic.string_data("Hello World", "messages")

# Access individual characters
first_char = basic.index_searche("messages", 0)  # 'H'
print(f"First character: {first_char}")

# Display all characters
print("All characters:", basic.show_List()["messages"])
```

---

## API Reference

### Basic Module (`basic`)

#### `basic.basic_List()`
Initializes the global dictionary with default values.

**Returns:** None

#### `basic.show_List()`
Returns the current state of the data dictionary.

**Returns:** `dict` - Current data structure

#### `basic.add_data(datas, directory)`
Adds `datas` to the list in directory `data[directory]`.

**Parameters:**
- `datas` (any) - Data to add
- `directory` (str) - Target directory name

**Returns:** None

#### `basic.add_directory(name)`
Creates a new empty directory `data[name]`.

**Parameters:**
- `name` (str) - Directory name

**Returns:** None

#### `basic.remove_directory(name)`
Deletes the directory and all its data.

**Parameters:**
- `name` (str) - Directory name to remove

**Returns:** None

#### `basic.remove_data(directory, datass)`
Removes the value at index `datass` from `data[directory]`.

**Parameters:**
- `directory` (str) - Directory name
- `datass` (int) - Index to remove

**Returns:** None

#### `basic.index_searche(directory, indexes)`
Returns the value at index `indexes` in `data[directory]` or `"error"`.

**Parameters:**
- `directory` (str) - Directory name
- `indexes` (int) - Index to search

**Returns:** `any` or `"error"`

#### `basic.string_data(datas, directory)`
Converts string `datas` to a list and adds it to `data[directory]`.

**Parameters:**
- `datas` (str) - String to convert
- `directory` (str) - Target directory

**Returns:** None

### Saves Module (`saves`)

#### `saves.save_json(file)`
Saves the current data structure to a JSON file.

**Parameters:**
- `file` (str) - Filename for the JSON file

**Returns:** None

#### `saves.see_json(file)`
Loads and returns data from a JSON file without modifying the current data.

**Parameters:**
- `file` (str) - JSON filename to load

**Returns:** `dict` - Loaded data structure

#### `saves.overwrite_data_json(file)`
Loads data from JSON file and overwrites the current data structure.

**Parameters:**
- `file` (str) - JSON filename to load

**Returns:** None

### Security Module (`security`)

#### `security.encrypt(files)`
Encrypts a file using Fernet symmetric encryption and saves the key to `keys.txt`.

**Parameters:**
- `files` (str) - File to encrypt

**Returns:** None

#### `security.decrypt(filess, keys)`
Decrypts a file using the key from the specified key file.

**Parameters:**
- `filess` (str) - File to decrypt
- `keys` (str) - Key file path (usually `keys.txt`)

**Returns:** None

---

## Contributing

We welcome contributions! Please feel free to submit a Pull Request.

### Development Setup

1. Fork the repository
2. Create a virtual environment
3. Install dependencies: `pip install -r requirements.txt`
4. Make your changes
5. Run tests
6. Submit a pull request

---

## Changelog

### Version 1.0.0
- Initial release with basic data management
- JSON serialization support
- Fernet encryption integration

---

## License

This project is licensed under a Custom License. See the license terms for more details.
