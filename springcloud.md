# Spring Cloud로 개발하는 마이크로서비스 애플리케이션(MSA)

## 1. Microservice와 Spring Cloud 소개
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

