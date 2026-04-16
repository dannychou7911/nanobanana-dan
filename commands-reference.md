# Nano Banana 指令參數參考

本文件整理 Nano Banana Gemini CLI extension 所有 slash command 的參數細節，讓使用者能快速查詢每個指令可輸入的項目。

---

## `/generate` 指令參數

**用途**：從文字提示生成單張或多張圖像，支援風格與變化控制。

**對應 MCP Tool**：`generate_image`

**必填**：
- `prompt`（引號字串） — 圖像描述，例如 `"a watercolor painting of a fox"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--count=N` | 1-8 | 1 | 生成張數 |
| `--styles="a,b"` | 逗號清單 | 無 | `photorealistic`, `watercolor`, `oil-painting`, `sketch`, `pixel-art`, `anime`, `vintage`, `modern`, `abstract`, `minimalist` |
| `--variations="a,b"` | 逗號清單 | 無 | `lighting`, `angle`, `color-palette`, `composition`, `mood`, `season`, `time-of-day` |
| `--format=` | 選項 | `separate` | `grid` 或 `separate` |
| `--seed=123` | 整數 | 無 | 可重現種子 |
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**範例**：
```
/generate "sunset over mountains" --count=3 --preview
/generate "friendly robot" --styles="anime,minimalist" --variations="color-palette"
/generate "mountain landscape" --styles="watercolor,oil-painting" --count=4 --format=grid
```

---

## `/icon` 指令參數

**用途**：生成 App icon、favicon、UI 元素，支援多尺寸與格式。

**對應 MCP Tool**：`generate_icon`

**必填**：
- `prompt`（引號字串） — 圖標描述，例如 `"coffee cup logo"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--sizes="16,32,64"` | 逗號清單 | 無 | `16`, `32`, `64`, `128`, `256`, `512`, `1024` |
| `--type=` | 選項 | `app-icon` | `app-icon`, `favicon`, `ui-element` |
| `--style=` | 選項 | `modern` | `flat`, `skeuomorphic`, `minimal`, `modern` |
| `--format=` | 選項 | `png` | `png`, `jpeg` |
| `--background=` | 字串 | `transparent` | `transparent`, `white`, `black` 或任何色彩名稱 |
| `--corners=` | 選項 | `rounded` | `rounded`, `sharp`（僅 app-icon 適用） |
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**範例**：
```
/icon "coffee cup logo" --sizes="64,128,256" --type="app-icon" --preview
/icon "company logo" --type="favicon" --sizes="16,32,64"
/icon "settings gear icon" --type="ui-element" --style="minimal"
/icon "productivity app with checklist" --sizes="64,128,256,512" --corners="rounded"
```

---

## `/pattern` 指令參數

**用途**：生成無縫重複圖案與紋理，適合背景、設計素材使用。

**對應 MCP Tool**：`generate_pattern`

**必填**：
- `prompt`（引號字串） — 圖案描述，例如 `"subtle geometric hexagons"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--size="WxH"` | 字串 | `256x256` | 例如 `128x128`, `256x256`, `512x512` |
| `--type=` | 選項 | `seamless` | `seamless`, `texture`, `wallpaper` |
| `--style=` | 選項 | `abstract` | `geometric`, `organic`, `abstract`, `floral`, `tech` |
| `--density=` | 選項 | `medium` | `sparse`, `medium`, `dense` |
| `--colors=` | 選項 | `colorful` | `mono`, `duotone`, `colorful` |
| `--repeat=` | 選項 | `tile` | `tile`, `mirror` |
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**範例**：
```
/pattern "subtle geometric hexagons" --type="seamless" --colors="duotone" --density="sparse"
/pattern "brushed metal surface" --type="texture" --style="tech" --colors="mono"
/pattern "floral design" --type="wallpaper" --density="sparse"
/pattern "geometric triangles" --type="seamless" --style="geometric" --preview
```

---

## `/story` 指令參數

**用途**：生成一連串相關圖像，用於說故事或逐步呈現流程。

**對應 MCP Tool**：`generate_story`

**必填**：
- `prompt`（引號字串） — 故事或流程描述，例如 `"a seed growing into a tree"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--steps=N` | 2-8 | `4` | 連續圖像數量 |
| `--type=` | 選項 | `story` | `story`, `process`, `tutorial`, `timeline` |
| `--style=` | 選項 | `consistent` | `consistent`, `evolving` |
| `--layout=` | 選項 | `separate` | `separate`, `grid`, `comic` |
| `--transition=` | 選項 | `smooth` | `smooth`, `dramatic`, `fade` |
| `--format=` | 選項 | `individual` | `storyboard`, `individual` |
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**範例**：
```
/story "a seed growing into a tree" --steps=4 --type="process" --preview
/story "idea to launched product" --steps=5 --type="process" --style="consistent"
/story "git workflow tutorial" --steps=6 --type="tutorial" --layout="comic"
/story "company logo evolution" --steps=4 --type="timeline" --transition="smooth"
```

