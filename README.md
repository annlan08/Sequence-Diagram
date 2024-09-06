![image](https://github.com/user-attachments/assets/c9748f30-e05c-4942-a04c-e2e72fdc849f)# Sequence-Diagram
使用VSCode產出循序圖所需套件(Extensions)及範例代碼

## 安裝所需套件
- Markdown Preview Enhanced (必)
- One Dark Pro
- Markdown All in One
- Markdownlint
- Mermaid Markdown Syntax Highlighting SQL 擴展套件

範例
```
```mermaid

sequenceDiagram

    

    Hangfire主機->>HTML圖片產生機器 : 1.呼叫執行照片製作
    activate Hangfire主機

    HTML圖片產生機器->>ET.HouseAI : 取得物件資訊及照片
    ET.HouseAI-->>DB.Rehouse : 存入取得物件資訊內容用以製作語音
    Note left of DB.Rehouse : 此處將所有被選定的物件資料<br>事先存放進資料庫中，以利製<br>作影片
    ET.HouseAI->>HTML圖片產生機器 : 回傳物件資訊及照片
    HTML圖片產生機器->>ET.HouseAI : 儲存的製作完成圖片
    ET.HouseAI-->>NAS.FileCenter : 上傳圖片檔案

    HTML圖片產生機器->>Hangfire主機 : 圖片製作完成
    deactivate Hangfire主機

    Hangfire主機->>ET.HouseAI : 2.請求製作導覽語音
    activate Hangfire主機

    ET.HouseAI-->>DB.Rehouse : 取得物件資訊內容用以製作語音
    Note left of DB.Rehouse : 使用先前存入的資料表<br>的資料作為依據
    DB.Rehouse-->>ET.HouseAI : 回傳用於製作語音的內容
    ET.HouseAI-->>NAS.FileCenter : 上傳語音檔案

    ET.HouseAI->>Hangfire主機 : 音訊製作完成
    deactivate Hangfire主機

    Hangfire主機->>影片製作機器 : 3.請求製作影片
    activate Hangfire主機

    影片製作機器->>ET.HouseAI : 請求所有圖片及音訊檔案
    ET.HouseAI-->>NAS.FileCenter : 取得所有圖片及音訊檔案
    NAS.FileCenter-->>ET.HouseAI : 回傳對應圖片及音訊檔案
    ET.HouseAI->>影片製作機器 : 回傳所有圖片及音訊檔案
    影片製作機器->>ET.HouseAI : 製作完成的影片
    ET.HouseAI-->>AWSS3影片存放庫 : 上傳影片檔案

    影片製作機器->>Hangfire主機 : 完成影片製作
    deactivate Hangfire主機
```
```





