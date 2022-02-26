### 15장 뉴스 기사 크롤링 및 분석 실습

* 파이썬을 이용해 뉴스 기사 데이터를 수집하는 과정을 자동화할 수 있습니다.

#### 1) BBC 뉴스 웹 사이트에서 뉴스 기사 데이터 수집하기

* 셀레니움을 활용해 BBC 뉴스 웹 사이트에 접속할 수 있습니다.

<pre>
import time
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

search = "programming"
url = "https://www.bbc.co.uk/search?q=" + search + "&page=1"

# 특정 웹 사이트에 접속하기
browser.get(url)
time.sleep(5) # 5초간 정지
</pre>

* BBC 뉴스 기사만 추출할 수 있습니다.
    * 개발자 도구(F12)를 실행하여 특정한 기사의 제목(headline)에 대하여 요소(element)를 확인합니다.

<pre>
import time
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

search = "programming"
url = "https://www.bbc.co.uk/search?q=" + search + "&page=1"

# 특정 웹 사이트에 접속하기
browser.get(url)
time.sleep(3) # 5초간 정지

headlines = []

# 웹 사이트 내 모든 <p> 태그 검색
p_list = browser.find_elements_by_tag_name("p")
for p in p_list:
    # class 속성이 존재하는 <p> 태그만 확인
    if p.get_attribute("class") != None:
        # class 속성의 값으로 "Headline"이 포함된 경우
        if "Headline" in p.get_attribute("class"):
            headline = p.text
            headlines.append(headlines)

print(headlines)
</pre>

* 첫 번째 페이지에서 끝나지 않고, 여러 개의 페이지에 대해서 연속적으로 크롤링합니다.

<pre>
import time
from selenium import webdriver

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

headlines = []
search = "programming"

for i in range(1, 11):
    url = "https://www.bbc.co.uk/search?q=" + search + "&page=" + str(i)
    browser.get(url) # 특정 웹 사이트에 접속하기
    
    # 웹 사이트 내 모든 <p> 태그 검색
    p_list = browser.find_elements_by_tag_name("p")
    for p in p_list:
        # class 속성이 존재하는 <p> 태그만 확인
        if p.get_attribute("class") != None:
            # class 속성의 값으로 "Headline"이 포함된 경우
            if "Headline" in p.get_attribute("class"):
                headline = p.text
                headlines.append(headline)

print(headlines)
</pre>

#### 2) 뉴스 기사 데이터 분석하기

* 뉴스 기사 중에서 가장 높은 빈도수로 등장한 단어에 대해서 분석하여 시각화합니다.
* 워드 클라우드(word cloud)를 활용할 수 있습니다.
    * 워드 클라우드 라이브러리 설치: pip install wordcloud
    * Matplotlib 라이브러리 설치: pip install matplotlib
* 워드 클라우드를 만들 때는 하나의 텍스트를 입력으로 넣습니다.
    * 텍스트 내에서 각 단어들을 공백을 기준으로 구분합니다.

<pre>
from wordcloud import WordCloud
from selenium import webdriver
import matplotlib.pyplot as plt

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

headlines = []
search = "programming"

for i in range(1, 3):
    url = "https://www.bbc.co.uk/search?q=" + search + "&page=" + str(i)
    browser.get(url) # 특정 웹 사이트에 접속하기
    
    # 웹 사이트 내 모든 <p> 태그 검색
    p_list = browser.find_elements_by_tag_name("p")
    for p in p_list:
        # class 속성이 존재하는 <p> 태그만 확인
        if p.get_attribute("class") != None:
            # class 속성의 값으로 "Headline"이 포함된 경우
            if "Headline" in p.get_attribute("class"):
                headline = p.text
                headlines.append(headline)

# 텍스트에서 워드클라우드 생성
text = ""
for headline in headlines:
    text += headline + " "
word_cloud = WordCloud(background_color='white').generate(text)

# 이미지 시각화 및 저장
plt.imshow(word_cloud)
plt.savefig("result.png")
plt.show()
</pre>
