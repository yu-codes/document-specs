# 壹、文件概述

## 1.1 文件目的

本文件規定 [填寫專案名稱] 專案之開發規範，確保團隊成員產出一致、高品質的程式碼。

## 1.2 適用範圍

- 適用對象：所有專案開發人員
- 適用語言：[填寫主要開發語言]
- 適用範圍：前端、後端、資料庫相關開發

## 1.3 版本歷史

| 版本 | 日期 | 異動內容 | 撰寫人 |
|------|------|---------|--------|
| 1.0 | YYYY-MM-DD | 初版建立 | [填寫] |

---

# 貳、程式碼命名規則

## 2.1 通用命名原則

- 使用有意義、可讀的名稱
- 避免縮寫（除非是廣泛認知的縮寫如 ID, URL, API）
- 名稱長度合理（變數 2-30 字元，函式 3-50 字元）
- 使用英文命名

## 2.2 變數命名

| 語言/環境 | 命名風格 | 範例 |
|---------|---------|------|
| TypeScript 變數 | camelCase | `userName`, `orderCount` |
| TypeScript 常數 | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_BASE_URL` |
| TypeScript 型別 | PascalCase | `UserProfile`, `OrderStatus` |
| CSS 類別 | kebab-case | `main-container`, `btn-primary` |
| 環境變數 | UPPER_SNAKE_CASE | `DATABASE_URL`, `JWT_SECRET` |

## 2.3 函式命名

| 類型 | 前綴 | 範例 |
|------|------|------|
| 取得資料 | get / fetch | `getUserById()`, `fetchOrders()` |
| 設定值 | set / update | `setUserName()`, `updateStatus()` |
| 布林判斷 | is / has / can | `isValid()`, `hasPermission()` |
| 事件處理 | handle / on | `handleClick()`, `onSubmit()` |
| 轉換 | to / format | `toUpperCase()`, `formatDate()` |
| 驗證 | validate / check | `validateEmail()`, `checkAuth()` |
| 建立 | create / build | `createUser()`, `buildQuery()` |
| 刪除 | delete / remove | `deleteUser()`, `removeItem()` |

## 2.4 類別命名

| 類型 | 風格 | 後綴 | 範例 |
|------|------|------|------|
| Controller | PascalCase | Controller | `UserController` |
| Service | PascalCase | Service | `AuthService` |
| Repository | PascalCase | Repository | `OrderRepository` |
| DTO | PascalCase | Dto | `CreateUserDto` |
| Entity | PascalCase | — | `User`, `Order` |
| Interface | PascalCase | I 前綴（可選） | `IUserService` |

## 2.5 檔案命名

| 類型 | 風格 | 範例 |
|------|------|------|
| 元件檔案 | PascalCase | `UserProfile.tsx` |
| 模組檔案 | kebab-case | `user-service.ts` |
| 測試檔案 | 同源檔案 + .spec/.test | `user-service.spec.ts` |
| 樣式檔案 | 同元件名 | `UserProfile.module.css` |
| 常數檔案 | kebab-case | `error-codes.ts` |

## 2.6 資料庫命名

| 項目 | 風格 | 範例 |
|------|------|------|
| 資料表 | snake_case 複數 | `users`, `order_items` |
| 欄位 | snake_case | `first_name`, `created_at` |
| 主鍵 | id | `id` |
| 外鍵 | {table_singular}_id | `user_id` |
| 索引 | idx_{table}_{columns} | `idx_users_email` |
| 唯一約束 | uq_{table}_{columns} | `uq_users_email` |

---

# 參、程式碼風格規範

## 3.1 縮排與格式化

| 項目 | 規範 |
|------|------|
| 縮排方式 | 空格（Spaces） |
| 縮排大小 | 2 個空格 |
| 行尾 | LF (Unix) |
| 最大行寬 | 100 字元 |
| 檔案結尾 | 空行 |
| 尾隨逗號 | 使用 (trailing comma) |
| 分號 | [使用/不使用] |
| 引號 | 單引號 (single quotes) |

## 3.2 註解規範

### 何時需要註解

- 複雜的業務邏輯
- 非顯而易見的演算法
- 暫時的解決方案 (TODO)
- 已知的限制或注意事項

### 註解格式

```typescript
// 單行註解：簡短說明

/**
 * 多行註解：函式/類別說明
 * @param userId - 使用者 ID
 * @returns 使用者資料
 */

// TODO: 待改善項目描述 [負責人] [預計日期]
// FIXME: 已知問題描述
// HACK: 暫時方案說明，正式解法為 [描述]
```

## 3.3 檔案結構

```typescript
// 1. 第三方套件 imports
import { Module } from '@nestjs/common';

// 2. 內部模組 imports（絕對路徑）
import { UserService } from '@/modules/users/user.service';

// 3. 相對路徑 imports
import { CreateUserDto } from './dto/create-user.dto';

// 4. 型別 imports
import type { User } from './entities/user.entity';

// 5. 常數定義

// 6. 型別定義

// 7. 主要內容（類別/函式）

// 8. 輔助函式
```

## 3.4 Linter & Formatter 設定

| 工具 | 用途 | 設定檔 |
|------|------|--------|
| ESLint | 程式碼品質 | `.eslintrc.js` |
| Prettier | 程式碼格式 | `.prettierrc` |
| Stylelint | CSS 品質 | `.stylelintrc` |
| EditorConfig | 編輯器統一設定 | `.editorconfig` |

---

**文件編號**: DEV-001  
**版本**: 1.0  
**最後更新**: YYYY-MM-DD
