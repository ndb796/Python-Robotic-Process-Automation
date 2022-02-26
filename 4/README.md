### 4장 매크로를 활용해 키보드와 마우스 조종하기

#### 매크로를 활용한 업무 자동화

* 반복적인 업무를 대체하는 가장 간단한 방법은, 프로그램을 이용해 키보드와 마우스를 직접적으로 조종하는 것입니다. 

#### 1) PyAutoGUI 설치

* PyAutoGUI를 사용해 키보드와 마우스를 원하는 대로 조종할 수 있습니다.
* PyAutoGUI 공식 홈페이지: https://pyautogui.readthedocs.io/en/latest/
* PyAutoGUI의 대표적인 기능은 다음과 같습니다.
    * 컴퓨터에서 실행한 다른 프로그램 화면을 클릭할 수 있습니다.
    * 컴퓨터에서 실행한 다른 프로그램 내에서 타이핑을 할 수 있습니다.
    * 모니터 화면에서 스크린샷을 찍거나 화면 내에서 특정한 이미지의 위치를 찾을 수 있습니다.
* PyAutoGUI를 설치합니다.

<pre>
pip install pyautogui
</pre>

* PyAutoGUI의 기본 코드

<pre>
import pyautogui

# 메인 모니터의 해상도 가져오기
screen_width, screen_height = pyautogui.size()
print(screen_width, screen_height)

# 현재 마우스의 XY 좌표 가져오기
current_mouse_X, current_mouse_Y = pyautogui.position()
print(current_mouse_X, current_mouse_Y)
</pre>

#### 2) PyAutoGUI로 키보드 조종하기

* 키보드를 조종할 때는 write() 메서드를 사용합니다.
    * interval: 각 글자를 입력할 때의 시간 간격을 의미합니다.

<pre>
import time
import pyautogui

time.sleep(2) # 2초간 기다리기
pyautogui.write("Hello World!\n", interval=0.1)
pyautogui.write("We are going to learn PyAutoGUI.", interval=0.1)
</pre>

* 한글 입력을 위해 일반적으로 pyperclip을 사용합니다.

<pre>
pip install pyperclip
</pre>

* pyperclip의 copy() 메서드를 이용해 우리가 원하는 한글 문자열을 통째로 복사할 수 있습니다.
    * 이후에 hotkey() 메서드를 이용하여 Ctrl + V로 붙여넣기를 진행할 수 있습니다.

<pre>
import time
import pyautogui
import pyperclip

time.sleep(2) # 2초간 기다리기
pyautogui.write("Hello World!\n", interval=0.1)

pyperclip.copy("한글을 입력하겠습니다.")
pyautogui.hotkey("ctrl", "v")
</pre>

#### 3) PyAutoGUI로 마우스 조종하기

* 실습용 예시 웹 사이트: http://dowellcomputer.com/main.jsp
* 웹 사이트의 <b>[로그인]</b> 버튼 위에 마우스 커서를 올려 본 뒤에 position() 메서드로 위치를 찾습니다.

<pre>
import time
import pyautogui
import pyperclip

time.sleep(2) # 2초간 기다리기
position = pyautogui.position()
print(position) # 현재 마우스 포인터의 위치 출력
</pre>

* 특정한 좌표에서 마우스를 클릭할 때는 click() 메서드를 이용하시면 됩니다. 

<pre>
import time
import pyautogui
import pyperclip

time.sleep(2) # 2초간 기다리기
position = pyautogui.position()
print(position) # 현재 마우스 포인터의 위치 출력

pyautogui.click(position)
</pre>
