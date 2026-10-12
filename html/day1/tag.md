📚 HTML 주요 태그 학습 정리

오늘 학습한 HTML 핵심 태그들과 각 태그의 개념, 주요 속성, 그리고 예시 코드를 정리한 문서입니다.

1. <head> 태그 (문서 메타데이터)

개념: 웹페이지의 보이지 않는 정보(메타데이터)를 담는 영역입니다. 문서의 제목, 스타일시트 링크, 문자셋 인코딩 등을 정의합니다.

주요 내용: <title>, <meta>, <link>, <style> 등의 태그가 포함됩니다.

예시 코드:

<head>
    <meta charset="UTF-8">
    <title>나의 웹페이지</title>
    <link rel="stylesheet" href="style.css">
</head>


2. <body> 태그 (문서 본문)

개념: 웹브라우저 화면에 실제로 렌더링되어 사용자에게 보여지는 모든 콘텐츠(텍스트, 이미지, 버튼 등)를 담는 컨테이너입니다.

예시 코드:

<body>
    <h1>환영합니다!</h1>
    <p>이곳은 본문 영역입니다.</p>
</body>


3. <p> 태그 (문단)

개념: 텍스트 단락(Paragraph)을 나타내는 블록 레벨 태그입니다. 위아래로 자연스러운 여백이 생깁니다.

예시 코드:

<p>이것은 첫 번째 문단입니다.</p>
<p>이것은 두 번째 문단입니다.</p>


4. <ul> 과 <ol> 태그 (목록)

목록을 만들 때 사용하는 태그로, 순서가 없는 목록과 순서가 있는 목록으로 나뉩니다.

① <ul> (Unordered List)

개념: 순서가 없는 목록을 생성하며, 각 항목 앞에 글머리 기호(점 등)가 붙습니다.

자식 태그: <li>(List Item)를 사용하여 항목을 나열합니다.

예시 코드:

<ul>
    <li>사과</li>
    <li>바나나</li>
    <li>포도</li>
</ul>


② <ol> (Ordered List)

개념: 순서가 있는 목록을 생성하며, 각 항목 앞에 숫자나 알파벳 등 순서 번호가 자동으로 매겨집니다.

주요 속성:

type: 번호의 종류 지정 (1, a, A, i, I)

start: 시작 번호 지정 (예: start="5"는 5부터 시작)

예시 코드:

<ol type="1" start="1">
    <li>첫 번째 단계</li>
    <li>두 번째 단계</li>
</ol>


5. <input> 태그 (사용자 입력)

개념: 사용자로부터 데이터를 입력받기 위해 사용하는 인라인-블록 레벨 태그입니다. type 속성에 따라 다양한 형태(텍스트, 비밀번호, 체크박스 등)로 바뀝니다.

주요 속성:

type: 입력 폼의 유형 (text, password, checkbox, radio, submit 등)

placeholder: 입력란에 희미하게 나타나는 안내 문구

value: 기본값 설정

required: 필수 입력 설정

예시 코드:

<form>
    <label for="username">아이디:</label>
    <input type="text" id="username" placeholder="아이디를 입력하세요" required>
    
    <label for="password">비밀번호:</label>
    <input type="password" id="password">
    
    <input type="submit" value="로그인">
</form>


6. <img> 태그 (이미지 삽입)

개념: 웹페이지에 이미지를 삽입하는 태그입니다. 닫는 태그가 없는 빈(empty) 태그입니다.

주요 속성:

src: 이미지 파일의 경로 (URL 또는 로컬 경로)

alt: 이미지가 로드되지 않았을 때 대신 보여줄 대체 텍스트 (웹 접근성에 중요)

width / height: 이미지의 가로/세로 크기 지정

예시 코드:

<img src="./해적왕.png" alt="해적왕 이미지" width="300">