<h1 id="datatype">datatype</h1>
<h3 id="관계형-데이터베이스">관계형 데이터베이스</h3>
<ul>
<li>프로그래밍 요소 제공(X),변수 없음</li>
<li>SQL &gt; 대화형 언어 &gt; 문장 단위의 작업으로 구성된다.</li>
<li>자료형 &gt; 테이블 정의할 때 사용 (= 컬럼의 자료형)</li>
</ul>
<h3 id="ansi-sql-자료형">ANSI-SQL 자료형</h3>
<pre><code>- 오라클 자료형</code></pre><h4 id="1-숫자형">1. 숫자형</h4>
<ul>
<li>정수, 실수
a. number <ul>
<li>(유효처리)38자리 이하의 숫자를 표현하는 자료형</li>
<li>5~22byte</li>
<li>1x10^-138 ~ 9.9999x10^125</li>
</ul>
</li>
</ul>
<ul>
<li><em><strong>number</strong></em> : 정수를 넣어도 되고 실수를 넣어도 됨,가장 넓은 범위 표시 가능</li>
<li><em><strong>number(precision)</strong></em> : 전체자리수 &gt; 정수만 저장, 소수를 입력시 정수만 저장, 반올림 됨, 123456789는 오버플로우,-999~999까지 출력가능</li>
<li><em><strong>number(precision, scale)</strong></em> : 전체 자리수 + 소수 이하 자리수 &gt; 정수/실수 저장, -99.99~99.99</li>
</ul>
<h4 id="2-문자형">2. 문자형</h4>
<ul>
<li>문자 + 문자열(문자만은 없다! 다 문자얼)</li>
<li>char vs nchar &gt; n의 의미? n : national(유니코드)</li>
<li>char vs varchar &gt; var의 의미?</li>
</ul>
<p>a. char(차 라고 읽음)</p>
<ul>
<li>고정 자릿수 문자열  &gt; 무조건 10자리를 확보해라!, 남는 자리는 스페이스로 채워라(10은 예시 숫자)</li>
<li>char(n) : 최대 n자리수 문자열, n(바이트) &gt; utf-8(영어1byte,한글3byte) &gt; 주로 사용<ul>
<li><em><strong>char(n byte)</strong></em> &gt; 바이트</li>
<li><em><strong>char(n char)</strong></em> &gt; 문자수</li>
</ul>
</li>
<li>최소 크기 : 1바이트</li>
<li>최대 크기 : 2000바이트</li>
</ul>
<p>b. nchar</p>
<ul>
<li>고정 자릿수 문자열</li>
<li><strong><em>nchar(n)</em></strong> : 최대 n자리수 문자열, n(문자 수) &gt; utf-16(영어2byte,한글2byte)<pre><code>      - 최소 크기 : 1문자
      - 최대 크기 : 1000문자</code></pre></li>
</ul>
<p>c. varchar2</p>
<ul>
<li>varchar(variable char, 바차 라고 읽음)</li>
<li>가변 자릿수 문자열 &gt; 삽입된 데이터 크기만의 공각만 차지한다. 나머지 7칸을 반환한다.(7는 예시 숫자)</li>
<li><strong>_ varchar2(n)_</strong> : 최대 n자기 문자열, n(바이트)<pre><code>       - 최소 크기 : 1바이트
       - 최재 크기 : 4000바이트 </code></pre></li>
</ul>
<p>d. nvarchar2</p>
<ul>
<li>varchar(variable char, 바차 라고 읽음)</li>
<li>가변 자릿수 문자열 &gt; 삽입된 데이터 크기만의 공각만 차지한다. 나머지 7칸을 반환한다.(7는 예시 숫자)</li>
<li><em><strong>varchar2(n)</strong></em> : 최대 n자기 문자열, n(문자 수)<pre><code>      - 최소 크기 : 1바이트
      - 최재 크기 : 4000바이트 </code></pre></li>
</ul>
<p>e. clob , nclob</p>
<ul>
<li>대용량 텍스트</li>
<li>character large object</li>
<li>최대 128TB</li>
</ul>
<h4 id="3-날짜시간형">3. 날짜/시간형</h4>
<p>a. date</p>
<ul>
<li>년 월 일 시 분 초</li>
<li>기원전 4712년 1월 1일 + 9999년 12월 31일</li>
</ul>
<p>b. timestamp</p>
<ul>
<li>년 월 일 시 분 초 + 밀리초 + 나노초</li>
</ul>
<p>c. interval</p>
<ul>
<li>시간</li>
<li>틱값 저장용</li>
</ul>
<h4 id="4-이전-데이터형">4. 이전 데이터형</h4>
<ul>
<li>비 텍스트 데이터</li>
<li>이미지, 동영상, 음악, 실행파일, 압축파일 등,,,</li>
<li>게시판 &gt; 첨부파일 &gt;파일명만 DB에 저장
a. blob, binary large object<pre><code>      - 최대 128TB</code></pre></li>
</ul>
<blockquote>
<p><em>** 결론적으로 사용할 데이터형**</em></p>
</blockquote>
<ol>
<li>숫자 &gt; number</li>
<li>문자열 &gt; varchar2</li>
<li>날짜 &gt; date</li>
</ol>
<h1 id="select">select</h1>
<h4 id="select문">SELECT문</h4>
<ul>
<li>DML, DQL</li>
<li>가장 중요한 Query</li>
<li>CRUD</li>
<li>데이터베이스의 테이블로부터 데이터를 가져오는 명령어</li>
</ul>
<blockquote>
<p>[WITH &lt;SUBQUERY&gt;] 
SELECT column_list
FROM table_name
[WHERE search_condition]
[GROUP BY group_by_expression]
[HAVING search_condition]
[ORDER BY order_expression [ASC | DESC]];
-&gt; 적는 순서, 대괄호는 생략 가능</p>
</blockquote>
<pre><code>SELECT column_list
FROM table_name</code></pre><h4 id="각-절의-순서반드시-외워야한다">각 절의 순서(<strong><em>반드시 외워야한다</em></strong>)</h4>
<ol>
<li>FROM 절 (거의 1등)</li>
<li>SELECT 절 (거의 꼴등)</li>
</ol>