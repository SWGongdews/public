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