### 7장 엑셀에서 다양한 방법으로 셀 다루기

* 일상에서 엑셀 업무를 할 때 일일이 하나씩 셀을 클릭하여 데이터를 추가하거나 수정하곤 합니다.
* 파이썬을 이용하면 엑셀에서 셀을 다루는 업무를 손쉽게 자동화할 수 있습니다.

#### 1) 셀 데이터 읽기

* 워크시트(worksheet)에서 특정한 셀은 행(row)과 열(column)로 표현될 수 있습니다. 
* cell() 메서드를 사용해 셀에 접근할 수 있습니다.
    * 행과 열의 번호를 직접 입력할 수 있습니다.
    * Range를 이용해 엑셀의 고유 인덱스를 표현할 수 있습니다.

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# Range를 이용해 셀에 접근하기
data = worksheet["B3"].value
print(data)

# cell() 메서드를 이용해 셀에 접근하기
data = worksheet.cell(row=3, column=2).value
print(data)
</pre>

* Range를 이용하여 특정 범위에 속하는 데이터를 모두 가져올 수 있습니다.
    * 특정한 범위의 셀들에 접근할 때는 행(row)과 열(column) 순서대로 접근하게 됩니다. 

<pre>
(
    (B3, C3, D3, E3),
    (B4, C4, D4, E4), 
    (B5, C5, D5, E5),
    (B6, C6, D6, E6),
)
</pre>

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# Range를 이용해 셀에 접근하기
cells = worksheet["B3:E6"]
print(cells)

for row in cells:
    for cell in row:
        print(cell.value)
</pre>

#### 2) 셀 데이터 쓰기

* openpyxl을 이용해 데이터를 쓸 때에도 값(value)에 접근하여 기록할 수 있습니다.

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# cell() 메서드를 이용해 셀에 접근하기
cells = worksheet.cell(row=3, column=2).value = "허준"

workbook.save("students.xlsx")
</pre>

#### 3) 셀 데이터 삭제

* 특정한 셀을 삭제할 때는 단순히 해당 셀의 값을 공백 문자열("")로 대체할 수 있습니다.

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# Range를 이용해 셀에 접근하기
cells = worksheet.cell(row=3, column=2).value = ""

workbook.save("students.xlsx")
</pre>

* 특정한 행을 통째로 삭제할 때는 delete_rows()를 사용할 수 있습니다.
    * 3번째 행부터 8개의 행을 삭제할 때는 delete_rows(3, 8)라고 기입합니다. 
* 특정한 열을 통째로 삭제할 때는 delete_cols()를 사용할 수 있습니다.

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# delete_rows()를 이용해 3번째 행부터 8개의 행을 삭제하기
worksheet.delete_rows(3, 8)

workbook.save("students.xlsx")
</pre>

#### 4) 최대 행과 최대 열

* 최대 행을 가져올 때는 max_row 변수를 사용합니다.
* 최대 열을 가져올 때는 max_column 변수를 사용합니다.

<pre>
import openpyxl

# 워크북(workbook) 불러오기
workbook = openpyxl.load_workbook("students.xlsx")

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 최대 열(max column) 구하기
max_column = worksheet.max_column

print(max_column)
</pre>
