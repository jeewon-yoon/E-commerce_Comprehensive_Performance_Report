# 프로젝트 개요
2015년 7월에 설립된 Olist는 중소기업들이 온라인 마켓플레이스에서 제품을 판매할 수 있도록 연결해주는 플랫폼을 제공하는 오픈 마켓 형식으로 운영되는 브라질의 이커머스 기업입니다.
본 프로젝트는 Olist가 보유하고 있는 매출, 주문 수, 제품 라인업 등 방대한 데이터셋을 적극적으로 활용, 분석 및 종합하여 
Olist에서 어떤 제품군이 매출을 주도하는지 파악하고 판매자를 지원(판매자들에게 더 나은 판매전략/가이드라인을 제안) 및 총 상품 거래액(GMV)을 파악하여 Olist의 경쟁력 강화를 위한 핵심 인사이트를 도출하고자 진행되었으며, 다음 2가지 핵심 영역에 대한 분석 결과와 전략적 제안을 제시합니다:

- **매출 트렌드 분석:** Olist의 과거(2016.09 ~ 2018.08) 매출 패턴을 전체 국가 수준과 26개 주별로 평가하여 매출액, 주문량, 평균 주문 금액(AOV)에 집중한 분석을 수행 
- **제품라인별 성과 분석:** Olist의 다양한 제품 라인을 다각적으로 분석하여 전체 매출에 미치는 영향을 파악
<br>  
다양한 비즈니스 문제 해결을 위한 맞춤형 SQL 쿼리 모음은 [링크]에서 확인하실 수 있습니다.
<br>
매출 트렌드을 실시간으로 탐색할 수 있는 동적 Tableau 대시보드는 [링크]에서 확인 가능합니다.     
<br><br>

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

