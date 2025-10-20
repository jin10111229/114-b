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
    }

    使用者 "1" --> "多" 課程 : 管理
    使用者 "1" --> "多" 成績 : 輸入/查詢
    使用者 "1" --> "多" 提醒 : 設定
    課程 "1" --> "1" 提醒 : 觸發提醒

## 使用案例1：管理課表（循序圖）

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
