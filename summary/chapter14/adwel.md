# 사용자 인터페이스

## 디지털을 향해
- UI는 사용자에게 제공하고자 하는 다양한 기능을 한데 엮는 곳
- 사용자 인터페이스를 제공할 때 누구에게 어떤 책임이 있는지와 같은 조직적 측면을 고려해야 함

## 소유권 모델
- UI 경계를 정의하고 팀을 구성하는 것이 독립적 배포 가능성이라는 목표를 달성하기 위해 가장 적합함
- 완전한 소유권을 갖게 되면 각 팀은 소프트웨어의 최종 사용자와 직접 접촉할 지점이 생기고 이는 성공 확률로 이어짐
- 
### 전담 프론트엔드 팀 추구
- 전문가 부족, 일관성 추구, 기술적 문제라는 세 가지 핵심 요소 때문에 전담 프론트엔드 팀을 구성하는 경우가 많음
- 앱 사용 경험을 제공하는데 필요한 기술적인 노하우가 있는 전문가가 있어야 함
- 유저가 동일한 시각과 경험을 할 수 있도록 일관성을 추구하기 위해 프론트엔드 팀을 따로 구성

## 스트림 정렬 팀을 향해
- 전담 프론트엔드 팀은 조직에 새로운 핸드오프 지점이 생겨 업무 속도가 느려질 수 있음
- 도메인 특정 부분에서 기능을 엔드투엔드로 제공하는 전담 팀이 효율적으로 일이 가능 (풀스택 개발자)
- 최종 사용자로부터 멀어질수록 성공 여부 판단이 어려워지고 정확한 목표를 찾기 어려워짐 따라서 풀스택 개발을 지향해야 함

### 전문가 공유
- 같은 기술을 가진 사람들이 동일한 팀에 배치되어 통제된다면 고립된 조직을 초래함
- 전문 기술을 가진 사람을 특정 도메인 팀에 배치하여 기술을 공유할 수 있는 환경을 제공하는 것이 좋음
- 전문 기술을 가진 사람도 더 어려운 문제에 집중할 수 있는 기회가 생기기도 함
- 활성화 팀(회사 내부 컨설팅 팀)을 만들어 피벗을 하고 있는 팀에게 배치하여 도움을 주는 방법도 있음

### 일관성 보장
- 전담 프론트 엔드 팀을 두지 않아도 UI의 일관적인 룩앤필을 보장할 수 있는 방법은 다양함
- 활성화 팀 모델을 사용하여 일관성을 어느정도 유지시키거나 공유 리소스(CSS 스타일, 컴포넌트)로도 해결 가능
- 때로는 일관성 보다 개인, 팀의 자율성을 존중하여 빠르게 성장하는 회사도 있긴 함(AWS)

## 모놀리식 프론트엔드
- 백엔드 마이크로서비스를 호출하고 모든 UI 상태와 동작이 UI 자체에 정의되는 아키텍처

### 적용 시점
- 전담 프론트엔트 팀이 필요, 프론트 엔드 팀 내부에서 도메인 경합이 발생할 수 있음
- 하나의 배포 가능한 단위(모놀리식 배포)에서 UI의 모든 구현과 동작을 처리하고 싶을 때 적합

## 마이크로 프론트엔드
- 프론트엔드의 여러 부분을 독립적으로 작업하고 배포할 수 있는 조직 패턴
- 마이크로엔트 프론트 엔드도 백엔드와 마찬가지로 독립적인 배포성을 제공할 수 있어야 함

### 구현
- 프론트엔드의 여러 부분을 분해하여 단일 화면으로 연결하는 위젯 기반 분해
- 페이지단위로 분해하는 페이지 기반 분해가 있음

