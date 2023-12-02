---
title: "[freeCodeCamp筆記]Basic HTML and HTML5"
categories: 
    - Web
tags: 
    - Web
    - freeCodeCamp
---

基礎html跟html5的筆記

## Basic HTML and HTML5
* 標題(由大到小)
    ```html
    <h1></h1>
    <h2></h2>
    <h3></h3>
    <h4></h4>
    <h5></h5>
    <h6></h6>
    ```
* 段落
    ```html
    <p></p>
    ```
* 註解
    ```html
    <!--
    <p></p>
    -->
    ```
* html5 tag
    ```html
    <main></main>
    <header></header>
    <footer></footer>
    <nav></nav>
    <video></video>
    <article></article>
    <section></section>
    ```
* 圖片
    ```html
    <img src="圖片的網址" alt="圖片的名稱">
    ```
    圖片後面不需要用`</img>`來當作結尾
* 連結
    ```html
    <a href="連結的網址"></a>
    <p><a href="連結的網址"></a></p>
    <!-- 跳連結到有這個id的位置 -->
    <a href="#contacts-header"></a>
    <!-- target是點連結後的動作，_blank是開啟新分頁 -->
    <a href="連結的網址" target="_blank"></a>
    <!-- 把圖片變成連結，href="#"是製作無效的連結 -->
    <a href="#"><img src="圖片的連結" alt="圖片的名稱"></a>
    
    <h2 id="contacts-header">Contacts</h2>
    ```
* list
    ```html
    <!-- 無序的list -->
    <ul>
        <li>milk</li>
        <li>cheese</li>
    </ul>
    
    <!-- 有序的list -->
    <ol>
        <li>Garfield</li>
        <li>Sylvester</li>
    </ol>
    ```
* Text Field
    ```html
    <!-- 產生一個輸入欄位 -->
    <input type="text">
    <!-- 輸入欄位中間要出現字 -->
    <input type="text" placeholder="cat photo URL">
    ```
* Form
    ```html
    <!-- form表單是用來跟後端做溝通的 -->
    <form action="https://www.freecatphotoapp.com/submit-cat-photo" method="GET">
        <!-- 後端要接收到的欄位，加上required代表說一定要填寫這個欄位 -->
        <input type="text" placeholder="cat photo URL" name="catPhotoURL" required>
        <!-- 確認表單輸出的按鈕 -->
        <button type="submit">Submit</button>
    </form>
    ```
    
    這邊補充一些form的知識[參考連結](https://medium.com/johnny%E7%9A%84%E8%BD%89%E8%81%B7%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%AD%86%E8%A8%98/node-js-html-form%E5%A6%82%E4%BD%95%E8%A8%AD%E8%A8%88-get%E5%92%8Cpost%E6%96%B9%E6%B3%95%E7%9A%84%E4%B8%8D%E5%90%8C-%E5%A6%82%E4%BD%95%E9%80%8F%E9%81%8Eexpress-req-query-req-body%E5%8F%96%E5%BE%97%E8%B3%87%E6%96%99-fa43bd73909d)
    * action指的是使用者按下送出後，資料會被送往哪個網址/頁面。注意不是使用者會被「帶到」哪個網址，按下送出後會發生的事是由後端決定的，跟HTML的屬性沒有關係
    * method有GET和POST，不寫的話預設是GET。
    * button要寫type=”submit”來告訴表單這個按鈕負責送出資料，如果沒有寫，也會預設是submit，但如果寫type=”button”，按下去就沒有任何效果。一般建議還是把它標示清楚。另外要注意，如果button寫在form外面，也不會有任何效果。
    * button:submit也可以用input:submit來替代: `<input type="submit" value="Submit">`
    * input的name attribute非常重要，在傳送資料到後端時，他會是資料的key，input的值則會是value。
* Radio buttons and Checkboxes
    ```html
    <!-- Radio buttons -->
    <label for="indoor">
        <input id="indoor" type="radio" name="indoor-outdoor">Indoor
    </label>
    <label for="outdoor">
        <input id="outdoor" type="radio" name="indoor-outdoor">Outdoor
    </label>
    ```
    Radio buttons是只說如果有很多選項要給使用者選擇的時候可以使用，重點是只能選擇一項，而不是多選，只要input的name是一樣的時候，使用者就只能選擇一個項目，label的用意是需不需要點到前面的圓圈，如果有加上label的話，只要點到字就可以了
    ```html
    <!-- Checkboxes -->
    <label for="test1"><input id="test1" type="checkbox" name="personality"> 1</label>
    <label for="test2"><input id="test2" type="checkbox" name="personality"> 2</label>
    <label for="test3"><input id="test3" type="checkbox" name="personality"> 3</label>
    ```
    Checkbox的使用時機是再多選的時候，基本用法大致上和Radio button差不多
    ```html
    <!-- value -->
    <!-- 再選項後面加上checked可以預設選擇某個欄位 -->
    <label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" checked> Indoor</label>
    <label for="outdoor"><input id="outdoor" type="radio" name="indoor-outdoor" value="outdoor"> Outdoor</label><br>
    <label for="loving"><input id="loving" type="checkbox" name="personality" value="loving" checked> Loving</label>
    <label for="lazy"><input id="lazy" type="checkbox" name="personality" value="lazy"> Lazy</label>
    <label for="energetic"><input id="energetic" type="checkbox" name="personality" value="energetic"> Energetic</label><br>
    ```
    當按下submit後，會把選擇的內容傳送到後端，這個時候後端要判斷送過去的資料是什麼的時候，就要使用value這個值。以Radio button為例，name叫做indoor-outdoor，如果沒有給value的話，預設會取得的值為indoor-outdoor=on，但是如果有設定value的話，後端才會取得indoor-outdoor=indoor。
* div元素
    ```html
    <!-- div -->
    <div></div>
    ```
    div是division的縮寫，主要是用來分配網站中的不同區塊，可以將其他元素包在這個元素中。
* Doctype
    ```html
    <!DOCTYPE html>
    <html>
      <h1>Hello</h1>
    </html>
    ```
    這個宣告是要告訴網頁使用最新版的html，有兩個重點
    1. 前面一定要加`!`
    2. DOCTYPE一定要大寫
    
    網頁中的全部資料都要包在兩個html的標籤中
* head跟body
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta />
      </head>
      <body>
        <div>
        </div>
      </body>
    </html>
    ```
    網站中的information都要寫在head中，包含link、meta、title、style，網站的內容才寫在body