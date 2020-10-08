<img width="1277" alt="레이아웃" src="https://user-images.githubusercontent.com/48181483/95404244-77afac00-094f-11eb-935e-3229ac85f907.png">

위 이미지를 분석하며 퍼블리싱 해보겠습니다. 



규칙 1. css 클래스 네이밍은 케밥케이스 사용(css 자체가 소문자 + '-' 하이픈의 조합)

-> 문서 편집기에서도 하이픈 작동, 선언의 일관성,

​         2 css id 네이밍은 카멜케이스 사용()

자바스크립트 코드에 id 사용할일이 많으므로 (window.localStorage, document.querySelect)

3. chrome extension에 Web develop의 Display ruler 기능을 사용하여 너비,높이를 측정하였습니다

   ->고정형 px단위 사용


4. 아이콘은 fontaswome사용
5. '기능'이 없이 디자인용 div가 필요한 경우에는 container라고 명명



HTML 구조부터 작성해보았습니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>publishing</title>
    <link rel="stylesheet" href="./css/style.css">
</head>
<body>    
    <div class="container"><!--ⓐ-->
        <div class="main"> <!--ⓑ-->
            <header></header> <!--ⓒ-->
            <div class="profile"></div> <!--ⓓ-->
            <div class="name-card"></div> <!--ⓔ-->
            <div class="more-btn"></div> <!-- ⓕ-->
            <div class="direct-message"></div> <!--ⓖ-->
            <div class="another-page"></div> <!--ⓗ-->
        </div>
    </div>
 </body>

</html>
```

가장최상단의 하늘색(?)을 가장밖에 깔리는 배경으로 보았으나 body태그에 직접적으로 배경을 입히지 않기 위해 '디자인용' div를 만들어 container라고 네이밍하였습니다. ⓐ

안에 흰색을 메인컨텐츠로 ⓑ 높이에 따라 큰틀을 잡으며 메인콘텐츠에 포함되는 마크업을 진행하였습니다.

ⓒ에는 네비게이션과 글쓰기(?)로 분석되는 컨텐츠가 들어갈 예정이며

ⓓ에는 프로필(사진), ⓔ에는 명함 + 자기소개 ⓕ더보기버튼 ⓖ페이스북/메일등 DM ⓗ다른 웹사이트로 

이동 기능을 넣을 예정으로 마크업을 1차 완료하였습니다.

```css
@charset 'utf-8';

*{
    margin:0px;
    padding:0px;
}

ol,ul{
    list-style: none;
}

a{
    text-decoration: none;
}

body .container{
    background-color: skyblue;
    padding:25px;
}

.container .main{
    background-color: white;
    width:380px;
    height:610px;
    margin: 0px auto;
}

.main header{
    background-color: red;
    height:50px;
}

.main .profile{
    background-color: orange;
    height:220px;
}

.main .name-card{
    background-color: yellow;
    height:70px;
}

.main .more-btn{
    background-color: green;
    height:60px;
}

.main .direct-message{
    background-color: blue;
    height:90px;
}

.main .another-page{
    background-color: purple;
    height:60px;
}

```



.container 위의 코드들은 reset.css의 일부만 사용하였습니다.



모든 css선택자는 가장가까운 부모+자신의 조합으로 작성해서 우선순위를 높이되,  길어지지 않게하였고 (좋은지 의문이 듭니다 나중에 변경될 수 있음)



<img width="1277" alt="initial layout" src="https://user-images.githubusercontent.com/48181483/95405381-96637200-0952-11eb-904d-db799bdc5229.png">



body태그에 직접적으로 background속성을 사용하지 않으려는 시도 때문에 container의 높이가 자식의 main태그들의 높이의 합을 자동으로 계산하여 영역을 유지하기 때문에 배경전체를 뒤덮지는 못했습니다( 추후 해결할문제)





header태그 배치를 위해



```html
<head>
  <script src="https://kit.fontawesome.com/e417ed1b75.js"crossorigin="anonymous"></script>
</head>


...
<header>
    <div class="header-content-container">
        <div class="navigation">
            <i class="fas fa-align-justify"></i>
        </div>
        <div class="write"></i>
        <i class="far fa-sticky-note"></i>
    </div>
    </div>
</header>
...
```

네비게이션과 쓰기 기능을 배치해야하는데 레이아웃 배치를 위해 컨테이너로 감싼후



```css
...
.main header{
    background-color: red;
    height:50px;
    padding:30px;
    box-sizing: border-box;
}
.main header .navigation{
    background-color: pink;
    float:left;
    font-size:20px;
}

