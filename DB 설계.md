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
# Review(리뷰), Product(상품), LikeProduct(좋아요한 상품)

## Review(리뷰)

| PK, FK | Name | Comment | Type |
| --- | --- | --- | --- |
| PK | reviewId | 리뷰 고유ID | Long |
| FK | productId | 상품ID | Long |
| FK | userId | 고객의 고유 ID | Long |
|  | reviewTitle | 리뷰 제목 | varchar(45) |
|  | reviewContent | 리뷰 내용 | varchar(45) |
|  | reviewDate | 리뷰 작성일 | Date |
|  | reviewImage | 리뷰에 담기는 사진 | varchar(45) |
|  | createdAt | 생성 시간 | timestamp |
|  | updatedAt | 업데이트 시간 | timestamp |
|  | status | 상태 | char |

## Product(상품)

| PK, FK | Name | Comment | Type |
| --- | --- | --- | --- |
| PK | productId | 상품 고유Id | Long |
|  | name | 상품명 | varchar(45) |
|  | price | 상품의 가격 | Long |
|  | category | 카테고리 | varchar(45) |
|  | unit | 판매 단위 | Long |
|  | volume | 판매 용량 | Long |
|  | delivery | 배송구분 | varchar(45) |
|  | expirationDate | 유통기한 | varchar(45) |
|  | detail | 상세정보 | varchar(45) |

## LikeProduct(좋아요한 상품)

| PK, FK | Name | Comment | Type |
| --- | --- | --- | --- |
| FK | productId | 좋아요한 상품의 Id | Long |
| FK | userId | 좋아요를 누른 고객의 Id | Long |
|  | status | 상태 | char |

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
###Search
###Category
###Delivery
# Search(검색), Category(카테고리, Delivery(배송)

Search Table

| PK, FK | Name | Comment | Type |
| --- | --- | --- | --- |
| PK | searchIdx | 검색 고유 인덱스 | long |
| FK | userIdx | 유저 고유 인덱스 | long |
|  | content | 입력값 | varchar(45) |
|  | createdAt | 생성 날짜 | timestamp |
|  | updatedAt | 업데이트 날짜 | timestamp |
|  | status | 유저 계정 상태 | char(45) |

Category Table

| Key | Name | Comment | Type |
| --- | --- | --- | --- |
| PK | categoryIdx | 카테고리 고유 인덱스 | long |
|  | categoryName | 카테고리명 | varchar(45) |
|  | categoryImage | 카테고리 이미지 | varchar(45) |
|  | createAt | 생성 날짜 | timestamp |
|  | updatedAt | 업데이트 날짜 | timestamp |
|  | status | 유저 계정 상태 | char(45) |

Delivery Table

| Key | Name | Comment | Type |
| --- | --- | --- | --- |
| PK | deliveryIdx | 배송 고유 인덱스 | long |
|  | deliveryCompany | 배송회사 | varchar(45) |
|  | deliveryPrice | 배송가격 | int |
|  | deliveryDate | 배송시간(며칠이 걸리는) | int |
|  | createAt | 생성 날짜 | timestamp |
|  | updatedAt | 업데이트 날짜 | timestamp |
|  | status | 유저 계정 상태 | char(45) |

`long`
