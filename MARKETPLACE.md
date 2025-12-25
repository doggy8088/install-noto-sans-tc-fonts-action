# GitHub Marketplace 發佈指南

本文件說明如何將 GitHub Actions 發佈到 GitHub Marketplace 的必要步驟與最佳實務建議。

## 必要步驟

### 1. 準備 `action.yml` 檔案

確保 `action.yml` 包含以下必要欄位：

- **name**: Action 的名稱（必須唯一）
- **description**: 簡短描述 Action 的功能
- **author**: 作者名稱
- **branding**: 品牌設定（可選但強烈建議）
  - **icon**: 圖示名稱（僅能使用 [Feather Icons](https://feathericons.com/) 提供的圖示）
  - **color**: 顏色主題（white, yellow, blue, green, orange, red, purple, gray-dark）

範例：
```yaml
name: 'Install Noto Sans TC fonts'
description: 'Install Noto Sans Traditional Chinese fonts'
author: doggy8088
branding:
  icon: type
  color: orange
```

### 2. 建立 Release

1. 在 GitHub 儲存庫中建立新的 Release
2. 勾選 "Publish this Action to the GitHub Marketplace" 選項
3. 選擇適當的版本標籤（建議使用語意化版本，如 `v1.0.0`）
4. 填寫 Release 說明

### 3. 分類選擇

發佈時需選擇適當的分類，幫助使用者找到你的 Action：

- Continuous integration
- Deployment
- Code review
- Monitoring
- Project management
- Testing
- Utilities
- 等等

## 最佳實務建議

### README.md 文件

- 提供清晰的使用範例
- 說明所有輸入參數
- 列出輸出結果（如有）
- 包含完整的工作流程範例

### 版本管理

- 使用語意化版本（Semantic Versioning）
- 提供主要版本的移動標籤（如 `v1`, `v2`）
- 在 Release Notes 中詳細說明變更內容

### 安全性

- 避免在程式碼中硬編碼敏感資訊
- 使用 GitHub Secrets 處理機密資料
- 定期更新依賴套件

### 測試

- 在發佈前充分測試 Action
- 提供測試工作流程範例
- 考慮建立自動化測試

### 授權條款

- 在儲存庫中包含 `LICENSE` 檔案
- 在 README 中說明授權方式

## Branding 圖示限制

**重要**: `action.yml` 中 `branding.icon` 屬性僅能使用 [Feather Icons](https://feathericons.com/) 提供的圖示。

常用圖示範例：
- `package`: 套件相關
- `download`: 下載相關
- `type`: 文字/字型相關
- `code`: 程式碼相關
- `terminal`: 終端機相關
- `check`: 檢查/驗證相關
- `shield`: 安全相關

完整圖示清單請參考：https://feathericons.com/

## 參考資源

- [GitHub Actions 文件](https://docs.github.com/en/actions)
- [發佈 Actions 到 Marketplace](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace)
- [Feather Icons](https://feathericons.com/)
- [Metadata syntax for GitHub Actions](https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions)
