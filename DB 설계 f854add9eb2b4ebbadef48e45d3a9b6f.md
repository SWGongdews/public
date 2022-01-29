# DB 설계

###User
###Basket
###Order

[User(유저), Basket(장바구니), Order(주문)](DB%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%80%E1%85%A8%20f854add9eb2b4ebbadef48e45d3a9b6f/User(%E1%84%8B%E1%85%B2%E1%84%8C%E1%85%A5),%20Basket(%E1%84%8C%E1%85%A1%E1%86%BC%E1%84%87%E1%85%A1%E1%84%80%E1%85%AE%E1%84%82%E1%85%B5),%20Order(%E1%84%8C%E1%85%AE%E1%84%86%E1%85%AE%E1%86%AB)%205fd46ee4406c4b80adc230a36578aea4.md)

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