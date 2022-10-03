# ViewModel과 Lifecycle 기초

## Activity Lifecycle

![활동 생명주기](https://developer.android.com/guide/components/images/activity_lifecycle.png?hl=ko)

## ViewModel

- Activity와 별도의 생명 주기를 가짐, activity 재생성시에도 ViewModel은 유지

```kotlin
// 인자가 없는 viewmodel
val viewModel = ViewModelProvider(this).get(MyViewModel::class.java)
// 초기값이 있는 viewmodel, factory 패턴 사용
val viewModel = ViewModelProvider(this, MyViewModelFactory(100)).get(MyViewModel::class.java)
// 위임 프로퍼티 사용
val viewModel: MyViewModel by viewModels()
// 위임 프로퍼티와 factory 패턴 사용
val viewModel: MyViewModel by viewModels { MyViewModelFactory(100) }
// fragment에서 fragment간 데이터 공유가 필요한 경우
val viewModel: MyViewModel by activityViewModels()
```

## ViewModel과 SavedInstanceState

|                               | ViewModel    | savedInstanceState         |
|-------------------------------|--------------|----------------------------|
| 저장소 위치                        | 메모리 내        | 디스크에 직렬화                   |
| 구성 변경 시에 유지                   | 예            | 예                          |
| 시스템에서 시작된 프로세스 중간 시에도 유지      | 아니요          | 예                          |
| 사용자의 완전한 활동 닫기, onFinish에서 유지 | 아니요          | 아니요                        |
| 데이터 제한                        | 복잡한 객체 가능    | 원시 유형 및 문자열                |
| 읽기/쓰기 시간                      | 빠름(메모리 액세스만) | 느림(직렬화, 역직렬화 및 디스크 액세스 필요) |

```kotlin
class MyViewModel(
    _counter: Int,
    private val savedStateHandle: SavedStateHandle
) : ViewModel() {
    var counter = savedStateHandle.get<Int>("counter") ?: _counter

    // 값이 바뀔 때마다 호출하도록 구현
    fun saveState() {
        savedStateHandle.set("counter", counter)
    }
}
```