# 파일 수정 사항 정리
- 날짜는 역순으로 정렬

## file tree
- climate 파일
	- climate_data_test.ipynb
		- 자료 정리 및 테스트 코드
        - 연습 및 코드 누적용
	- climate_data_crawling.ipynb
		- API 이용한 자료 다운로드 코드
    - climate_list_download.ipynb
        - 기준 자료 정리 코드
    - climate_data_country.ipynb
        - 국가 코드, 국가명, 파일 이름을 연결
        - 모든 파일의 첫 번째 행을 불러와 df로 연결함
            - 지리정보를 확인하기 위함
	- rawdata_climate 폴더
		- 원본 자료
		- country-list.txt
			- 국가코드와 국가명
		- filelist.txt
			- 지점코드와 용량
		- 지점코드.txt
			- API로 읽어 저장함
	- document_climate 폴더
		- 참고 자료 정리
			- GSOM_readme.txt
				- 자료 소개서
			- GSOM_documentation.pdf
				- 자료 설명서
			- GSOM_GSOY_Description_Document_v1.0.2_20200219.pdf
				- 연/월 통합 상세 설명서
	- data_climate 폴더
		- 프로젝트에 활용할 정제된 데이터
		- 기준 자료 정리
			- country_list.csv
			- file_list.csv
		- 활용 자료
			- 지점코드.csv
				- 바로 csv로 저장할지 txt를 변환할지 못정함
        - gsom-latest 폴더
            - NCEI 홈페이지에서 직접 받은 csv 파일
            - API 허브에서 받은 것과 동일함
        - dfLocation_sample.csv
            - 우선 1000개 자료만 정리함
	- NCEI_data 폴더
		- gsom_sample_csv.csv
			- 데이터 샘플
		- stations.csv
			- 지역별 위치, 지점코드 정보를 얻을 수 있음
---

## Describtion

### 20240710 2200
- 와중에 주피터 노트북이 비밀번호를 내놓으라고 함. 한 번 도 없던 일인데 프롬프터에 뜬 `pip install -U "jupyter-server<2.0.0"` 문구로 해결함
    - forbidden되어 server 접근이 안 되어 저장이 불가능해짐
    - 저장이 되는지 꼭꼭꼭 확인해야함........
- 10000개씩 끊어서 작업해 올리는 중...
    - 무척 오래걸림,, 오류가 있으면 추후에 한 번에 몰아서 작업해야할듯

<br>

### 20240710 1800
- NCEI 모든 파일의 첫 번째 행을 가져와 정리중
    - iloc가 빠르다는 말과 loc가 빠르다는 말이 다 다르다. 왤까.. 왤까....
        - https://devocean.sk.com/blog/techBoardDetail.do?ID=164657&boardType=techBlog
        - https://m.blog.naver.com/draco6/221680932777
    - 생각해보니 이 작업을 꼭 python으로 해야 하나...? 다른 곳에서 csv 파일들 헤더를 제외한 첫 번째 행을 빠르게 추추하는 방법은 없을까?
<br>

### 20240710 1740
- NCEI 모든 파일의 첫 번째 행을 가져와 정리중
    - 총 갯수가 122041개라 오래 걸림
    - 오래 걸리는 이유가 df의 insert 작업 때문이라고 함, 일단 시간이 없어서 돌려보면서 함수 고치는 중
    
<br>
<br>
<br>
<br>

### 20240709 2110
- 파이썬 코드 기능 별로 분리함, file tree 참고
- climate_data_country.ipynb
    - file list와 country list를 병합하여 파일의 국가명을 정리함
    - NCEI에서 받은 대용량 파일을 정리함
        - data_climate 폴더의 gsom-latest 폴더 내부에 존재함
    - 직접 받은 파일들과 file list가 동일한지 확인
        - 16개 자료는 파일은 있으나 국가 코드 확인이 안 됨
        - 추후 필요시 수기로 찾아봐야 함
- 데이터 위치 지도로 확인 가능
    - https://www.ncei.noaa.gov/maps/monthly/
	<img src = "./img/NCEI_greece.png">

<br>

### 20240709 1940
- 개인 고유 인증키, 각자 버전 활용해야 함
    - AUTH = "secrets Leak alerts로 인해 마스킹처리, 코드 run 원할시 기상청 API 허브 가입 후 활용해 주세요."
    
<br>
<br>
<br>
<br>

### 20240707 0220
- 기상청 API 허브 말고 NCEI 홈페이지를 직접 이용하는 방법이 있어 Bulk 버전 파일을 따로 다운받고 있음
	- 링크: https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month
	- Global Summary of the Month (GSOM), Version 1
	- File Count/Limit: 10000/1000   Total File Count: 122041
