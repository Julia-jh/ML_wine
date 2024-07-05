# 파일 수정 사항 정리
- 날짜는 역순으로 정렬

## file tree
	- climate_data_crawling_2.ipynb
		- 자료 정리 코드
	- sample_ALL_KSM00047108.txt
		- 샘플로 확인한 코드
	- rawdata_climate 폴더
		- 원본 자료
			- country-list.txt
				- 국가코드
			- filelist.txt
				- 지점코드
	- document_climate 폴더
		- 참고 자료 정리
			- GSOM_readme.txt
				- 자료 소개서
			- GSOM_documentation.pdf
				- 자료 설명서
			- GSOM_GSOY_Description_Document_v1.0.2_20200219.pdf
				- 연/월 통합 상세 설명서
	- data 폴더
		- 프로젝트에 활용할 정제된 데이터
		- 기준 자료 정리
			- country_list.csv
			- file_list.csv
---

## Describtion
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