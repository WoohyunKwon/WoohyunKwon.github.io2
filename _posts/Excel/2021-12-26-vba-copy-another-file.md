--- 
layout: post
title:  "[Excel/VBA] 다른 엑셀 파일에서 데이터 가져오기"
categories: Excel
tags: [Excel, VBA]
---

## 같은 폴더에 있는 특정 엑셀 파일의 시트 복사하기

<전체 코드>

```
Sub 시트_복사하기()

    Dim fileName As String
    Dim filePath As String
    Dim shtName As String
    
    '시트를 가져올 파일명
    fileName = ActiveSheet.Cells(1, 2).Value

    '가져올 시트명 
    shtName = ActiveSheet.Cells(2, 2).Value
    
    '가져올 엑셀파일의 경로
    filePath = ThisWorkbook.Path + "\" + fileName
    
    '해당 파일 열기
    Application.DisplayAlerts = False
    Workbooks.Open fileName:=filePath
    
    '열린 파일에서 원하는 시트 가져 오기
    ActiveWorkbook.Sheets(shtName)).Copy Before:=ThisWorkbook.Sheets(1)
    
    '열린 파일 닫기
    Workbooks(fileName).Close

End Sub
```

<코드 설명>

- `.ThisWorkbook` : 현재 실행중인 파일 
- `.Worksheets(n)` : n번째 시트를 말하며, `.sheets("시트이름")`을 이용하면 "시트이름"의 시트를 말한다 
- `.CopyBefore:=ThisWorkbook.Sheets(1)` : Sheet1을 기준으로 앞에 복사한다. CopyAfter를 이용하면 뒤에 복사할 수 있다.

## 특정 값만 가져오기

시트 전체가 아닌 특정 값만 필요한 경우가 있다. 다음은 추가 코드이며 필요에 따라 수정하면 되겠다.

<추가 코드>
```
    '값 입력하기
    Worksheets("기존 시트").Range("기존 셀").Value = Worksheets("복사해온 시트").Range("가져올 셀").Value

    '값 정렬하기 상단(xlTop), 가운데(xlCenter), 하단(xlBottom)
    Worksheets("기존 시트").Range(“$$:$$”).HorizontalAlignment = xlCenter

    '값 정렬하기 좌측(xlLeft), 가운데(xlCenter), 우측(xlRight)
    Worksheets("기존 시트").Range(“$$:$$”).HorizontalAlignment = xlLeft

    '가져온 시트 삭제하기
    Application.DisplayAlerts = False
    Sheets(1).Delete
```

## References

- [원하는 시트를 다른 엑셀 파일로 복사하기](https://ybworld.tistory.com/105)
- [다른 엑셀 파일에서 원하는 시트 가져오기](https://ybworld.tistory.com/106)