### 12장 파이썬을 활용한 웹 크롤링 기초

* 파이썬의 기초적인 라이브러리를 활용해 웹 크롤링을 진행할 수 있습니다.

#### 1) 웹 페이지의 내용을 읽어 오기

* 특정한 웹 사이트의 내용은 모두 HTML 형식으로 작성되어 있습니다.
    * 개발자 도구(F12)를 실행하여 웹 페이지를 분석할 수 있습니다.
* requests 모듈을 사용하여 HTML 소스코드를 가져올 수 있습니다.

```
import requests

# 요청(Request) 객체를 생성합니다.
request = requests.get('http://dowellcomputer.com/main.jsp')

# 웹 사이트의 HTML 소스코드를 추출합니다.
html = request.text.strip()

print(html)
```

* 원하는 부분이 HTML 코드 상에서 어떤 부분인지 확인하기 위해 요소(element) 탐색기를 사용합니다.
* find() 메서드를 이용해 가장 먼저 등장하는 특정한 태그를 가져올 수 있습니다.
    * 웹 사이트 내에서 <b>최근 강의</b> 목록이 studyViewBox 클래스 안에 포함되어 있습니다.
    * 여러 개의 &lt;td&gt; 태그 내에서 &lt;a&gt; 태그가 내부에 포함된 태그만 접근합니다.

```
import requests
from bs4 import BeautifulSoup

# 요청(Request) 객체를 생성합니다.
request = requests.get('http://dowellcomputer.com/main.jsp')

# 웹 사이트의 HTML 소스코드를 추출합니다.
html = request.text.strip()

# HTML 소스코드를 파이썬 BeautifulSoup 객체로 변환합니다.
soup = BeautifulSoup(html, 'html.parser')

# 특정한 클래스 이름으로 접근합니다.
data = soup.find('div', class_='studyViewBox')

# <td> 태그 내부에서 <a> 태그를 포함하는 경우를 추출합니다.
data = data.select('td > a')

# 모든 링크에 하나씩 접근합니다.
for link in data:
    # 텍스트(글 제목) 부분만 출력합니다.
    print(link.text)
```

* 더 보기 좋게 출력되도록 코드를 조금 바꾸어 볼 수 있습니다.

```
import requests
from bs4 import BeautifulSoup

# 요청(Request) 객체를 생성합니다.
request = requests.get('http://dowellcomputer.com/main.jsp')

# 웹 사이트의 HTML 소스코드를 추출합니다.
html = request.text.strip()

# HTML 소스코드를 파이썬 BeautifulSoup 객체로 변환합니다.
soup = BeautifulSoup(html, 'html.parser')

# 특정한 클래스 이름으로 접근합니다.
data = soup.find('div', class_='studyViewBox')

# <tr> 태그를 추출합니다.
data = data.select('tr')[2:] # 첫 번째와 두 번째는 제외

# 각 게시글에 하나씩 접근합니다.
for i in range(len(data)): 
    print(f'[{i + 1}번째 최근 강의]')
    columns = data[i].select('td')
    print('선생님:', columns[0].text.strip())
    print('제목:', columns[1].text.strip())
    print('날짜:', columns[2].text.strip())
```

#### 2) 여러 개의 페이지에 걸쳐서 내용을 읽어 오기

* 여러 개의 페이지에 걸쳐서 글을 추출할 수 있습니다.
    * 게시판에서 페이지를 넘겨 가면서 최신 글 100개를 수집합니다.
    * 한 페이지당 10개의 글을 가지고 있다면, 총 10개의 페이지에 접근하면 됩니다.
* 특정한 게시물을 읽을 때 <b>글 번호</b>가 파라미터로 사용됩니다.
    * 각 게시물마다 글 번호를 이용해 <b>내용</b>에 접근한 뒤에 함께 

```
import requests
from bs4 import BeautifulSoup

URL = "http://dowellcomputer.com/talk/talkListForm.jsp"

# 1번째 페이지부터 10번째 페이지까지
for page in range(1, 11):
    current = URL + '?currentPage=' + str(page)
    print('현재 페이지:', current)
    
    # 요청(Request) 객체를 생성합니다.
    request = requests.get(current)

    # 웹 사이트의 HTML 소스코드를 추출합니다.
    html = request.text.strip()

    # HTML 소스코드를 파이썬 BeautifulSoup 객체로 변환합니다.
    soup = BeautifulSoup(html, 'html.parser')

    # 특정한 ID 이름으로 접근합니다.
    data = soup.find('div', id='viewBox')

    # <tr> 태그를 추출합니다.
    data = data.select('tr')[2:] # 첫 번째와 두 번째는 제외

    # 각 게시글에 하나씩 접근합니다.
    for i in range(len(data)): 
        columns = data[i].select('td')
        number = columns[0].text.strip()
        title = columns[3].text.strip()

        inside_URL = "http://dowellcomputer.com/talk/talkViewForm.jsp?talkID=" + number
        inside_request = requests.get(inside_URL)
        inside_html = inside_request.text.strip()
        inside_soup = BeautifulSoup(inside_html, 'html.parser')
        inside_data = inside_soup.find('div', id='viewBox')
        content = inside_data.select('tr')[4].select('td')[1].text

        print('글 번호:', number, '/ 제목:', title, '/ 내용:', content.strip())
```
