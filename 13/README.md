### 셀레니움(Selenium)을 활용한 웹 크롤링

* 웹에 있는 정보를 자동으로 수집하기 위해서 셀레니움(Selenium)을 사용할 수 있습니다. 
* 셀레니움을 사용하면 좋은 상황은 다음과 같습니다.
    * 웹 사이트에 로그인을 한 뒤에 데이터를 가져와야 하는 경우
    * 기본적인 크롤링 라이브러리로 웹 사이트에 접근할 수 없는 경우

#### 1) 셀레니움(Selenium) 라이브러리 설치

* 파이썬에서 pip 명령어를 사용하여 간단히 셀레니움(Selenium)을 설치할 수 있습니다.

<pre>
pip install selenium
</pre>

#### 2) 웹 브라우저 드라이버 다운로드

* 셀레니움은 웹 브라우저를 직접적으로 조작하므로, 적절한 브라우저 드라이버를 설치할 필요가 있습니다.
* 일반적으로 웹 사이트 접속을 위해 가장 많이 사용하는 브라우저로 크롬(Chrome) 브라우저가 있습니다.
* 크롬 브라우저 설치: https://www.google.com/intl/ko/chrome/
* 크롬 드라이버 설치: https://chromedriver.chromium.org/home/
    * 크롬 드라이버(Chrome Driver)는 파이썬 프로그램과 같은 폴더에 놓아주세요.
* 다음의 코드로 크롬 브라우저를 실행할 수 있습니다.

<pre>
from selenium import webdriver

browser = webdriver.Chrome('./chromedriver')
</pre>

#### 3) 셀레니움(Selenium)으로 특정 웹 사이트 접속하기

* 셀레니움을 활용해 특정한 웹 사이트에 접속할 때는 get() 메서드를 사용합니다.

<pre>
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)
</pre>

#### 4) 셀레니움(Selenium)을 활용한 자동 로그인

* 셀레니움의 다양한 메서드를 사용하여 HTML 문서의 각 요소에 접근할 수 있습니다.
    * find_elements_by_id(): HTML 문서의 id 속성을 이용하여 접근하기
    * find_elements_by_name(): HTML 문서의 name 속성을 이용하여 접근
    * find_elements_by_class_name(): HTML 문서의 class 속성을 이용하여 접근
* 텍스트를 작성할 때는 send_keys() 메서드를 사용합니다.

<pre>
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_elements_by_name("memberID")
password = browser.find_elements_by_name("memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id[0].send_keys("pyautogui")
password[0].send_keys("pyautogui")
</pre>

* <b>코드 업데이트</b>

<pre>
from selenium.webdriver.chrome.service import Service
from selenium import webdriver
import time

path = "./chromedriver.exe"

service = Service(executable_path=path)
browser = webdriver.Chrome(service=service)

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_element("name", "memberID")
password = browser.find_element("name", "memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id.send_keys("pyautogui")
password.send_keys("pyautogui")

time.sleep(120)
</pre>

* 일반적으로 버튼을 클릭할 때는 셀레니움(Selenium)에서 XPath를 사용합니다.
     * 개발자 도구(F12)를 연 뒤에, 우리가 원하는 버튼의 HTML 코드의 XPath를 복사합니다.

<pre>
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_elements_by_name("memberID")
password = browser.find_elements_by_name("memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id[0].send_keys("pyautogui")
password[0].send_keys("pyautogui")

# XPath로 버튼 요소(element)에 접근
button = browser.find_element_by_xpath('//*[@id="blackBox"]/input[1]')
button.click()
</pre>

* <b>코드 업데이트</b>

<pre>
from selenium.webdriver.chrome.service import Service
from selenium import webdriver
import time

path = "./chromedriver.exe"

service = Service(executable_path=path)
browser = webdriver.Chrome(service=service)

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_element("name", "memberID")
password = browser.find_element("name", "memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id.send_keys("pyautogui")
password.send_keys("pyautogui")

# XPath로 버튼 요소(element)에 접근
button = browser.find_element('xpath', '//*[@id="blackBox"]/input[1]')
button.click()

time.sleep(50)
</pre>

#### 5) 셀레니움(Selenium)을 활용한 자동 크롤링

* 동적 웹 페이지: 로그인 이후에 사용자마다 다른 웹 문서를 보여주는 사이트
* 로그인 이후에 특정한 페이지에 있는 데이터를 가져올 수 있습니다.

<pre>
from this import d
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_elements_by_name("memberID")
password = browser.find_elements_by_name("memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id[0].send_keys("pyautogui")
password[0].send_keys("pyautogui")

# XPath로 버튼 요소(element)에 접근
button = browser.find_element_by_xpath('//*[@id="blackBox"]/input[1]')
button.click()

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/study/study.jsp")
# 게시물 제목에 접근
box = browser.find_element_by_class_name("studyViewBox")
rows = box.find_elements_by_tag_name("tr")

# 파일 객체를 쓰기 모드로 열기
f = open("result.txt", "w", encoding="utf8")

# 처음 두 개의 줄(row)은 제외하고 하나씩 확인
for row in range(2, len(rows)):
    cells = rows[row].find_elements_by_class_name("tail")
    name = cells[0].text
    title = cells[1].text
    date = cells[2].text
    # 이름, 제목, 날짜 데이터를 파일에 저장
    text = f"선생님: {name}\n제목: {title}\n날짜: {date}\n"
    f.write(text)

f.close()
</pre>

* <b>코드 업데이트</b>

<pre>
from selenium.webdriver.chrome.service import Service
from selenium import webdriver
import time

path = "./chromedriver.exe"

service = Service(executable_path=path)
browser = webdriver.Chrome(service=service)

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/member/memberLoginForm.jsp")

# 현재 웹 페이지의 정보 출력하기
print(browser.title)

# 아이디와 비밀번호 입력 창에 접근
id = browser.find_element("name", "memberID")
password = browser.find_element("name", "memberPassword")

# 각 요소(element)에 원하는 문자열 입력
id.send_keys("pyautogui")
password.send_keys("pyautogui")

# XPath로 버튼 요소(element)에 접근
button = browser.find_element('xpath', '//*[@id="blackBox"]/input[1]')
button.click()

# 특정 웹 사이트에 접속하기
browser.get("http://www.dowellcomputer.com/study/study.jsp")
# 게시물 제목에 접근
box = browser.find_element("class name", "studyViewBox")
rows = box.find_elements("tag name", "tr")

# 파일 객체를 쓰기 모드로 열기
f = open("result.txt", "w", encoding="utf8")

# 처음 두 개의 줄(row)은 제외하고 하나씩 확인
for row in range(2, len(rows)):
    cells = rows[row].find_elements("class name", "tail")
    name = cells[0].text
    title = cells[1].text
    date = cells[2].text
    # 이름, 제목, 날짜 데이터를 파일에 저장
    text = f"선생님: {name}\n제목: {title}\n날짜: {date}\n"
    f.write(text)

f.close()

time.sleep(50)
</pre>
