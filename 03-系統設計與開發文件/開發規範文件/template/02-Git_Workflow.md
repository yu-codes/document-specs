# 肆、Git Workflow 與提交規範

## 4.1 分支策略

### 分支模型：[Git Flow / Trunk-Based / GitHub Flow]

```
main (production)
  ├── develop (development)
  │   ├── feature/[ticket-id]-[description]
  │   ├── feature/[ticket-id]-[description]
  │   └── ...
  ├── release/[version]
  ├── hotfix/[ticket-id]-[description]
  └── ...
```

### 分支用途

| 分支類型 | 命名規則 | 來源 | 合併目標 | 生命週期 |
|---------|---------|------|---------|---------|
| main | main | — | — | 永久 |
| develop | develop | main | main (via release) | 永久 |
| feature | feature/PROJ-123-add-login | develop | develop | 功能完成後刪除 |
| release | release/1.2.0 | develop | main + develop | 發佈後刪除 |
| hotfix | hotfix/PROJ-456-fix-crash | main | main + develop | 修復後刪除 |

## 4.2 分支命名規則

```
{type}/{ticket-id}-{short-description}
```

| 類型 | 說明 | 範例 |
|------|------|------|
| feature | 新功能 | feature/PROJ-123-user-login |
| fix | 修復 | fix/PROJ-456-login-error |
| refactor | 重構 | refactor/PROJ-789-auth-module |
| docs | 文件 | docs/PROJ-101-api-docs |
| chore | 雜項 | chore/PROJ-202-update-deps |

## 4.3 Commit Message 規範

### 格式（Conventional Commits）

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### Type 定義

| Type | 說明 | 範例 |
|------|------|------|
| feat | 新功能 | feat(auth): add login API |
| fix | 修復 | fix(ui): fix button alignment |
| docs | 文件 | docs(api): update API docs |
| style | 格式調整（不影響邏輯） | style: format code with prettier |
| refactor | 重構 | refactor(auth): simplify token logic |
| perf | 效能改善 | perf(db): optimize query |
| test | 測試 | test(auth): add login unit tests |
| chore | 維護 | chore: update dependencies |
| ci | CI/CD | ci: add deployment pipeline |

### 範例

```
feat(users): add user registration API

- Add POST /api/v1/users/register endpoint
- Implement email verification flow
- Add input validation with class-validator

Closes #123
```

## 4.4 Pull Request 流程

### PR 標題格式

```
[PROJ-123] feat: add user registration
```

### PR Template

```markdown
## 變更描述
[簡述此 PR 的變更內容]

## 變更類型
- [ ] 新功能 (feature)
- [ ] 修復 (fix)
- [ ] 重構 (refactor)
- [ ] 文件 (docs)
- [ ] 其他: ___

## 測試
- [ ] 已新增/更新單元測試
- [ ] 已通過本地測試
- [ ] 已通過 CI 測試

## 影響範圍
[說明此變更可能影響的模組或功能]

## 截圖（如適用）
[附上畫面截圖]

## 相關 Issue
Closes #[issue-number]
```

## 4.5 Code Review 規範

### 審查者職責

- 確認程式碼符合規範
- 檢查邏輯正確性
- 評估效能影響
- 確認測試覆蓋
- 提供建設性回饋

### 審查標準

| 項目 | 檢查重點 |
|------|---------|
| 正確性 | 邏輯是否正確、邊界案例處理 |
| 安全性 | 是否有安全漏洞 |
| 效能 | 是否有效能問題 |
| 可讀性 | 命名是否清楚、結構是否合理 |
| 測試 | 是否有適當測試覆蓋 |
| 規範 | 是否符合團隊規範 |

### 審查流程

- 每個 PR 至少需要 [填寫] 位審查者 Approve
- 審查回應時間：[填寫] 個工作天內
- 如有 Request Changes，作者應於 [填寫] 個工作天內回應

## 4.6 合併策略

| 情境 | 合併方式 | 說明 |
|------|---------|------|
| feature → develop | Squash Merge | 壓縮為單一 commit |
| release → main | Merge Commit | 保留完整歷史 |
| hotfix → main | Merge Commit | 保留修復紀錄 |

## 4.7 版本標籤

### 語義化版本 (SemVer)

```
MAJOR.MINOR.PATCH
```

| 版本變更 | 說明 | 範例 |
|---------|------|------|
| MAJOR | 不相容的 API 變更 | 1.0.0 → 2.0.0 |
| MINOR | 向後相容的功能新增 | 1.0.0 → 1.1.0 |
| PATCH | 向後相容的修復 | 1.0.0 → 1.0.1 |

### 標籤命名

```
v{MAJOR}.{MINOR}.{PATCH}
例: v1.2.3
```

---

**文件編號**: DEV-002  
**版本**: 1.0  
**最後更新**: YYYY-MM-DD
