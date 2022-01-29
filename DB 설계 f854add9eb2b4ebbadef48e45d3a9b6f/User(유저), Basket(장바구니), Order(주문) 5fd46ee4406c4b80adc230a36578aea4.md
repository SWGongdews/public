# User(유저), Basket(장바구니), Order(주문)

### User Table

| PK, FK | Name | Comment | Type | Null | Default |
| --- | --- | --- | --- | --- | --- |
| PK | userIdx | 유저 고유 인덱스 | long | not null |  |
|  | userID | 유저 아이디 | varchar(45) | not null |  |
|  | userPassword | 유저 패스워드 | varchar(45) | not null |  |
|  | userName | 유저 이름 | varchar(45) | not null |  |
|  | userEmail | 유저 이메일 | varchar(45) | null |  |
|  | userPhoneNum | 유저 전화번호 | varchar(45) | null |  |
|  | userLocation | 유저 주소 | varchar(100) | null |  |
|  | userGender | 유저 성별 | varchar(45) | null |  |
|  | userBirth | 유저 생년월일 | timestamp | null | default CURRENT_TIMESTAMP |
|  | createdAt | 생성 날짜 | timestamp | null | default CURRENT_TIMESTAMP |
|  | updatedAt | 업데이트 날짜 | timestamp | null | default CURRENT_TIMESTAMP |
|  | status | 유저 계정 상태 | char | null | default 'Y' |

### Basket

| PK, FK | Name | Comment | Type | Null | Default |
| --- | --- | --- | --- | --- | --- |
| PK | basketIdx | 장바구니 고유 인덱스 | long | not null |  |
| FK | userIdx | 유저 아이디 | varchar(45) | not null |  |
| FK | productIdx | 유저 패스워드 | varchar(45) | not null |  |
|  | createdAt | 생성 날짜 | timestamp | null | default CURRENT_TIMESTAMP |
|  | updatedAt | 업데이트 날짜 | timestamp | null | default CURRENT_TIMESTAMP |
|  | status | 장바구니 계정 상태 | char | null | default 'Y' |

```
constraint FK_basket_userIdx_user_userIdx
    foreign key (userIdx) references user (userIdx),
```

### Order

| PK, FK | Name | Comment | Type | Null | Default |
| --- | --- | --- | --- | --- | --- |
| PK | userIdx | 주문 고유 인덱스 | long | not null |  |
| FK | basketIdx | 장바구니 고유 인덱스 |  | null |  |
| FK | productIdx | 상품 고유 인덱스 |  | not null |  |
|  | count | 개수 | long | not null | default 1 |
|  | totalPrice | deliveryPrice를 제외한 count * 가격의 상품 | long | not null |  |
|  | deliveryPrice | 주문 배송비 |  | null |  |
|  | createdAt | 생성 날짜(주문 날짜) |  | null | default CURRENT_TIMESTAMP |
|  | updatedAt | 업데이트 날짜 |  | null | default CURRENT_TIMESTAMP |
|  | status | 주문 상태 |  | null | default 'Y' |

```
constraint FK_order_baksetIdx_bakset_baksetIdx
    foreign key (baksetIdx) references basket (baksetIdx),
constraint FK_order_productIdx_product_productIdx
    foreign key (productIdx) references user (productIdx)
```