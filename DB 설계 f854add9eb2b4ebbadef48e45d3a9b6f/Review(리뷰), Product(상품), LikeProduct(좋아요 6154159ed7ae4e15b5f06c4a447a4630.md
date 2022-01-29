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