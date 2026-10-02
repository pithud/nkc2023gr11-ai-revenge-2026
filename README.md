# nkc2023gr11-ai-revenge-2026

2022年の卒業研究で制作された面接練習および出席管理Webアプリケーション「nkc2023gr11」を、クライアントサイドWeb技術で再構成したリポジトリ。

## 概要

当時のDjangoアプリケーションにおける画面構成および画面遷移をハッシュルーティング（`#/`）で再現し、静的ホスティング環境で動作する構成としている。

## 画面一覧と実装内容

| 画面名 / 当時パス | ハッシュルート | 主な機能・実装 |
| :--- | :--- | :--- |
| ホーム / `/` | `#/` | ナビゲーションメニュー、各種機能へのリンク |
| 面接練習 / `/mensetu/<id>` | `#/mensetu/:id` | 質問文表示、Web Speech APIによる音声読み上げ、音声認識による回答入力 |
| 出席管理 / `/attend` | `#/attend` | 学籍番号別の出席データ一覧、平均・標準偏差に基づく偏差値算出、Chart.jsによるグラフ表示 |
| 回答一覧 / `/feedback` | `#/feedback` | 登録済み回答の閲覧 |
| フィードバック / `/feedback_let/<id>` | `#/feedback_let/:id` | 回答に対するフィードバック投稿および閲覧 |
| 未評価一覧 / `/feedback_yet` | `#/feedback_yet` | フィードバック未入力の質問一覧 |
| 質問投稿 / `/question` | `#/question` | 質問登録フォーム |
| 質問一覧 / `/question_List` | `#/question_List` | カテゴリ別質問一覧 |
| 質問管理 / `/hensyu` | `#/hensyu` | 質問の編集・削除 |
| 質問編集 / `/update/<id>` | `#/update/:id` | 質問内容の更新 |
| 一括入力 / `/allinput` | `#/allinput` | 複数項目の一括入力フォーム |
| CSV管理 / `/csvDLUP` | `#/csvDLUP` | 質問データのCSVエクスポートおよびインポート |
| PDFテキスト抽出 / `/pdf_read` | `#/pdf_read` | PDF.jsを用いたブラウザ内テキスト抽出 |
| プロフィール / `/profile` | `#/profile` | ユーザー情報表示・編集 |
| ユーザー管理画面 / `/mail` | `#/mail` | 投稿・回答・リクエストの管理 |
| 認証 / `/login`, `/signup` | `#/login`, `#/signup` | 簡易ログインおよびアカウント切り替え |

## データ仕様

- 出席データは学籍番号（19CT001〜19CT059）のみを扱い、個人名は含まない構成。
- 偏差値計算式: `(出席数値 - 平均) / 標準偏差 * 10 + 50`。
- データ保存先: ブラウザのLocalStorage。

## 技術スタック対比

| 項目 | 2022年版 | 2026年版 |
| :--- | :--- | :--- |
| 構成 | Django, Gunicorn, Nginx, PostgreSQL | 静的HTML/CSS/JavaScript（GitHub Pages） |
| 音声合成（TTS） | Azure Speech SDK | Web Speech API（`speechSynthesis`） |
| 音声認識（STT） | Azure Speech SDK | Web Speech API（`SpeechRecognition`） |
| PDF解析 | Python `pdfminer.six` | Mozilla PDF.js |
| グラフ描画 | Python `matplotlib` / `seaborn` | Chart.js |
| データ保存 | PostgreSQL, SQLite3 | LocalStorage |