- 지점 코드를 활용해 API 호출하고 바로 csv로 저장하여 df로 불러오는 것까지 수행
	- globals() 함수 활용
	- 랜덤으로 열어본 파일에서 날짜 결측치와, 주요 변수 결측치가 존재하는 것을 확인함
	- 호출 횟수나 용량은 데이터를 살펴보는 데에는 문제 없을 것으로 보임, 정해지고 나서는 날짜를 나눠서 데이터를 받으면 될 것으로 보임
- 지점 코드를 해석하는 방법에 대해 고민이 있음.
	- 앞의 두 글자는 국가, 중간에 문자 하나가 더 있을 경우 망, 뒤에 지점번호는 9글자라고 나와있지만 실제로는 8글자인 경우가 많음. 무슨 일인지 질문해야 함
	- feature 요소
		- "STATION","DATE","LATITUDE","LONGITUDE","ELEVATION","NAME","CDSD","CDSD_ATTRIBUTES","CLDD","CLDD_ATTRIBUTES","DP01","DP01_ATTRIBUTES","DP10","DP10_ATTRIBUTES","DP1X","DP1X_ATTRIBUTES","DT00","DT00_ATTRIBUTES","DT32","DT32_ATTRIBUTES","DX32","DX32_ATTRIBUTES","DX70","DX70_ATTRIBUTES","DX90","DX90_ATTRIBUTES","DYNT","DYNT_ATTRIBUTES","DYXP","DYXP_ATTRIBUTES","DYXT","DYXT_ATTRIBUTES","EMNT","EMNT_ATTRIBUTES","EMXP","EMXP_ATTRIBUTES","EMXT","EMXT_ATTRIBUTES","HDSD","HDSD_ATTRIBUTES","HTDD","HTDD_ATTRIBUTES","PRCP","PRCP_ATTRIBUTES","TAVG","TAVG_ATTRIBUTES","TMAX","TMAX_ATTRIBUTES","TMIN","TMIN_ATTRIBUTES"
	- 값에 ,가 존재하는 경우 어떻게 해석해야하 할지 모르겠음..
- 만약에 GTS로 갈아탄다고 하면 너무 울것 같음.
	- 내일은 GTS에 결측치가 어떻게 나오는지 확인해야겠음
	- 데이터 정합성이 더 좋다면 갈아타야할 수도 있음..
	- GTS의 일일 데이터를 월 통계로 변환하는 작업이 필요할지도 모르겠음
#### 다음 할 일
- GTS 활용법 확인
	- GTS 자료와 NCEI 자료 비교 가능하다면 확인 필요
- txt로 저장 후 csv 변환과 csv로 바로 저장한 버전에 자료 손실 등으로 인한 차이가 있는지 확인하기
- NCEI 지점코드 해석법 필요함
- NCEI 자료와 국가 코드를 연결하여 컬럼을 하나 추가해야 함
#### 새롭게 발견한 사실
- csv 파일 전체 다운받음
	- gsom-latest.tar.gz
	- 1.5기가이지만, tar까지 풀면 9기가 넘음

<br>
<br>
<br>
<br>

### 20240706 0200
- 기상청 API 허브 내에서 세계기상 월별 평균 자료를 활용할 것이므로 NCEI 관측. 통계 자료를 활용함
	- GTS는 XML, JSON 파일로 얻을 수 있기 때문에 추후에 변경 시 많은 노력이 필요할 것
- 기준 데이터 정리가 중요했음
	- 국가명이 나와있는 국가 코드
	- 신청 요인 중 stn값으로 들어가는 지점 코드
- 이후 유럽 혹은 전세계를 활용할 지에 따라 국가 코드 선별작업이 들어갈 것
	- 유럽만 활용한다면 유럽 국가명 정리한 파일을 추가하여 stnNm 리스트 값을 추린 stnNmEU 리스트를 만들것
- 시기도 마찬가지임, 구멍난 데이터가 어디일지 확인하기에 너무 양이 많으므로 우선적으로 활용 지역을 알아야 함
- 데이터를 불러와 저장하고 다시 불러서 DF 정리한 뒤 csv로 저장하는 과정이 너무 쓸데없이 복잡함.
	- 우선 시간 절약을 위해 홈페이지에 나와있는 python 코드를 참고하기만 함
	- 이후 코드를 간결하게 고치는 과정이 필요함
	- 지점코드만 변화하고 나머지는 그대로일 것이므로 함수를 만드는 것도 필요함
	- 시기가 달라질 수도 있으므로 그것 또한 고려해야 함