### 11장 웹 사이트 구성 요소 핵심 요약

* 파이썬을 이용해 웹 사이트에서 다양한 데이터를 가져올 수 있습니다.
* 성공적인 웹 자동화를 위해서 웹 사이트가 어떻게 구성되는지 이해할 필요가 있습니다.

#### 1) HTML이란?

* HTML(Hypertext Markup Language): 웹 문서를 작성하기 위해 사용하는 언어입니다.
    * HTML 파일은 간단히 설명하자면 한 페이지의 문서와 같습니다.
* HTML 문서는 일반적으로 태그(tag)를 사용해 작성합니다.
    * HTML 문서는 &lt;HTML&gt; 태그로 시작하고 &lt;/HTML&gt; 태그로 종료합니다.
    * &lt;HEAD&gt; 태그는 웹 사이트의 제목이나 메타 정보 등을 포함합니다.
    * &lt;BODY&gt; 태그는 실질적으로 웹 문서의 내용을 보여줍니다.

<img src="/figures/1.jpg" width="400px">

* 일반적으로 웹 서버는 다양한 HTML 문서를 포함합니다.
    * 한 번 자기소개서 웹 사이트의 URL이 있다고 가정합시다.
    * 웹 브라우저로 해당 웹 사이트의 a.html 문서에 접근할 때는 다음과 같습니다.

<img src="/figures/2.jpg" width="560px">

#### 2) 간단한 웹 사이트 만들어 보기

* HTML 문서를 작성한 뒤에 .html 확장자를 갖도록 합니다.
    * 일반적인 컴퓨터에서 HTML 문서는 바로 웹 브라우저를 통해 실행됩니다.
    * &lt;meta&gt; 태그의 UTF-8 인코딩: 한글과 같은 유니코드 문자열을 정상적으로 출력합니다.

```
<!DOCYTYPE HTML>
<html>
    <head>
        <title>기본적인 HTML 문서</title>
        <meta charset="UTF-8">
    </head>
    <body>
        기본적인 HTML 문서를 작성해 봅시다.
    </body>
</html>
```

#### 2) HTML의 다양한 태그 사용해 보기

* HTML을 구성하는 4가지 구성 요소에 대해 알아봅시다.
    1. 요소(element): HTML에서 사용되는 명령어를 의미합니다.
    2. 태그(tag): HTML 요소를 표현하기 위한 방법으로, 문서에 내용을 출력합니다.
    3. 속성(attribute): 태그를 더 구체적으로 표현합니다.
    4. 변수(value): 속성에 적용되는 값을 의미합니다.

* 제목(heading)
    * 제목을 얼마나 크게 표현할 것인지에 따라서 &lt;h1&gt;부터 &lt;h6&gt;까지 요소가 존재합니다.

```
<!DOCYTYPE HTML>
<html>
    <head>
        <title>기본적인 HTML 문서</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <h1>문서의 제목 1</h1>
        <h2>문서의 제목 2</h2>
        <h3>문서의 제목 3</h3>
        <h4>문서의 제목 4</h4>
        기본적인 HTML 문서를 작성해 봅시다.
    </body>
</html>
```

* 문단(paragraph)
    * &lt;p&gt; 태그는 기본적으로 문단을 작성할 때 사용하는 태그로, 자동으로 문서 내에 약간의 여백이 적용됩니다.

```
<!DOCYTYPE HTML>
<html>
    <head>
        <title>기본적인 HTML 문서</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <h1>파이썬이란?</h1>
        <p>파이썬은 쉽게 시작할 수 있는 프로그래밍 언어 중 하나입니다. 파이썬은 다음의 순서로 배우면 좋습니다.</p>
        <h1>HTML이란?</h1>
        <p>HTML은 웹 페이지를 작성하기 위한 마크업 언어 중 하나입니다. HTML 구성 요소는 다음과 같습니다.</p>
    </body>
</html>
```

* 리스트(list)
    * 특정한 항목들을 나열하여 표현할 수 있습니다.
    * 순서가 있는 리스트(ordered list)는 &lt;ol&gt; 태그를 사용합니다.
    * 순서가 없는 리스트(unordered list)는 &lt;ul&gt; 태그를 사용합니다.

```
<!DOCYTYPE HTML>
<html>
    <head>
        <title>기본적인 HTML 문서</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <h1>파이썬이란?</h1>
        <p>파이썬은 쉽게 시작할 수 있는 프로그래밍 언어 중 하나입니다. 파이썬은 다음의 순서로 배우면 좋습니다.</p>
        <ol>
            <li>표준 입출력</li>
            <li>수 자료형</li>
            <li>문자열 자료형</li>
            <li>리스트 자료형</li>
            <li>조건문</li>
            <li>반복문</li>
        </ol>
        <h1>HTML이란?</h1>
        <p>HTML은 웹 페이지를 작성하기 위한 마크업 언어 중 하나입니다. HTML 구성 요소는 다음과 같습니다.</p>
        <ul>
            <li>요소(element)</li>
            <li>태그(tag)</li>
            <li>속성(attribute)</li>
            <li>변수(value)</li>
        </ul>
    </body>
</html>
```

* 링크(link)
    * &lt;a&gt; 태그는 다른 웹 문서로 넘어갈 수 있도록 해주는 링크(link) 기능을 제공합니다.

```
<!DOCYTYPE HTML>
<html>
    <head>
        <title>기본적인 HTML 문서</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <h1>파이썬이란?</h1>
        <p>파이썬은 쉽게 시작할 수 있는 프로그래밍 언어 중 하나입니다. 파이썬은 다음의 순서로 배우면 좋습니다.</p>
        <ol>
            <li>표준 입출력</li>
            <li>수 자료형</li>
            <li>문자열 자료형</li>
            <li>리스트 자료형</li>
            <li>조건문</li>
            <li>반복문</li>
        </ol>
        <h1>HTML이란?</h1>
        <p>HTML은 웹 페이지를 작성하기 위한 마크업 언어 중 하나입니다. HTML 구성 요소는 다음과 같습니다.</p>
        <ul>
            <li>요소(element)</li>
            <li>태그(tag)</li>
            <li>속성(attribute)</li>
            <li>변수(value)</li>
        </ul>
        <a href="https://www.google.com/">구글(Google)</a>
        <a href="https://www.facebook.com/">페이스북(Facebook)</a>
    </body>
</html>
```
