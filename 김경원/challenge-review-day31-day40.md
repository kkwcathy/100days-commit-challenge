# 지난 10일 나의 목표는?!
- [ ] 프로젝트의 기본적인 작동 플로우 완성하기 (게임 시작 -> 결과)

# 10일 돌아보면 잘한 점
- 이상한 오류를 고쳐가며 메모리 관리 면에서 많은 공부를 했다.

# 10일 돌아보며 아쉬운 점
- 오류 고치느라 목표를 못이뤘다...

# 10일 동안 공부한 내용
현재 진행 프로젝트: WinAPI로 지뢰찾기 만들기
목표: C++ 공부

- WinAPI
  - WinProc 함수 내 마우스 오른쪽 버튼 처리
    - WM_RBUTTONDOWN 메시지 사용
      정작 처리가 필요한 버튼 위에서는 받지 않았다.
    - WM_CONTEXTMENU 메시지 사용
      버튼 위에서도 성공적으로 마우스 오른쪽 입력을 받았으나, 좌표값이 창 내 기준이 아닌 전체 화면 기준이어서 ClientToScreen 함수를 통해 값을 보정해주었다.
  - 버튼 색상 변경
    - WM_CTLCOLORBTN 메시지 사용
      버튼을 그리기 전에 발생하는 메시지이다. 해당 case 문 내에서 버튼에 사용될 HBRUSH 값을 반환하면 버튼 색상이 변경된다길래 써보았는데 안됐다. 버튼 컨트롤이 배경을 직접 처리하는 방식 때문이라고 한다. 던졌다.
    - WM_DRAWITEM 메시지 사용
      버튼 핸들을 생성할 때 기본 스타일인 BS_DEFPUSHBUTTON이 아닌 BS_OWNERDRAW로 생성하면 위 메시지에서 직접 그리는 것이 가능해서 시도해보았는데 성공했다.
  - 버튼 스타일 변경 
    - 주로 비트 XOR 할당 연산자 사용
      예 :  
            // 현재 버튼의 스타일을 가져옴
            LONG_PTR style = GetWindowLongPtr(hButton, GWL_STYLE);

            // 스타일을 변경 (예: 토글 버튼 스타일 추가/삭제)
            style ^= BS_DEFPUSHBUTTON;  // 기본 스타일을 토글

            // 스타일 적용
            SetWindowLongPtr(hButton, GWL_STYLE, style);
    - 여러 스타일을 조합할 땐 OR 연산자 사용
      예 : WS_TABSTOP | WS_VISIBLE | WS_CHILD | BS_DEFPUSHBUTTON
    - 몇가지 주요 스타일
      - BS_PUSHBUTTON: 일반적인 버튼 스타일.
      - BS_CHECKBOX: 체크박스 스타일.
      - BS_RADIOBUTTON: 라디오 버튼 스타일.
  - 버튼 메시지 처리 시 주의사항
    - 버튼 메시지를 처리할 때 웬만하면 (버튼 핸들 != 윈도우 핸들) 예외처리를 해주는 것이 좋다. (예: hButton != hWnd) 이유는 메시지가 창 자체에서 발생했는지 버튼에서 발생했는지를 구별하기 위함이다.

- C++
  - 레이블(label) 역할에 관해
    프로그램의 흐름을 특정 위치로 점프 하거나 제어를 이동시키는 기능을 가지고 있다. C++에서는 switch 문 내 case, default 등이 해당 역할을 한다.
  - 클래스 타입 지역 변수 사용 주의사항
    함수 내에서 할당한 지역 객체를 참조로 반환한 경우, 다른 곳에서 사용했을 때 파괴돼서 이상한 값을 가진 객체가 될 수 있으니 주의하기. 

  
# 앞으로 10일 동안 나의 목표는?!
- [ ] (2트) 프로젝트의 기본적인 작동 플로우 완성하기 (게임 시작 -> 결과)
- [ ] 미뤘던 리팩토링 진행하기