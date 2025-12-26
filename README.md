# install-noto-sans-tc-fonts-action

在 GitHub Actions 的 Linux runner 上安裝 Noto Sans CJK (思源黑體) 繁體中文 (TC) 字型，避免測試、產報表或截圖時出現「中文字變方框」或字形不一致的問題。

## 適用環境

- 僅支援 Linux runner，且需要 `apt` 與 `sudo` 權限 (例如 Ubuntu / Debian 系)。
- GitHub-hosted Ubuntu runners (已於 CI 測試)：
  - `ubuntu-22.04`
  - `ubuntu-24.04`
  - `ubuntu-latest`

## 快速開始

最基本用法：

```yaml
steps:
  - uses: doggy8088/install-noto-sans-tc-fonts-action@v1
```

若想顯示步驟名稱：

```yaml
steps:
  - name: Install Noto Sans TC fonts
    uses: doggy8088/install-noto-sans-tc-fonts-action@v1
```

## 參數 (Inputs)

- `extra` (預設值：`'false'`)：是否額外安裝更多字重。`'true'` 會額外安裝 `fonts-noto-cjk-extra` (Thin/Light/Medium...)，預設僅安裝 `fonts-noto-cjk` (Regular/Bold)。

安裝額外字重範例：

```yaml
steps:
  - uses: doggy8088/install-noto-sans-tc-fonts-action@v1
    with:
      extra: 'true'
```

注意：Composite Action 的 input 目前不穩定支援布林值，建議一律用字串 `'true'` / `'false'`。只有填入字串 `'true'` 才會啟用額外字重安裝。

## 建議設定

字型安裝屬於系統套件安裝流程，建議加上 timeout 與容錯，避免偶發的套件源問題影響整體 CI：

```yaml
steps:
  - uses: doggy8088/install-noto-sans-tc-fonts-action@v1
    timeout-minutes: 10

  - name: your next step
    if: always()
```

## 驗證安裝

安裝完成後，可用 `fontconfig` 查詢字型是否存在：

```bash
fc-list | grep "Noto Sans CJK TC"
```

## 常見問題

| 問題                                  | 原因                                                             | 建議處理                                                                                                   |
| ------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| 顯示成日文漢字 (例如「復」字寫法不同) | Noto CJK 同時包含多種語系變體，應用程式或環境可能挑到 JP/KR 變體 | 在應用程式中明確指定字體 (例如使用 "Noto Sans CJK TC"／"Noto Sans TC")，或調整字型 fallback / 語系優先順序 |
| 缺少特定字重                          | `fonts-noto-cjk` 只含 Regular/Bold                               | 將 `extra` 設為 `'true'` 安裝 `fonts-noto-cjk-extra`                                                       |

## 版本策略

採用語意化版本 (SemVer)：

- 主版本分支：`v1`
- 具體版本 tag：`v1.0.0`

## 安全性建議 (Supply Chain)

若你希望避免 tag 被移動 (供應鏈風險)，可將 `uses:` 固定到特定 commit SHA (最嚴格但需要自行升級)：

```yaml
permissions:
  contents: read

steps:
  - uses: doggy8088/install-noto-sans-tc-fonts-action@<commit-sha>
```

若你只想用主版本分支 (較方便)，可繼續使用：

```yaml
permissions:
  contents: read

steps:
  - uses: doggy8088/install-noto-sans-tc-fonts-action@v1
```

## 授權

- 本專案：[MIT License](LICENSE)
- Noto Sans 字型：[SIL Open Font License 1.1](https://openfontlicense.org/open-font-license-official-text/) (OFL) (詳見 [Licensing](https://fonts.google.com/knowledge/glossary/licensing) 說明)
