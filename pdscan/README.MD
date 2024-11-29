### 1. pdscan 요약
```
1)특정 폴더 및 파일 / 각종 DB등에 대해 암호화되지않은 개인정보를 검색할 수 있음.
2)본 프로그램은 별도의 설치 과정 없이, 실행이 가능함
3)윈도우 OS의 경우 pdscan-win.exe 를 cmd 에서 실행하고, 리눅스 OS의 경우 pdscan-linux를 shell에서 실행
```
### 2. pdscan 사용법 

Elasticsearch
```
1. 기본 검색 
pdscan-win.exe elasticsearch+http://user:pass@host:9200 
2. 특정 인덱스 검색
pdscan-win.exe elasticsearch+http://user:pass@host:9200/index1
```
File
```
1. 파일 검색 
pdscan-win.exe file://C:\path\to\file.txt
2. 디렉토리 검색 
pdscan-win.exe file://C:\path\to\dir
```
참고 : 리눅스에서 절대경로 이용시 file:///absolute/path/to/file.txt 같이 이용

MariaDB 
```
1. 특정 DB 검색
pdscan-win.exe mariadb://user:pass@host:3306/dbname
```
Mongodb
```
1. 특정 DB 검색
pdscan-win.exe mongidb://user:pass@host:27017/dbname
```
Mysql
```
1. 특정 DB 검색 
pdscan-win.exe mysql://user:pass@host:3306/dbname
```
### 3. 명령줄 옵션 
```
1) 특정 타입의 개인정보만 검색 
pdscan-win.exe --only email,phone,location 

2) 특정 타입의 개인정보를 제외
pdscan-win.exe --except ip,mac

3) 검색된 개인정보의 실제 데이터를 출력 
pdscan-win.exe --show-data

4) Confidence에 상관하지 않고 데이터 출력/ 
pdscan-win.exe --show-all

5) 출력 포맷 변경
pdscan-win.exe --format ndjson 
```
### 4. 룰 수정

개인정보 검출 룰을 수정하기 위해서는, pdscan 실행파일을 실행하기 전에 수정이 이미 완료된 상태로 rule.json파일을 저장해야 검출에 반영됩니다.
정규식 룰을 추가하기 위해서는 rule.json 파일의 regexRules 배열에 오브젝트를 추가합니다. 
예시, 
```

    ...
    {
      "name": "jumin_first",
      "display_name": "Jumin First",
      "String": "(\\b\\d{6}\\b)"
    }
    ...

``` 

name 필드 : (필수) pdscan 내부적으로 처리하는 변수 이름으로 json 형태로 출력시에 name 필드에 들어갈 내용입니다.
display_name : (필수)pdscan을 이용하여 데이터 출력 시, 출력결과에 나타날 이름입니다.
String : (필수)검출하기위한 정규식입니다. 특이사항으로 역슬래시(\) 입력을 위해서는 한개의 역슬래시가 아닌 예시 처럼 두개의 역슬래시를 이용해야 정상적으로 처리됩니다.
confidence : (선택)정규표현식의 신뢰가능한 정도를 지정합니다. confidence가 설정되지 않은 룰에 대해서는 기본 pdscan 실행시에 검출되지 않으며, --show-all 명령을 추가해야만 출력됩니다.

nameRules, multiNameRules, tokenRules 의 경우 파일형태가 아닌 별도의 저장소 (mysql 등)에서 사용되는 룰 로써, 추후 테스트 후 가이드 작성 예정

### 5. 제약사항
현재 한글검색에 대해서는 정상적으로 진행되지 않습니다. 차후 진행예정

### 6. 라이선스
본 검색 툴의 라이선스는 MIT 라이선스를 따릅니다.
