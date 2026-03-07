# テーブル定義

## `paints`

| column_name         | type                      | constraints | index                             | notes |
|:--------------------|:--------------------------|:------------|:----------------------------------|:------|
| id                  | text                      | PK          | PRIMARY KEY                       | paint ID |
| name                | varchar(100)              | NOT NULL    | INDEX                             | |
| model_number        | varchar(50)               | NOT NULL    | UNIQUE (`brand_id`, `model_number`) | |
| model_number_prefix | varchar(50)               |             | INDEX (`model_number_prefix`, `model_number_number`) | model number sort key |
| model_number_number | integer                   |             | INDEX (`model_number_prefix`, `model_number_number`) | model number sort key |
| brand_id            | text                      | FK NOT NULL | INDEX                             | FK -> `brands.id` |
| paint_type_id       | text                      | FK NOT NULL | INDEX                             | FK -> `paint_types.id` |
| gloss_id            | text                      | FK NOT NULL | INDEX                             | FK -> `glosses.id` |
| price               | numeric(10,2)             | NOT NULL    |                                   | |
| description         | varchar(500)              |             |                                   | |
| image_url           | varchar(200)              |             |                                   | |
| hex                 | text                      | NOT NULL    |                                   | |
| rgb_r               | integer                   | NOT NULL    |                                   | |
| rgb_g               | integer                   | NOT NULL    |                                   | |
| rgb_b               | integer                   | NOT NULL    |                                   | |
| hsl_h               | real                      | NOT NULL    |                                   | |
| hsl_s               | real                      | NOT NULL    |                                   | |
| hsl_l               | real                      | NOT NULL    |                                   | |
| created_at          | timestamp with time zone  | NOT NULL    |                                   | DEFAULT CURRENT_TIMESTAMP |
| updated_at          | timestamp with time zone  | NOT NULL    |                                   | DEFAULT CURRENT_TIMESTAMP |
| is_deleted          | boolean                   | NOT NULL    |                                   | DEFAULT false (soft delete) |

**query filter**
- `WHERE is_deleted = false`

---

## `brands`

| column_name | type        | constraints | index       | notes |
|:------------|:------------|:------------|:------------|:------|
| id          | text        | PK          | PRIMARY KEY | brand ID |
| name        | varchar(50) | NOT NULL    | INDEX       | |
| description | text        |             |             | nullable |

---

## `paint_types`

| column_name | type        | constraints | index       | notes |
|:------------|:------------|:------------|:------------|:------|
| id          | text        | PK          | PRIMARY KEY | paint type ID |
| name        | varchar(50) | NOT NULL    |             | |
| description | text        |             |             | nullable |

---

## `glosses`

| column_name | type        | constraints | index       | notes |
|:------------|:------------|:------------|:------------|:------|
| id          | text        | PK          | PRIMARY KEY | gloss ID |
| name        | varchar(50) | NOT NULL    |             | |
| description | text        |             |             | nullable |

---

## `tags`

| column_name     | type                      | constraints | index       | notes |
|:----------------|:--------------------------|:------------|:------------|:------|
| id              | text                      | PK          | PRIMARY KEY | tag ID |
| name            | varchar(50)               | NOT NULL    |             | |
| tag_category_id | text                      | FK NOT NULL | INDEX       | FK -> `tag_categories.id` |
| hex             | varchar(7)                |             |             | |
| effect          | text                      |             |             | |
| description     | text                      |             |             | |
| created_at      | timestamp with time zone  | NOT NULL    |             | DEFAULT CURRENT_TIMESTAMP |
| updated_at      | timestamp with time zone  | NOT NULL    |             | DEFAULT CURRENT_TIMESTAMP |
| is_deleted      | boolean                   | NOT NULL    |             | DEFAULT false (soft delete) |

**query filter**
- `WHERE is_deleted = false`

---

## `tag_categories`

| column_name | type        | constraints | index       | notes |
|:------------|:------------|:------------|:------------|:------|
| id          | text        | PK          | PRIMARY KEY | tag category ID |
| name        | varchar(50) | NOT NULL    |             | |
| description | text        |             |             | nullable |

---

## `paint_tags`

| column_name | type | constraints | index | notes |
|:------------|:-----|:------------|:------|:------|
| paint_id    | text | PK, FK      | INDEX | FK -> `paints.id` |
| tag_id      | text | PK, FK      | INDEX | FK -> `tags.id` |

**composite primary key**
- (`paint_id`, `tag_id`)

---

## 制約・インデックス方針

- PK は全テーブルで `id`（`paint_tags` は複合PK）。
- FK は結合性能のためインデックスを付与。
- UNIQUE 制約は `paints(brand_id, model_number)`。
- 複合インデックスは `paints(model_number_prefix, model_number_number)`。
- 論理削除は `paints` と `tags` のみ適用。
