# 📣 올라 백엔드 과제 안내

안녕하세요! 여러분의 관심과 지원에 감사드립니다.🤗

아래 내용을 꼼꼼히 읽고 조건에 맞춰 과제를 완성해주세요.  

<br>

# 🏅 과제 제출 방법

Private Repository를 생성한 뒤 과제를 진행해주세요.  
Repository명은 allra-backend-assignment로 설정해주세요.

과제가 완성되면 README.md 상단에 **지원자분의 성함**을 적어주세요.  
그리고 **dev@allra.co.kr** 계정을 멤버로 초대하여 과제를 제출해주세요.

1. GitHub 과제 Repository 접속
2. Settings 탭 클릭
3. 좌측 Collaborators and teams 메뉴 클릭
4. add people 클릭하여 'dev@allra.co.kr' 초대

<br>

# ✏️ 과제 개요

올라 마켓의 백엔드 시스템을 구축합니다. 이 시스템은 다음과 같은 기능을 제공해야 합니다.

1. 상품 조회 : 구매 가능한 상품 목록을 불러옵니다.

2. 장바구니 : 상품을 장바구니에 추가하고 수량을 관리합니다.

3. 주문 및 결제 : 주문을 제출하고 결제를 처리합니다.

4. 주문 내역 조회 : 사용자의 완료된 주문 기록을 조회합니다.

<br>

# 📝 요구 사항

## 1️⃣ 기술적 요구사항

- Java 17 이상을 사용해주세요.
- SpringBoot 버전은 3.x 이상을 사용해주세요.
- Database는 MariaDB 10.x를 사용해주세요. (필요에 따라 추가적인 저장소도 함께 활용해도 됩니다.)
- Database 상호작용에는 JPA를 사용해주세요.
- Git을 사용해 작업 내용을 관리해주세요.
- README.md를 반드시 작성해주세요.

<br>

## 2️⃣ 기능적 요구사항

### ✅ 상품 조회
상품 목록을 불러오는 API를 구현해주세요.  
상품에 대한 테이블 정의는 아래 DDL을 참고해주세요.  

```
-- 해당 DDL은 가이드입니다. 필요에 따라 새롭게 설계하여도 괜찮습니다. 
CREATE TABLE product (
    id BIGINT AUTO_INCREMENT PRIMARY KEY COMMENT '상품 ID (고유 키)',
    name VARCHAR(255) NOT NULL COMMENT '상품 이름',
    description VARCHAR(1000) COMMENT '상품 설명',
    price BIGINT NOT NULL COMMENT '상품 가격',
    stock INT NOT NULL COMMENT '재고 수량',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP NOT NULL COMMENT '생성 시간',
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP NOT NULL COMMENT '수정 시간'
);
```

### ✅ 장바구니
사용자별 장바구니에 상품을 추가, 수정, 삭제할 수 있는 기능을 구현해주세요.  
사용자에 대한 테이블 정의는 아래 DDL을 참고해주세요.  
**(회원가입 및 인증/인가 기능은 필수가 아니므로, 필요에 따라 임의로 구현하시거나 더미 데이터를 활용하셔도 됩니다.)**
```
-- 해당 DDL은 가이드입니다. 필요에 따라 새롭게 설계하여도 괜찮습니다.
CREATE TABLE customer (
    id BIGINT AUTO_INCREMENT PRIMARY KEY COMMENT '고객 ID (고유 키)',
    name VARCHAR(50) NOT NULL UNIQUE COMMENT '고객 이름',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP NOT NULL COMMENT '생성 시간',
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP NOT NULL COMMENT '수정 시간'
);

```

### ✅ 주문 및 결제
주문을 처리하는 API를 구현해주세요.  

```
[주문 및 결제 상세 요구사항]
- 주문 요청 시 장바구니에 담긴 모든 상품들의 금액을 합산하여 결제를 진행해야 합니다.
- 주문 요청 시 상품의 재고를 관리해야합니다.
- 결제 요청은 외부 결제 API를 사용하여 처리해야 합니다. (아래 제공된 모의 API 스펙을 참고해주세요.)
- 결제 요청 이력을 관리할 수 있어야 합니다.
- 결제 성공 및 실패 여부에 따라 적절한 응답을 반환해야 합니다.
```

실제 결제 처리는 아래 스펙을 참고하여 모의 API를 만들어 구현해주세요.  

- 모의 API 생성 사이트
  - https://beeceptor.com/
  - 익숙한 방식이 있다면 다른 방식을 사용해도 괜찮습니다.
- 모의 API fake data 생성 방법
  - https://beeceptor.com/docs/dummy-random-data-generation-during-mock/
- 모의 결제 API 스펙

```
HTTP Method : POST
URL : '/api/v1/payment'

[Request Header]
Content-Type: application/json

[Request Body]
{
    "orderId": String,  // 주문 ID
    "amount": Number    // 결제 금액
}

[Response]
// 아래 성공 응답을 그대로 복사,붙여넣기 시 beeceptor에서 사용가능합니다
{
    "status": "SUCCESS",
    "transactionId": "txn_{{faker 'number.bigInt'}}",
    "message": "Payment processed successfully"
}

// 아래 실패 응답을 그대로 복사,붙여넣기 시 beeceptor에서 사용가능합니다
{
    "status": "FAILED",
    "transactionId": null,
    "message": "Something wrong!"
}

```

<br>

📣

# 🙏 공지 사항

✔️  스스로 문제를 정의하고 해결하는 과정을 통해 과제를 완성해주세요.  
✔️  문제 해결 과정에서 고민이 있었던는 부분은 Issue로 남겨주시면 더욱 좋아요.  





