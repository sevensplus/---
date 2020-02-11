## 部落格實作
1. 產品規劃
- 前台
    - index.php 所有文章
    - article.php?id=x 單一文章
    - about.php 關於我
- 後台
    - admin.php 後台管理頁面
    - add.php 新增文章；handle_add.php 處理新增文章
    - update.php 修改文章；handle_update.php 處理修改
    - delete.php 刪除文章

    - admin__category.php 管理種類
    - add__category.php 新增種類；handle__category__add.php 處理修改
    - update__category.php 更新種類；handle__category__update.php 處理更新
    - delete__category.php 刪除種類


2. 資料結構與 database
- 文章
    - id
    - title
    - content
    - category_id
    - create_at

- 分類
    - category_id 
    - name
3. 後台：分類管理
- conn.php
- admin.php

4. 後台：文章管理
5. 前台：部落格頁面
6. 串接資料
7. 新增草稿
8. 關於我頁面管理
9. 評論功能
10. 多個分類
11. 搜尋功能