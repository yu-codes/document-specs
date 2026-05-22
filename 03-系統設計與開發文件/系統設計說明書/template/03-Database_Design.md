# 伍、資料庫設計

## 5.1 資料庫技術選擇

| 項目 | 說明 |
|------|------|
| 主資料庫 | [PostgreSQL/MySQL/MongoDB] v[填寫] |
| 快取資料庫 | Redis v[填寫] |
| 搜尋引擎 | [Elasticsearch] v[填寫]（如適用） |
| 連線池 | [填寫] |
| ORM/ODM | [填寫] |

## 5.2 ERD 圖

[插入完整 ERD 圖]

## 5.3 資料表設計

### users（使用者）

| 欄位 | 類型 | 約束 | 說明 |
|------|------|------|------|
| id | UUID | PK | 主鍵 |
| email | VARCHAR(255) | UNIQUE, NOT NULL | 登入帳號 |
| password_hash | VARCHAR(255) | NOT NULL | 密碼雜湊 |
| display_name | VARCHAR(100) | NOT NULL | 顯示名稱 |
| role_id | UUID | FK → roles.id | 角色 |
| status | ENUM | NOT NULL, DEFAULT 'active' | 狀態 |
| created_at | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() | 建立時間 |
| updated_at | TIMESTAMPTZ | NOT NULL | 更新時間 |

### [資料表名稱]

| 欄位 | 類型 | 約束 | 說明 |
|------|------|------|------|
| [填寫] | [填寫] | [填寫] | [填寫] |

## 5.4 索引策略

| 資料表 | 索引名稱 | 索引欄位 | 類型 | 用途 |
|--------|---------|---------|------|------|
| users | idx_users_email | email | UNIQUE | 登入查詢 |
| users | idx_users_status | status | B-tree | 狀態篩選 |
| [填寫] | [填寫] | [填寫] | [填寫] | [填寫] |

## 5.5 資料遷移計畫

| 遷移編號 | 說明 | 檔案名稱 | 執行順序 |
|---------|------|---------|---------|
| 001 | 建立基礎表 | 001_create_initial_tables | 1 |
| 002 | 加入索引 | 002_add_indexes | 2 |
| [填寫] | [填寫] | [填寫] | [填寫] |

---

**文件編號**: SDD-003  
**版本**: 1.0  
**最後更新**: YYYY-MM-DD
