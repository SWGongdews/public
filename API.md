# API
- [ 공통 ]
  - return status는 성공/실패 시 각각 ok, bad request로
  - url주소
    1. 사용자 관련: /user/...
    2. 상품 관련: /product/...
    3. 주문 관련: /order/...
<br><br>
  
## PART1. 회원 관련(고유한 ID URL에 사용하기)

### 1. 회원가입
/users/signup<br>
: 성공 여부를 status로 리턴<br>
<전달값>
- 아이디 id
- 비밀번호 password
- 이름 name
- 이메일 email
- 휴대폰 번호 phone
- 우편번호 postcode
- 주소 address
- 성별 gender
- 생년월일(-로 구분해서 전달, ex.2022-01-01) birth<br>

<가져오는 값>
- 회원 가입 성공 여부 status 값

<br><br>


### 2. 중복확인
2-1. 아이디 중복확인<br>
 /users/duplicationidcheck
: 성공여부 return true/false<br>
<전달값>
- 아이디<br>

<가져오는 값>
- 성공 여부의 status 값


2-2. 이메일 중복확인<br>
/users/duplicationemailcheck
: 성공여부 return true/false<br>
<전달값>
- 이메일<br>

<가져오는 값>
- 성공 여부의 status 값
<br><br>

### 3. 로그인
/users/login <br>
: 성공 여부를 status로 리턴<br>
<전달값>
- 아이디 
- 비밀번호

<가져오는 값>
- 성공 여부의 status 값

=> 로그인 성공 시 홈 화면으로 이동
<br><br>

### 4. 아이디 찾기
: 성공했을 때 아이디 값(변수는 id로)과 status, 실패했을 때는 status만<br>
4-1. [휴대폰 인증]<br>
/users/findidphone<br>
<전달값>
- 이름
- 휴대폰번호<br>

<가져오는 값>
- 성공 시 아이디 값 + status 값, 실패 시 status만

4-2. [이메일 인증]
/users/findidemail<br>
- 이름
- 이메일

<가져오는 값>
- 성공 시 아이디 값 + status 값, 실패 시 status만

=> 성공 시 바로 아이디 사용자 화면에 출력
<br><br>

### 5. 비밀번호 찾기
: 성공 여부를 status로 리턴<br>
5-1. [휴대폰 인증]<br>
/users/findpw/id<br>
<전달값>
- 아이디
- 휴대폰번호<br>

<가져오는 값>
- 성공 여부의 status 값

5-2. [이메일 인증]<br>
/users/findpw/email<br>
<전달값>
- 아이디
- 이메일

<가져오는 값>
- 성공 여부의 status 값

=> 비밀번호 찾기에 성공하면 비밀번호 변경 페이지로 이동
<br><br>


### 6. 장바구니
6-1. 장바구니 넣기<br>
/basket/put/{userIdx}<br>
: 밑의 3개의 값을 받아서 테이블에 넣기, 실패 성공을 return status<br>
<전달값>
- 상품 고유아이디
- 사용자 아이디
- 상품수량

<가져오는 값>
- 성공 여부의 status 값

6-2. 장바구니 보기<br>
/basket/view/{userIdx}<br>
: 사용자 아이디를 받아 이 사용자와 관련된 데이터 베이스에서 프론트에서 필요한 값을 전달<br>
<전달값>
- 사용자 아이디

<가져오는 값>
- 장바구니 페이지를 만들기 위한 데이터들

=> 디비에서 받아오는 필요한 정보를 잘 짜서 장바구니 페이지를 만드는데 사용
<br><br>

### 7. 리뷰쓰기
/review/{userIdx}<br>
: 리뷰 작성 여부를 데이터 베이스에 true/false로 저장 후 프론트의 요청이 있을 때 이 true/false를 리턴, 프론트가 리뷰 페이지를 만드는데 필요한 정보들을 프론트에 전달<br>
(1) 작성가능 후기 - true로 표시<br>

(2) 작성한 후기 - false으로 표시<br>
[(1),(2) 공통]<br>
<전달값>
- 사용자 아이디

<가져오는 값>
- 리뷰 작성 여부를 true/false로, 리뷰 페이지를 만들기 위한 데이터들

=> 백에서 true/false값과 해당하는 정보를 반환하면 잘 맞게 사용해 페이지 구성
<br><br>




## PART3. 상품 관련
- 상품 등록(POST): products/create                  보내는거(그냥 OK만 보낼 수 있고 원하면 만들어진 상품객체를 보낼 수 있음)
- 모든 상품 정보 가져오기(GET): /products/getAll    보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 상품 디테일(GET): /products/get/{id}              보내는거(공부중..)
- 이 상품 어때요?(GET): products/random-items       보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 놓치면 후회할 가격!(GET): products/sale-items     보내는거(JSON body에 상품 정보들을 묶어서 보냄)


## PART2. 주문 관련



+ Nav
상품 관련 카테고리들을 객체로 프론트에게 전달
