# 프로젝트 개요
Olist는 2015년 7월에 설립된 브라질의 이커머스 기업으로, 중소기업들이 다양한 온라인 마켓플레이스에서 제품을 판매할 수 있도록 연결하는 플랫폼을 제공합니다. 본 프로젝트는 Olist의 매출, 주문 수, 제품 라인업 등 방대한 데이터셋을 종합하고 분석하여, Olist의 시장 경쟁력을 강화할 인사이트를 도출하는 것을 목표로 진행되었으며 다음 2가지 핵심 영역에 대한 분석 결과와 전략적 제안을 제시합니다:

- **매출 트렌드 분석:** 2016년 9월부터 2018년 8월까지의 총 상품 거래액(GMV) 변동을 분석하여 소비 트렌드, 지역별 경제적 요인 등이 플랫폼에 미치는 영향을 파악. 이를 위해 브라질 전체 및 26개 주별로 매출액, 주문량, 평균 주문 금액(AOV)에 집중한 분석을 수행. 
- **제품라인별 성과 분석:** 71개의 제품 라인을 유사한 특성에 따라 제품군으로 재분류하여 각 제품군이 전체 매출에 미치는 영향을 파악하고 어떤 카테고리가 매출을 주도하는지 파악함으로써 판매자들에게 효과적인 판매 전략과 가이드라인을 제공.
<br>  
다양한 비즈니스 문제 해결을 위한 맞춤형 SQL 쿼리 모음은 [링크]에서 확인하실 수 있습니다.
<br>
매출 트렌드을 실시간으로 탐색할 수 있는 동적 Tableau 대시보드는 [링크]에서 확인 가능합니다.       
<br><br><br>  

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
<br><br>      
데이터 분석을 시작하기 전, 데이터 품질 관리를 위한 다양한 검증 작업을 수행하고 검토를 통해 데이터셋을 숙지하는 과정을 거침.<br><br>     
      
