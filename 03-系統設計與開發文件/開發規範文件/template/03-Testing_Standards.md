# 伍、測試規範

## 5.1 測試策略（測試金字塔）

```
        /\
       /  \        E2E Tests (少量)
      /────\
     /      \      Integration Tests (適量)
    /────────\
   /          \    Unit Tests (大量)
  /────────────\
```

| 測試類型 | 佔比 | 執行速度 | 維護成本 | 信心度 |
|---------|------|---------|---------|--------|
| 單元測試 | ~70% | 快 | 低 | 中 |
| 整合測試 | ~20% | 中 | 中 | 高 |
| E2E 測試 | ~10% | 慢 | 高 | 最高 |

## 5.2 單元測試規範

### 命名規則

```
describe('[測試對象]', () => {
  describe('[方法/情境]', () => {
    it('should [預期行為] when [條件]', () => {
      // Arrange
      // Act
      // Assert
    });
  });
});
```

### 範例

```typescript
describe('AuthService', () => {
  describe('login', () => {
    it('should return token when credentials are valid', async () => {
      // Arrange
      const credentials = { email: 'test@test.com', password: 'pass123' };
      
      // Act
      const result = await authService.login(credentials);
      
      // Assert
      expect(result.accessToken).toBeDefined();
    });

    it('should throw UnauthorizedError when password is wrong', async () => {
      // ...
    });
  });
});
```

### 單元測試規則

| 規則 | 說明 |
|------|------|
| 隔離 | 使用 Mock/Stub 隔離外部依賴 |
| 單一 | 每個測試案例只驗證一件事 |
| 可重複 | 不依賴外部狀態，可重複執行 |
| 快速 | 單一測試 < 100ms |
| 獨立 | 測試之間不互相依賴 |

## 5.3 整合測試規範

| 項目 | 說明 |
|------|------|
| 測試範圍 | API 端點、資料庫操作、服務整合 |
| 測試資料 | 使用測試資料庫、每次重置 |
| 外部服務 | 使用 Mock Server 或測試環境 |
| 環境 | Docker Compose 管理測試環境 |

## 5.4 端對端測試規範

| 項目 | 說明 |
|------|------|
| 工具 | [Playwright/Cypress] |
| 範圍 | 關鍵使用者流程 |
| 資料 | 種子資料 + 自動清理 |
| 環境 | 獨立測試環境 |
| 執行時機 | CI/CD pipeline、發佈前 |

## 5.5 測試覆蓋率要求

| 指標 | 最低要求 | 建議目標 |
|------|---------|---------|
| 行覆蓋率 (Line) | [填寫]% | [填寫]% |
| 分支覆蓋率 (Branch) | [填寫]% | [填寫]% |
| 函式覆蓋率 (Function) | [填寫]% | [填寫]% |
| 語句覆蓋率 (Statement) | [填寫]% | [填寫]% |

### 覆蓋率例外

- 設定檔（config）
- 型別定義（types）
- 自動產生的程式碼
- 第三方套件封裝

## 5.6 CI/CD 整合

### Pipeline 階段

| 階段 | 動作 | 通過條件 | 失敗處理 |
|------|------|---------|---------|
| Lint | 程式碼檢查 | 無 error | 阻止合併 |
| Build | 編譯專案 | 編譯成功 | 阻止合併 |
| Unit Test | 單元測試 | 100% 通過 | 阻止合併 |
| Integration Test | 整合測試 | 100% 通過 | 阻止合併 |
| Coverage | 覆蓋率檢查 | ≥ 門檻值 | 警告/阻止 |
| Security | 安全掃描 | 無高風險漏洞 | 阻止合併 |
| E2E Test | 端對端測試 | 100% 通過 | 阻止部署 |
| Deploy | 部署 | 部署成功 | 回滾 |

### Quality Gates

| 門檻 | 標準 | 強制性 |
|------|------|--------|
| 編譯通過 | 0 error | 強制 |
| Lint 通過 | 0 error, 0 warning | 強制 |
| 測試通過 | 100% pass | 強制 |
| 覆蓋率 | ≥ [填寫]% | 強制 |
| 安全掃描 | 無 Critical/High | 強制 |
| PR 審查 | ≥ [填寫] approve | 強制 |

---

# 陸、文件撰寫規範

## 6.1 README 規範

每個專案/模組應包含 README.md：

```markdown
# 專案名稱

## 概述
[一段話描述專案用途]

## 快速開始
[安裝與啟動步驟]

## 環境需求
[列出必要的執行環境]

## 開發指南
[開發相關命令與流程]

## 部署
[部署方式與注意事項]
```

## 6.2 API 文件規範

- 使用 OpenAPI 3.0 (Swagger) 規格
- 所有 API 必須有描述、請求/回應範例
- 錯誤回應必須文件化

---

# 柒、依賴管理規範

## 7.1 套件管理

| 項目 | 規範 |
|------|------|
| 套件管理器 | [npm/pnpm/yarn] |
| 版本鎖定 | 使用 lock file (package-lock.json / pnpm-lock.yaml) |
| 版本限制 | 使用精確版本或 ^（minor 更新） |
| 新增套件 | 需說明用途、評估大小與安全性 |
| 移除套件 | 確認無引用後移除 |

## 7.2 安全掃描

| 項目 | 工具 | 頻率 |
|------|------|------|
| 依賴漏洞掃描 | [npm audit / Snyk / Dependabot] | 每次 CI 執行 |
| 授權合規檢查 | [license-checker] | 每次新增套件 |
| 版本更新 | [Renovate / Dependabot] | 每週自動 PR |

## 7.3 禁止使用的授權

| 授權類型 | 原因 |
|---------|------|
| GPL-3.0 | 病毒式授權，可能影響商業使用 |
| AGPL-3.0 | 網路傳播條款 |
| [填寫] | [填寫] |

---

# 簽核頁

| 角色 | 姓名 | 簽章 | 日期 |
|------|------|------|------|
| 技術主管 | | | |
| 開發團隊代表 | | | |
| 專案經理 | | | |

---

**文件編號**: DEV-003  
**版本**: 1.0  
**最後更新**: YYYY-MM-DD
