# DB 설계

###User
###Basket
###Order
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
###Review
###Product
###LikeProduct

[Review(리뷰), Product(상품), LikeProduct(좋아요한 상품)](DB%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%80%E1%85%A8%20f854add9eb2b4ebbadef48e45d3a9b6f/Review(%E1%84%85%E1%85%B5%E1%84%87%E1%85%B2),%20Product(%E1%84%89%E1%85%A1%E1%86%BC%E1%84%91%E1%85%AE%E1%86%B7),%20LikeProduct(%E1%84%8C%E1%85%A9%E1%87%82%E1%84%8B%E1%85%A1%E1%84%8B%E1%85%AD%206154159ed7ae4e15b5f06c4a447a4630.md)

###Search
###Category
###Delivery

[Search(검색), Category(카테고리, Delivery(배송)](DB%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%80%E1%85%A8%20f854add9eb2b4ebbadef48e45d3a9b6f/Search(%E1%84%80%E1%85%A5%E1%86%B7%E1%84%89%E1%85%A2%E1%86%A8),%20Category(%E1%84%8F%E1%85%A1%E1%84%90%E1%85%A6%E1%84%80%E1%85%A9%E1%84%85%E1%85%B5,%20Delivery(%E1%84%87%E1%85%A2%E1%84%89%E1%85%A9%E1%86%BC)%207e582fb7ca324a44aa1c899878ef07e6.md)

```
create table animal
(
    animalIdx     int auto_increment comment '동물 인덱스'
        primary key,
    centerIdx     int                                 not null comment '보호소 인덱스',
    animalSpecies varchar(45)                         null comment '동물 종',
    animalName    varchar(45)                         null comment '동물 이름',
    animalAge     varchar(45)                         null comment '동물 나이',
    animalGender  char                                null comment 'F : 여, M : 남',
    animalWeight  int                                 null comment '동물 무게',
    createdAt     timestamp default CURRENT_TIMESTAMP null comment '동물 생성',
    updatedAt     timestamp default CURRENT_TIMESTAMP null comment '동물 업데이트',
    status        char      default 'N'               null comment 'A : 입양중, P : 보호중, F : 펀딩중, Y : 입양완료, N : None',
    constraint FK_Animal_centerIdx_Center_centerIdx
        foreign key (centerIdx) references center (centerIdx)
)
    comment '동물 테이블';

```
