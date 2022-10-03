# LiveData와 Observer Pattern 기초

## LiveData

- 값의 변경을 감지할 수 있는 data holder
- 뷰모델의 각각의 데이터 필드를 가지고 있도록 설계됨, 다른 모듈 간에 데이터 공유에도 사용될 수 있음

## Observer Pattern

- Subject의 상태 변화를 관찰하는 Observer들을 객체와 연결
- Subject의 상태 변화를 초래하는 이벤트가 발생하면 객페가 그 이벤트를 직접 Observer에 통지

## Observable VS LiveData

- Observable: 콜백 등록
    - lifecycle 알 수 없으므로 등록한 콜백이 상시 작동해야
    - 작동 필요 없어지면 removeOnPropertyChangedCallback 호출하여 콜백을 수동으로 제거해야
- LiveData: lifecycleOwner 전달
    - lifecycle이 STARTED, RESUMED로 활성화 상태인 경우만 observe 수행
    - 나머지 상태에서는 자동으로 비활성화

## LiveData 이점

- UO와 데이터 상태의 일치 보장
- 메모리 누수 없음
- 중지된 활동으로 인한 비정상 종료 없음
- 수명 주기를 더 이상 수동으로 처리하지 않음
- 최신 데이터 유지
- 적절한 구성 변경
- 리소스 공유

## Transformations로 LiveData 변환

- 전달받은 LiveData에 변경이 일어났을 때, 람다 함수를 실행시키고 다시 liveData를 반환
- 원본 데이터 변경 없이 새로운 LiveData 생성 가능

```kotlin
val userLiveData: LiveData<User>
val useNameLiveData: LiveData<String> = Transformations.map(userLiveData) { user ->
    "${user.firstName} ${user.lastName}"
}
```

```kotlin
val userLiveData: LiveData<User>
val userNameLiveData: LiveData<String> = Transformations.switchMap(userLiveData) { user ->
    MutableLiveData(user.firstName + user.lastName)
}
```

- map(): 정적 변환
  - 데이터 변환이 있을 떄 즉각적으로 변환만 하면 되는 경우
- switchMap(): 동적 변환
  - 즉각적으로 데이터 변환이 어려워 초기화 구간에 사용할 수 없는 경우
  - 시간이 오래걸리는 작업