## UML 類別圖

```mermaid
%% UML 類別圖
classDiagram
    class 使用者 {
        +登入()
        +登出()
    }

    class 課程 {
        +課名
        +時間
        +地點
        +新增課程()
        +修改課程()
        +刪除課程()
        +檢查重疊()
    }

    class 成績 {
        +科目
        +分數
        +平均分數
        +輸入成績()
        +計算平均()
        +查詢成績()
    }

    class 提醒 {
        +提醒時間
        +通知內容
        +設定提醒()
        +發送提醒()
        +更新提醒()


---

## 使用案例 1：管理課表 — 循序圖

```markdown
```mermaid
sequenceDiagram
    participant User as 使用者
    participant UI as 系統介面
    participant Course as 課程模組
    participant DB as 資料庫

    User ->> UI: 新增/編輯/刪除課程
    UI ->> Course: 傳送課程資料
    Course ->> Course: 檢查時間重疊
    Course ->> DB: 更新課表資料
    DB -->> Course: 回傳成功狀態
    Course -->> UI: 顯示更新結果
    UI -->> User: 顯示課表更新成功

### 活動圖 — 管理課表

```markdown
```mermaid
flowchart TD
    A[開始] --> B[登入系統]
    B --> C[新增/編輯/刪除課程]
    C --> D{時間是否重疊?}
    D -- 是 --> E[提示錯誤訊息]
    D -- 否 --> F[更新課表資料庫]
    F --> G[顯示更新結果]
    G --> H[結束]

