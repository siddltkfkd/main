<서버>
1. 접속 관리
	1) 연결 host 정보 -> 생성시 처리
	2) 블랙 리스트 관리 -> 서버에 리스트 생성

2. 리소스 사용 현황 -> 데이터 가져오기
	1) CPU 사용률
	2) 메모리 현황
	3) Storage 현황

3. 웹 서비스 구성
	1) URL parsing
	2) GET, POST는 다른 노드에서 처리
	3) 쿠키를 통한 접속 상태 관리 -> 접속 요청할때 쿠키를 같이 보냄
	4) 데이터 형식 : JSON, HTML, XML ...
	

<웹서비스>
1. 데이터 수집 -> 디바이스 관리 서버에서 얻기 
	-> 디바이스 정보 (모델, 일련번호)
	-> 센서 수집 정보 -> (센서 종류, 수집 주기, 센서 값)
2. 수집한 데이터는 파일에 저장
	-> 데이터는 일정 시간 간격으로 정리됨
	-> 정리된 후, 지정된 형식(JSON)을 갖는 파일에 저장됨
3. 요청이 오면 저장된 데이터를 보여줌


<노드 구성>
1. Input Node
	1) stdIn
		표준 입력 데이터를 flow 메시지로 변환
		flow에 넣기
	2) socketIn
		socket에서 들어온 데이터를 flow 메시지로 변환
		flow에 넣기

2. Output Node
	1) stdOut
		Flow에서 처리된 결과를 표준출력으로 출력
	2)	socketOut
		Flow에서 처리된 결과를 소켓으로 출력

3. Process Node
	1) HTTP client Node
		지정된 host에 연결
		연동된 socketIn/Out Node를 통해 서버와 통신
	2) HTTP server Node
		Client가 연결되기를 기다림
		연결 되면 연동된 socketIn/Out Node를 통해 클라이언트와 통신
	3) Filter Node
		메세지 데이터 분석하기
		통과 or 버리기
	4) Predicate Node
		Message 결과를 조건식에 맞춰 true/false로 결정
	5) Selection Node
		특정 메시지를 특정 출력 port로 내보냄
	6) Trace Node
		로그 출력
		Exception 처리
	7) Extra Node
		추가 기능 구현
		
<Pipe 구성>
메시지가 이동하는 파이프
1. 특정 갯수 메시지 저장
2. 일정 시간이 지난 패킷은 폐기
3. 패킷의 종류에 따라 우선순위 매기기
