# 如何使用Python獲得Facebook的塗鴉牆資料

假如我們可以使用Python來處理網頁資料，我們是否也可以使用Python來擷取Facebook的塗鴉牆資料，這樣的好處可以有利於行銷人員、專案經理人、或者分析師可以更有效率的分析競爭品牌情報或者目前的與論風向，因此我們現在就要來介紹如何透過Python程式語言來幫助我們更優雅方便的獲得這些珍貴的資料內容。

過去我們可能需要借助一些工具來幫我們達成這項感覺有些許困難的工作，例如`scrapy`(網頁擷取工具)。然而Facebook目前已經針對許多開發者提供了很多友善的SDK工具，可以幫助我們用更少的力氣完成更多的事情。使用Facebook的`Graphic API`是一件相當方便的工具選擇，可以促使我們從各種Facebook的網頁節點擷取我們需要的資訊，例如`/page`可以取得粉絲專頁的資料，進而從`/feed`可以取得該粉專的塗鴉牆內容。

> [Facebook Graphic API documents](https://developers.facebook.com/docs/graph-api/reference)

## 從ID來存取單篇的內容，包含Likes、Comments

基於我們可以從兩個Nodes(`/page`,`/feeds`)來獲取相關的內容，我們可以從獲得的`ID`裡面來擷取我們需要知道的單篇內容，包含該內容中的`likes`以及`comments`等等。通常我們可以使用ID並且配合網址來查找該篇貼文的內容(使用瀏覽器即可)，例如:https://www.facebook.com/5281959998_10150628170209999，我們可以獲得貼文的主要文摘`message`，文章的超連結`link`，以及網頁名稱`name`，以及發布的文章類型`type`(是文章還是照片還是分享的內容)，最後還有使用者建立文摘的時間`create_time`。
