# 陸、API 規格設計

## 6.1 API 設計原則

| 原則 | 說明 |
|------|------|
| 風格 | RESTful API |
| 版本管理 | URL 路徑版本 (v1, v2) |
| 命名規範 | 小寫、連字號分隔 (kebab-case) |
| 回應格式 | JSON |
| 分頁方式 | cursor-based / offset-based |
| 排序 | ?sort=field&order=asc\|desc |
| 篩選 | ?filter[field]=value |

## 6.2 認證與授權

| 項目 | 說明 |
|------|------|
| 認證方式 | [JWT Bearer Token / OAuth2] |
| Token 存放 | [HttpOnly Cookie / Authorization Header] |
| Token 有效期 | Access: [填寫] 分鐘，Refresh: [填寫] 天 |
| 重新整理 | POST /api/v1/auth/refresh |
| 權限檢查 | RBAC，每個 API 標註所需角色 |

## 6.3 API 端點清單

### 認證模組 (Auth)

| 方法 | 路徑 | 說明 | 權限 |
|------|------|------|------|
| POST | /api/v1/auth/login | 使用者登入 | 公開 |
| POST | /api/v1/auth/register | 使用者註冊 | 公開 |
| POST | /api/v1/auth/refresh | 重新整理 Token | 已認證 |
| POST | /api/v1/auth/logout | 使用者登出 | 已認證 |
| POST | /api/v1/auth/forgot-password | 忘記密碼 | 公開 |
| POST | /api/v1/auth/reset-password | 重設密碼 | Token 驗證 |

### 使用者模組 (Users)

| 方法 | 路徑 | 說明 | 權限 |
|------|------|------|------|
| GET | /api/v1/users | 使用者列表 | ADMIN |
| GET | /api/v1/users/:id | 使用者詳情 | ADMIN, SELF |
| POST | /api/v1/users | 建立使用者 | ADMIN |
| PATCH | /api/v1/users/:id | 更新使用者 | ADMIN, SELF |
| DELETE | /api/v1/users/:id | 刪除使用者 | ADMIN |
| GET | /api/v1/users/me | 目前使用者 | 已認證 |

### [模組名稱]

| 方法 | 路徑 | 說明 | 權限 |
|------|------|------|------|
| GET | /api/v1/[resource] | 列表 | [填寫] |
| GET | /api/v1/[resource]/:id | 詳情 | [填寫] |
| POST | /api/v1/[resource] | 建立 | [填寫] |
| PATCH | /api/v1/[resource]/:id | 更新 | [填寫] |
| DELETE | /api/v1/[resource]/:id | 刪除 | [填寫] |

## 6.4 API 詳細規格範例

### POST /api/v1/auth/login

**描述**: 使用者登入，取得 Access Token

**Request Body:**

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Success Response (200):**

```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbG...",
    "refreshToken": "eyJhbG...",
    "expiresIn": 3600,
    "user": {
      "id": "uuid",
      "email": "user@example.com",
      "displayName": "使用者名稱",
      "role": "USER"
    }
  }
}
```

**Error Response (401):**

```json
{
  "success": false,
  "error": {
    "code": "AUTH_INVALID_CREDENTIALS",
    "message": "帳號或密碼錯誤"
  }
}
```

## 6.5 錯誤碼定義

| 錯誤碼 | HTTP Status | 說明 | 使用者訊息 |
|--------|------------|------|-----------|
| AUTH_INVALID_CREDENTIALS | 401 | 帳號密碼錯誤 | 帳號或密碼錯誤 |
| AUTH_TOKEN_EXPIRED | 401 | Token 過期 | 登入已過期，請重新登入 |
| AUTH_FORBIDDEN | 403 | 權限不足 | 您沒有執行此操作的權限 |
| RESOURCE_NOT_FOUND | 404 | 資源不存在 | 找不到此資源 |
| VALIDATION_ERROR | 422 | 驗證失敗 | 輸入資料有誤 |
| RATE_LIMIT_EXCEEDED | 429 | 超過速率限制 | 請求過於頻繁，請稍後再試 |
| INTERNAL_ERROR | 500 | 伺服器內部錯誤 | 系統發生錯誤，請稍後再試 |

## 6.6 API 版本管理

| 版本 | 狀態 | 維護期限 | 說明 |
|------|------|---------|------|
| v1 | 目前版本 | — | 主要版本 |
| v2 | 規劃中 | — | 未來版本 |

- 舊版 API 維護至新版上線後 [填寫] 個月
- 版本棄用前 [填寫] 個月發出通知

---

**文件編號**: SDD-004  
**版本**: 1.0  
**最後更新**: YYYY-MM-DD
