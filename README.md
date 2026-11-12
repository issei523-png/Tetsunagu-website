# 株式会社Tetsunagu コーポレートサイト

Vercel で公開する静的サイトです（HTML / CSS / 少量の JavaScript のみ。ビルド不要）。

## ファイル構成

| パス | 内容 |
|---|---|
| `index.html` | トップページ |
| `news/` | お知らせ一覧 |
| `news1/`〜`news5/` | お知らせ記事（旧サイトと同じURL。熊本地震の記事のみ `/news5/` に変更し、旧URLから転送） |
| `recruit/` | 採用情報 |
| `privacy-policy/` | プライバシーポリシー |
| `404.html` | ページが見つからないときの表示 |
| `assets/img/` | 写真・ロゴ |
| `vercel.json` | URL設定と、旧サイトURL（/company/ /about/ /contact/ /column/ など）からの転送 |
| `sitemap.xml` / `robots.txt` | 検索エンジン向け |

## 1. お問い合わせフォーム（Formspree）の設定

1. https://formspree.io でアカウントを作成し、「New Form」でフォームを作る（通知先メールアドレスを指定）。
2. 発行されたURL（例：`https://formspree.io/f/abcdwxyz`）をコピー。
3. `index.html` のフォームの `action` にそのURLを設定（設定済み：`https://formspree.io/f/xvkaovew`）。

- 送信はページ遷移なしで行われ、完了・失敗のメッセージがフォーム内に表示されます。
- メール件名は「【ホームページ】お問い合わせがありました」です（`_subject` で変更可）。
- 簡易的なスパム対策（見えない入力欄 `_gotcha`）を入れています。

## 2. Vercel で公開

1. Vercel にログイン →「Add New… → Project」→ このGitHubリポジトリを選んで「Import」。
2. Framework Preset は「Other」のまま、ビルド設定は空欄で「Deploy」。
3. 発行された `〜.vercel.app` のURLで表示とフォーム送信を確認。

以後、GitHub に変更を push すると自動で反映されます。

## 3. 独自ドメイン（tetsunagu.co.jp）の切り替え

現在のDNS（2026年11月12日時点で確認）:

| ホスト | 種類 | 現在の値 | 切り替え後 |
|---|---|---|---|
| tetsunagu.co.jp | A | 157.120.209.18（WordPress） | **Vercel の画面に表示される値（通常 76.76.21.21）に変更** |
| www.tetsunagu.co.jp | A | 157.120.209.18 | **削除して CNAME（Vercel の画面に表示される値）を追加** |
| tetsunagu.co.jp | MX | 10 mail1038.onamae.ne.jp | **変更しない** |
| mail.tetsunagu.co.jp | A | 157.120.209.11 | **変更しない** |
| tetsunagu.co.jp | TXT | v=spf1 include:_spf.onamae.ne.jp ~all | **変更しない** |

ネームサーバーは `ns-rs1.gmoserver.jp` / `ns-rs2.gmoserver.jp`（お名前.com レンタルサーバー）です。
DNSレコードの編集は、お名前.com Navi のドメイン設定ではなく、**レンタルサーバー側のコントロールパネル**で行う可能性が高いです。

手順:
1. Vercel のプロジェクト →「Settings → Domains」で `tetsunagu.co.jp` と `www.tetsunagu.co.jp` を追加し、表示される値を控える。
2. DNS管理画面で上表の「切り替え後」のとおり、Webサイト用の2件だけを変更する。
3. 数十分〜数時間で反映され、Vercel が自動で https 化します。

### 注意
- **メールはお名前.com のレンタルサーバーで動いています。** サイトを Vercel に移しても、レンタルサーバーの契約は解約しないでください（解約するとメールが止まります）。
- 問題があれば、A レコードを元の値（157.120.209.18）に戻せば旧サイトに戻ります。
- WordPress のデータは切り替え前にバックアップしておくと安心です。
