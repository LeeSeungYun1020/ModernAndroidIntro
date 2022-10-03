# Repository Pattern 기초

## Repository Pattern
- 데이터가 네트워크 응답인지 DB 응답인지 관계 없이 동일한 인터페이스를 통해 데이터에 접근할 수 있도록 하는 패턴
- 데이터에 접근하는데 필요한 로직을 캡슐화한 것을 repository라고 함
- 데이터와 로직을 분리하여 결합도를 낮춤

## Repository Pattern 구현
- view -> viewModel -> repository -> dataSource