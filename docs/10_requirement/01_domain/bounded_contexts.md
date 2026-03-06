# 境界づけられたコンテキスト

PlasticModelAppの **境界づけられたコンテキスト** (Bounded Context, BC)を定義する。

## 1. コンテキスト一覧

| ID | 名称 | 種別 | 説明 |
| - | - | - | - |
| BC1 | Selection | コア | ユーザーに、塗料比較・選定の体験を提供する。 |
| BC2 | Catalog | 補完 | 他BCやユーザーに、塗料の事実データを提供する。 |
| BC3 | Operation | 補完 | 他BCやユーザーに、塗料の在庫管理や再購入あり/なしの管理を提供する。 |
| BC4 | Auth | 一般 | 他BCやユーザーに、認証や認可を提供する。 |

## 2. コンテキストマップ

```mermaid
graph TD
    Auth[Auth<br/>認証・認可]
    Catalog[Catalog<br/>塗料カタログ]
    Operations[Operations<br/>在庫管理]
    Selection[Selection<br/>選定機能]

    Auth -->|Conformist| Catalog
    Auth -->|Conformist| Operations
    Auth -->|Conformist| Selection

    Catalog -->|Customer/Supplier| Operations
    Catalog -->|Customer/Supplier| Selection

    Operations -.->|Independent| Selection

    style Auth fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style Catalog fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style Operations fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style Selection fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
```

**凡例**:

- **実線矢印**: 依存関係（下流→上流）
- **点線**: 独立関係（依存なし）
