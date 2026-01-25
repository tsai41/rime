# Rime Onion Mixin Configuration (洋蔥注音 Mixin 方案)

本倉庫為 Rime 輸入法（鼠鬚管 Squirrel）的用戶設定備份，主要基於 **洋蔥 (Onion)** 方案系列進行高度自定義。

## ⚠️ 注意事項
- **環境限定**：本設定僅保證在我的 **MacBook Desktop** 環境下正常運作。
- **版本資訊**：
  - **Squirrel**: v1.1.2
  - **Onion Settings**: 2026-01-25 更新

## 🛠️ 常見配置
- **切換單行/雙行顯示**：
  - 編輯 `bo_mixin[1-4].custom.yaml`。
  - 修改 `translator/preedit_format` 項目的 `__include` 路徑：
    - **單行 (Back 樣式)**：`element_bopomo:/preedit_b_...`
    - **雙行 (Paragraph 樣式)**：`element_bopomo:/preedit_p_...`
- **Shift 鍵中英切換**：
  - 編輯 `default.custom.yaml`。
  - 在 `ascii_composer/switch_key` 下設定 `Shift_L` 或 `Shift_R`：
    - `inline_ascii`: 切換為英文，輸入內容留在預編輯區。
    - `commit_text`: 提交當前候選字並切換為英文。
    - `noop`: 停用該按鍵的單獨切換功能。
  - 修改後務必點擊 **「佈署」 (Deploy)** 生效。

## 🔗 相關連結
- [洋蔥方案原始倉庫 (Onion_Rime_Files)](https://github.com/oniondelta/Onion_Rime_Files)
- [Rime 官方文件](https://github.com/rime/home/wiki)

---
*本倉庫僅供私人備份與學習交流使用。*