### 적용시점
- 계층화된 아키텍처에서 벗어나 엔드투엔드 스트림 정렬 팀을 도입해야 할 경우
- 프론트엔드 기능이 너무 켜저 여러 전담 프론트엔드 팀이 필용한 상황일 경우
- 마이크로서비스가 제공하는 기능이 위젯이나 페이지에 딱 맞아 떨어지지 않을 수 있기 때문에 신중해야 함
 
## 페이지 기반 분해
- UI는 여러 웹 페이지로 분해되고, 서로 다른 마이크로서비스에서 서로 다른 페이지들을 제공할 수 있음
- 팀의 변경 사항이 사용자에게 미치는 여향을 해당 팀이 쉽게 알 수 있음

### 적용대상
- 웹기반인 경우 사용자 인터페이스 분해 방법에 대한 가장 간단하고 분명한 기술이기 때문에 기본 선택지가 될 수 있음 
- SPA 사용이 급격히 늘어나면서 억지로 끼워 맞치는 경우가 있기 때문에 주의해야 함

## 위젯 기반 분해
- 인터페이스의 화면에 독립적으로 변경할 수 있는 위젯이 포함
- 지원하는 마이크로서비스와 컴포넌트를 모두 소유하는 팀에게 적절
 
### 구현
- 위젯을 UI에 연결하는 방법은 UI가 생성되는 방식에 따라 달라짐 
- 웹의 경우는 충돌을 방지하기 위해 패키징을 사용할 수 있음
- 하지만 모듈화의 개념이 요즘 주로 사용하고 있는 SPA에서는 주요 관심사가 아님

### 의존성
- iframe을 사용하면 서버 측 템플릿을 사용해 UI에 연결되거나 클라이언트 측의 브라우저에 동적으로 삽입 가능
- 다만 iframe은 크기 조정과 프론트엔드의 서로 다른 부분 간 통신을 어렵게 만듬
- 위젯에 따라 다른 개발 프레임워크, 버전, 스타일 라이브러리를 사용하는 것이 가능해짐
- 스타일이 분산되어 있어 효율적이지 않기 때문에 페이지 로드 크기가 상당히 늘어날 수 있음

### 페이지 내 위젯 간 통신
- 위젯을 독립적으로 빌드하고 배포할 수 있지만, 여전히 서로 상호작용하길 원함
- 상호작용은 이벤트 처리로 많이 구현할 수 있음 (발행 및 구독)

### 적용 시점
- 여러 팀이 동일한 페이지(UI) 에서 작업이 가능하기 때문에 더 많은 유용성 제공
- SPA를 활용하고 프론트엔드에 대한 책임을 분리하려는 상황이 온다면 위젯 기반 분해를 강력히 제안
- 컴포넌트를 번들링하고 패키징하는 사전 작업 시간이 생김
- 한 위젯의 종속성을 추가할 때 페이지의 크기가 늘어날 수 있기 때문에 이를 방지하는 검사를 배치하는 것이 좋음

## 제약
- 핵심 서비스가 동일하더라도 각 인터페이스 타입과 사용자의 요구 사항, 그로 인한 제약 조건에 맞춰 이를 조정할 방법 필요
- 요구 사항은 사용자의 편의성 뿐만 아닌 장애인에 대한 맞춤 UI 같은 인간적이고 윤리적인 측면(장애인 접근성)도 고려해야 함

## 중앙 집계 게이트 웨이
- 외부 사용자 인터페이스와 다운스트림 마이크로서비스 사이에 위치하며 모든 사용자 인터페이스에 대한 호출의 필터링과 집계를 수행함
- 집계 게이트웨이를 사용하면 단일 호출로 여러 마이크로 서비스에서 필요한 데이터를 필터링하여 가져올 수 있음
- 이는 대역폭을 줄이고 애플리케이션의 대기 시간을 개선하는 측면에서 상당한 이점이 있음