- 데이터를 점검하고 정제하는데 사용된 Python 코드는 여기에서 확인할 수 있습니다: [링크].<br>     
- 데이터 클렌징 과정에서 이루어진 모든 변경사항에 관한 기록(데이터 수정 내역; changelog)은 [여기](https://raw.githubusercontent.com/jeewon-yoon/E-commerce_Comprehensive_Performance_Report/master/Changelog.xlsx)에서 확인할 수 있습니다.<br> 
- 유사한 제품군을 묶어서 정리한 카테고리 테이블은 [여기](https://raw.githubusercontent.com/jeewon-yoon/E-commerce_Comprehensive_Performance_Report/master/category_table.pdf)에서 확인할 수 있습니다.
<br><br>

# 핵심 요약 
### 주요 발견 사항(분석 결과 개요)
2016년 4분기 매출은 10월($49,157)을 제외하고 바닥(11월: $0 / 12월: $11)을 기록한 후, 2017년 1월($114,090)과 2월($246,890)에 걸쳐 **2개월 연속 100K 이상 급증**하며 상승세로 전환되었습니다. 이후 2017년 3월부터 안정적인 성장 추세를 보였으며, 예측선에 따라 향후 지속적 상승이 전망됩니다.  
특히 **2017년 11월**에는 전월 대비 **49%의 MoM 성장률**을 기록하며 최대 매출 증가율을 보였으나, 2018년에는 상승과 하락이 반복되는 변동성이 증가했습니다. 예를 들어, **2018년 6월(-15%)과 7월(-8%)** 에는 연속적인 매출 감소가 발생했습니다.  
한편, 평균 구매 금액(AOV)은 전월 대비 **±10% 범위 내에서 안정적**이었으며, 예측 모델에 따르면 향후 **$135 수준**을 유지할 것으로 예상됩니다.  
다음 섹션에서는 2016년 말 매출이 바닥이었던 이유와 2018년 성장세 둔화의 원인(경제 환경, 경쟁사 영향 등)을 심층 분석하고, 운영 효율성 제고를 위한 전략을 제시합니다.<br>  

<img width="600" height="300" alt="Image" src="https://github.com/user-attachments/assets/2f6a014e-7f76-410c-8197-792a2c504a3e" />
<br><br>      

# 심층 분석
### 1. 매출 트렌드:
* **2016년 9월 중순부터 2018년 8월말의 기간 중 최고 매출액은 2018년 5월, $999,398였고 최저 매출액은 2016년 말, $0**
  * 2014~2016년까지는 브라질의 심각한 경기침체기로 소비 심리가 위축되어 고객들의 이커머스 지출이 감소했을 것으로 해석
  * 2017년 1월부터 매출이 수직 상승(급상승)하였고 장기적인 관점에서 성장세가 뚜렷함.
  * 2018년에 들어서면서 비교적 매출 증감율 변동성이 커지고 예측을 통해 9월 이후에도 지속적으로 매출이 3% 정도의 증가율을 보일 것으로 예상됨.
    
* **2017년 11월 최다 주문 건수, 전월 대비 매출액 증가률 49%로 최대**
  * 11월 4째주 블랙 프라이데이가 포함되어 있고 크리스마스 사전 구매를 위한 연말 쇼핑으로 소비 증가 효과가 나타난 것으로 해석됨
	
* **평균 구매 금액(AOV)은 큰 변동이 없음**
  * 안정적인 성장시기(2017년 3월~)에 접어든 이후 전월 대비 증감율은 10% 이내
  * 2018년 9월 이후 예측선에도 $135로 일정함

* **지역별 성과**
  * 평균 구매 금액은 파라이바가 $215로 최대 상파울루가 $124로 최소. 
  * 상파울루 매출액, 주문수에서 가장 큰 성과를 보이지만 평균 구매 금액을 보면 $125로 전체 평균 구매 금액인 $136.9보다 적음.
    * 상파울루 인구는 약 4600만명으로 브라질의 주중 가장 많은 인구를 보유하고 있으며 도시
  * 파라이바는 매출액, 주문수에서 17위를 차지하지만 평균 구매 금액 순위는 $216로 가장 큼.
  
[Visualization specific to category 1]      
<br>

### 2. 제품라인별 성과:
(총 71개의 sub 카테고리를 14개의 제품군으로 분류)

* **매출 1순위 제품군은 가구/인테리어, 매출 1순위 카테고리는 건강/뷰티**
  * 가구/인테리어 제품군 내 최다 주문 및 구매개수 카테고리는 "침구/욕실/테이블"
  * 시계/선물 카테고리는 평균 가격이 $200로 최다 구매개수가 7위이지만 매출액은 2위  
  * 주문 수와 구매개수 순위는 1~3위까지 동일하지만 4위에서 주문수는 컴퓨터/액세서리, 구매개수는 가구/인테리어.

* **매출액 상위 10%(~7위)에 랭킹된 sub카테고리 대부분 2017년 11월 정점을 찍고 매출액이 감소하는 추세** 
  * 2017년 말/2018년 초 이후 매출액이 점점 감소하는 카테고리: 스포츠/레저(4위), 컴퓨터/악세서리(5위), 특별 상품(7위)
  * 2017년 말/2018년 초 이후에도 매출액이 꾸준히 증가하는 제품: 건강/뷰티(1위)


[Visualization specific to category 2]   
<br><br>    

# 권장사항
분석 결과를 바탕으로 다음과 같은 전략적 권장사항을 제시합니다.

**매출액이 큰 비중을 차지하지만 주문이 감소하는 제품에 대해 블랙 프라이데이와 같은 할인행사 또는 프로모션 전략 적용**
* 시계/선물, 스포츠/레저, 컴퓨터/악세서리 제품라인은 모두 매출액 5위안에 드는 제품라인들로 전체 매출의 7~9%를 차지하지만 2017년 말 이후 꾸준히 매출액이 감소하는 추세. 이 제품라인들에 대해 프로모션 행사 적용.

**지역별로 제품라인 구매에 따른 소비패턴을 통한 맞춤형 마케팅.** 
* 상파울루는 브라질 전체 인구의 22%가 거주하는 메가시티로 중산층 이상 인구 비중이 높아 소비 시장이 활발. 기존 고객들이 재구매하고 꾸준히 매출이 성장하는 제품라인에 집중.
* 파라이바는 인구가 적지만 고객당 높은 구매력(LTV)을 보유한 잠재 시장. 고객 세분화를 통해 고소득층의 거주지인 주앙페소아에 거주하는 고객을 대상으로 파라이바에서 인기있는 컴퓨터 또는 시계/선물 제품라인에 대해서 프로모션 가능.

**전체적으로 평균 배달 기간이 9~10일**
* 배달기간을 단축시킬 필요성이 있음.
<br><br><br>      


# 가정 및 한계
본 분석 과정에서 데이터 상의 한계 또는 문제점을 서술하였으며 이를 해결하기 위해 설정한 가정 및 세부사항은 아래와 같습니다.

* **Olist의 영업이익 산출 한계**: Olist의 수익 구조은 판매자에게 플랫폼 수수료를 징수하는 비즈니스 모델. 즉 GMV는 판매자들이 플랫폼을 통해 판매한 전체 상품의 판매액 합계로 Olist의 직접적인 매출은 아니지만 플랫폼의 규모와 성장성을 보여주는 핵심 지표. 높은 GMV는 Olist가 많은 거래를 중개하고 있으며, 시장에서 경쟁력을 갖추고 있다는 뜻으로 이는 투자자나 내부 경영진이 Olist의 성과를 평가할 때 중요한 기준.
  * **Olist의 실제 매출을 알기 위해 요구되는 지표들**: 수수료율, 물류 및 이행 비용, 운영 비용 등
* 데이터 정제 과정에서 누락값 및 오류가 포함된 행을 제거함에 따라 2016년 말의 주문건수 및 매출액이 실제와 상이할 수 있습니다.
* 고객식별 한계: 고객 고유 ID 개수와 주문 건수가 동일하여 반복 구매 고객 추적 불가. 따라서 지역별 주문 수 분석은 해당 지역의 고유 고객 수를 반영.
* 제품라인 정보 미비: 제품 라인의 구체적 구성(브랜드, 상품명 등)이 명시되지 않아 제품 단위 심층 분석이 불가능합니다.


