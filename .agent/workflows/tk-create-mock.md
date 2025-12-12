---
description: Generate all mock artifacts
---

# Setup

1.  **Set `commandName`**: `create-mock`
2.  **Set `baseDir`**: `specs`
3.  **Get `specDir`**: Read the first argument passed to the slash command.
    -   If no argument is provided, display the error message: "Error: `specDir` argument is required. Usage: `/tk-create-mock <specDir>`" and **STOP** execution immediately.

# Execution

Execute the following instructions using `baseDir` and `specDir`.

## Execution Steps

### 1. Pre-check

Verify that required files exist before proceeding:

- **Target Files**:
  - `{{baseDir}}/{{specDir}}/feature.yml`
  - `{{baseDir}}/{{specDir}}/status.json`

- **Validation**:
  - If any of these files do not exist → Display the message "Error: `status.json` or `feature.yml` does not exist. Please run /tk-clean" and **STOP** execution.

### 2. Execute Commands

- 1. `/tk-generate-story {{specDir}}`
- 2. `/tk-generate-usecase {{specDir}}`
- 3. `/tk-generate-ui {{specDir}}`
- 4. `/tk-generate-mock {{specDir}}`
- 5. `/tk-generate-screenflow {{specDir}}`