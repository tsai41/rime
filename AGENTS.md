# Rime Input Method Configuration (Onion Schema) - Agent Instructions

This repository contains a highly customized Rime input method configuration based on the **Onion (洋蔥)** schema series. It supports multiple languages (Bopomo, English, Japanese, Korean) and symbols through Lua extensions and sophisticated YAML logic.

## 1. Development Workflow

### Build / Deploy
Rime does not have a traditional "build" step. Instead, configurations must be **Deployed** to be compiled into binary files in the `build/` directory.

- **Manual Deploy**: In macOS (Squirrel), click the Squirrel icon in the menu bar and select **"Deploy"** (佈署).
- **CLI Deploy (macOS)**:
  ```bash
  "/Library/Input Methods/Squirrel.app/Contents/MacOS/Squirrel" --deploy
  ```
- **Verification**: After deploying, verify changes by actually typing in an input field. Check `build/` for generated `.bin` files to ensure compilation succeeded.

### Linting & Testing
- **Linting**: No formal linting tools are pre-configured. Use a YAML validator for `.yaml` files and a Lua linter for `.lua` files if available.
- **Testing**: There are no automated tests. Manual verification is mandatory for all changes. Use the log files to debug issues:
  - macOS: `~/Library/Rime/rime.log` (or check console output during deploy).

## 2. Code Style Guidelines

### YAML (Schemas & Dictionaries)
- **Indentation**: **2 spaces** exactly. YAML is whitespace-sensitive.
- **Naming**: Use `snake_case` for keys (e.g., `schema_list`, `key_binder`).
- **Structure**:
  - `*.schema.yaml`: Defines the input engine, segmentors, translators, and filters.
  - `*.dict.yaml`: Contains the vocabulary and lookup tables.
  - `*.custom.yaml`: Used to patch global or schema-specific settings (e.g., `default.custom.yaml`, `bo_mixin4.custom.yaml`).
- **Comments**: Use `#` for documentation. Large blocks of schemas often use comments for organization (e.g., `######## 洋蔥注音 ########`).

### Lua (rime.lua & lua/*)
- **Indentation**: **2 spaces**.
- **Naming**: 
  - File names: `snake_case` (e.g., `filter_charset_cjk.lua`).
  - Functions: `snake_case` for Rime-facing functions (e.g., `charset_cjk_filter`).
- **Modularity**: 
  - The entry point is `rime.lua`. It loads modules from the `lua/` directory.
  - Follow the `require` pattern established in `rime.lua`:
    ```lua
    local module = require("module_name")
    exported_function = module.exported_function
    ```
- **Error Handling**: Use `pcall` or check for `nil` if interacting with external resources or complex Rime APIs, although most logic here is performance-critical and should be robust.
- **Comments**: Use `---` for function/module headers and `--` for inline comments.

## 3. Project Architecture

### Onion Mixin System
The core of this repo is the `bo_mixin` series (1-4). These schemas are "Mixins" that combine:
- **Bopomo**: Primary input.
- **Easy English**: Triggered via prefix `3`.
- **Japanese**: Triggered via prefix `4`.
- **Cyrillic/Greek**: Triggered via prefixes `6`/`7`.

### Lua Extensions
Lua is used extensively for:
- **Filters**: Character set filtering (CJK extensions), candidate reordering.
- **Translators**: Dynamic content like dates, calculations, and specialized phrase lookups.
- **Processors**: Key binding overrides and mode switching logic.

### OpenCC
Located in `opencc/`, used for:
- Simplified/Traditional Chinese conversion.
- Symbol and Emoji mappings.

## 4. Agent Best Practices
- **Mandatory Version Reminder**: Whenever the user updates the Squirrel version or setting files, you **MUST** remind them to provide the specific version/date for both. 
  - *Example*: "I see you're updating the settings. Please remember to note the versions (e.g., Squirrel v1.1.2, Onion settings updated on 2026-01-25)."
- **Atomic Changes**: Modify one schema or dictionary at a time.
- **Sync Dependencies**: When adding a new Lua filter, update BOTH the implementation in `lua/` and the registration in `rime.lua`.
- **Include Patterns**: Use `__include` in YAML to keep schemas modular.
- **Dictionary Updates**: After adding words to a `.dict.yaml`, ensure it's imported by a schema's dictionary (usually `bo_mixin.extended.dict.yaml`) and trigger a Deploy.
- **No Type Suppression**: If using a Lua environment with types, do not use `@ts-ignore` or equivalent; ensure Rime Lua API calls match the expected signature.
