# DataBinding 기초

## DataBinding

- 프로그래밍 방식이 아닌 선언적 형식으로 레아아웃의 UI 구성요소를 앱의 데이터 소스와 결합할 수 있는 지원 라이브러리
- 코틀린 코드와 XML의 UI 컴포넌트를 연결

## DataBinding의 특징

- findViewById 제거
- Custom Binding Adapter
- Two-way Data Binding

## DataBinding 사용

- build.gradle(Module:app)에 dataBinding 추가
- layout xml에 <layout> 태그로 둘러쌈
- layout xml에 <data> 태그 추가

```xml

<layout>
  <data>
    <variable
      name="viewmodel"
      type="com.example.databinding.MyViewModel"/>
  </data>
  <ConstraintLayout>
    <TextView
      android:text="@{viewmodel.counter.toString()}"/>
    />
  </ConstraintLayout>
</layout>
```

```kotlin
val binding = DataBindingUtil.setContentView<ActivityMainBinding>(this, R.layout.activity_main)
binding.lifecycleOwner = this
binding.viewmodel = MyViewModel
```