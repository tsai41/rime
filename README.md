# Rime Onion Mixin Configuration (洋蔥注音 Mixin 方案)

本倉庫為 Rime 輸入法（鼠鬚管 Squirrel、小狼毫 Weasel、ibus-rime 等）的用戶設定備份，主要基於 **洋蔥 (Onion)** 方案系列進行高度自定義。

## 🌟 特色功能

本方案核心為 `bo_mixin` 系列，旨在提供一個「全能型」的輸入環境，支援多國語言與豐富的擴展功能：

- **多語言輸入**：
  - **注音 (Bopomo)**：核心輸入法，基於注音符號。
  - **Easy English**：透過前綴 `3` 觸發，支援自動補全與大小寫轉換。
  - **日語 (Japanese)**：透過前綴 `4` 觸發，支援假名轉換。
  - **韓語 (Korean)**：透過前綴 `5` (依具體配置) 或特定模式觸發。
  - **斯拉夫語 (Cyrillic)**：透過前綴 `6` 觸發。
  - **希臘語 (Greek)**：透過前綴 `7` 觸發。
- **Lua 強力擴展**：
  - 動態翻譯：支援日期、時間、計算機、萬年曆等。
  - 進階濾鏡：包含 CJK 字符集過濾、候選項重排序、自動註釋等。
  - 按鍵處理：最佳化空白鍵行為、標點符號切換等。
- **豐富符號庫**：整合 OpenCC 實現 Emoji 提示、各類特殊符號映射。
- **跨平台支援**：主要在 macOS (Squirrel) 上測試，亦相容於其他 Rime 平台。

## 📂 目錄結構

- `*.schema.yaml`: 輸入方案定義文件。
- `*.dict.yaml`: 詞庫與字典文件。
- `rime.lua`: Lua 擴展的入口與註冊點。
- `lua/`: 存放各個獨立的 Lua 模組。
- `opencc/`: 存放字體轉換、Emoji 與符號映射配置。
- `default.custom.yaml`: 全域設定（方案列表、快捷鍵等）。

## 🚀 安裝與使用

1. **備份舊設定**：在安裝前，建議先備份您現有的 Rime 用戶資料夾。
2. **複製檔案**：將本倉庫的所有內容複製到您的 Rime 用戶資料夾中：
   - macOS: `~/Library/Rime`
   - Windows: `%APPDATA%\Rime`
   - Linux: `~/.config/ibus/rime`
3. **佈署 (Deploy)**：
   - 點擊 Rime 圖示，選擇 **「佈署」 (Deploy)**。
   - 等待佈署完成（通常需要幾秒鐘）。
4. **切換方案**：使用 `Control + ` ` (Backtick) 或 `F4` 開啟方案選單，選擇 `bo_mixin1` ~ `bo_mixin4` 即可開始使用。

## 🛠️ 開發與自定義

- **修改 Lua 功能**：編輯 `lua/` 下的對應檔案，並在 `rime.lua` 中確認掛載。
- **新增詞彙**：修改對應的 `.dict.yaml` 文件（如 `bo_mixin.extended.dict.yaml`），然後重新佈署。
- **調整快捷鍵**：修改 `default.custom.yaml` 中的 `key_binder/bindings` 部分。

## 🔗 相關連結

- [洋蔥方案原始倉庫 (Onion_Rime_Files)](https://github.com/oniondelta/Onion_Rime_Files)
- [Rime 官方文件](https://github.com/rime/home/wiki)

---
*本倉庫僅供私人備份與學習交流使用。*
