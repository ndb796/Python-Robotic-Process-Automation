### 5장 파이썬 매크로 실전 예제

#### 매크로를 활용한 일상적인 업무의 자동화

* 파이썬 매크로 프로그램은 다양한 목적에 맞게 사용할 수 있습니다.
    * 자동으로 로그인을 한 뒤에 게시글을 작성할 수 있습니다.
    * 여러 개의 게시글을 차례대로 확인하여 스크린샷을 캡처할 수 있습니다.

#### 1) 자동 로그인

* 실습용 웹 사이트: http://dowellcomputer.com/
    * 아이디: pyautogui
    * 비밀번호: pyautogui
* PyAutoGUI에서는 특정한 이미지가 존재하는 영역을 찾는 함수인 locateOnScreen() 메서드를 제공합니다.
* 화면에서 특정한 버튼 이미지를 캡처할 수 있습니다.
    * 윈도우(Windows) 운영체제의 <b>[캡처 도구]</b> 혹은 <b>[윈도우 키 + Shift + S]</b>를 사용할 수 있습니다.
    * 이미지는 기본적으로 .png 형식으로 저장합니다.
* 특정한 이미지가 존재하는 위치를 계산할 수 있습니다.
    * locateOnScreen() 메서드는 Pillow 라이브러리를 요구합니다.
<pre>
pip install pillow 
</pre>
* locateOnScreen() 메서드로 [로그인] 버튼의 위치를 찾을 수 있습니다.
    * locateOnScreen() 메서드는 기본적으로 이미지가 정확히 일치할 때만 위치를 찾을 수 있습니다.
    * 화면(screen)에서 해당 이미지를 찾지 못한 경우엔 None 값을 반환합니다.
<pre>
import pyautogui

image_location = pyautogui.locateOnScreen("login.png")
print(image_location)
</pre>
* locateOnScreen() 메서드의 confidence 속성의 값을 활용할 수 있습니다.
    * OpenCV를 설치할 필요가 있습니다.

<pre>
pip install opencv-python
</pre>

* 일치율이 50% 이상인 이미지를 찾는다면, confidence 값으로 0.5를 기입합니다.
<pre>
import pyautogui

image_location = pyautogui.locateOnScreen("login.png", confidence=0.5)
pyautogui.moveTo(image_location)
print(image_location)
</pre>

* 자동 로그인 기능을 구현할 수 있습니다.
     * 이미지를 인식하여 버튼을 누르는 과정이 포함되어 있기 때문에, 오작동할 가능성이 있습니다.
     * PyAutoGUI 대신에 HTML 웹 문서 소스 코드를 분석하여 웹 사이트 업무를 자동화할 수도 있습니다.
     * 윤리적으로 실서버에 피해를 주지 않고 합당하게 수행할 수 있는 작업만을 매크로를 통해 수행해야 합니다.

<pre>
import time
import pyautogui

# 로그인 페이지로 이동
page_location = pyautogui.locateOnScreen("login_1.png", confidence=0.5)
pyautogui.moveTo(page_location)
pyautogui.click()

time.sleep(1) # 1초간 기다리기

# 아이디 입력
id_location = pyautogui.locateOnScreen("id.png", confidence=0.6)
pyautogui.moveTo(id_location) # 커서를 아이디 위치로 이동
pyautogui.moveRel(300, 0) # 오른쪽으로 300px 이동
pyautogui.click() # 입력창 클릭
pyautogui.typewrite("pyautogui") # 아이디 입력

# 비밀번호 입력
password_location = pyautogui.locateOnScreen("password.png", confidence=0.6)
pyautogui.moveTo(password_location) # 커서를 비밀번호 위치로 이동
pyautogui.moveRel(300, 0) # 오른쪽으로 300px 이동
pyautogui.click() # 입력창 클릭
pyautogui.typewrite("pyautogui") # 비밀번호 입력

# 로그인 진행
login_location = pyautogui.locateOnScreen("login_2.png", confidence=0.6)
pyautogui.moveTo(login_location) # 커서를 로그인 버튼 위치로 이동
pyautogui.click() # 로그인 버튼 클릭
</pre>
