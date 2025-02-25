# Docker MCP Notion Server

NotionのAPIを使用してClaudeがNotion workspaceと対話できるようにするMCPサーバーのDockerイメージです。

## 使用方法

### Docker Hubから直接実行

```bash
docker run -e NOTION_API_TOKEN=your-token ghcr.io/tatsuiman/docker-mcp-notion-server:main
```

### ローカルでビルドして実行

```bash
git clone https://github.com/tatsuiman/docker-mcp-notion-server.git
cd docker-mcp-notion-server
docker build -t mcp-notion-server .
docker run -e NOTION_API_TOKEN=your-token mcp-notion-server
```

## セットアップ手順

1. **Notion Integrationの作成**:
   * [Notion Integrations](https://www.notion.so/my-integrations)ページにアクセス
   * "New Integration"をクリック
   * インテグレーションに名前を付け、必要な権限を選択（例："Read content", "Update content"）

2. **シークレットキーの取得**:
   * インテグレーションの"Internal Integration Token"をコピー
   * このトークンは認証に使用されます

3. **ワークスペースへのインテグレーション追加**:
   * Notionでインテグレーションにアクセスを許可したいページまたはデータベースを開く
   * 右上のメニューボタンをクリック
   * "Connect to"ボタンをクリックし、作成したインテグレーションを選択

4. **Claude Desktopの設定**: `claude_desktop_config.json`に以下を追加:

```json
{
    "mcpServers": {
        "notion": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "-e",
                "NOTION_API_TOKEN=your-integration-token",
                "ghcr.io/tatsuiman/docker-mcp-notion-server:main"
            ]
        }
    }
}
```

## トラブルシューティング

権限エラーが発生した場合:

1. インテグレーションに必要な権限が付与されているか確認
2. インテグレーションが対象のページやデータベースに招待されているか確認
3. トークンと設定が`claude_desktop_config.json`に正しく設定されているか確認

## 利用可能なツール

このMCPサーバーは以下のNotion APIツールを提供します：

1. `notion_append_block_children` - ブロックに子ブロックを追加
2. `notion_retrieve_block` - ブロック情報の取得
3. `notion_retrieve_block_children` - ブロックの子要素の取得
4. `notion_delete_block` - ブロックの削除
5. `notion_retrieve_page` - ページ情報の取得
6. `notion_update_page_properties` - ページプロパティの更新
7. `notion_create_database` - データベースの作成
8. `notion_query_database` - データベースのクエリ
9. `notion_retrieve_database` - データベース情報の取得
10. `notion_update_database` - データベースの更新
11. `notion_create_database_item` - データベースアイテムの作成
12. `notion_search` - ページやデータベースの検索
13. `notion_list_all_users` - ユーザー一覧の取得
14. `notion_retrieve_user` - ユーザー情報の取得
15. `notion_retrieve_bot_user` - ボットユーザー情報の取得
16. `notion_create_comment` - コメントの作成
17. `notion_retrieve_comments` - コメントの取得

各ツールの詳細な使用方法については、[オリジナルのリポジトリ](https://github.com/suekou/mcp-notion-server)を参照してください。

## 参考記事

* 英語版: [Operating Notion via Claude Desktop using MCP](https://dev.to/suekou/operating-notion-via-claude-desktop-using-mcp-c0h)
* 日本語版: [MCPを使ってClaude DesktopからNotionを操作する](https://qiita.com/suekou/items/44c864583f5e3e6325d9)

## ライセンス

このプロジェクトはMITライセンスの下で提供されています。詳細については、[LICENSE](LICENSE)ファイルを参照してください。 