# 프로젝트 개요
2015년 7월에 설립된 Olist는 중소기업들이 온라인 마켓플레이스에서 제품을 판매할 수 있도록 연결해주는 플랫폼을 제공하는 오픈 마켓 형식으로 운영되는 브라질의 이커머스 기업입니다.
본 프로젝트는 Olist가 보유하고 있는 매출, 주문 수, 제품 라인업 등 방대한 데이터셋을 적극적으로 활용, 분석 및 종합하여 Olist의 경쟁력 강화를 위한 핵심 인사이트를 도출하고자 진행되었으며, (전반적인 매출과 제품 라인별 성과) 다음 2가지 핵심 영역에 대한 분석 결과와 전략적 제안을 제시합니다:

- **매출 트렌드 분석:** Olist의 과거(2016.09 ~ 2018.08) 매출 패턴을 전체 국가 수준과 26개 주별로 평가하여 매출액, 주문량, 평균 주문 금액(AOV)에 집중한 분석을 수행 
- **제품라인별 성과 분석:** Olist의 다양한 제품 라인을 다각적으로 분석하여 전체 매출에 미치는 영향을 파악   
<br>  

The SQL queries used to inspect and clean the data for this analysis can be found here [link].
Targed SQL queries regarding various business questions can be found here [link].
An interactive Tableau dashboard used to report and explore sales trends can be found here [link].     
<br>

# 데이터 구조 및 초기 점검
Olist의 주요 데이터베이스는 총 97,898개의 레코드를 가진 5개의 테이블(customer, items, orders, products, payments)로 구성되어 있음. 

각 테이블 설명:
- **olist_customers:** 고객 아이디, 우편번호, 도시이름, 주 이름 등의 고객정보
- **olist_items:** 주문 아이디, 제품 아이디, 배달시작 날짜, 가격, 배송비
- **olist_orders:** 주문 아이디, 고객 아이디, 주문 상태, 구매 날짜시간, 주문 승인 날짜시간, 배달업체 배송된 시간날짜, 배달 시작 시간날짜, 예상 배달도착 시간날짜 
- **olist_products:** 제품 아이디, 제품 카테고리명, 카테고리명 글자수, 제품 설명 글자수, 제품 사진 퀄리티 등
- **olist_payments:** 주문 아이디, 결제 유형, 결제금액 등

<br>    
<img width="698" alt="Image" src="https://github.com/user-attachments/assets/7173a3ee-e897-46f6-85c0-83e038e2f34d" />

데이터 분석을 시작하기 전, 데이터 품질 관리를 위한 다양한 검증 작업을 수행하고 검토를 통해 데이터셋을 숙지하는 과정을 거침.
  
[체인지로그 엑셀 파일 다운받기]    
<br>

# 핵심 요약 
### 주요 발견 사항/분석 결과 개요
- 2016년 10월을 제외하고 4분기 매출이 바닥($0/$11)을 기록한 이후, 다음달 2017년 1월에 급격히 상승하여 최고 증가율을 보였음($114,090). 2017년 2월에도 전월대비 매출 증가율이 116%(MoM 116%), 주문건수는 132% 증가. 2017년 3월부터 안정적인 증가 추세에 접어든 이후 가장 큰 매출 증가율을 보인 날짜는 2017년 11월 (MoM 49%). 
- 매출, 주문 모두 전반적으로 증가 추세이며 예측선을 통해 추후에도 지속적으로 상승할 것으로 예측됨. 
- 평균 구매 금액은 2016년 11월, 12월 바닥을 기록하고 다시 평균 금액 선에 안착됨. 평균 구매 금액 증감율 모두 전월 대비 10% 이내. 평균 구매 금액은 추후 $139로 지속될 것으로 예측됨. 
- 다음 섹션에서 추가적으로 현상에 기여한 원인을 심층 분석하고 개선될 수 있는 부분에 대해서 알아봄.

[전체 트렌드 시각화 또는 대시보드 스냅샷 삽입!]     
<br>    

# 심층 분석
### 1. 매출 트렌드:
* **2016년 9월 중순부터 2018년 말까지 최고 매출액은 $999,398 최저 매출액은 $0**
  * 2016년 말 매출/주문이 0으로 바닥
* **2017년부터 매출이 수직 상승(급상승)하였고 3월 이후 부터 전반적인 상승세를 유지**
  *	2017년 5월과 11월에 매출 증가율 40% 이상으로 큰 폭으로 상승 
  * 2018년 9월 이후부터 지속적으로 매출이 3%정도의 증가율을 보일 것으로 예상됨.
* **2017년 11월 최다 주문 건수, 전월 대비 매출액 증가률 49%로 최대**
  * More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
* **평균 구매 금액(AOV)는 큰 변동이 없음**
  * 2018년 9월 이후 예측선에도 $139로 일정함
* **지역별 성과**
  * 상파울루 매출액, 주문수에서 가장 큰 성과를 보이지만 평균 구매 금액을 보면 상파울루가 $125로 전체 평균 구매 금액인 $137보다 적음.
  * 평균 구매 금액(AOV)은 파라이바가 $216로 가장 큼.
  * 다른 지역들과 확연한 차이는 없음. 

[Visualization specific to category 1]      
<br>

### 2. 제품라인별 성과:
* **총 71개의 제품라인 중 최고 수익 제품은 "건강/뷰티"이고 최다 주문 및 구매개수 제품은 "침구/욕실/테이블"**
  * 시계/선물 제품은 평균 가격이 $200로 최다 구매개수가 7위이지만 매출액은 2위  
  * 주문 수와 구매개수 순위는 1~3위까지 동일하지만 4위에서 주문수는 컴퓨터/액세서리, 구매개수는 가구/인테리어.
* **가장 수익성이 좋은 제품은**
  *	2017년 
  * 2018년
* **평균 구매개수에 미치지 못하는 제품라인은 56개**
* **매출이 점점 증가하는 제품**
* **매출이 점점 감소하는 제품**

[Visualization specific to category 2]   
<br>  

# 권장사항:
Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following: 
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**      
<br>



# 가정 및 한계:
본 분석 과정에서 데이터 상의 문제를 해결하기 위해 여러 가정을 설정하였으며 이에 대한 가정과 한계의 세부사항은 아래와 같습니다.
* 2016년 말 주문건수/매출액이 데이터 클렌징 과정에서 누락된 값이나 오류가 포함된 행 제거로 사라졌을 경우 정확한 주문건수/매출액이 아닐 수 있음
* 매출액은 계산가능하나 실제 기업의 영업이익은 알 수 없음. 판매자들이 상품을 올리면서 내는 수수료에 대한 정확한 정보가 요구됨.
* 고객의 고유한 아이디 개수는 주문 건수와 동일함. 즉, 반복구매한 고객을 찾아볼 수는 없었음 (지역별 주문수 = 지역별 고객 수)
* 제품라인안에 어떤 구체적인 제품이 포함되어 있는지 알 수 없음


