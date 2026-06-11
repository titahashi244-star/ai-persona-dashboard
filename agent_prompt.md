# 毎朝8時 AIペルソナ業界動向収集エージェント

## 役割
DNP（大日本印刷）のAIペルソナサービス営業企画担当向けに、毎朝の業界動向をまとめたHTMLメールを作成・送信する。

## 収集する情報（3カテゴリ）

### 1. 競合動向（AIペルソナ関連全域）
以下のクエリで直近1週間のニュースを検索：
- `AIペルソナ OR デジタルヒューマン OR AIアバター OR 仮想インフルエンサー OR AIタレント 新サービス OR リリース OR 発表`
- `AIペルソナ OR デジタルヒューマン 企業 参入 OR 開発 OR 提供開始 OR 事業`
- `バーチャルヒューマン OR バーチャルインフルエンサー OR AIキャラクター ビジネス OR 商用 OR サービス`
- `生成AI アバター OR キャラクター マーケティング OR PR OR 接客 新サービス OR スタートアップ`

### 2. 潜在顧客動向（全業界 DX・マーケ・顧客体験）
以下のクエリで直近1週間のニュースを検索：
- `金融 OR 銀行 OR 保険 AI キャラクター OR アバター OR 顧客対応 OR マーケティング`
- `インフラ OR 電力 OR 通信 OR 鉄道 AI 顧客体験 OR DX OR デジタル 施策`
- `メディア OR 放送 OR 出版 AI タレント OR キャラクター OR コンテンツ 活用`
- `企業 AI 顧客コミュニケーション OR ブランドアンバサダー OR 接客 DX 導入`
- `消費財 OR 小売 OR 食品 OR 化粧品 AI マーケティング OR デジタル OR 販促 施策`

### 3. 導入事例・プレスリリース
以下のクエリで直近1週間のニュースを検索：
- `AIペルソナ OR AIアバター OR デジタルヒューマン 導入 事例 OR プレスリリース`
- `仮想タレント OR バーチャルインフルエンサー 企業 採用 OR 活用`
- `site:prtimes.jp AIペルソナ OR デジタルヒューマン`

## 実行手順

1. 上記クエリでWebSearch（各カテゴリ2〜3クエリ）
2. 各カテゴリから最も重要なニュースを3〜5件選定
3. 各ニュースを以下フォーマットで整理：
   - title: 記事タイトル（簡潔に）
   - url: 記事のURL（必ず実在するURLを入れる。不明な場合は空文字）
   - summary: 要約（2〜3文、営業企画視点で重要ポイントを含む）
   - source: 媒体名
   - date: 日付（YYYY/MM/DD）
   - tag: ラベル（例：新サービス、導入事例、DX施策、投資・M&A など）
4. 下記HTMLメールテンプレートに埋め込む
5. Resend APIでt.itahashi244@gmail.comに送信

## メール送信コマンド（Resend API）

```bash
curl -X POST https://api.resend.com/emails \
  -H "Authorization: Bearer RESEND_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "from": "dashboard@resend.dev",
    "to": "t.itahashi244@gmail.com",
    "subject": "【AIペルソナ動向】YYYY/MM/DD",
    "html": "HTML_CONTENT_HERE"
  }'
```

## HTMLメールテンプレート

下記のindex.htmlをベースに、収集したデータをインライン化したHTMLを生成する。
CSSはすべてinlineスタイルに変換すること（メールクライアント対応）。

## 注意事項
- 日本語情報のみ収集（英語は除外）
- 情報が見つからないカテゴリは「本日は該当情報がありません」と表示
- 各カテゴリ最大5件まで
- PRタイムスや日経、ITmedia、AdverTimes等の信頼性の高いソースを優先
