<div align="center">
  <img src="icon.svg" width="96" alt="DocCam icon">

  # DocCam — Document Camera

  **A simple document camera app — runs entirely in your browser.**

  [**▶ Live demo**](https://akichika.github.io/doc-cam/) · [日本語](#日本語)

</div>

---

DocCam turns any webcam (or a screen share) into a presentation document camera. Zoom in on a page, freeze a frame, point with a laser, dim everything but a spotlight, drop a ruler or grid on top, and grab a screenshot — all without installing anything and without sending a single frame to a server.

Everything happens locally in the browser using the `getUserMedia` / `getDisplayMedia` APIs. No backend, no build step — it's a single static `index.html`.

<img width="2330" height="1450" alt="スクリーンショット 2026-06-16 232019" src="https://github.com/user-attachments/assets/a04bf900-4681-4cf4-8c6f-759bb589fcf9" />

## Features

- 🎥 **Camera & screen share** — pick any connected camera from a dropdown, or share a screen/window. A checkbox next to each source toggles show/hide instantly without disconnecting the stream.
- 📷 **Dual camera** — when 2 or more cameras are connected, a second camera dropdown appears automatically. Each camera remembers its own zoom, pan, and keystone state for the session.
- 🔦 **Flashlight** — on mobile devices with a rear camera, a torch button appears next to the camera when the hardware supports it (`MediaTrackCapabilities.torch`).
- 🪟 **Dual view** — show two sources side-by-side (left/right or top/bottom) with a draggable divider, or choose:
  - **Corner PiP** — small overlay window with 8-point position anchor grid, adjustable opacity, drag to reposition, resize handle
  - **Semi-transparent overlay** — one source layered over the other at adjustable opacity
  - One-tap source swap at any time
- 🔍 **Zoom & pan** — slider with ◀▶ step buttons, presets, **fit-width / fit-height**, double-tap / `0` to reset. Pan works in all modes including keystone correction.
- ⏸️ **Freeze & screenshot** — pause the live image and save a clean PNG.
- 🔄 **Rotate / mirror / keystone** — 90° clockwise rotation, horizontal flip, and projector-style trapezoid correction (vertical / horizontal / angle).
- 🔴 **Laser pointer** — 8 colors, 4 sizes, glowing fade-out trail; cursor preview dot visible even without clicking.
- 🖌️ **Highlighter pen** — persistent semi-transparent strokes in 6 colors, 3 widths, adjustable opacity; re-toggling clears all strokes.
- 🔦 **Spotlight** — circle / ellipse / square / rectangle, adjustable size, darkness and softness.
- 📏 **Ruler** — pseudo-infinite ruler with solid / translucent / ticks-only styles, adjustable scale & angle, optional cross ruler with angle arc, draggable.
- ▦ **Grid** — halves, quarters, 3×3, 4×4, or a custom square grid (adjustable cell size); re-toggling restores the last-used type.
- 🎚️ **Image adjust** — brightness, contrast, saturation, white balance, and one-click **auto** tuned for document cameras.
- 💾 **Save settings** — save all current settings to `localStorage` with the Save button; restored automatically on next load. Reset from the Settings panel.
- 🌗 **High-contrast mode** for accessibility.
- 🌐 **9 languages** (EN / 日本語 / 中文 / 한국어 / ES / FR / DE / PT / AR), auto-detected from the browser.
- 📲 **Installable PWA** — install from Chrome or Edge on desktop/Android; on iPhone tap **Share → Add to Home Screen** in Safari (iOS 16.4+).
- ⌨️ **Keyboard shortcuts** and tooltips throughout, with an auto-hiding UI.

## Install as an app (PWA)

DocCam can be installed as a standalone app on any platform — no app store required.

### iPhone / iPad (iOS 16.4+)
1. Open [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) in **Safari**.
2. Tap the **Share** button (rectangle with arrow) at the bottom of the screen.
3. Tap **Add to Home Screen**.
4. Tap **Add** — the app icon appears on your home screen.

> Safari only. Chrome and other browsers on iOS cannot install PWAs.

### Android
1. Open [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) in **Chrome**.
2. Tap the **⋮ menu** (top right) → **Add to Home screen** (or an install banner may appear automatically).
3. Tap **Install** — the app icon appears on your home screen and in the app drawer.

### Windows / Mac / Linux (desktop)
1. Open [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) in **Chrome** or **Edge**.
2. Click the **install icon** (⊕) in the address bar (right side), or open the browser menu → **Install DocCam**.
3. Click **Install** — the app opens in its own window and a shortcut is added to your taskbar / dock.

> Firefox does not support PWA installation.

## Mobile limitations

| Feature | iOS Safari | Android Chrome |
| --- | --- | --- |
| Camera | ✅ | ✅ |
| Front + rear camera simultaneously | ❌ Not supported | ❌ Not supported |
| Screen share | ❌ Not supported | ✅ |
| Flashlight | ✅ (if hardware supports it) | ✅ (if hardware supports it) |
| PWA install | ✅ Safari → Share → Add to Home Screen | ✅ Chrome → Install |

## Keyboard shortcuts

| Key | Action | Key | Action |
| --- | --- | --- | --- |
| `Space` / `K` | Freeze | `L` | Laser pointer |
| `C` | Screenshot | `H` | Spotlight |
| `M` | Mirror | `U` | Ruler |
| `R` | Rotate | `G` | Grid |
| `T` | Keystone | `Y` | Highlighter pen |
| `Z` | Zoom panel | `Q` | Image adjust |
| `0` | Reset zoom | `V` | Layout |
| `+` / `-` | Zoom in / out | `X` | Swap sources |
| `F` | Fullscreen | `S` | Screen share |
| `P` | Picture-in-Picture | `Esc` | Exit tool / close panel |

## Usage

1. Open the [live demo](https://akichika.github.io/doc-cam/) (or run it locally — see below).
2. Click **Start** (the DocCam icon at top-left), then allow camera access.
3. Use the **top bar** to select cameras, toggle screen share, and switch layout.
4. Use the **bottom toolbar** for zoom, freeze, rotate, tools, and settings.
5. Press **V** or the layout button to open the layout panel (appears just below the top bar).
6. Click **Save** to persist your current settings across reloads.

> A secure context (`https://` or `localhost`) is required for camera access. GitHub Pages serves over HTTPS, so the live demo works out of the box.

## Run locally

It's a static site — any HTTP server works:

```bash
# from the project folder
npx serve -l 3000 .
# then open http://localhost:3000
```

## Privacy

DocCam has no server component. Camera and screen frames stay in your browser and are never uploaded. Screenshots are saved directly to your device via a normal browser download.

## Tech

- Single-file vanilla HTML / CSS / JavaScript — no framework, no build step.
- HTML5 Canvas for laser, highlighter, spotlight, ruler and grid overlays.
- CSS transforms for zoom / pan / rotate / keystone; SVG `feColorMatrix` for white balance.
- `getUserMedia` / `getDisplayMedia` for camera and screen capture.
- `MediaTrackCapabilities.torch` for flashlight support detection.
- `localStorage` for optional settings persistence.
- A minimal service worker + web manifest make it an installable PWA.

## License

[MIT](LICENSE) © akichika

---

<a name="日本語"></a>

## 日本語

**内蔵カメラやWebカメラを書画カメラとして使えるアプリです。インストール不要、ブラウザだけで完結します。**

[**▶ デモを開く**](https://akichika.github.io/doc-cam/)

ズーム・静止・スクリーンショット保存に加え、レーザーポインター／蛍光ペン／スポットライト／ルーラー／グリッド／台形補正／画質調整などをブラウザ内だけで実行します。映像はサーバーに送信されず、すべて手元で処理されます（バックエンド無し・ビルド不要の単一 `index.html`）。

<img width="2330" height="1450" alt="スクリーンショット 2026-06-16 232019" src="https://github.com/user-attachments/assets/a04bf900-4681-4cf4-8c6f-759bb589fcf9" />

### 主な機能

- 🎥 **カメラ選択・画面共有** — プルダウンでカメラを選択、または画面共有を開始。各ソースのチェックボックスで接続を維持したまま映像の表示／非表示を即切り替え可能
- 📷 **デュアルカメラ** — 2台以上のカメラが接続されると、カメラ2のプルダウンが自動表示。ズーム・パン・台形補正などカメラごとに状態を維持
- 🔦 **フラッシュライト** — スマホ・タブレット等の背面カメラ搭載機種でライトボタンが自動表示（`MediaTrackCapabilities.torch` 対応機のみ）
- 🪟 **デュアルビュー** — 2ソースを左右／上下分割（境界線ドラッグ可）で表示、または：
  - **コーナーPiP** — 8方向アンカーで配置、透明度調整、ドラッグ移動、ハンドルでリサイズ
  - **半透明重畳** — 片方を透かして重ねる（透明度調整可）
  - いつでもワンタップでソース入替
- 🔍 **ズーム／パン** — スライダー（◀▶ステップボタン付き）・プリセット・縦/横フィット・リセット。台形補正中もパン可能
- ⏸️ **静止・スクリーンショット** — 映像を一時停止してPNG保存
- 🔄 **90°回転・左右反転・台形補正**（上下／左右／角度）
- 🔴 **レーザーポインター** — 8色・4サイズ・発光トレイル、クリック前もカーソルプレビュー表示
- 🖌️ **蛍光ペン** — 6色・3サイズ・透明度調整。再タップで全消去
- 🔦 **スポットライト** — 円/楕円/正方形/長方形・サイズ・暗さ・ぼかし
- 📏 **ルーラー** — 擬似無限長・3スタイル・目盛り/角度・十字定規・ドラッグ移動
- ▦ **グリッド** — 2/4/9/16分割・カスタムマス目サイズ・最後に使ったグリッドをトグルで復元
- 🎚️ **画質調整** — 明るさ・コントラスト・彩度・ホワイトバランス・書画カメラ向け自動調整
- 💾 **設定保存** — 保存ボタンで全設定をローカルストレージに保存、次回起動時に自動復元
- 🌗 **ハイコントラストモード**
- 🌐 **9言語対応**（EN / 日本語 / 中文 / 한국어 / ES / FR / DE / PT / AR）自動判定
- 📲 **PWA対応** — Chrome・Edgeからインストール可能（iPhoneはSafariで「ホーム画面に追加」）

### アプリとしてインストール（PWA）

アプリストア不要で、どのプラットフォームにもスタンドアロンアプリとしてインストールできます。

#### iPhone / iPad（iOS 16.4以降）
1. **Safari** で [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) を開く。
2. 画面下部の**共有ボタン**（四角＋矢印）をタップ。
3. **「ホーム画面に追加」** をタップ。
4. **「追加」** をタップ — ホーム画面にアイコンが追加されます。

> SafariのみPWAインストールに対応しています。iOS版ChromeなどではPWAインストールできません。

#### Android
1. **Chrome** で [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) を開く。
2. 右上の **⋮ メニュー** → **「ホーム画面に追加」**（または画面下部にインストールバナーが自動表示される場合あり）をタップ。
3. **「インストール」** をタップ — ホーム画面とアプリ一覧にアイコンが追加されます。

#### Windows / Mac / Linux（デスクトップ）
1. **Chrome** または **Edge** で [https://akichika.github.io/doc-cam/](https://akichika.github.io/doc-cam/) を開く。
2. アドレスバー右端の**インストールアイコン（⊕）**をクリック、またはブラウザメニュー → **「DocCam をインストール」** をクリック。
3. **「インストール」** をクリック — 専用ウィンドウで起動し、タスクバー／Dockにショートカットが追加されます。

> FirefoxはPWAインストールに対応していません。

### モバイルの制限事項

| 機能 | iOS Safari | Android Chrome |
| --- | --- | --- |
| カメラ使用 | ✅ | ✅ |
| フロント・背面カメラの同時使用 | ❌ 不可 | ❌ 不可 |
| 画面共有 | ❌ 非対応 | ✅ |
| フラッシュライト | ✅（対応機のみ） | ✅（対応機のみ） |
| PWAインストール | ✅ Safari「ホーム画面に追加」 | ✅ Chrome「インストール」 |

### キーボードショートカット

| キー | 機能 | キー | 機能 |
| --- | --- | --- | --- |
| `Space` / `K` | 静止 | `L` | レーザーポインター |
| `C` | スクリーンショット | `H` | スポットライト |
| `M` | 左右反転 | `U` | ルーラー |
| `R` | 回転 | `G` | グリッド |
| `T` | 台形補正 | `Y` | 蛍光ペン |
| `Z` | ズームパネル | `Q` | 画質調整 |
| `0` | ズームリセット | `V` | レイアウト |
| `+` / `-` | ズームイン/アウト | `X` | ソース入替 |
| `F` | 全画面 | `S` | 画面共有 |
| `P` | ピクチャーインピクチャー | `Esc` | ツール終了/パネルを閉じる |

### 使い方

1. [デモ](https://akichika.github.io/doc-cam/) を開く（またはローカル起動）。
2. 左上の**DocCamアイコン**をクリックしてカメラを許可。
3. **トップバー**でカメラ選択、画面共有の開始、レイアウト切り替えを操作。
4. **下部ツールバー**でズーム・静止・回転・各ツール・設定を操作。
5. **V キー**またはレイアウトボタンでレイアウトパネルを開く（トップバー直下に表示）。
6. 右上の**保存**ボタンで設定をブラウザに保存（次回起動時に自動復元）。

> カメラ利用には安全なコンテキスト（`https://` または `localhost`）が必要です。GitHub Pages はHTTPS配信のためそのまま動作します。

### ライセンス

[MIT](LICENSE) © akichika
