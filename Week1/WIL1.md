1-7장 정리 // 자율전공학부 C035231 신호림

1장. 자바스크립트의 개요
    자바스크립트(javascript) js(확장자 이름)
        - 인터프리트 언어(한줄씩 기계어로 번역) : 느림 but 오류가 있어도 그 부분 제외 실행가능
            - 특이사항 : JIT compiler(just in time compiler) 내장 -> 실행 속도 빨라짐, 덕분에 웹 어플구현 가능
        - 객체 지향 + 함수형 (말 그대로 객체도 쓰고 함수도 쓴다)
            - 객체 지향 : 다른 언어들과 달리 class 가 아니라 prototype 을 상속
                - property - 멤버 변수 / method - 멤버 함수 (c++과 비교)
                - 객체만든 후에도 멤버들 동적 추가 가능, 이하 동적 프로토타입 기반 객체지향언어
        - 동적 타입 -> 변수 타입이 없다. (float, double, int 등...없이 그냥 var하나로)
        - 함수를 인수로 가능 + 함수가 클로저를 정의
    기술적 요소
        - ECMA 스크립트8 (코어 언어)
        - 클라이언트 측 자바스크립트 -> 웹 브라우저에서 동작
            - 코어 언어 + 웹 브라우저의 API 
                API - window interface + DOM + XMLHttpRequest
        - 서버 측 자바스크립트 -> 웹 서버에서 동작
            - Node.js + Rhino + Aptana Jaxer

2장. 작성법 & 실행법
    - 작성법
        - 텍스트 편집기(메모장) or 프로그램 작성용 편집기(vscode)로 코드 생성
        - 특이사항 : 
            - 1. 어휘 분석 / 구문 분석
                - js 인터프리터 : 프로그램 -> 토큰(어휘) 분해(어휘 분석) -> 문법 검사(구문 분석)
                - 빈 문장 - ;
                - 세미콜론 ; 자동 추가
    - 실행법
        - 1. 크롬 콘솔 쓰기
        - 2. html문서에 코드 넣고 크롬 등 웹브라우저 콘솔쓰기
        - 3. Node.js에서 실행
            - 대화형 (터미널에 node 입력)
            - 편집기 모드 (.editor 입력) -> .exit (종료)
            - 파일읽어와서 실행
                - 윈도우의 경우 cd 입력, 엔터치고 주소 입력

3장. 변수와 값
    - 변수
        - 변수 타입없음 -> var로 통일 ex) var sum; // 선언만 하면 undefined값이 채워짐
        - var안쓰고 x=2; 이렇게 선언 -> 전역변수(global) (함수 안팎에서 모두 적용되는 특징임)
        - 일단 호출하고 나중에 변수 선언해도 끌어올려서 실행(hoisting) 
            - 주의사항 : var x = 5; 이렇게 초기화도 한 경우는 hoisting X
    - 데이터 타입 : 원시 타입과 객체 타입
        - 원시 타입 : 숫자, 문자열, boolean (논리값), 특수값(undefined, null)
        - 비원시 타입 -> "객체"
        - 동적 타입과 정적 타입
            동적 타입 : 정해진 데이터 타입이 없다.
            정적 타입 : int, float, double, bool 등 정해짐
    - 수
        - 리터럴 : 직접 쓸 수 있는 상수(const)값
    - 심벌 (new 추가!)
        - Symbol()사용해서 만듬 ex) var sym1 = Symbol();
        - 특이사항 : 호출할 때마다 값이 달라진다. (python의 random같은 느낌)
        - 문자열이랑 연결 가능
            var sym1 = Symbol("club");
            var sym2 = Symbol("club");
            console.log(sym1 == sym2); // sym1, sym2를 club으로 연결함 -> sym1 == sym2
            문자열 값 찾는 방법? console.log(Symbol.keyFor(sym1)); // club

