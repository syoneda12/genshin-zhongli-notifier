# 岩王帝君の余録（Genshin Daily Note Notifier）

> 「契約は永遠ではない。ゆえに、更新するたびに理が続くのだ。」

原神のデイリーノート情報を取得し、Discord に鍾離（岩王帝君）の語り口で通知する Google Apps Script です。  
樹脂の回復、洞天宝銭、探索派遣、参量物質変化器、デイリー報酬の状況を自動チェックします。

※ これを真似をして公式から怒られても責任は取れません。

---

## 📜 概要 / Overview

このスクリプトは HoYoLab の非公開 API  
`https://bbs-api-os.hoyoverse.com/game_record/genshin/api/dailyNote`  
を用いて以下の情報を取得します。

| 項目 | 通知タイミング | 内容 |
|------|----------------|------|
| 天然樹脂 | 2時間ごと | 上限到達・残り時間 |
| 洞天宝銭 | 3時間ごと | 上限到達・残り時間 |
| 探索派遣 | 4時間ごと | 完了数の通知 |
| 参量物質変化器 | 6時間ごと | 使用可能／残り時間 |
| デイリー報酬 | 21時・23時 | 未受取の報酬通知 |

通知文はすべて「鍾離の独白」風に構成され、  
header（情景描写）＋本文（ステータス）＋footer（哲学的余韻）の三段構成になっています。

※現在はコメントアウトして本文（ステータス）のみにしています。

---

## 🧩 構成 / Structure
- src/main.gs : エントリーポイント
- src/api.gs : HoYoLab APIアクセス
- src/notify.gs : Discord通知
- src/logger.gs : ログ管理（Logger）
- src/util.gs : 時刻変換など
- src/config.gs : 設定情報（Webhook、UID、Cookieなど）

---

## ⚙️ セットアップ手順 / Setup
1. Google Apps Scriptに新規プロジェクトを作成
2. `src/` 内のファイルを追加し、内容をコピー
3. `config.gs` にUID、Cookie、Webhook、スプレッドシートIDを設定
4. トリガーを設定して毎時で `notifyGenshinDailyNote()` を実行

---

## 🪵 ログ管理 / Log
- GASの `Logger` へ出力

## 🕒 定期実行設定
- GASの「トリガー」メニューから
  - 関数: `notifyGenshinDailyNote`
  - イベント: 時間主導型 → 毎時
