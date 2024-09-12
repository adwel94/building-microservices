# 워크 플로
`
마이크로 서비스 환경에서 분산 트랜잭션을 처리 할 수 있는 다양한 방법을 알아보자
`

## 데이터베이스 트랜잭션

### ACID 트랜잭션
데이터 저장소의 내구성과 일관성을 보장하기 위한 트랜잭션의 주요 속성
- 원자성 
- 일관성
- 격리성
- 내구성
### ACID 이지만 원자성이 부족한가?
- 마이크로 서비스 내부에서 사용하는 데이터베이스의 원자성은 보장 할 수 있음
- 다른 서비스와 상호작용하여 데이터를 관리해야 한다면 고려해야할 트랜잭션이 여러개 라는걸 인식해야 함
- 이러한 원자성 결여는 시스템 마이그레이션에서 심각한 문제를 발생
## 분산 트랜잭션 - 2단계 커밋
- 분산 시스템 환경에서 트랜잭션을 관리하기 위한 알고리즘, 투표 단계와 커밋 단계로 나누어 진행
- 투표 단계에서 트랜잭션에 관련된 모든 워커에게 상태 변경이 가능 여부를 요청, 승인을 받으면 커밋
- 분산 트랜잭션을 보장하기 위해 각 워커노드는 2단계 커밋 과정이 끝날 때 까지 데이터베이스 잠금을 수행할 수 있음
- 따라서 지연 시간이 발생할 수록 문제 발생, 격리성이 보장 되지 않음

## 분산 트랜잭션 - 그냥 안된다고 하라
- 원자성과 일관성을 반드시 보장해야 한다면 단일 서비스(모놀리스)로 남겨 두는게 편함

## 사가 패턴
- 자원을 잠그지 않고 상태 변경을 조절 할 수 있음
- 장기 트랜잭션(LLT)을 하위 트랜잭션으로 분해하여 처리 (마이크로 서비스 단위)
- 하위 트랜잭션은 내부 데이터베이스 에서 ACID 트랜잭션 처리

### 사가 실패 모드
개별 트랜잭션으로 분해하려면 실패 처리 방법을 고려해야 함
- 역박향 복구 - 이전의 커밋된 트랜잭션을 취소 하여 롤백
- 정방향 복구 - 실패가 발생한 지점에서 처리, 트랜잭션을 재시도 
- 사가패턴은 복구는 기술적인 것보다는 비즈니스로 푸는 것이 초점 (주문 취소 등등..)

#### 사가 롤백
- 이미 발생한 커밋을 롤백 할수 있는 기능(트랜잭션을) 따로 구현

#### 롤백을 줄이는 워크플로의 단계 재정렬
- 워크플로우를 재 조정하여 롤백 연산을 단순화 할 수 있음 (주문 발생시 포인트 지급 등)

#### 역방향 실패 및 벙방향 실패 상황의 혼합
- 역방향 복구, 정방향 복구를 같이 사용하는 것은 매우 적절

### 사가 패턴 구현

#### 오케스트레이션 사가
- 오케스트레이터 역할을 담당하는 서비스 지정하여 실행 순서(워크플로)를 정의
- 시스템 한 곳에서 워크플로우를 알 수 있음
- 오케스트레이터 서비스와 하위 서비스 사이에 높은 결합도, 중앙 집중화가 발생
- 중앙 집중화를 피하기 위해 오케스트레이터 역할을 여러 서비스에게 부여할 수 있음

#### 코레오그래피형 사가
- 사가 운영에 대한 책임을 여러 서비스로 분할
- 실패 이벤트 발행하고 관심있는 마이크로 서비스가 수신하여 동작
- 결합도를 크게 낮추고 중앙 집중 비즈니스 피할 수 있음
- 서비스의 워크 플로우를 이해 하기 어려운 단점이 있음

#### 혼합모델
- 두 가지 방식을 혼합하여 사용
- 두 방식 모두 사가의 상태를 추적할 수 있는 ID와 같은 개념이 필요

#### 어느것을 선택할 지?
- 한 팀이 전체 사가의 구현을 담당할 경우 오케스트레이션 사가가 적합
- 팀이 분산되어 있고 이벤트 발행/수신 모델이 익숙하다면 코레오그래피 사가가 적합

### 사가와 분산트래잭션 비교
- 분산 트랜잭션은 큰 서비스 일수록 가용성이 떨어짐
- 비즈니스를 사가패턴을 통해 명시적으로 모델링 하면 분산 트랜잭션으로 인한 다양한 문제를 피할 수 있음



