# myCat
🐈🐈‍⬛ 수업에서 들은 Sass를 이용하여 고양이 반응형 랜딩페이지 만들어보았습니다.

[🔗 Git pages 보러가기](https://jaycode-git.github.io/myCat/)

## 1. 변수 설정
``` scss
// size
$width : min(100%, 1320px);
$size: 10px, 20px, 30px, 40px, 50px, 60px, 70px, 80px, 90px, 100px, 110px, 120px;

// color
$primary : #5288D9;
$secondary : #6882a7;
$thirdary : #e7edf3;
$b : black;
$w : white;
$g : #767676;
$blue : #263140;


// display
$display: (
  "b":block,
  "ib":inline-block,
  "i":inline,
  "f":flex,
  "g":grid
);


// font
$family : 'Spoqa Han Sans Neo',
'sans-serif';
$font-size: (
  "h2":clamp(24px, 4vw, 48px),
  "h3":clamp(24px, 4vw, 36px),
  "p":clamp(14px, 4vw, 16px),
  "desc":14px
);
$font-weight: (
  "b":700,
  "m":400,
);

// String
$path : '../img/';
```

## 2. Mixin
``` scss
// mixin Background url
@mixin bg($name, $color: null, $size: center, $position: cover, $repeat : no-repeat) {
  background: $color url($path + $name)$repeat $size/$position;
  @content;
}


// mixin Pseudo content
@mixin pseudo($content: '') {
  content: $content;
  @content;
}


// mixin Margin Auto
@mixin m-auto($top: 0, $bottom: null) {
  @content;

  @if($top ==0) {
    margin: 0 auto;
  }

  @else {
    margin: $top auto $bottom;
  }
}

// mixin Flex
@mixin flex($align: null, $way: row) {
  display: flex;
  flex-direction: $way;
  @content;

  @if(#{$align}=='center') {
    justify-content: center;
    align-items: center;
  }

  @else if (#{$align}=='leftCenter') {
    align-items: center;
  }

  @else if (#{$align}=='spaceCenter') {
    justify-content: space-between;
    align-items: center;
  }

  @else if (#{$align}=='space') {
    justify-content: space-between;
  }
}

// mixin mediaQuery
$media-pc: 1024px;
$media-tab: 768px;
$media-m-lg: 425px;
$media-m-sm: 375px;

@mixin media($size) {

  @if $size=='m-sm' {
    @media (max-width:$media-m-sm) {
      @content;
    }
  }

  @else if $size=='m-lg' {
    @media (max-width:$media-m-lg) {
      @content;
    }
  }

  @else if $size=='tab' {
    @media (max-width:$media-tab) {
      @content;
    }
  }

  @else if $size=='pc' {
    @media (max-width:$media-pc) {
      @content;
    }
  }

  @else {
    @media (max-width:$size) {
      @content;
    }
  }
}
```

## 3. Components
``` Scss

.wrapper {
  width: $width;
  height: 100%;
  @include m-auto(0);
  padding: 0 nth($size, 2);
}

a[class^='btn'],
button[class^='btn'] {
  background: $primary;
  color: $w;
  font-size: map-get($font-size, "p");
  padding: clamp(10px, 2vw, 15px) clamp(24px, 2vw, nth($size, 3));
  cursor: pointer;
  border: none;
  border-radius: nth($size, 4);
  -webkit-border-radius: nth($size, 4);
  -moz-border-radius: nth($size, 4);
  -ms-border-radius: nth($size, 4);
  -o-border-radius: nth($size, 4);

  &:hover {
    box-shadow: inset 0 10px 0 0 rgba(0, 0, 0, .2)
  }
}
```