4장 객체 / 배열/ 함수 기초
    객체 : 원시 타입이 아닌 모든 데이터 타입
        - 프로퍼티(property) - 멤버 변수 / 메소드(method) - 멤버 함수 (c++과의 비교..?)
            - 동적 데이터 타입이기 때문에 객체 만들고 나서도 property or method 추가 가능
            - 객체 리터럴 (object literal)
                - var p = {x: 1.0, y: 2.5}; // 이렇게 중괄호 안에 나열, 가독성을 위해 엔터쳐서 줄 나눠도 된다. 한 줄에 한 프로퍼티씩!
        - 메소드(method) - 사실 메소드도 프로퍼티가 맞다. 대신 프로퍼티에 함수(동작)가 저장되면 메소드
            - card라는 객체가 있다고 하면, var a = card; 라고하면 a, card는 모두 같은 객체를 가리키는 중(참조 -> 별명 개념임)
    함수 : 
        - function square(x) {return x*x}; // 정의 방법
            - 함수가 객체임. 즉 함수 이름 = 객체 이름 / square는 함수를 참조하고 있다.
        - square(3); // 호출 방법
        - 변수 선언과 마찬가지로 함수 선언문도 소급 적용(일단 쓰고 뒤에 선언 가능 - hoisting(끌어올림)덕분)
        - call by reference vs call by value
            - 원시값을 인수로 넘기면 값이 복사-> call by value
            - 객체를 인수로 넘기면 그 객체의 참조값이 전달 -> call by reference
                - 함수 안에서 바꿔도 객체의 참조가 인수로 들어가서 실제 객체도 바뀜
        - 객체도 인수로 넘길 수 있음 -> 을 이용한 인수 여러 개 편하게 전달하기
            - 여러 인수를 묶어서 하나의 객체를 만들고 그 객체를 전달하기
                - var parameters = {
                    x: 0;
                    y: 0;
                };
                setBallproperties(parameters); // parameters 객체를 인수로 전달
        - 변수 충돌 시 - 지역 변수 사용(지역 변수의 범위에서 충돌할 경우)
        - 블록 유효 범위 let & const : {} 안에서만 유효
            - let : {}안에서만 유효한 변수 선언
            - const : {}안에서만 유효한 일회성 상수 선언
            - let 특이사항 : {}밖에서 썼을 때는 전역 변수처럼 동작. {}안의 같은 이름의 변수와 충돌? 그런거없다. 그냥 inner x, outer x 따로따로 존재
            - const 특이사항 : 수정 불가 but 상수 값이 객체or배열이면 그들의 프로퍼티 수정 가능
        - 함수 리터럴로 함수 정의
            - 원래 정의 : function square(x) {return x*x} // ; 안붙여도 된다.
            - 리터럴 정의 : var square = function(x) {return x*x}; // 특이사항 : 리터럴은 ; 꼭 붙여야! + hoisting(소급 적용) 안먹힘
        - 객체의 메소드 정의
            var circle ={
                center: {x: 1.0, y: 2.0},
                radius = 2.5;
                area: function(){ // 프로퍼티값으로 함수 리터럴 대입
                    return Math.PI * this.radius * this.radius;
                } // 여기까지 함수 리터럴.
            };

            실행은 circle.area() (;안써도 된다.)
            결론 : 메소드도 객체 선언 후에 함수 리터럴을 이용해서 추가할 수 있다!
    생성자 : var card = new Card("하트", "A"); // 생성자를 이용한 객체 생성, new연산자 쓰기 -> 프로퍼티 양식에 맞게 인수 전달 및 생성
    내장 객체 : built in object
    배열 : 
        - 배열 리터럴 : var evens= [2,"pi",6.8,8]; // int float bool 다양한 타입 전부 가능 var로 선언
        - Array 생성자 : var evens = new Array(2,4,6,8); 
        // 이렇게 2가지 방법
        배열도 객체다!
            - var a = ["a", "b", "c"];
            console.log(a["2"]); // c나옴
            공리 : 당연한 사실 : 배열이든 함수든 없는 프로퍼티 읽으려고 하면? undefinded 뜬다.
        - 요소 추가&제거 방법
            - a.push("d");
            - a[3] = "d";
            - delete [1]; // 1 index의 요소를 지워라. 그러면 undefinded로 채워짐. 길이는 그대로. 알아서 당겨지고 그런거 없다.
5장. 표현식과 연산자
    특이사항 : 문자열과 숫자가 섞일 수 있다.
        - ex) 1+"2month" -> "12month" // 문자열이랑 섞이면 다른 숫자도 문자열로 바뀌어서 합쳐진다.
        - Math객체(자동 내장된)의 프로퍼티에 이것저것 많다.
    문자열 제어
        - String 객체 : 원시 값을 String 객체로 변환 (래핑, wrapping). 
        - var msg = "Heeee";
        - var msgObj = new String(msg); // msg 를 msgObj로 바꾼다. 객체로.
        - 당연하지만 문자열을 객체가 아니라 배열로도 처리할 수 있다. ex) msg[3] -> e 이런 식
6장. 웹 브라우저에서의 입출력
    6.1 대화 상자
        - Window객체 - 웹 브라우저의 전역 객체,  3개의 메소드
            - window.alert : 경고
            - window.prompt : 문자열 입력 (프롬프터)
            - window.confirm : 확인(confirm) or not 버튼 표시 ex) 링크를 표시하시겠습니까?
    6.2 console객체 - 출력시 사용하는 console.log()도 console객체 맞음
        - 주로 콘솔에 값을 출력할 때 씀
        - 타이머
            console.time("answer_time");
            alert("확인 버튼을 누르세요"); // 실행시간 측정
            console.timeEnd("answer_time"); // 걸린 시간이 뜬다.
    6.3 이벤트 처리기
        - 이벤트 (마우스로 클릭, 키보드로 입력 등) 발생 시 미리 매치해둔 작업 수행
        ex) 클릭버튼을 누르면 현 시간을 알려준다
        - 다양한 이벤트 처리기가 이미 준비됨.
        - DOM(document object model) : js 프로그램이 html요소를 조작할 수 있게 하는 interface
        
7장. 제어 구문
    사실 제어 구문은 c, c++, python과 다를게 없음...
    딱히 특이사항이 없다.
