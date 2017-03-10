# 如何使用Python獲得Facebook的塗鴉牆資料

假如我們可以使用Python來處理網頁資料，我們是否也可以使用Python來擷取Facebook的塗鴉牆資料，這樣的好處可以有利於行銷人員、專案經理人、或者分析師可以更有效率的分析競爭品牌情報或者目前的與論風向，因此我們現在就要來介紹如何透過Python程式語言來幫助我們更優雅方便的獲得這些珍貴的資料內容。

過去我們可能需要借助一些工具來幫我們達成這項感覺有些許困難的工作，例如`scrapy`(網頁擷取工具)。然而Facebook目前已經針對許多開發者提供了很多友善的SDK工具，可以幫助我們用更少的力氣完成更多的事情。使用Facebook的`Graphic API`是一件相當方便的工具選擇，可以促使我們從各種Facebook的網頁節點擷取我們需要的資訊，例如`/page`可以取得粉絲專頁的資料，進而從`/feed`可以取得該粉專的塗鴉牆內容。

> [Facebook Graphic API documents](https://developers.facebook.com/docs/graph-api/reference)

## 從ID來存取單篇的內容，包含Likes、Comments

基於我們可以從兩個Nodes(`/page`,`/feeds`)來獲取相關的內容，我們可以從獲得的`ID`裡面來擷取我們需要知道的單篇內容，包含該內容中的`likes`以及`comments`等等。通常我們可以使用ID並且配合網址來查找該篇貼文的內容(使用瀏覽器即可)，例如:`https://www.facebook.com/5281959998_10150628170209999`，我們可以獲得貼文的主要文摘`message`，文章的超連結`link`，以及網頁名稱`name`，以及發布的文章類型`type`(是文章還是照片還是分享的內容)，最後還有使用者建立文摘的時間`create_time`。

然而其實在Facebook的官方API文件中，很少提及到如何獲取likes以及comments以及share的內容。幸運的是，我們已經在**stackoverflow**找到了一些可以處理這些問題的答案，你如果要知道這些訊息，你需要修改你的程式碼，例如`likes.limit(1).summary(true)` 而不是單純的使用like

奇怪的是，Facebook並不打算在查詢的API上做`任何的查詢速度限制`，因此在我們使用了100次的查詢後，我們並沒有感受到我們的查詢速度降低或者有相關性的影響。所以這樣的程式碼足以應付我們面對大多的使用情境。

現在我們可以選擇一些範例粉絲專業來測試看看我們的程式碼是否如我們想像的方便以及流暢


## 查詢Yahoo新聞的粉絲專業看看吧
![](./assets/yahoo_icon.jpg)  

```python
def testFacebookPageFeedData(page_id, access_token)
    
    #建構你的URL字串
    base = "https://graph.facebook.com/v2.4"
    node = "/" + page_id + "/feed" # changed
    parameters = "/?access_token=%s" %access_token
    url = base + node + parameters

    # 取得資料
    data = json.loads(request_until_succeed(url))
    
    print(json.dumps(data,indent=4,sort_key=True))

testFacebookPageFeedData(page_id, access_token)
```

如果你覺得要重複撰寫一樣的程式碼太過麻煩，建議你可以直接在`Github`上下載sample code，其中有包含沒一個抓取步驟地介紹以及使用方法，我強烈建議你可以先閱覽一番再進行。

首先，我們需要了解如何去存取Facebook的API，然而Facebook的API不是公眾使用，因此它需要透過`access token`來做為使用者認證。一般來說我們獲得的`access token`會很快就會過期，因此就正式開發的條件來說，我們不建議使用。然而我們可以透過一個小技巧來獲取更長時間的`access_token`,就是利用`APP ID`的方式，使用者可以在FB上面建立一個APP應用程式，我們可以因此獲得`App Secret`，透過`App Secret`你可以獲得一個永遠不會過期的`access token`，當然這會存在一些安全風險。因此我們建議您可以單獨創建一個APP來擷取資料，並且重設你的API Secret 如果你已經知道。

如果我們想要去擷取`Yahoo 新聞`的Fanpage 我們可以使用以下的`request`去拜訪該節點，拜訪的url如下: `https://graph.facebook.com/v2.4/nytimes?access_token=XXXXX`

add test to here:
