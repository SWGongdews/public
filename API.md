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

### 8. 개인 정보 수정
: 새비밀번호, 이름, 이메일, 휴대폰, 성별, 생년월일(새비밀번호, 생년월일은 빈문자열로 갈 수도 있다.) 백에게 전달하면 개인 정보 update




## PART2. 상품 관련
- 상품 등록(POST): products/create                  보내는거(그냥 OK만 보낼 수 있고 원하면 만들어진 상품객체를 보낼 수 있음)
- 모든 상품 정보 가져오기(GET): /products/getAll    보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 상품 디테일(GET): /products/get/{id}              보내는거(공부중..)
- 이 상품 어때요?(GET): products/random-items       보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 놓치면 후회할 가격!(GET): products/sale-items     보내는거(JSON body에 상품 정보들을 묶어서 보냄)


[프론트]
1. main 페이지의 상품들<br>
프론트에서 title('이 상품 어때요?' ~ '인기 신상품 랭킹' 중 하나)을 보내면<br>
백에서 title에 맞는 상품고유아이디, 상품이미지, 상품이름, 할인율, 할인가격, 원래가격 전달<br>
2. 각 상품의 detail<br> 
프론트에서 상품고유아이디(id)를 보내면<br>
백에서 상품이미지, 상품이름, 할인가격, 할인률, 원가, 판매단위, 중량/용량, 배송구분, 원산지, 포장타입, 유통기한 전달<br>
장바구니에 담기를 누르면?
장바구니 테이블에 맞게 해당 상품에 대한 값 전달 


## PART3. 주문 관련
1. 주문 페이지
2. 주문 내역 페이지
3. 주문 내역 detail 페이지