데이터를 점검하고 정제하는데 사용된 Python 코드는 여기에서 확인할 수 있습니다: [링크].<br> 
데이터 클렌징 과정에서 이루어진 모든 변경사항에 관한 기록은 여기에서 확인할 수 있습니다: [데이터 수정 내역(changelog) 엑셀 파일 다운받기](https://raw.githubusercontent.com/jeewon-yoon/E-commerce_Comprehensive_Performance_Report/master/Changelog.xlsx) 
유사한 제품군을 묶어서 정리한 카테고리 테이블은 여기에서 확인할 수 있습니다: [링크]    
<br><br>

# 핵심 요약 
### 주요 발견 사항/분석 결과 개요
* 2016년 10월을 제외하고 4분기 매출이 바닥($0/$11)을 기록한 이후, 연속 2달 동안 급격히 상승하여 $100K씩 증가($114,090). 
* 2017년 3월 안정기에 접어들면서 전반적으로 긍정적인 성장 추세이며 예측선을 통해 추후에도 지속적으로 상승할 것으로 예측됨. 
* 안정적인 성장세 진입한 이후 가장 2017년 11월 가장 큰 매출 증가율(MoM 49%)을 보임
* 2018년은 보다 큰 폭의 상승과 하락이 반복, 6월과 7월 연속해서 매출이 감소
* 평균 구매 금액(AOV) 증감율 모두 전월 대비 10% 이내. 추후 $135로 지속될 것으로 예측됨. 

다음 섹션에서 추가적으로 현상에 기여한 원인을 심층 분석하고 개선될 수 있는 부분에 대해서 알아봄.
[전체 트렌드 시각화 또는 대시보드 스냅샷 삽입!]     
<br><br>      

# 심층 분석
### 1. 매출 트렌드:
* **2016년 9월 중순부터 2018년 8월말까지 최고 매출액은 $999,398 최저 매출액은 $0**
  * 2014~2016년까지는 브라질의 심각한 경기침체기로 소비 심리가 위축되어 고객들의 이커머스 지출이 감소했을 것으로 해석
  * 2017년 1월부터 매출이 수직 상승(급상승)하였고 장기적인 관점에서 성장세가 뚜렷함.
  * 2018년은 비교적 변동성이 커지고 예측을 통해 9월 이후에도 지속적으로 매출이 3%정도의 증가율을 보일 것으로 예상됨.
    
* **2017년 11월 최다 주문 건수, 전월 대비 매출액 증가률 49%로 최대**
  * 11월 4째주 블랙 프라이데이가 포함되어 있고 크리스마스 사전 구매를 위한 연말 쇼핑으로 소비 증가 효과가 나타난 것으로 해석됨
	
* **평균 구매 금액(AOV)은 큰 변동이 없음**
  * 안정적인 성장세 접어든 이후 전월 대비 증감율은 10% 이내
  * 2018년 9월 이후 예측선에도 $135로 일정함

* **지역별 성과**
  * 평균 구매 금액은 파라이바가 $215로 최대 상파울루가 $124로 최소. 
  * 상파울루 매출액, 주문수에서 가장 큰 성과를 보이지만 평균 구매 금액을 보면 $125로 전체 평균 구매 금액인 $136.9보다 적음.
    * 상파울루 인구는 약 4600만명으로 브라질의 주중 가장 많은 인구를 보유하고 있으며 도시
  * 파라이바는 매출액, 주문수에서 17위를 차지하지만 평균 구매 금액 순위는 $216로 가장 큼.
  
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
<br><br>    

# 권장사항
분석 결과를 바탕으로 다음과 같은 전략적 권장사항을 제시합니다.
* 매출액이 큰 비중을 차지하지만 주문이 감소하는 제품에 대해 프로모션 전략. **스포츠/레저와 "컴퓨터/악세서리" 제품라인은 매출액 4위로 전체 매출의 7%를 차지하지만 주문 및 평균 구매금액(AOV)이 감소 추세.**
**매출액 5위인 "스포츠/레저"와 6위인 "컴퓨터/악세서리"의 매출이 감소 추세.**

* 지역별로 제품라인 구매에 따른 소비패턴을 통한 맞춤형 마케팅. **상파울루는 브라질 전체 인구의 22%가 거주하는 메가시티로 중산층 이상 인구 비중이 높아 소비 시장이 활발. 기존 고객들이 재구매하고 꾸준히 매출이 성장하는 제품라인에 집중.**
**파라이바는 인구가 적지만 고객당 높은 구매력(LTV)을 보유한 잠재 시장. 고객 세분화를 통해 고소득층의 거주지인 주앙페소아에 거주하는 고객을 대상으로 파라이바에서 인기있는 컴퓨터 또는 시계/선물 제품라인에 대해서 프로모션 가능.**
<br><br>    

# 가정 및 한계
본 분석 과정에서 데이터 상의 한계 또는 문제점을 서술하였으며 이를 해결하기 위해 설정한 가정 및 세부사항은 아래와 같습니다.

* Olist의 영업이익 산출 한계: Olist에 상품을 올리는 중소기업 판매자들의 정보, 판매자들이 상품을 올리면서 내는 플랫폼 수수료, 운송업체 비용 등에 대한 정보가 부재. 
  * 판매자들에게 제품라인별 성과를 분석하여 판매 가이드라인을 제시하기 위한 분석을 진행. 
  * 소비자들이 실제 어떤 제품을 더 구매하는지 보여주기 위해 유사한 아이템끼리 그룹화하여 제품라인 분석
* 데이터 정제 과정에서 누락값 및 오류가 포함된 행을 제거함에 따라 2016년 말의 주문건수 및 매출액이 실제와 상이할 수 있습니다.
* 고객식별 한계: 고객 고유 ID 개수와 주문 건수가 동일하여 반복 구매 고객 추적 불가. 따라서 지역별 주문 수 분석은 해당 지역의 고유 고객 수를 반영.
* 제품라인 정보 미비: 제품 라인의 구체적 구성(브랜드, 상품명 등)이 명시되지 않아 제품 단위 심층 분석이 불가능합니다.


