

```
import requests

# 요청(Request) 객체를 생성합니다.
request = requests.get('http://dowellcomputer.com/main.jsp')

# 웹 사이트의 HTML 소스코드를 추출합니다.
html = request.text.strip()

print(html)
```


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