.main header .write{
    background-color: aqua;
    float:right;
    font-size:20px;
}

main header .header-content-container::before{
    content: '';
    clear : both;
    display: block;
}
...
```



navigation에는 float left, write에는 float right준후 header-content-container에 플로팅을 해제하였습니다.  그후 안에 폰트어썸 라이브러리의 아이콘을 사용해 넣어주었는데 나중에 특정 기능을 추가할 수 있을 것 같아 div로 감싸주었고 이는 다른태그로의 전환 또는 이벤트등을 추가할 수 있을 것 같습니다 ( 수정할 수 도있습니다 div없애는 방향으로)

폰트어썸 아이콘이기 때문에 font-size로 크기조절 가능합니다.



각각 레이아웃 배치를 위해 padding으로 위치조절 및 박스상자가 늘어나는것을 방지하기위해

box-sing: border box와 (전역 유지보수 예약)

padding:30px을 주었습니다



<img width="1277" alt="header" src="https://user-images.githubusercontent.com/48181483/95412359-c7986e00-0963-11eb-8b1e-2a4fd27a6e56.png">









```css
...
.main .profile{
    background-color: orange;
    height:220px;
    width:200px;
    border-radius: 100px;
    margin: 0px auto;
    box-shadow: 8px 9px 11px blue;
}
...
```



profile영역 레이아웃을 위해 높이에 비례하여 radius속성으로 원 레이아웃을 구성한후,

가운데 정렬 및 box-shadow 속성으로 그림자 레이아웃을 잡아두었습니다

<img width="1277" alt="profile" src="https://user-images.githubusercontent.com/48181483/95412226-78523d80-0963-11eb-9ac9-5170cdd87ef4.png">

---



```css
.main .name-card{
    background-color: yellow;
    height:70px;
    padding-top:15px;
}

.name-card div{
    text-align: center;
}
```

name-card 영역을 레이아웃하기 위해

아래에 이름칸과 소개칸용 div를 만들어두고, 컨텐츠만 가운데 정렬을 위해 text-align 속성을 사용하였고 profile과의 여백을 위해 padding-top속성을 사용하였습니다 배경이 사라지면 여백이 느껴질것입니다.

<img width="1277" alt="name-card" src="https://user-images.githubusercontent.com/48181483/95412183-56f15180-0963-11eb-95bb-e264f60d9a34.png">

---

```html
...
<div class="more-btn">
    <button>view more</button>
</div>
...
```

```css
.main .more-btn{
    background-color: green;
    height:60px;
    padding-top:15px;
}

.more-btn button{
    background-color: white;
    text-align: center;
    width: 175px;
    height:30px;
    display:block;
    margin:0px auto;
    box-shadow: 15px 10px 45px white;
    text-shadow:0px 0px 1rem black;
}
```

더보기 버튼 영역을 위해 마크업을 추가한후, 

글자 가로 가운데정렬, 버튼 가로가운데정렬, 글자와 박스 모두 쉐도우를 주었습니다.



<img width="1277" alt="view mor btn" src="https://user-images.githubusercontent.com/48181483/95412114-2b6e6700-0963-11eb-9d62-294714a0ef8e.png">

---

```html
...
<div class="direct-message">
    <div>
        <button><i class="fab fa-facebook"></i>Visit My Facebook page</button>
    </div>
    <div class="email">
        <button><i class="far fa-envelope"></i>hadaboni80@naver.com</button>
    </div>
</div>
```

```css
.main .direct-message{
    background-color: blue;
    height:90px;
    padding:0px 30px;;
    box-sizing: border-box;
}

.direct-message div{
    height: 40px;
    background-color: #fff;
    text-align: center;
    line-height: 40px;
    font-size:16px;
}

.direct-message .email{
    border-top: 1px solid darkblue
}

.direct-message button{
    background-color: #fff;
}

.direct-message i{
    margin-right: 10px;
}
```



direct-message 영역 layout을 위해 div를 2개만들어서 각자의 높이를 주고 세로 가운데 정렬과 글자 가로 가운데 정렬한후

아랫div의 border-top속성만 주어서 구분선을 만들었습니다 아이콘과 메시지를 보낼것이라 예상되어 버튼 태그로 구성하였고

버튼의 외곽선 문제가 발생하였습니다.



![image-20201008135229395](C:\Users\82109\AppData\Roaming\Typora\typora-user-images\image-20201008135229395.png)