### 소유권
- 중앙 집계 게이트웨이트를 통과하는 마이크로 서비스가 늘어나면 소유권에 대한 분쟁의 소지가 될 가능성이 있음
- 중앙 집계 게이트웨이는 외부 사용자 인터페이스 요구 사항에 따라 결정됨으로 UI를 만드는 팀이 소유하는것이 일반적
- 하지만 UI 개발자는 일반적으로 백엔드에 대한 기술 스택이 부족할 수 있음
- 어떠한 팀이 소유하든간에 여러 마이크로 서비스가 걸쳐 있으므로 배포하는데 병목 지점이 될 가능성이 있음

### 다양한 종류의 사용자 인터페이스
- 데스크탑에서 모바일까지 다양한 사용자 인터페이스를 지원하려면 백엔드에 추가 기능이 필요
- 여러 인터페이스를 호환하기 위하여 게이트웨이는 점점 비대해 질 수 있음
- 게이트웨이는 단일 유닛이나 UI는 여러개 임으로 경합 발생할 수 있음

### 여러 문제
- 호출 집계와 필터링 외에도 API키나 관리자 사용자 인증, 호출 라우팅등 다른 문제도 있음
- 비용을 지불하여 제품으로 대체 가능하나 조직, 서비스에 맞춰서 사용하려면 굉장히 제한적일 수 있음

### 적용 시점
- 한 팀이 사용자 인터페이스와 백엔드를 모두 개발한다면 그리 필요하지 않을 수 있음
- 호출 필터링 및 집계를 수행하는 개념은 UI대한 경험을 최적화 한다는 점에서 매우 중요
- 여러 팀으로 구성된 조직에서 중앙 게이트웨이를 사용하면 팀 간에 조율이 필수적이라 병목 발생

## 프론트엔드를 위한 백엔드 (BFF)
- 사용자 인터페이스의 다양한 문제를 처리하는 데 매우 성공적인 패턴으로 입증
- BFF는 자체 고유한 특성으로 인해 중앙 집계 게이트웨이 관련된 일부 우려사항을 회피함
- BFF는 특정 사용자 경험과 밀접하게 결합돼 있으며 일반적으로 사용자 인터페이스와 동일한 팀에서 주로 관리

## 얼마나 많은 BFF가 필요한가?
- 하나의 유형의 클라이언트에 하나의 BFF를 엄격하게 유지하는게 좋음
- 적은 수의 BFF를 유지하려는 것은 너무 많은 중복을 피하려고 서버 측 기능을 재사용하는데 목적이 있음

### 재사용과 BFF
- UI당 하나의 BFF 구조는 많은 중복 코드가 발생하고 클라이언트까지 이어질 경우가 있음
- 비용이 저렴하지만 더 많은 문제가 발생할 수 있는 공유라이브러리를 추출로 BFF 중복을 제거할 수 있음
- BFF 중복을 추출하여 새로운 마이크로 서비스로 만드는 방법도 있음

### 데스크톱과 그 이상을 위한 BFF
- 서버측에서 웹 UI의 더 많은 부분을 생성할 때 BFF는 최적의 장소가 됨
- 다운스트림 서비스를 숨기고 BFF 만 노출하면 호환성이 깨지는 문제를 방지할 수 있음
- 
### 적용 시점
- 모바일 UI나 제삼자에게 특정 기능을 제공해야 하는 순간
- BFF가 배포하고 관리하는 비용 많이 드는지 확인해봐야 함
- BFF를 통한 관심사 분리는 대부분의 경우에 상당히 이점을 가져다 줄것임

## 그래프 QL
- 클라이언트과 원하는 정보를 쿼리로 정확히 정의할 수 있음
- 원하는 필드를 정확히 요청하는데 도움이 될 뿐 아니라 호출 횟수도 줄일 수 잇음
- 서버측 변경없이 수행되는 쿼리를 동적으로 변경하도록 해주는 그래프 SQL 유연성 덕분에 BFF에 적용하기 좋음

## 하이브리드 방식
- 앞서 언급한 다양한 옵션을 필요에 따라 적용