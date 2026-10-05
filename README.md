# 若葉色的四重奏　開源中文補丁（UTF-8 / BGI）

基於 BGI／Ethornell 的《若葉色のカルテット》（Wakabairono Quartet）中文補丁。  
中文標題：**若葉色的四重奏**（視窗標題：若葉色的四重奏）  
目前版本：**v3.1（Latest）**

- 繁體：BIG5
- 簡體：GBK
- 視窗標題字串為 UTF-8，寫在 `ipl._bp`

玩家下載請走 Releases，不要用 `/blob/` 頁面：  
**https://github.com/k25c2yf/BGI-WakabaironoQuartet/releases/latest**

| 版本 | 檔案 |
|---|---|
| 繁體＋簡體 | `WakabaironoQuartet_CHT_CHS_V3.1.7z` |

### 相對本版（v3.1）

1. 劇本整份重翻、重潤。說話人行維持日文，Ruby 只譯底字、讀音留日文。
2. 系統檔 `_bp` 內文字改中文。視窗標題改為 UTF-8「若葉色的四重奏」／「若叶色的四重奏」。
3. 用語固定：若葉莊、夕斗醬、夕斗先生（日和口中）、索菲婭、峰岸小姐、都小姐、愛醬、喵子、埃里杜羅涅、斯緹羅族、戶津田學園、獸耳、正妻。
4. 繁體、簡體放在同一個 7z，不要混用兩邊的腳本和圖片。

---

## 年齡分級

本作為 **18+** 成人遊戲。未滿十八歲（或未達你所在地區法定成年年齡）請勿下載、安裝或遊玩。

---

## 玩家使用方式

