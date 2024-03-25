### 14장 포털 사이트 이미지 수집 및 가공 실습

* 셀레니움(Selenium)으로 포털 사이트에서 빠르게 이미지를 수집하고 가공할 수 있습니다.
* 이미지를 수집하여 실질적으로 활용할 때는 저작권 이슈가 없는 이미지만 활용해야 합니다.
    * 본 차시에서는 이미지를 수집하여 가공하는 방법 자체에만 집중합니다.

#### 1) 구글(Google)에서 이미지 수집하기

* 구글의 이미지 검색 페이지에 접속하여 원하는 내용을 검색합니다.
    * 구글 이미지 검색 페이지의 query(q) 파라미터에 적절한 문자열을 넣습니다.

<pre>
import os
import cv2
import time
from selenium import webdriver
from urllib.request import urlretrieve

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

search = "무료 풍경 사진"
url = "https://www.google.com/search?q=" + search + "&tbm=isch&hl=ko"

# 특정 웹 사이트에 접속하기
browser.get(url)
time.sleep(5) # 5초간 정지
</pre>

* 이미지를 수집할 때는 request 라이브러리의 urlretrieve() 메서드를 사용할 수 있습니다. 
    * 특정한 URL에서부터 파일을 다운로드하는 메서드입니다.
    * &lt;img&gt; 태그를 확인하여, 이미지 태그의 소스(source) 경로로부터 이미지를 다운로드합니다.

<pre>
import os
import cv2
import time
from selenium import webdriver
from urllib.request import urlretrieve

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

search = "무료 풍경 사진"
url = "https://www.google.com/search?q=" + search + "&tbm=isch&hl=ko"

# 특정 웹 사이트에 접속하기
browser.get(url)
time.sleep(5) # 5초간 정지

# 이미지 태그 찾기
images = browser.find_elements_by_tag_name("img")

# 이미지를 저장할 폴더 생성
directory = "./images/"
if not os.path.exists(directory):
    os.mkdir(directory)

# 이미지를 하나씩 확인하며
limit = 30
cnt = 0
for image in images:
    image_source = image.get_attribute("src") # 이미지 URL
    if image_source != None:
        target = directory + str(cnt) + ".png"
        urlretrieve(image_source, target) # 이미지 다운로드
    cnt += 1
    if cnt == limit: # 원하는 만큼 이미지를 다운로드한 경우
        break
</pre>

* <b>코드 업데이트</b>

<pre>
from selenium.webdriver.chrome.service import Service
from selenium import webdriver
import time
from urllib.request import urlretrieve
import os

path = "./chromedriver.exe"

service = Service(executable_path=path)
browser = webdriver.Chrome(service=service)

search = "무료 풍경 사진"
url = "https://www.google.com/search?q=" + search + "&tbm=isch&hl=ko"

# 특정 웹 사이트에 접속하기
browser.get(url)

time.sleep(3)

# 이미지 태그 찾기
images = browser.find_elements("tag name", "img")

# 이미지를 저장할 폴더 생성
directory = "./images/"
if not os.path.exists(directory):
    os.mkdir(directory)

# 이미지를 하나씩 확인하며
limit = 50
cnt = 0
for image in images:
    image_source = image.get_attribute("src") # 이미지 URL
    if image_source != None:
        target = directory + str(cnt) + ".png"
        urlretrieve(image_source, target) # 이미지 다운로드
    cnt += 1
    if cnt == limit: # 원하는 만큼 이미지를 다운로드한 경우
        break
</pre>

#### 2) 구글(Google)에서 이미지 가공하기

* 원하는 이미지만 수집한 뒤에 이미지의 크기를 적절하게 바꿀 수 있습니다.
* 파이썬의 OpenCV 라이브러리의 resize()를 사용해 크기가 변경된 이미지 객체를 얻습니다.
    * 필요시 pip3 install opencv-python 명령어로 OpenCV를 설치합니다.

<pre>
import os
import cv2
import time
from selenium import webdriver
from urllib.request import urlretrieve

# 크롬(Chrome) 브라우저 실행하기
browser = webdriver.Chrome('./chromedriver')
# 로깅(logging) 메시지 줄이기
options = webdriver.ChromeOptions()
options.add_experimental_option('excludeSwitches', ['enable-logging'])

search = "무료 풍경 사진"
url = "https://www.google.com/search?q=" + search + "&tbm=isch&hl=ko"

# 특정 웹 사이트에 접속하기
browser.get(url)
time.sleep(5) # 5초간 정지

# 이미지 태그 찾기
images = browser.find_elements_by_tag_name("img")

# 이미지를 저장할 폴더 생성
directory = "./images/"
if not os.path.exists(directory):
    os.mkdir(directory)

# 이미지를 하나씩 확인하며
limit = 30
cnt = 0
for image in images:
    image_source = image.get_attribute("src") # 이미지 URL
    if image_source != None:
        target = directory + str(cnt) + ".png"
        urlretrieve(image_source, target) # 이미지 다운로드
        # 이미지의 크기가 너무 작다면 이미지 제거하기
        img = cv2.imread(target)
        height, width, channel = img.shape
        if height < 120 or width < 120:
            os.remove(target)
            continue
        # 이미지의 크기를 200 X 200 크기로 조절
        res = cv2.resize(img, dsize=(200, 200))
        cv2.imwrite(target, res)
        cnt += 1
    if cnt == limit: # 원하는 만큼 이미지를 다운로드한 경우
        break
</pre>
