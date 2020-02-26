## Session
### Session 是什麼
- Session：以登入來說，在網站後端，會有session id（亂碼）和內容（用戶名）
- cookie：瀏覽器存資料的地方
- 登入後 → server回傳response，要求瀏覽器內放入id（如h9wr03j0）→ 瀏覽下一頁、發送request時，瀏覽器會自動帶上id值 → server查詢後找到資料，確定身分。
- 有點像是申請（登入）、確認（登入成功）、發放識別證（cookie紀錄id）的概念

-----

## Cookie
### 為什麼要有 cookie

### Cookie 是什麼

-----

## Cache
- 緩存、暫存，CPU、瀏覽器、Server side 都可能有
- 讀取：從記憶體、資料庫、硬碟(讀取速度快到慢)
- 當要求資料不用很精確(或隨時更新)的時候，可以把東西存起來隨時讓人讀取，就不用每次都拿一遍資料，比較有效率
- [循序漸進理解 HTTP Cache by huli](https://blog.techbridge.cc/2017/06/17/cache-introduction/)


-----
## 比較
cookie：是伺服器傳送給使用者的片段，通常用來記錄登入狀態。每次向網站提交 request 時會帶上
sessionStorage：僅在當前有效，關閉網頁會被清除。
localStorage：通常是永久保存。