1. 請先自行持有正版《若葉色のカルテット》。本倉庫**不提供**原版遊戲本體。
2. 到 [Releases](https://github.com/k25c2yf/BGI-WakabaironoQuartet/releases/latest) 下載 `WakabaironoQuartet_CHT_CHS_V3.1.7z`。
3. 解壓後依包內說明安裝。繁體、簡體不要混用。
4. 防毒軟體有時會誤報自行封裝的執行檔。

---

## 自行編譯／重新打包

以下給要從原始檔重建補丁的人。一般玩家不必做這段。

### 環境

- Windows
- [Python 3](https://www.python.org/downloads/)（安裝時勾選 Add Python to PATH）
- 7-Zip 或能解 `.7z` 的工具
- [Enigma Virtual Box](https://enigmaprotector.com/en/aboutvb.html)（倉庫內有 `Enigma Virtual Box`）

下載整個倉庫（Code → Download ZIP，或 `git clone`）後，在倉庫**根目錄**操作。

先確認這些路徑存在：

| 路徑 | 用途 |
|---|---|
| `source/` | 原版腳本 |
| `big5/` | 繁中劇本 txt |
| `jp/jpname/` | 各章原日文人名表（對應 `●編號●`，見下方說明） |
| `big5pic.7z` | 繁中圖片包（需先解壓） |
| `gbkpic.7z` | 簡中圖片包（需先解壓） |
| `ui/big5/` | 繁中系統 `_bp`（含改過標題的 `ipl._bp`） |
| `ui/gbk/` | 簡中系統 `_bp` |
| `WakabaironoQuartet.exe` | Enigma 主程式 |
| `outputbig5.bat` / `outputgb.bat` | 封包腳本 |
| `繁體中文轉簡體中文.py` | 繁→簡劇本 |
| `BGIScriptRepacker-jp.py` | 把說話人行套回日文 |

### `jp/jpname`：人名必須還原成日文

`jp/jpname/` 裡的檔對應翻譯劇本裡同一條 `●數字●` 的**原日文人名**（說話人欄）。

封包時要用這些檔把該標號還原成日文。遊戲是靠**日文原名**去對人名圖片（名牌立繪字）；改成中文或其他文字後，引擎對不到圖，畫面上只會出現普通文字名牌。

因此：

- 不要把 `jp/jpname` 裡的人名改成中文。
- 中文名只寫在 `big5/`（或轉出的簡體劇本）對白與旁白。
- `outputgb.bat` 會呼叫 `BGIScriptRepacker-jp.py`，把 `./jp/jpname/` 套回編譯結果。繁中流程若也要顯示人名圖，同樣必須經過這一步，不可省略。

### 1. 解圖片壓縮包

把 `big5pic.7z` 解成**資料夾**，不要只留 7z。  
簡體同樣處理 `gbkpic.7z`。

解完後應能直接看到圖片／bin，而不是只有一個壓縮檔。

### 2. 繁體：編譯腳本

在根目錄執行：

```bat
outputbig5.bat
```

成功後會出現 `outputbig5/`（以及過程用的暫存目錄）。

### 3. 繁體：Enigma Virtual Box 打包

1. 開啟 Enigma Virtual Box。
2. **主程式 %Input File%**：選根目錄的 `WakabaironoQuartet.exe`。
3. 把下列內容加進虛擬盒（Files）：
   - `big5pic.7z` 解壓出來的**全部檔案**
   - `outputbig5/` 裡的全部檔案
   - `ui/big5/` 裡的繁中系統 `_bp`（含改過標題的 `ipl._bp`），覆蓋到遊戲讀取的位置
4. 輸出檔名可設為  
   `WakabaironoQuartet-BIG5-v3.1.exe`
5. Process / 開始封裝。

系統檔檔名要跟遊戲原本一致（例如 `ipl._bp`），不要多包一層多餘資料夾導致引擎找不到。

### 4. 簡體：轉劇本並編譯

在根目錄依序執行：

```bat
python 繁體中文轉簡體中文.py
outputgb.bat
```

- 轉換腳本讀 `./big5`，寫出簡體劇本
- `outputgb.bat` 讀簡體劇本，並用 `./jp/jpname/` 把 `●編號●` 說話人還原成日文，產出 `outputgbk/`
- 簡體視窗標題用 UTF-8「若叶色的四重奏」的 `ipl._bp`，不要和繁體那份混用

### 5. 簡體：Enigma Virtual Box 打包

1. 主程式同樣用 `WakabaironoQuartet.exe`。
2. 加入：
   - `gbkpic.7z` 解壓出來的**全部檔案**
   - `outputgbk/` 裡的全部檔案
   - `ui/gbk/` 裡的簡中系統 `_bp`
3. 輸出檔名可設為  
   `WakabaironoQuartet-GBK-v3.1.exe`

---

## v3.1 範圍（摘要）

- 劇本繁／簡中文化（`●ID●`、說話人行、Ruby、重複行）
- 系統 UI 文字
- 視窗標題 UTF-8：若葉色的四重奏／若叶色的四重奏
- 相關圖片與缺字

系統字串受引擎碼表限制時，部分用字採可編碼漢字。標題本身走 UTF-8，不走 BIG5／GBK。

---

## 注意與免責

- 遊戲著作權歸原製作公司（Lump of Sugar）及相關權利人。本專案只提供粉絲翻譯／技術適配，與官方無關。
- 補丁免費、僅供個人學習與研究。禁止販售。
- 解包、改檔、使用封裝工具的風險由使用者承擔。
- 文本含機器翻譯再修，歡迎開 Issue／PR。

---

## 倉庫說明

根目錄的 `WakabaironoQuartet.exe` 與 `WakabaironoQuartet_CHT_CHS_V3.1.7z` 僅供開發對照。正式發布以 **Releases** 為準。  
`big5`、`jp`、`source`、`ui` 與各種 `.py` 是製作材料，一般玩家不需要。`jp/jpname` 只還原日文人名以對人名圖片，勿改成中文。

---

## 回報問題

請開 Issue，並附：使用繁體或簡體、章節／對話 ID（如 `●000140●`）、截圖。
