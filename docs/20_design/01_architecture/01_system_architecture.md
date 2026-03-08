# システムアーキテクチャ

| 項目 | 技術 | バージョン | 目的 |
| ------ | ------ | ------------ | ------ |
| アプリケーション | Blazor / .NET 10 | 10.0+ | UI + API 統合 |
| データベース | PostgreSQL | 17.x | データ永続化 |
| 認証 | Google OAuth | - | ユーザー認証 |
| 認可 | JWT | - | API 認可 |
| CI/CD | GitHub Actions | - | ビルド・テスト・デプロイ |
| ホスティング | Render.com | - | PaaS ホスティング |

```mermaid
graph TD
    Client[ブラウザ]
    App[Blazor .NET 10<br/>UI + API]
    DB[(PostgreSQL)]
    Auth[Google OAuth / JWT]
    GitHub[GitHub]
    Actions[GitHub Actions]
    Render[Render.com]

    Client --> App
    App --> DB
    App --> Auth
    GitHub --> Actions
    Actions --> Render
```
