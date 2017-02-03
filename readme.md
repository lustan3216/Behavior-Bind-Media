

##**何謂class行為化？ 何謂綁定media？**

「行為」就是指我要讓元素置中、往上往下、偏左、靠兩邊

假如你要讓div裡面的元素垂直置中且下移30px 則定義class為
```scss
.flex-vertical-center{
    display: flex;
    align-items: center;
}
.mt30{
    margin-top: 30px !improtant;
}
```
然後在html上
```html
<div class="flex-vertical-center mt30">
    <h3>Foo</h3>
    <h3>Bar/h3>
</div>
```
這樣Foo跟Bar 就會垂直置中且下移30px了


假如你只要讓【平板以上】(意即不含手機)作用，讓div裡面的元素垂直置中且下移30px 則定義class為
```scss
@media (min-width: $screen-sm-min) {
    .flex-vertical-center-sm{
        display: flex;
        align-items: center;
    }
    .mt30-sm{
        margin-top: 30px !improtant;
    }
}
```
##**為什麼要這樣？ 有什麼好處？**

1. 你一定遇過這狀況！! 假如定義登入或註冊的區塊class(模板)名字為.auth_wrapper，用著用著隔沒多久，設計師來了個稿，在使用者的編輯畫面也用到相同的模板，這時你要改class名字？
如果再取一個.user_edit_wrapper然後改成 .auth_wrapper,.user_edit_wrapper{ code } 呢？實務上絕對不會如此簡單，一定都會有些許地方要修改，工程師長卡在這種進退兩難的狀況。
    * 你不用為了該class或name想名字，想名字絕對是前端工程師最頭痛的點之一。

2. 假如你在首頁定義了第一塊是Banner，所以上了一個.banner的class，接著第二三個畫面也一樣，所以理所當然的沿用，當第四個畫面的Banner某個元素要垂直置中，
一般人的選擇是再多補一個只有這個地方能用的class或name，_但我想傳達的理念是直接上.flex-vertical-center的class_。

    * 當多個地方使用.banner該class時，你絕對會害怕改了某個小地方而引響到所有畫面，_但class行為化不會，因垂直置中的class裡面的語法理所當然是置中不會是置頂置左置右，mt30裡面其實是位移20px的情況
    * 如果你是很多個地方都要垂直置中，你必須多一個class或name，且須在css檔裡再寫一次垂直置中的語法，但如果照以上方式可以重複利用該行為化class。

3. 一般前端工程師會在 @media 下了一堆長長無用的class只是因為在定義CSS屬性時有權重覆蓋的問題，權重必須要比之前的權重相等或較大，所以常造成 @media 底下屬性不多但class卻一長串。
```scss
@media (max-width: 480px){
  .modal{
    .grouped.fields{
      .field{
        width: 50%;
        padding-left: 25px;
      }
    }
  }
}
```

而行為化綁定媒體的實際用法如下 
    
```html
tal  為Emmet簡寫 taxt-align:left;
tac  為Emmet簡寫 taxt-align:center;
mt30 為Emmet簡寫 margin-top:30px;

<div class="tal-sm tac-md mt30-sm mt50-md">
    <h3>Foo</h3>
    <h3>Bar/h3>
</div>

這樣就可表達出 Foo Bar 在平板時靠左且下移30px，在電腦版以上時置中且下移50px，完全不用再多寫任何CSS及class  
想像一下如果不是用行為化綁定媒體的方法你需要多寫多少東西？！
```

3. 可以應付設計師的設計缺陷，大部分設計畫面的設計師是“平面設計師”，對RWD及模組概念不多，所以需制定一個彈性的Library。常因設計師沒有模板概念導致每個頁面的版型不太相同，找不出規則製作模板。

4. 重複使用率高可以省code，一般接案設計師的案子很難模組化，這個情況下用此概念平均一個頁面可以省下約300行的CSS語法。

5. 維護修改變簡單。你不再需要去尋找CSS檔裡怎麼寫，不用再去語法寫在哪去哪改，不用再去查編譯出來的權重，因為一切都直接表達在class上。

##**簡單幾個SCSS檔就足夠應付所有大大小小畫面？**
需額外載入Boostrap以下三個 Component
* "bootstrap/variables"
* "bootstrap/utilities"
* "bootstrap/responsive-utilities"

且建議使用Boostrap Grid
* "bootstrap/grid"

是的，以上這些已能應付80%的前端複雜RWD畫面，tool.scss內是筆者在專案累積出來實用方法，可套用在專案上。
另外20%需靠工程師自行解決。


##**如何使用**
#####library內的用法目前包含 margin,padding,text-align,display
#####另外tool.scss內方法請自行參閱或自行增加

    用法解釋   *表示數字 數字可以是 0px,5px,15px,20px~~150px 以5為單位
    -------------------------------------------------------
            xs(320up) | sm(768up) | md(992up) | lg(1200up)
    -------------------------------------------------------
    mt*-xs     Yes    |    Yes    |    Yes    |    Yes
    mt         Yes    |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    mt*-sm     No     |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    mt*-md     No     |    No     |    Yes    |    Yes
    -------------------------------------------------------
    mt*-lg     No     |    No     |    No     |    Yes
    -------------------------------------------------------
    
            xs(320up) | sm(768up) | md(992up) | lg(1200up)
    -------------------------------------------------------
    tal-xs     Yes    |    Yes    |    Yes    |    Yes
    tal        Yes    |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    tal-sm     No     |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    tal-md     No     |    No     |    Yes    |    Yes
    -------------------------------------------------------
    tal-lg     No     |    No     |    No     |    Yes
    -------------------------------------------------------    
     Yes 表示有作用的區域 No表示沒作用的區域
      
     以下為範例 
     mt10 = mt10-xs = 手機版以上(所有media)作用 margin-top:10px 
     ml20-sm = 平板以上作用 margin-left:20px
     mb35-md = 電腦版以上作用 margin-bottom:35px
     mr100-lg = 大型螢幕以上作用 margin-right:100px
     mtn = mtn-xs = 手機版以上(所有media)作用 margin-top: 0px
     
     tac-sm = 平板以上作用 text-align:center
     tal-md = 電腦版以上作用 text-align:center
     tar-lg = 大型螢幕以上作用 text-align:center
     tan = tan-xs = 手機版以上(所有media)作用 text-align:inherit
     
     df-sm = 平板以上作用 display:flex
     dib-md = 電腦版以上作用 display:inline-block
     di-lg = 大型螢幕以上作用 display:inline
     db = db-xs = 手機版以上(所有media)作用  display:block
     
