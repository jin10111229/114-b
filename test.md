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

---

## 使用案例 2：輸入與查詢成績 — 循序圖

```markdown
```mermaid
sequenceDiagram
    participant User as 使用者
    participant UI as 系統介面
    participant Grade as 成績模組
    participant DB as 資料庫

    User ->> UI: 輸入成績資料
    UI ->> Grade: 傳送成績資訊
    Grade ->> Grade: 驗證輸入格式
    Grade ->> DB: 儲存成績
    Grade ->> Grade: 計算平均分數
    DB -->> Grade: 儲存成功
    Grade -->> UI: 顯示平均與結果
    UI -->> User: 顯示成績查詢結果

### 活動圖 — 輸入與查詢成績

```markdown
```mermaid
flowchart TD
    A[開始] --> B[選擇課程]
    B --> C[輸入成績]
    C --> D{輸入格式正確?}
    D -- 否 --> E[提示重新輸入]
    D -- 是 --> F[儲存成績]
    F --> G[計算平均分數]
    G --> H[顯示成績與平均]
    H --> I[結束]

---

## 使用案例 3：接收上課提醒 — 循序圖

```markdown
```mermaid
sequenceDiagram
    participant User as 使用者
    participant Reminder as 提醒模組
    participant Schedule as 課程模組
    participant System as 通知服務

    User ->> Reminder: 設定提醒時間
    Schedule ->> Reminder: 傳送課程時間
    Reminder ->> System: 排程提醒通知
    System -->> User: 發送通知
    Schedule ->> Reminder: 若課程修改，更新提醒設定

### 活動圖 — 接收上課提醒

```markdown
```mermaid
flowchart TD
    A[開始] --> B[設定提醒時間]
    B --> C[系統比對課程時間]
    C --> D[建立提醒排程]
    D --> E{上課時間到?}
    E -- 否 --> D
    E -- 是 --> F[發送上課通知]
    F --> G[課程修改時自動更新提醒]
    G --> H[結束]

    }

    使用者 "1" --> "多" 課程 : 管理
    使用者 "1" --> "多" 成績 : 輸入/查詢
    使用者 "1" --> "多" 提醒 : 設定
    課程 "1" --> "1" 提醒 : 觸發提醒
