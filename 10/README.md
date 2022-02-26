### 10장 엑셀에서 서식 다루기

* <b>서식</b>이란 서류를 꾸미는 방식을 지칭할 때 사용하는 용어입니다. 
* 우리는 파이썬을 이용해 엑셀의 <b>서식</b>을 다룰 수 있습니다.
    * 텍스트의 글꼴이나 색상을 설정할 수 있습니다.
    * 정렬(alignment)을 수행할 수 있습니다.
    * 엑셀의 셀에 대하여 테두리(border)를 설정하여 엑셀 파일을 예쁘게 꾸밀 수 있습니다.

#### 1) 폰트(Font, 글꼴) 다루기

* 다양한 글자에 대하여 글자의 크기, 글꼴, 색상 등을 설정할 수 있습니다.
    * 색상을 넣을 때는 원하는 RGB 값을 넣으면 됩니다. (빨강: #FF0000)

<pre>
from openpyxl import Workbook
from openpyxl.styles.fonts import Font

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 특정한 셀에 폰트 적용하기
worksheet["C3"].value = "텍스트 1"
worksheet["C3"].font = Font(size=15, bold=True) # 크기, 굵은 글씨

worksheet["D4"].value = "텍스트 2"
worksheet["D4"].font = Font(size=40, underline='single', italic=True) # 크기, 밑줄, 이탤릭체

worksheet["E5"].value = "텍스트 3"
worksheet["E5"].font = Font(strikethrough=True, color="FF0000") # 취소선, 색상(빨강)

worksheet["F3"].value = "텍스트 4"
worksheet["F3"].font = Font(size=30, name="굴림") # 크기, 글씨체

# 워크북(workbook) 저장하기
workbook.save("result.xlsx")
</pre>

#### 2) 셀 색상 다루기

* openpyxl은 특정한 셀의 색상을 채우는 기능을 제공합니다.
    * fill_type: 셀에 색상을 넣는 형태
    * fgColor: 넣고자 하는 색상의 RGB 값

<pre>
from openpyxl import Workbook
from openpyxl.styles import PatternFill

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 특정한 셀에 문자열 기입하기
worksheet["C3"].value = "셀 색상 1"
worksheet["D4"].value = "셀 색상 2"

# 특정한 셀에 색상 채우기
"""
- fill_type = "solid", "darkDown", "darkGray" 등
- fgColor (배경색)
"""
worksheet["C3"].fill = PatternFill(fill_type="solid", fgColor="FF0000")
worksheet["D4"].fill = PatternFill(fill_type="darkDown", fgColor="0000FF")

# 워크북(workbook) 저장하기
workbook.save("result.xlsx")
</pre>

#### 3) 정렬(Alignment) 다루기

* 엑셀이 지원하는 정렬 기능을 openpyxl을 활용해 거의 유사하게 사용할 수 있습니다.
* 텍스트를 정렬할 때는 수직 정렬과 수평 정렬을 모두 고려해야 합니다.

<pre>
from openpyxl import Workbook
from openpyxl.styles import Alignment

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 특정한 셀에 문자열 기입하기
worksheet["C3"].value = "텍스트 정렬 1"
worksheet["D4"].value = "텍스트 정렬 2"

# 특정한 행과 열의 크기 설정하기
worksheet.row_dimensions[3].height = 100 # 3행의 높이를 100으로 설정
worksheet.row_dimensions[4].height = 50 # 4행의 높이를 70으로 설정
worksheet.column_dimensions["C"].width = 50 # C열의 너비를 80으로 설정
worksheet.column_dimensions["D"].width = 50 # C열의 너비를 80으로 설정

# 텍스트 정렬
"""
horizontal: "left", "right", "center"
vertical: "top", "bottom", "center"
"""
worksheet["C3"].alignment = Alignment(horizontal="left", vertical="top")
worksheet["D4"].alignment = Alignment(horizontal="center", vertical="center")

# 워크북(workbook) 저장하기
workbook.save("result.xlsx")
</pre>

#### 4) 테두리(Borderline) 다루기

* 특정한 셀의 테두리의 경우 상하좌우 4가지 측면(side)에 대하여 각각 개별적으로 설정합니다.

<pre>
from openpyxl import Workbook
from openpyxl.styles import Border, Side

workbook = Workbook() # 워크북(workbook) 생성

# 활성화된 워크시트(worksheet) 가져오기
worksheet = workbook.active

# 특정한 셀에 문자열 기입하기
worksheet["C3"].value = "테두리 1"
worksheet["D4"].value = "테두리 2"

# 테두리 설정
"""
- 테두리는 top, bottom, left, right 각각 측면(side)에 개별적으로 적용 가능
- 이때, 각 측면(side)마다 스타일(border_style)과 색상(color) 적용 가능
"""
worksheet["C3"].border = Border(
    top = Side(border_style="double", color="0000FF"),
    bottom = Side(border_style="double", color="0000FF"),
    left = Side(border_style="thin", color="FF0000"),
    right = Side(border_style="thin", color="FF0000")
)
worksheet["D4"].border = Border(
    top = Side(border_style="thick"),
    bottom = Side(border_style="thick"),
    left = Side(border_style="thick"),
    right = Side(border_style="thick")
)

# 워크북(workbook) 저장하기
workbook.save("result.xlsx")
</pre>
