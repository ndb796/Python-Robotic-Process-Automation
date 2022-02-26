### 9장 엑셀에서 함수 다루기

#### 프로그래밍을 제어하기 위한 문법

* 사무직 업무를 볼 때는 엑셀에서의 다양한 함수를 사용하게 됩니다.
    * 데이터의 합계나 평균을 구하는 작업은 흔하게 요구됩니다.
* students.xlsx 파일을 이용하여 실습을 진행합니다.

#### 1) 함수 다루기

* 각 열마다 점수의 평균을 구하고자 할 때는 엑셀에서 AVERAGE 함수를 사용합니다.
    * C열부터 E까지에 각 학생들의 (점수1, 점수2, 점수3)이 적혀 있습니다. 
* 각 점수에 대하여 모든 학생의 평균 점수를 구할 수 있습니다.

<pre>
import openpyxl
from collections import Counter

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 최대 행(max row) 구하기
max_row = worksheet.max_row

# C부터 E까지의 모든 열(column)에 대하여 평균값 계산
worksheet["C" + str(max_row + 1)].value = "=AVERAGE(C1:C" + str(max_row) + ")"
worksheet["D" + str(max_row + 1)].value = "=AVERAGE(D1:D" + str(max_row) + ")"
worksheet["E" + str(max_row + 1)].value = "=AVERAGE(E1:E" + str(max_row) + ")"

workbook.save("function.xlsx")
</pre>

* 학생별로 세 점수의 평균을 구할 수 있습니다.

<pre>
import openpyxl
from collections import Counter

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 최대 행(max row) 구하기
max_row = worksheet.max_row

for row in range(1, max_row + 1):
    # 각 줄마다 함수 적용
    worksheet["H" + str(row)].value = "=AVERAGE(C" + str(row) + ":E" + str(row) + ")"

# C부터 E까지의 모든 열(column)에 대하여 평균값 계산
worksheet["C" + str(max_row + 1)].value = "=AVERAGE(C1:C" + str(max_row) + ")"
worksheet["D" + str(max_row + 1)].value = "=AVERAGE(D1:D" + str(max_row) + ")"
worksheet["E" + str(max_row + 1)].value = "=AVERAGE(E1:E" + str(max_row) + ")"

workbook.save("function.xlsx")
</pre>
