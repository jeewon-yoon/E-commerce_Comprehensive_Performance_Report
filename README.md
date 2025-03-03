## 프로젝트 개요
2015년 7월에 설립된 브라질의 이커머스 기업 Olist는 중소기업들이 온라인 마켓플레이스에서 제품을 판매할 수 있도록 연결해주는 플랫폼을 제공하는 오픈 마켓 형식으로 운영됩니다.
본 프로젝트는 Olist가 보유하고 있는 매출, 주문 수, 제품 라인업 등 방대한 데이터셋을 적극적으로 활용, 분석 및 종합하여 Olist의 경쟁력 강화를 위한 핵심 인사이트를 도출하고자 진행되었으며, (전반적인 매출과 제품 라인별 성과) 다음 2가지 핵심 영역에 대한 분석 결과와 전략적 제안을 제시합니다:

- **매출 동향 분석/전반적인 매출 개요:**
- **제품라인별 성과분석:**     
<br>  

(Backround about the company, including the industry, active years, business model, and key business metrics. Explain this from the POV of a data analyst who is working at the company.
Insights and recommendations are provided on the following key areas:)
- **Category 1:** 
- **Category 2:** 
- **Category 3:** 
- **Category 4:** 

The SQL queries used to inspect and clean the data for this analysis can be found here [link].
Targed SQL queries regarding various business questions can be found here [link].
An interactive Tableau dashboard used to report and explore sales trends can be found here [link].     
<br>

## 데이터 구조 및 초기 점검
Olist의 주요 데이터베이스는 총 X개의 레코드를 가진 4개의 테이블(customer, items, orders, products)로 구성되어 있음. 

각 테이블 설명:
- **customers:** 고객 아이디, 우편번호, 도시이름, 주 이름 등의 고객정보
- **items:** 주문 아이디, 제품 아이디, 배달시작 날짜, 가격, 배송비
- **orders:** 주문 아이디, 고객 아이디, 주문 상태, 구매 날짜시간, 주문 승인 날짜시간, 배달업체 배송된 시간날짜, 배달 시작 시간날짜, 예상 배달도착 시간날짜 
- **products:** 제품 아이디, 제품 카테고리명, 카테고리명 글자수, 제품 설명 글자수, 제품 사진 퀄리티 등
<br>    
<img width="698" alt="Image" src="https://github.com/user-attachments/assets/7173a3ee-e897-46f6-85c0-83e038e2f34d" />

데이터 분석을 시작하기 전, 데이터 품질 관리를 위한 다양한 검증 작업을 수행하고 검토를 통해 데이터셋을 숙지하는 과정을 거침.

[Entity Relationship Diagram here]    
[체인지로그 엑셀 파일 다운받기]    
<br>

## 핵심 요약 
#### 주요 발견 개요(사항)
Explain the overarching findings, trends, and themes in 2-3 sentences here. This section should address the question: "If a stakeholder were to take away 3 main insights from your project, what are the most important things they should know?" You can put yourself in the shoes of a specific stakeholder - for example, a marketing manager or finance director - to think creatively about this section.

[전체 트렌드 시각화 또는 대시보드 스냅샷 삽입!]


## 심층 분석(통찰)
### 카테고리 1:
* **주요 인사이트 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 1]      
<br>


## 권장사항:
Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following: 
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**      
<br>



## 가정 및 한계:
Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:
* Assumption 1 (ex: missing country records were for customers based in the US, and were re-coded to be US citizens)
* Assumption 1 (ex: data for December 2021 was missing - this was imputed using a combination of historical trends and December 2020 data)
* Assumption 1 (ex: because 3% of the refund date column contained non-sensical dates, these were excluded from the analysis)


