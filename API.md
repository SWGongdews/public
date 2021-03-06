# API
- [ 공통 ]
  - return status는 성공/실패 시 각각 ok, bad request로
  - url주소
    1. 사용자 관련: /users/...
    2. 상품 관련: /products/...
    3. 주문 관련: /orders/...
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
...

<가져오는 값>
- 성공 여부의 status 값

6-2. 장바구니 보기<br>
/basket/view/{userIdx}<br>
: 사용자 아이디를 받아 이 사용자와 관련된 데이터 베이스에서 프론트에서 필요한 값을 전달<br>
<전달값>
- 사용자 아이디

<가져오는 값>
- 상품 이미지, 상품 이름, 상품 수량, 상품 할인된 가격, 상품 원가격
<br><br>

### 7. 리뷰쓰기
/review/{userIdx}<br>
(1) 작성가능 후기 - 주문테이블에서<br>

1-1. 후기 등록 가능한 상품 데이터<br>
<전달값>
- 사용자 아이디
<가져오는 값>
- 상품 이미지, 상품 이름, 할인된 가격, 원래 가격, 수량

1-2. 후기 등록<br>
<전달값>
- 후기 내용

<가져오는 값>
- 후기 잘 저장되었는지 status retrun

(2) 작성한 후기 - 후기테이블<br>
<전달값>
- 사용자 아이디
<가져오는 값>
- 상품 이미지, 상품 이름, 할인된 가격, 원래 가격, 수량


<br><br>

### 8. 개인 정보 수정
/users/update
: 새비밀번호, 이름, 이메일, 휴대폰, 성별, 생년월일(새비밀번호, 생년월일은 빈문자열로 갈 수도 있다.) 백에게 전달하면 개인 정보 update
<br>
<전달값><br>
-requestbody로 객체 전달 -> 비어있어도 전달해주면 알아서 채워줌
<br>
<가져오는 값><br>
-개인정보 잘 저장 되었는지 status return
<br>
프론트에서 주는 회원 id로 회원 정보 조회후 update <br>

## PART2. 상품 관련
- 상품 등록(POST): products/create                  보내는거(그냥 OK만 보낼 수 있고 원하면 만들어진 상품객체를 보낼 수 있음)
- 모든 상품 정보 가져오기(GET): /products/getAll    보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 상품 디테일(GET): /products/get/{id}              보내는거(공부중..)
- 이 상품 어때요?(GET): products/random-items       보내는거(JSON body에 상품 정보들을 묶어서 보냄)
- 놓치면 후회할 가격!(GET): products/sale-items     보내는거(JSON body에 상품 정보들을 묶어서 보냄)


[프론트]
1. main 페이지의 상품들<br>
프론트에서 title('이 상품 어때요?' ~ '인기 신상품 랭킹' 중 하나)을 보내면<br>
백에서 title에 맞는 상품고유아이디(productID), 상품이미지(imageUrl), 상품이름(productName), 할인율(saleRate), 할인가격(salePrice), 원래가격(originalPrice) 전달<br>
2. 각 상품의 detail<br> 
프론트에서 상품고유아이디(id)를 보내면<br>
백에서 상품이미지, 상품이름, 할인가격, 할인률, 원가, 판매단위, 중량/용량, 배송구분, 원산지, 포장타입, 유통기한 전달<br>
- 장바구니에 담기를 누르면?
프론트는 장바구니 테이블에 맞게 해당 상품에 대한 값 전달 
백은 성공하면 status 값 반환


## PART3. 주문 관련
1. 주문 페이지
프론트에서 회원 아이디를 주고
백에서 상품 이미지, 상품 이름, 상품 수량, 상품 할인된 가격, 상품 원가격, 적립금 받아옴
2. 주문 내역 페이지
해당 년도에 맞는 데이터 받아온다.
년도 값은 'all', '2022', '2021', '2020'이고 프론트에서 이 값을 주면 
백에서 년도에 맞는 주문 번호, 상품 이름, 상품 개수, 상품 이미지, 주문번호, 결제금액 전달
3. 주문 내역 detail 페이지
프론트에서 주문번호를 전달하면
백엔드는 상품 이미지, 상품 이름, 할인가격, 원래가격, 개수 전달
