# Setup

Read the following files to understand the RDRA structure:
- `1_RDRA/BUC.tsv`
- `1_RDRA/関連データ.txt`
- `2_RDRASpec/論理データモデル.md`
- `1_RDRA/アクター.tsv`
- `1_RDRA/条件.tsv`
- `2_RDRASpec/business_rule.md`
- `1_RDRA/バリエーション.tsv`
- `1_RDRA/状態.tsv`

# Execution

## Mission

Create user stories and feature-based directory structure from RDRA data.

## Execution Steps

### Step 1: Extract information from BUC.tsv

Read `1_RDRA/BUC.tsv` and extract data with the following filter conditions:
- Filter conditions:
  - Column 6: Strings other than "ユースケース"
  - Column 7: "画面" or "情報"
- Data extraction:
  - When Column 7 is "画面": Verify that Column 9 is "アクター", then extract Column 10 as the actor for the use case in Column 6
  - When Column 7 is "情報": Extract Column 12 as the "目的" (purpose)

### Step 2: Create user stories

Based on the extracted information, create user stories in the following format:
- Format: "{{アクター}}として、{{目的}}がしたい。なぜならば、{{背景}}だからだ。"

### Step 3: Output user stories in TSV format

Create a TSV file with the following columns:
- Column 1: 業務 (Business)
- Column 2: BUC
- Column 3: アクティビティ (Activity)
- Column 4: アクター (Actor)
- Column 5: 画面 (Screen)
- Column 6: ユーザーストーリー (User Story - refine Japanese expressions if needed)
- Filename: `ユーザーストーリー.tsv`

### Step 4: Load the created user stories file

Read the `ユーザーストーリー.tsv` file created in Step 3.

### Step 5: Extract unique business names

Create a unique list from Column 1 "業務" (Business) by removing duplicates.

### Step 6: Convert business names to feature names

Convert each business name to {{FeatureName}} to create a feature list:
- Conversion rules:
  - Naming convention: UpperPascalCase
  - Must not duplicate with other names
  - Use appropriate and concise names

### Step 7: Determine data creation order

Read `1_RDRA/関連データ.txt` and `2_RDRASpec/論理データモデル.md` to understand the data creation order.

### Step 8: Update feature list order

Update the feature list order to correspond with the data creation order.

### Step 9: Create commands.md file

Create a `commands.md` file and output the feature list as a command list:
- Output format:
  - `- [ ] mkdir -p specs/{{creation_order(integer)}}_{{FeatureName}}`

### Step 10: Read command list

Read the command list from the `commands.md` file created in Step 9.

### Step 11: Get next pending command

Retrieve one command that has not yet been completed from the TODO list.

### Step 12: Check specs directory existence

Check if the `specs` directory exists under the pms-RDRA directory.

### Step 13: Create feature directories

If the `specs` directory does not exist under the pms-RDRA directory, execute the retrieved command to create a directory for each feature.

### Step 14: Create README.md for each feature

If `README.md` does not exist under `specs/{{creation_order(integer)}}_{{FeatureName}}`, create it:
- Based on `1_RDRA` and `2_RDRA` content, filter `1_RDRA/BUC.tsv` by {{FeatureName}} and write the following sections:
  - # 機能名（業務単位）(Feature Name - Business Unit)
  - ## 背景 (Background)
  - ## 目的 (Purpose)
    - Summarize the purpose from `1_RDRA/BUC.tsv` and business overview
  - ## 主要アクター (Main Actors)
    - Extract from `1_RDRA/BUC.tsv`
  - ## 業務概要 (Business Overview)
    - Summarize business overview from `1_RDRA/BUC.tsv`
  - ## 要求 (Requirements)
    - Extract from `1_RDRA/アクター.tsv`
  - ## 機能 (Functions)
    - Extract from `1_RDRA/BUC.tsv`
  - ## ビジネスルール (Business Rules)
    - Extract from `1_RDRA/条件.tsv`, `2_RDRASpec/business_rule.md`
  - ## ビジネスパラメーター (Business Parameters)
    - Extract from `1_RDRA/バリエーション.tsv`, `1_RDRA/状態.tsv`

### Step 15: Mark command as completed

Mark the executed command as completed.

### Step 16: Repeat until all commands are completed

Repeat Steps 11-15 until all commands in the command list are completed.

## Execution Example

### Output Example

```tsv
業務	BUC	アクティビティ	アクター	画面	ユーザーストーリー
顧客管理	顧客登録	新規顧客入力	営業担当者	顧客登録画面	営業担当者として、新規顧客情報を登録したい。なぜならば、顧客情報を一元管理したいからだ。
```

### Output Format

Commands will be generated in the following format:
```markdown
- [ ] mkdir -p specs/1_CustomerManagement
- [ ] mkdir -p specs/2_OrderProcessing
```
