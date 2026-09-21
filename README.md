# Policy Scope for Claude

日本の政策・審議会資料を検索する、Claude向けMCPプラグインです。

## 状態

Community Marketplaceへの申請準備中です。Policy Scope MCPのOpenAI環境での動作確認は提供者により完了しています。Claude Code固有のOAuth接続・実動作は未確認です。Claude Codeのプラグイン形式検証と本番MCPの認証メタデータ取得は確認済みです。

## 利用条件

- プラグイン対応のClaude Code
- Policy ScopeアカウントとMCP利用権限（`mcp.read`）
- 本番サービスへのインターネット接続

プラグインの導入だけではPolicy Scopeの有料機能やMCP利用権限は付与されません。利用可能な契約条件はサービス提供者へ確認してください。

## インストール

Claude Codeで次を実行します。このリポジトリの配布用マーケットプレイスから導入できます。

```text
/plugin marketplace add SONOBA-org/policy-scope-claude-plugin
/plugin install policy-scope@policy-scope-marketplace
```

導入後に `/mcp` でPolicy Scopeの接続を選択し、OAuth認証を進めます。Community Marketplaceへの掲載承認を示すものではありません。

## ソースから試す

このプラグインのディレクトリを指定して起動します。

```sh
git clone https://github.com/SONOBA-org/policy-scope-claude-plugin.git
claude plugin validate ./policy-scope-claude-plugin
claude --plugin-dir ./policy-scope-claude-plugin
```

実際の保存先に応じてパスを変更してください。Claude Code内で `/mcp` を開き、Policy Scopeの接続を選択してOAuth認証を進めます。接続先は `https://policyscope.jp/api/mcp` です。

## 使用例

- 「Policy Scopeで電力政策に関する審議会資料を検索して」
- 「直近30日の資料を取得して、主な論点を整理して」
- 「この政策文書の詳細と出典を確認して」

## 提供ツール

読み取り専用の次のツールを提供します。

`search_policies`, `get_document`, `get_latest_documents`,
`list_documents_chronological`, `get_related_documents`,
`get_popular_documents`, `get_meeting`, `find_meetings`,
`list_meetings_by_council`, `list_councils`, `list_ministries`

検索結果から説明を作成する際は文書詳細と原典を確認してください。収録範囲や更新状況により、検索結果が政策情報のすべてを網羅するとは限りません。

## Privacy Policy

このパッケージはリモートMCP接続設定を含みます。ツールの検索語・引数はPolicy Scopeへ送信され、取得結果は利用中のClaudeへ返ります。認証はOAuthを使い、このパッケージに認証情報は含みません。

- [Policy Scopeプライバシーポリシー](https://policyscope.jp/privacy)
- [Policy Scope利用規約](https://policyscope.jp/terms)

公開前にサービス側の説明を実際のClaude連携の取り扱いと整合させます。

## トラブルシューティング

- 認証に失敗する場合は `/mcp` から接続状態を確認し、再認証してください。
- 接続後にアクセスを拒否される場合はMCP利用権限と対象組織を確認してください。
- 問題を報告する際は、トークン・パスワード・個人情報を含めないでください。

サービス情報: https://policyscope.jp

問い合わせ: policy-scope@sonoba.or.jp
