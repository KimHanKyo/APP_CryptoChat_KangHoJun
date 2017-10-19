# CryptoChat  
## AES-256 암호화, Socket.IO를 사용한 보안 채팅 어플리케이션 

팀 : 이 오픈소스는 무료로 해줍니다
참가자 : 강호준

---------------
### 어플리케이션 소개

훈련이나 평시에 직접 만날 수 없는 거리에 있는 군인끼리 군사정보를 주고받아야 하는 경우가 발생하기도 하는데, 비문통신에 필요한 장비가 없으면 매우 난감한 상황이 발생합니다.
현재 군 간부들은 스마트폰을 많이 사용합니다. 그래서 급한대로 들고있는 스마트폰으로 정보를 보내버릴 수도 있는데, 이 경우 보안사고로 연결됩니다. 
그럴 때, 이 어플리케이션을 사용하면 안전하게 메세지를 주고 받을 수 있습니다.

상호간에 합의된 암호키를 알고있지 않은 이상, 중간에 통신 데이터를 가로채가도 AES알고리즘으로 암호화된 내용을 해독하기란 불가능 합니다.
암호키는 상호간의 구두로 합의된 키여도 되고, 비문으로 매일 매일 새로운 암호키가 할당되어 있어도 좋습니다. 
보내는 쪽과 받는 쪽이 같은 키를 알고만 있으면 상관없습니다.

항상 들고있는 스마트폰으로 간편하고 안전하게 암호화된 메세지를 주고 받을 수 있는 어플리케이션이 있으면 편하지 않을까 하고 이 앱을 개발하게 되었습니다. 

---------------
### 자세한 설명

#### 어플리케이션 관련
1. 이 어플리케이션은 socket.IO를 사용하여 소켓통신을 주고받습니다.
2. 주고받는 메세지는 AES-256 알고리즘으로 암호화되어 서버로 송신됩니다. 서버는 이미 암호화된 데이터를 받기 때문에 암호화에 사용한 문자열을 알 수 없습니다.
3. AES-256 암호화에 필요한 키는 사용자가 입력한 암호키(문자열)를 SHA-256 해시 암호 알고리즘을 사용해 해시값으로 만들어서 사용합니다.
4. 따라서 송신, 수신 측 모두 같은 암호키를 입력하지 않으면 서로의 메세지를 복호화 할 수 없습니다. 
5. 서로의 암호키가 다를 경우, 메세지내용은 보이지 않습니다. 
6. 사용자는 채팅 도중 암호키(문자열)을 변경하는 것이 가능합니다. 이 경우 기존의 메세지들(로그)는 사라지지 않습니다.
7. ID / Password로 로그인을 할 때 Password는 SHA-256 해시로 만들어 DB에서 대조합니다.

#### 서버 / DB 관련
1. 서버는 Node.js 를 사용합니다.
2. socket.io, express, mysql 모듈이 필요합니다.
3. 콘솔 로그로 사용자가 서버에 보낸 메시지(암호화 된 상태), 현재 채팅 접속자 수를 찍어줍니다. (동작 확인용)
4. DB에는 ID, Password, Name 이 저장되어있습니다.
5. DB에 Password는 SHA-256 해시값으로 저장되어 있어 원래 암호가 무엇인지 알 수 없습니다. 

---------------
### 사용시 주의사항 

1. 안드로이드 어플리케이션에서 서버의 ip는 **ServerIPConfig.java** 에서  `SERVER_IP` 라는 스트링만 수정하시면 됩니다.
2. 로그인 가능한 ID / Pw 조합은 다음과 같습니다.

    {ID / Pw}   

    { 12-123456 / abcd }
    { 15-12345  / 1234 }
    { 17-11111  / a1b2 }
    { 16-111111 / 4567 }


3. DB Name : OSAM / Table Name : kanghojun

---------------
### 개선을 위한 toDoList

1. 채팅 room 개설 - 모두가 한 room에서 메세지를 주고 받지 않고, 자기가 원하는 사람과 메세지를 주고 받을 수 있게 개선합니다.
2. UI 이쁘게 바꾸기 - 보기좋게!

