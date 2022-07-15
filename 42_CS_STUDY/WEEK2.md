# 2주차 - 데브옵스(DevOps)

데브옵스(DevOps)

Development + Operations의 합성어

소프트웨어 개발자와 정보기술 전문가 간의 소통, 협업 및 통합을 강조하는 개발 환경이나 문화를 의미한다.


목적 : 소프트웨어 제품과 서비스를 빠른 시간에 개발 및 배포하는 것


결국, 소프트웨어 제품이나 서비스를 알맞은 시기에 출시하기 위해 개발과 운영이 상호 의존적으로 대응해야 한다는 의미로 많이 사용하고 있다.



데브옵스의 개념은 애자일 기법과 지속적 통합의 개념과도 관련이 있다.

애자일 기법
실질적인 코딩을 기반으로 일정한 주기에 따라 지속적으로 프로토타입을 형성하고, 필요한 요구사항을 파악하며 이에 따라 즉시 수정사항을 적용하여 결과적으로 하나의 큰 소프트웨어를 개발하는 적응형 개발 방법

지속적 통합
통합 작업을 초기부터 계속 수행해서 지속적으로 소프트웨어의 품질 제어를 적용하는 것
-출처: [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Software%20Engineering/%EB%8D%B0%EB%B8%8C%EC%98%B5%EC%8A%A4(DevOps).md]

## DevOps
DevOps는 애플리케이션 개발의 품질과 속도를 개선하고 신규 또는 수정된 소프트웨어 기능이나 제품의 릴리즈 주기 단축을 장려하는 새로운 철학이자 프레임워크입니다.

DevOps 사례는 애플리케이션 개발 팀(Dev)과 해당 IT 운영 팀(Ops) 팀 간의 원활하고 지속적인 커뮤니케이션, 협업, 통합, 가시성 및 투명성을 장려합니다.

"Dev"와 "Ops" 간의 이러한 긴밀한 관계는 초기 소프트웨어 계획부터 코딩, 구축, 테스트 및 릴리즈 단계와 구축, 운영 및 지속적인 모니터링에 이르는 DevOps 라이프사이클의 모든 단계에 걸쳐 계속됩니다. 이러한 관계는 추가 개선, 개발, 테스트 및 구축에 대한 지속적인 고객 피드백 루프를 추진하는 원동력이 됩니다. 이러한 노력이 제공하는 결과 중 하나는 필요한 기능 변경 또는 추가 기능을 더 빠르고 지속적으로 릴리즈할 수 있다는 것입니다.

혹자는 DevOps 목표를 문화, 자동화, 측정 및 공유(CAMS)의 네 가지 범주로 그룹화하는데 DevOps 툴을 사용하여 이 모든 영역을 지원할 수 있습니다. 이러한 툴을 사용하면 개발 및 운영 워크플로우의 효율성 및 협업 기능을 개선하여 통합, 개발, 테스트, 구축 또는 모니터링과 관련된 기존의 시간 소모적인 수동 또는 정적 작업을 자동화할 수 있습니다.

- development와 operations를 하나의 파이프라인으로 묶어 자동화하는 것이 목표인 거 같다. 일종의 패러다임?
    개발부터 릴리즈의 단계까지 자동화를 통해 빠른 속도를 보장한다.
- 이렇게 DevOps를 실현하기 위한 여러가지 방법론들이 개발됐고 그 중 몇가지를 소개하고자 한다.
    - 스크럼: 스크럼은 개발 및 QA 프로젝트를 가속하기 위한 팀원의 협력 방법을 정의합니다. 스크럼 사례에는 주요 워크플로 및 특정 용어(Sprint, 시간 상자, 일별 스크럼\[회의\])와 전담 역할(스크럼 마스터, 제품 소유자)이 포함됩니다.
    - 칸반: 칸반은 Toyota 공장에서 얻은 효율에서 비롯되었습니다. 칸반은 진행 중인 소프트웨어 프로젝트 작업 상태(WIP)를 칸반 보드로 추적할 것을 지시합니다.
    - 애자일: 초기 애자일 소프트웨어 개발 방법이 여전히 DevOps 사례 및 툴에 영향을 미치고 있습니다. 스크럼 및 칸반을 비롯한 많은 DevOps 방법에는 애자일 프로그래밍 요소가 포함되어 있습니다. 일부 애자일 사례는 변화하는 요구 및 요구사항에 빠르게 대응하고 요구사항을 사용자 사례로 문서화하며 매일 아침 회의를 수행하고 지속적인 고객 피드백을 포함하는 것과 관련됩니다. 또한 애자일은 기존의 긴 "폭포수" 개발 방법 대신 짧은소프트웨어 개발 라이프사이클을 사용할 것을 지시합니다.

* water pool?: 폭포수가 위에서 아래로 떨어지는 것처럼 단계가 순차적으로 진행되며 완료된 단계는 되돌리기 어려운 특성을 가진 개발 방법론
요구사항분석->설계->구현->테스트->유지보수로 나뉜다.
여러단계가 병렬적으로 진행되거나 역으로 진행되는 경우가 없음
특징

- 체계화된 문서를 바탕으로 안정적 진행가능
- 단계가 완료된 다음 진행하기 때문에 리스크가 적음
- 이미 단계가 진행한 뒤에 요구사항 및 설계 등이 변경되면 문제가 발생할 수 있다.
- 사전 분석 단계에 많은 시간이 소요된다.
- 협업의 경우 각각 개발방안에 의해 진행된다(?)
- 다양한 개별 업무시스템을 사용한다.
- 관리가 용이하다.
- 목표물이 후반에 가시화 되는 특성이 있다.

개발 방법론 이후 중요하게 연결되는 것이 CI와 CD다.

- CI (Continuous Integration: 지속적 통합)
    빌드/테스트 자동화 과정
    애플리케이션에 대한 새로운 코드 변경 사항이 정기적으로 빌드 및 테스트되어 공유 리포지토리에 통합되므로 여러 명의 개발자가 동시에 애플리케이션 개발과 관련된 코드 작업을 할 경우 서로 충돌할 수 있는 문제를 해결할 수 있다.

    지속적 통합은 소스/버전 관리 시스템에 대한 변경 사항을 정기적으로 커밋하여 모든 사람에게 동일 작업 기반을 제공하는 것으로 시작합니다.
    
    __커밋할 때마다 빌드와 일련의 자동 테스트가 이루어져 동작을 확인하고 변경으로 인해 문제가 생기는 부분이 없도록 보장합니다.
- CD (Continuous Delivery: 지속적 제공(?))
    빌드, 테스트 및 배포
CD*(Continuous Deploy: 지속적 배포)
![CI/CD Flow](https://www.redhat.com/cms/managed-files/styles/wysiwyg_full_width/s3/ci-cd-flow-desktop_edited_0.png?itok=TzgJwj6p)