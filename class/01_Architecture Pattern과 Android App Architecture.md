# Architecture Pattern과 Android App Architecture

## 아키택처 패턴
- 자주 발생하는 문제에 대해 반복적으로 사용 가능한 효율적인 구조를 정리한 것
- 안드로이드에서는 MVC, MVP, MVVM 등이 사용됨
- 패턴을 도입하는 목적은 관심사를 분리하여 프로그램을 안전하면서 확장 가능하게 만드는 것

## MVC
- Model, View, Controller
- Model: 데이터와 비즈니스 로직 (UI와 관련 X)
- View: UI
- Controller: Model과 View 사이의 상호작용 관리, 외부 입력 처리하여 뷰 내용 갱신 및 화면 그리기 요청
- Model은 쉽게 테스트 가능하나 Controller가 안드로이드에 종속되어 테스트 어려움
- 안드로이드 특성상 액티비티가 View와 Controller 역할을 같이 수행하여 두 요소의 결합도가 높아짐

## MVP
- Model, View, Presenter
- Presenter: controller와 같은 역할하지만 view의 참조를 가지지 않고 인터페이스로 교신하기 떄문에 결합이 느슨해짐
- Presenter는 View와 Model의 참조를 가져 view에서 action을 전달 받고 필요한 경우 model로부터 데이터를 취득하여 view에 전달
- View와 Model 사이의 데이터 흐름이 사라지고 Presenter가 중간에서 데이터 흐름을 제어
- 인터페이스 추가 구현 필요, 구현 비용 상승
- View와 Presenter가 1:1로 대응해야 하여 앱이 커질수록 두 요소의 의존성이 강해짐

## MVVM
- Model, View, ViewModel
- ViewModel: View를 만드는데 필요한 로직을 가짐.
- View와 Model 사이에 의존성이 없으며 ViewModel도 View에 의존성을 가지지 않음
- 참조는 View -> ViewModel -> Model 순으로 단방향으로 일어남

## 안드로이드 앱 아키텍처
- 초기에는 Activity, Fragment > ViewModel > Repository > Model(Room), RemoteDataSource(Retrofit) > API, DB
- 안정정인 MVVM 같은 아키텍처 도입 가능
- 현재 UI Layer(UI elements > state holders) > Domain Layer(optional) > Data Layer(Repositories > Data Sources)
- 클린 아키텍처 패턴