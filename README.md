# Spring Cloud로 개발하는 마이크로서비스 애플리케이션(MSA)

## Microservice와 Spring Cloud 소개
1. Software 발전 과정
    * 1960~1980: 메인프레임의 시대. 하드웨어로 모든 서비스 들이 이루어짐
    * 1990~2000: 분산 시스템 발전. Robust,Distributed의 시기
    * 2010~: Fragile과 반대되는 Anti-fragile,Resilient 시대. Cloud Native를 활용한 시스템이 활발하게 구축
2. Sortware Architecture
    * Anti-fragile
        - Auto Scaling : 자동 확장성, 사용량에 따라 자동으로 인스턴스 증가
        - MicroServices : 기존의 서비스들이 하나의 거대한 형태로 이뤄진 것과 달리 전체 서비스를 구축하고 있는 개별적인 모듈 및 기능을 독립적으로 개발,배포 운영할 수 있는 세분화된 서비스 ex) 넷플릭스
        - Chaos Engineering : 시스템이 급격하고 예측할 수 없는 상황에서도 견딜 수 있고 신뢰성을 쌓기 위해 운영 중인 소프트웨어 시스템에 실행하는 방법이나 규칙
        - Continuous deployments: CI/CD와 같은 배포
            + CI/CD란? Cloud Native Application은 수 십개~수 백개의 서비스로 구성. 이를 일일히 빌드,테스트,배포를 수작업으로 한다면? 시스템 자체의 복잡성을 떠나서 어플리케이션을 구성하고 있는 각각의 서비스를 구성하고 빌드하는 것이 하나의 커다란 업무가 되어버릴 것, 이렇기 때문에 자동화된 시스템을 구축하고 하나의 작업에서 다른 작업으로 연계되는 과정을 파이프라인으로 연결 시켜놓으면 전체적인 시스템 업그레이드를 빠르게 적용 가능. 즉, Cloud Native와 Micro Service에 빠질 수 없는 기술!

## Cloud Native Architecture
1. 확장 가능한 아키텍처 (시스템은 필요에 따라 확장 가능한 형태)
    * 시스템의 수평적 확장에 유리(더 많은 사용자의 요청 처리 가능)
    * 확장된 서버로 시스템의 부하 분산, 가용성 보장
        - 시스템 확장을 의미하는 스케일은 스케일업(CPU나 메모리 스펙을 높이는 작업), 스케일아웃(같은 사양의 서버 즉, 인스턴스를 여러개 배치하므로서 동시에 더 많은 사용자 요청을 처리) 
    * 시스템 또는 Service Application단위의 컨테이너 기반 가상화
    * 모니터링
2. 탄력적 Architecture
    * CI/CD기법 적용
    * 분할된 서비스 구조
    * 무상태 통신 프로토콜
    * 서비스의 추가와 삭제를 자동으로 감지,
    * 변경된 서비스 요청에 따라 사용자 요청 처리(동적 처리)
3. 장애 격리(Fault Isolation)
    * 특정 서비스에 오류가 발생해도 다른 서비스에는 영향을 끼치지 않음 (Micro Service는 하나의 작은 독립적인 Application이므로 문제점이나 오류사항은 다른쪽 서비스로의 영향을 최소화)
    * 배포된 Micro Service들은 자신의 위치를 등록을 해야함. 다른 서비스들이 해당 서비스를 검색하고 사용할 수 있음 (Micro Service는 Discovery Service라는 곳에 등록하고 삭제 되도록 설정해야함)