---

## `/diagram` 指令參數

**用途**：從文字描述生成技術圖表、流程圖、架構圖。

**對應 MCP Tool**：`generate_diagram`

**必填**：
- `prompt`（引號字串） — 圖表內容與結構描述，例如 `"user login process"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--type=` | 選項 | `flowchart` | `flowchart`, `architecture`, `network`, `database`, `wireframe`, `mindmap`, `sequence` |
| `--style=` | 選項 | `professional` | `professional`, `clean`, `hand-drawn`, `technical` |
| `--layout=` | 選項 | `hierarchical` | `horizontal`, `vertical`, `hierarchical`, `circular` |
| `--complexity=` | 選項 | `detailed` | `simple`, `detailed`, `comprehensive` |
| `--colors=` | 選項 | `accent` | `mono`, `accent`, `categorical` |
| `--annotations=` | 選項 | `detailed` | `minimal`, `detailed` |
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**範例**：
```
/diagram "user login process" --type="flowchart" --style="professional" --preview
/diagram "CI/CD pipeline with testing stages" --type="flowchart" --complexity="detailed"
/diagram "chat application architecture" --type="architecture" --style="technical"
/diagram "REST API authentication flow" --type="sequence" --layout="vertical"
/diagram "social media database schema" --type="database" --annotations="detailed"
```

---

## `/edit` 指令參數

**用途**：依文字指示編輯既有圖像。

**對應 MCP Tool**：`edit_image`

**必填**：
- `filename`（第一個參數） — 輸入圖像檔名，例如 `my_photo.png`
- `prompt`（引號字串） — 編輯指示，例如 `"add sunglasses to the person"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**使用格式**：`/edit filename "edit instructions" [--preview]`

**範例**：
```
/edit my_photo.png "add sunglasses to the person"
/edit portrait.jpg "change background to a beach scene" --preview
```

---

## `/restore` 指令參數

**用途**：修復或增強既有圖像（例如去除刮痕、補色、提升清晰度）。

**對應 MCP Tool**：`restore_image`

**必填**：
- `filename`（第一個參數） — 輸入圖像檔名，例如 `old_family_photo.jpg`
- `prompt`（引號字串） — 修復指示，例如 `"remove scratches and improve clarity"`

**選填參數**：

| 選項 | 類型 | 預設 | 可選值 |
|---|---|---|---|
| `--preview` | 旗標 | 無 | 自動開啟預覽 |

**使用格式**：`/restore filename "restoration instructions" [--preview]`

**範例**：
```
/restore old_family_photo.jpg "remove scratches and improve clarity"
/restore damaged_photo.png "enhance colors and fix tears" --preview
```

---

## `/nanobanana` 指令參數

**用途**：以自然語言描述需求，由模型自動判讀並路由到最適合的 MCP tool。不需要手動指定旗標。

**對應 MCP Tool**：依語意自動選擇
- `generate_image` — 單張／多張圖像生成
- `edit_image` — 圖像編輯
- `restore_image` — 圖像修復
- `generate_icon` — 圖標
- `generate_pattern` — 圖案紋理
- `generate_story` — 故事序列
- `generate_diagram` — 技術圖表

**必填**：
- 自然語言描述（整段句子）

**選填參數**：
- 無固定旗標；所有調整透過自然語言表達（例如「請生成 5 張」、「請以水彩風格」）。

**範例**：
```
/nanobanana create a logo for my tech startup
/nanobanana I need 5 different versions of a cat illustration in various art styles
/nanobanana fix the lighting in sunset.jpg and make it more vibrant
```

---

## 共通說明

- **輸出目錄**：所有生成的圖像儲存於 `./nanobanana-output/`。
- **通用旗標**：幾乎所有指令都支援 `--preview`（產圖後自動開啟預設圖檢視器）。
- **API 金鑰**：透過環境變數設定，優先順序為 `NANOBANANA_API_KEY` → `NANOBANANA_GEMINI_API_KEY` → `NANOBANANA_GOOGLE_API_KEY` → `GEMINI_API_KEY` → `GOOGLE_API_KEY`。
- **模型覆寫**：可用環境變數 `NANOBANANA_MODEL` 覆寫預設的 `gemini-3.1-flash-image-preview`。
