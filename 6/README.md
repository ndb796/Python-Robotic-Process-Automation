### 6장 여러 개의 텍스트 파일에서 필요한 정보만 엑셀에 정리하기

#### 다양하게 존재하는 데이터를 엑셀 파일로 옮기기

* 많은 사무직에서는 특히나 엑셀을 활용해 반복적인 작업을 해야 하는 경우가 많습니다. 
* 컴퓨터 내에서 다양하게 존재하는 데이터를 선택적으로 엑셀 파일로 옮겨서 처리할 수 있습니다.

#### 1) openpyxl 라이브러리 설치

* 파이썬에서 엑셀 업무를 도와주기 위한 라이브러리로 openpyxl이 있습니다.

<pre>
pip install openpyxl
</pre>

* openpyxl 웹 사이트: https://openpyxl.readthedocs.io/en/stable/
* 일반적으로 워크북(workbook)은 전체 엑셀 파일 자체를 의미합니다.
* 하나의 워크북에는 여러 개의 워크시트(worksheet)가 존재할 수 있습니다.

<pre>
from openpyxl import Workbook

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 한 줄(row)씩 데이터 입력하기
worksheet.append(["이순신", 97, 3])
worksheet.append(["홍길동", 85, 2])
worksheet.append(["장보고", 100, 3])

# 워크북(workbook) 저장하기
workbook.save("output.xlsx")
</pre>

#### 2) 여러 개의 텍스트 파일에서 필요한 정보만 엑셀에 정리하기

* 실습을 위해 준비된 두 개의 메모장 파일을 확인합니다.
    * students.txt
    * students2.txt
    * students3.txt
* 파이썬을 이용해 파일에서 데이터를 읽어 오기 위해 파일 객체를 생성합니다.
    * open(): 파일 객체를 생성하는 함수
    * read(): 파일의 전체 내용을 문자열 형태로 읽어오는 함수

<pre>
"""
open(파일 이름, 모드, 인코딩) 함수를 이용해 파일 객체를 생성할 수 있습니다.
r: 읽기 모드로, 파일을 읽기만 할 때 사용합니다.
UTF8: 한글과 같은 유니코드를 처리하기 위한 인코딩 방식입니다.
"""

file = open('./students.txt', 'r', encoding='UTF8') # 파일 객체 생성

text = file.read() # 파일의 전체 내용을 문자열로 반환
print(text)

file.close() # 파일 객체 닫기
</pre>

* 결과적으로 텍스트 파일에서 문자열을 읽어와 엑셀 파일에 기록할 수 있습니다.
    * 텍스트 파일에서 각 학생 정보는 한 줄에 하나씩 문자열 형태로 기록되어 있습니다.
    * 각 데이터(번호, 이름, 점수 등)는 공백을 기준으로 구분되어 있습니다.

<pre>
from openpyxl import Workbook

def read_files(file_names):
    text = ""
    for file_name in file_names: # 파일 이름을 하나씩 확인하며
        # 파일을 열어 text 변수에 추가
        with open(file_name, 'r', encoding='UTF8') as file:
            text += file.read()
        text += "\n" # 줄바꿈 추가
    return text

text = read_files(["students.txt", "students2.txt"])
text = text.strip() # 앞 뒤로 공백 제거

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

student_list = []
# 한 줄씩 확인하며
for line in text.split('\n'):
    # [번호, 이름, 점수1, 점수2, 점수3, 학과, 학번]을 차례대로 확인
    id, name, score1, score2, score3, depart, grade = line.split(' ')
    # 수 데이터는 수 자료형으로 변환
    id = int(id)
    score1 = int(score1)
    score2 = int(score2)
    score3 = int(score3)
    grade = int(grade[0]) # 학년에 해당하는 숫자 데이터만 저장
    student = [id, name, score1, score2, score3, depart, grade]
    student_list.append(student)

for student in student_list:
    # 한 줄(row)씩 학생 정보 입력하기
    worksheet.append(student)

# 워크북(workbook) 저장하기
workbook.save("students.xlsx")
</pre>
