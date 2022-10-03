# ViewBinding 기초

## 뷰 바인딩의 필요성
- 뷰 요소를 불러오기 위해 findViewById를 사용
- kotlin-android-extensions 플러그인으로 findViewById를 생략할 수 있었으나 서로 다른 xml에서 같은 id를 사용하는 문제가 있었음
- 안드로이드 스튜디오 4.1부터 kotlin-android-extensions 지원을 중단하고 뷰 바인딩을 사용하도록 함

## 뷰 바인딩이란?
- 뷰 바인딩 활성화시 각 xml 파일에 대해 ViewBinding 클래스를 상속 받는 개별 뷰 바인딩 클래스가 자동으로 생성
- onCreate()에서 뷰 바인딩 클래스의 인스턴스를 생성
- 인스턴스가 뷰의 ID를 프로퍼티로 제공하게 한다.

## 뷰 바인딩의 장점
- Null-safe: 서로 다른 레이아웃의 같은 id를 가진 view를 정확히 구분 가능. 참조 불가능할 경우 @Nullable로 만들어 사용할 수 없게 한다.
- Type-safe: 잘못된 타입을 지정할 우려가 없음, 뷰의 타입을 정확히 알 수 있고 캐스팅을 하지 않아도 된다.

## 예시
```kotlin
// MainActivity.kt
private lateinit var binding: ActivityMainBinding
    // onCreate()에서
    binding = ActivityMainBinding.inflate(layoutInflater)
    setContentView(binding.root)

// FirstFragment.kt
private var _binding: FragmentFirstBinding? = null
private val binding get() = _binding!!
    // onCreateView()에서
    _binding = FragmentFirstBinding.inflate(layoutInflater, container, false)
    // onDestroyView()에서
    _binding = null
```
- fragment를 사용하지 않을 때 binding 자원을 반환할 수 있도록 함