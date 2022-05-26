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

## Cloud Native Architecture
* Cloud Native Application를 개발하거나 서비스를 운영할 때 고려해야할 12가지
* 클라우드 서비스중 FaaS 형태의 서비스를 제공하는 Heroku(허로쿠) 회사가 제시
    1. 코드 통합(Base Code) : 형상 관리를 위해 코드를 한 곳에서 배포하는 것이 주 목적
    2. 종속성 배제(Dependency Isolation) : 각 Micro Service는 자체 종속성을 가지고 패키징 되어있음 전체 시스템에 영향을 주지않는 형태에서 변경 되어야 함
    3. 환경설정의 외부 관리(Configuration) : 코드의 외부에서 관리 도구를 통해 Micro Service에 필요한 작업들을 구성할 수 있어야함
    4. 백업 서비스의 분리(Backing Services) : 응용프로그램 자체에서 필요한 백업 서비스를 분리하게 됨으로서 서로 상호가능한 서비스 자체를 종속성 없는 상태에서 작업 가능
    5. 개발 환경과 테스트 운영 환경의 분리(Build, Release, Run) : 빌드, 릴리즈, 실행환경을 분리. 개발 서버에서 만들어진 코드 배포 하기위해 실행단계 까지 옮기는 환경을 엄격하게 관리
    6. 상태관리(Processes) : 프로세스 각각의 Micro Service들은 실행되는 서비스와 분리된 채, 자체 프로세스에서 운영가능해야 함(독립성과 일치)
    7. 포트 바인딩(Port Binding) : 다른 Micro Service와 격리를 위해 각각의 Micro Service는 자체 포트에서 노출되는 인터페이스 및 자체에 포함되는 기능이 있어야 함
    8. 동시성(Concurrency) : 하나의 서비스가 여러가지 인스턴스에 동일한 형태로 복사되면서 운영됨으로서 부하 분산이 가능
    9. 서비스의 올바른 상태 유지(Disposability) : 서비스의 인스턴스 자체가 삭제가 가능 하며 확장성을 높이고 정상적으로 종료 될 수 있는 환경이 되어야 함
    10. 개발과 production단계 구분(Dev/Prod Parity) : 환경자체를 최대한 다른 쪽에 있는 작업과 중복되지 않고 종속되지 않는 상태로서 서비스를 유지할 수 있어야
    11. Log의 분리(Logs) : Log를 출력시키는 Logic은 기존에 있었던 Application Logic과 분리 되어서 Application 자체가 실행되지 않는 상태라 해도 Logging만은 정상적으로 작동해야 함
    12. 관리 프로세스(Admin Processes) : 현재 운영되고 있는 모든 Micro Service들이 어떤 상태이며 어떤 리소스로 구성되어있는지 파악하기 위해 관리 도구. 이러한 작업에는 리포팅할 수 있는 기술이 포함되어 있어야 하고 데이터 정리 및 데이터를 분석하는 기능이 포함될 수 있음
    
> * 12Factors + 3개의 항목(Pivotal 회사가 발표)
    >   1. API First : 모든 Micro Service는 API형태로 서비스 제공. API를 구축함에 있어서 사용자 측에서 어떤 형태로 사용할 것인지 먼저 고민하고 개발해야 함
    >   2. Telemetry : 모든 지표는 수치화 및 시각화 되어야 함
    >   3. Autentication and Authorization : API를 사용함에 있어서 인증 과정 필수

## Monolithic vs MSA

1. Monolithic
* 모든 업무 로직이 하나의 어플리케이션 형태로 패키지 되어 서비스
* 어플리케이션에서 사용하는 데이터가 한곳에 모여 참조되어 서비스되는 형태
* Application을 구성하는 서비스들 간 의존성을 가짐
    * 문제점 - 부분의 장애가 서비스 전체적인 장애, scale out 불가능, 시스템 일부만 수정을 하여도 전체 시스템을 다시 패키징 하고 빌드-테스트-배포 해야함
2. MSA
* 함께 작동하는 작은 규모의 서비스들 - Sam Newman
* scale out 가능
* 유지보수 및 변경사항이 적용이 쉬움
* 통일된 언어를 사용하지 않아도 됨
* 서로 다른 언어 및 서로 다른 Database를 사용가능
* 각각의 제공해야하는 Service를 restAPI를 통해서 제공 가능 및 다른 Micro Service들과 통신 가능
    * 문제점 - 트랜잭션이 불편, 개발 시간 증가, 성능 이슈
>   * 최근에는 Application 개발 시 사용자들의 다양한 Smart Device를 고려해야 함
>   * Web Browser 뿐 아니라 스마트 워치, 스마트폰, 태블릿, 노트북 등의 Device도 고려해야함
>   * 사용자가 요청하는 형태로 응답이 가능 해야하기 때문에 RestAPI를 사용
