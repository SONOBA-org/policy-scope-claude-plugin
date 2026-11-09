# Policy Scope for Claude

日本の政策・審議会資料を、Claude から検索・閲覧するための MCP サーバー（コネクタ）です。
省庁の審議会などで公開された資料を、キーワード、省庁、審議会、会議日で探し、本文や関連資料、会議の情報を取得できます。

- 提供：一般社団法人SONOBA
- 接続先：`https://policyscope.jp/api/mcp`
- 認証：OAuth（Policy Scope のアカウントでログイン）
- 11 個の機能はすべて読み取り専用で、データを書き換えません。

## 利用条件

- Policy Scope のアカウント
- MCP 連携の利用権限（法人向けプランで利用できます。詳しくは [料金ページ](https://policyscope.jp/pricing) をご覧ください）

コネクタやプラグインを追加しただけでは、Policy Scope の有料機能や MCP の利用権限は付きません。

## claude.ai・Claude アプリで使う

1. Claude の「設定」→「コネクタ」を開きます。
2. 「カスタムコネクタを追加」を選び、URL に `https://policyscope.jp/api/mcp` を入力します。
3. Policy Scope のログイン画面が開いたら、ご自身のアカウントでログインし、連携を許可します。
4. チャットで、たとえば「再生可能エネルギーの出力制御に関する最新の審議会資料を探して」と頼みます。

## Claude Code で使う

このリポジトリはプラグインとしても配布しています。Claude Code で次を実行します。

```text
/plugin marketplace add SONOBA-org/policy-scope-claude-plugin
/plugin install policy-scope@policy-scope-marketplace
```

導入後に `/mcp` で Policy Scope を選び、OAuth の認証を進めます。

ソースから試す場合は次のとおりです。保存先に応じてパスを変えてください。

```sh
git clone https://github.com/SONOBA-org/policy-scope-claude-plugin.git
claude plugin validate ./policy-scope-claude-plugin
claude --plugin-dir ./policy-scope-claude-plugin
```

## 提供する機能

| 機能 | 内容 |
|---|---|
| `search_policies` | キーワード、省庁、審議会、日付で政策文書を検索します。 |
| `get_document` | 文書 ID を指定し、文書の詳細と本文を取得します。 |
| `get_latest_documents` | 指定した期間内の最新の審議会資料を、新しい順で取得します。 |
| `list_documents_chronological` | 審議会、省庁、期間、キーワードで絞り、会議日順に資料を取得します。 |
| `get_related_documents` | 意味の近い資料、同じ審議会、または同じ会議の資料を取得します。 |
| `get_popular_documents` | 指定期間によく閲覧された資料を取得します。 |
| `get_meeting` | 会議 ID を指定し、会議の情報、資料、参加者、議事録の有無を取得します。 |
| `find_meetings` | 「第27回」などの回次や審議会名から会議を探します。 |
| `list_meetings_by_council` | 審議会の会議を一覧にします。 |
| `list_councils` | 審議会を省庁の情報付きで一覧にします。 |
| `list_ministries` | 省庁の一覧を取得します。 |

## 使用例

- 「再生可能エネルギーの出力制御に関する最新の審議会資料を探して」
- 「その資料と内容の近い資料を5件教えて」
- 「料金制度専門会合の最近の会議を一覧にして」
- 「直近30日の資料を取得して、主な論点を整理して」
- 「この政策文書の詳細と出典を確認して」

検索結果をもとに説明を作るときは、文書の詳細と原典を確認してください。
収録範囲や更新の状況により、検索結果が政策情報のすべてを網羅するとは限りません。

## データの取り扱い

- 機能を呼び出すと、検索語などの引数が Policy Scope に送られ、結果が利用中の Claude に返ります。
- Policy Scope が受け取るのは、機能の呼び出しに含まれる引数だけです。Claude との会話の内容は受け取りません。
- 認証は OAuth で行います。このリポジトリに認証情報は含まれていません。

- [Policy Scope プライバシーポリシー](https://policyscope.jp/privacy)
- [Policy Scope 利用規約](https://policyscope.jp/terms)

## トラブルシューティング

- 認証に失敗する場合は、コネクタ（Claude Code では `/mcp`）の接続状態を確認し、もう一度認証してください。
- 接続後にアクセスを拒否される場合は、MCP 連携の利用権限と所属する組織を確認してください。
- 問題を報告するときは、トークン、パスワード、個人情報を含めないでください。

## お問い合わせ

- サービス：https://policyscope.jp
- メール：policy-scope@sonoba.or.jp
