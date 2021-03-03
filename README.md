# Important_Android_
안드로이드를 배우면서 중요한 것들을 공유하는 레포지트리입니다.

# 안드로이드에서 Mysql을 쓰지마라! 🧐

I would very explicitly NOT develop a MySQL App on the Android. 

안드로이드에서 MySQL 개발을 하지 마십시오.

While you could perhaps get the JDBC driver to run on Android, this is the wrong approach from a architectural standpoint.

Android에서 돌리기 위해 JDBC 드라이버를 얻어야 할텐데요, 설계적 관점에서 이는 잘못된 접근 방식입니다.

You won't get the performance, scalability, maintainability, reliability, nor security characteristics you'd like. 

수행성, 가용성, 관리성, 신뢰성, 보안성.. 그 어느것 하나 제대로 되지 않을겁니다.

Instead, expose your client-side functionality in a web service.

대신, 웹 서비스를 통해 클라이언트 쪽 기능을 하게 할 수는 있습니다.

For most purposes, I'd suggest a RESTfull web service, but SOAP is also an option.

대부분은, RESTfull 방식의 웹 서비스를 추천하지만 SOAP 또한 방법 중 하나죠.

JSON is often a good alternative to XML -- especially if you will be interacting with this service via a browser. 

JSON은 XML을 훌륭하게 대체해 줍니다. 특히 브라우저를 통해 서비스 통신을 하게 된다면 말이죠.

If you put SQL in your client, you are basically screwed.

SQL을 클라이언트에 넣었다면, 근본적으로 완전 망하는겁니다.

You will NEVER be able to alter your schema, or introduce some non-DB processing, or split the data between databases, or make any of a host of other changes, because some people may never upgrade their apps.

스키마 변환이라든가 non-DB prosessing, DB 간 데이터 분리, 어떤 변화를 가지는 host 생성, 등은 절대 불가능 하겠죠. 왜냐하면 일부 유저는 프로그램 업데이트를 하지 않으니까요.

Well, OK, you can say "screw them", and change it anyway, but they'll ding you in the marketplace ratings. 

뭐, 망하면 망할테라지라고 해버리고 어떻게든 바꿔버린다면, 뭐 시장 결과는 뻔하겠죠.

Especially in a mobile app, you want a looser coupling.

특히 모바일 app에서는 느슨한 커플링이 필요합니다.

With a web service, you can simultaneously provide multiple versions of the same service (perhaps distinguished only by a revision indicator).

웹서비스를 통해서라면, 같은 서비스를 여러 버전으로 하여 지속적으로 제공해 줄 수 있습니다. (아마 revision indicator를 통해야만 하겠죠.)

You can do server-side caching to take a load off your database. You could even move to a different database entirely. 

또 데이터베이스 서버측의 로드를 줄여줄 수도 있습니다. 데이터베이스 전체를 다 바꿔버릴수도 있구요.

Also, connection failures will be frequent. With MySQL, you'd have to pay considerable attention to recovering from connection failures.

또한, 연결 실패가 빈번하게 일어날텐데, MySQL을 쓰면 연결 실패를 복구하는것에 대해 아주 신중하게 고려해야만 하죠.

With a web service, a single call may fail, but because the communication itself is stateless (if designed well), you can just retry that one failing call. 

웹서비스를 이용한다면, 단일 호출이 실패하더라도 설계가 잘 되있는한 통신 자체는 stateless(?)이기 때문에 그냥 실패한 호출을 재시도하기만 하면 되죠.

You do have to think carefully about transaction boundaries, and try to accomplish more with a single call, rather than beginning a transaction, doing a bunch of stuff, and the committing.

트랜젝션 바운더리에 대해서도 신중해야 할텐데 하나 이상의 호출을 수행해야 한다면, 그냥 트랜젝션의 시작부터 모든 일들을 한꺼번에 수행하고 마지막에 committing만 하면 되죠.

That's a good thing -- you'll get much better performance, because the round-trip time through the mobile network will be poor.

이건 매우 좋은겁니다 -- 수행성이 훨씬 나아지죠. 왜냐하면 모바일 네트워크를 통해 데이터가 왔다갔다 하는건 엄청난 시간이 걸리는 작업이니까요.

You'll also be rewarded with much superior reliability -- a single MAKE-ALL-THESE-CHANGES call happens in a shorter period of time, and is much less likely to fail due to the network than a series of BEGIN-EDIT-EDIT-EDIT-EDIT-COMMIT operations. 

그리고 훨씬 나은 보안성을 얻을 수 있구요. 한번으로 여러 호출을 한꺼번에 수행하는것은 시간도 더 짧게 들고 네트워크를 통한 호출 실패를 확 줄여줍니다.

All in all, there's very good reason why nobody uses MySQL on Android, and it has nothing to do with limitations on Android.

이 모든것들이 아무도 Android 에서 MySQL 을 쓰지 않는 이유가 되겠죠. 안드로이드의 한계와는 아무 상관이 없습니다.

The same arguments actually apply to ANY client-side use of MySQL, it's just that they get even stronger on a mobileplatform.

MySQL 을 사용하는 어떠한 클라이언트 라도 동일한 논쟁이 발생합니다. 단지 모바일 플랫폼 상에서는 더욱 강력하게 발생할 뿐이죠.



# What is MVVM? 🧐

먼저 MVVM 패턴은 무엇인지에 대해 알아보겠습니다. MVVM 패턴은 1990년대 마틴 파울러에 의해 나온 MVP 패턴에서 파생된 패턴입니다. MVVM(Model-View-ViewModel) 패턴은 비즈니스 및 프레젠테이션 로직을 UI와 완전히 분리하는데 도움이 되며 비즈니스 로직과 UI를 명확하게 분리하여 더 쉽게 테스트 할 수 있고 유지 보수에 용이합니다. View, ViewModel, Model에 대해 각각 알아보겠습니다.

# View

View는 화면에 보이는 레이아웃 구조를 담당합니다. 또한 UI와 관련된 로직을 수행할 수 있습니다.

# ViewModel

ViewModel은 View에 연결된 데이터와 명령을 구현하고 변경 알림 이벤트를 통해 상태의 변경을 View에 알립니다. 그리고 상태 변경 알림을 받은 View는 변경을 적용할지 말지를 결정하게 됩니다. 여기서 말하는 ViewModel과 AAC(Android Architecture Component)의 ViewModel은 다릅니다. AAC에서의 ViewModel은 화면 회전같은 변화에서 View에 사용되는 데이터를 유지시키기 위한, Lifecycle을 알고있는 클래스입니다. 안드로이드 개발을 하면서 MVVM 패턴을 사용하려고 한다면, 반드시 AAC의 ViewModel을 사용하지 않아도 구현은 가능합니다.

# Model

Model은 사용하려는 데이터를 가지고 있는 비시각적 클래스입니다. 예를 들어 DTO(Data Transfer Object), POJO(Plain Old Java Object)나 엔티티 개체 등이 있습니다. 일반적으로 데이터를 액세스하거나 캐싱이 필요한 서비스 또는 리포지토리와 함께 사용됩니다.

![mvvm](https://user-images.githubusercontent.com/66651059/85481270-7656af80-b5fc-11ea-964a-3b3d3b9fc7f3.png)

위 그림을 보면 알 수 있듯이 ViewModel은 Model은 알지만 View를 모르고 View는 Model을 모르지만 ViewModel을 알 수 있습니다.

# MVVM과 MVC 디자인 패턴의 차이점 🧐

![mvvm (1)](https://user-images.githubusercontent.com/66651059/85481589-101e5c80-b5fd-11ea-86b4-0d6925dd6106.png)

[ MVVM, 그림 1 ]

![mvc](https://user-images.githubusercontent.com/66651059/85481593-10b6f300-b5fd-11ea-837c-a179263bc77d.png)

[ MVC, 그림 2 ]

MVC는 컨트롤러가 뷰와 모델을 둘 다 처리하기 때문에 상대적으로 MVVM에 비해 유지보수를 하기엔 많이 실용성이 떨어집니다.
반면에 MVVM은 뷰, 뷰 모델, 모델을 통하여 ViewModel과 Model이 서로 상호작용하며, View가 ViewModel에게 관련 작업을 요청하는 디자인 패턴입니다. 
그리고 Model과 View는 서로를 모르기 때문에 유지보수가 훨씬 더 쉬움을 강조하고 있습니다.


# What is CleanArchitecture? 🧐

좋은코드란 무엇일까요?  가독성이 좋은코드? 테스트커버리지가 높은코드? 
여러가지 기준이 있겠지만 그중하나인 유지보수하기쉬운 코드(변화에 잘 대응할 수 있는 코드) 또한 좋은코드의 기준중 하나일 것입니다.
유지보수하기 쉬운코드는 변화에따른 코드변경이 적다는 것일것입니다. 
그러기 위해서는 코드가 잘 분리되어있어야 합니다.

그 방법중 하나인 Clean Architecture에 대하여 알아보도록 하겠습니다.

# CleanArchitecture 알아보기.
![다운로드(1)](https://user-images.githubusercontent.com/66651059/86120852-ffe01300-bb0f-11ea-8241-9f73333031cb.jpg)

[ 클린 아키텍쳐의 구성 ]

Robert Martin이 소개한 CleanArchitecture 다이어그램입니다.
양파모양의 4개의 Layer가 존재합니다. 가장 바깥쪽의 Frameworks & Drivers 가 사용자와 접점에 있는 Presentation이고,
가장 안쪽의 Entities가 사용자가 실제로 생각하는 개념의 단위입니다. Clean Architecture는 서버쪽 내용이지만 안드로이드에서도 이 개념을 적용시켜, UI를 독립시키고 데이터베이스를 분리시키고, 외부적인 설정에 독립적인 구조를 적용하여 프레임워크에 의존적이지않은 독립적인 코드를 짤 수 있습니다.

![cc](https://user-images.githubusercontent.com/66651059/86121057-551c2480-bb10-11ea-9ddc-2f67487487c1.png)

android에서 Clean Architecture를 적용할때 4개의 레이어로 분리한 위와같은 사진으로 적용됩니다.


![bbs](https://user-images.githubusercontent.com/66651059/86121062-564d5180-bb10-11ea-8807-83a365d095ec.png)

안드로이드 계층을 4개로 사용자에게 보여지는 로직과 관련된 Presentation Layer , Network를 포함한 데이터를 가져오는 Data Layer,

사용자의 Use case 로 분리되는 Domain Layer, 사용자의 개념을 정의하는 Entity Layer로 나눕니다.

이 레이어 간의 의존성은 안쪽으로만 발생하여야 합니다. 가장 하단부의 레이어일 수록 의존성이 낮아야합니다.

Presentation Layer는 Data Layer를 알지만 , Data Layer는 Presentaion Layer를 몰라야 합니다.

이 덕분에 맨 아래 Entity Layer는 순수한 Java 또는 Kotlin 모듈이 될 수 있고 (안드로이드에 의존성을 가질수있고) , 

안드로이드에 의존성을 가지지 않을수도 있습니다.(다른플랫폼에서도 사용가능, 의존성이 적기 때문)

 

이러한 분리를 통해 어떤 데이터베이스에 저장될지, 어떤 뷰에 보일지 고민하지 않고 Entity를 작성할 수 있고, 이에 대한 유스케이스로 

Domain Layer를 작성할 수 있습니다. 또한 트랜잭션을 가져오는 것을 Data에서 어떻게 보여줄 것인지를 Presentation에서 정할 수 있습니다.


# Entitiy
엔티티는 순수한 Java 또는 Kotlin모듈 이므로 안드로이드와 의존성이 없습니다.

안드로이드에서만 사용하는 것이아니라고 생각하고 작성해야 합니다.

(다른플랫폼의 같은서비스를 만든다면 Android, iOS ,Server모두 같은 이름과 타입을 사용하는 동일한 형태여야 합니다)

따라서 넘기는 데이터를 Parcelable등으로 정의하는 등의 행위는 삼가해야합니다.

정리하자면 사용자가 생각하는 형태대로 도메인(비즈니스로직)에서 파생되는 개념을 표현합니다.

 

# Domain Layer
도메인 레이어도 순수한 Java나 Kotlin 모듈 입니다.

실제로 사용자가 하는 일련의 행동들 즉 유스 케이스를 적용하는 것인데, 이 역시 안드로이드에 의존할 필요가 없기 때문입니다.

유스케이스를 구성할 때는 데이터베이스가 뭔지 뷰가 어떤것인지 고민하지 않고, 도메인에서 정의한 적당한 

레파지토리를 이용하여 구축하므로 코드가 사고의 흐름처럼 구성될 수 있습니다.

 

# Data Layer
Data Layer에서 하는 한가지 일을 고르자면, 도메인레이어를 알고 있으므로 

도메인레이어에 정의된 Repository를 실제로 구현하는 것입니다.

또한 여기에서는 Data Source 에의 의존성이 생기므로, 안드로이드 의존성이 생길 수 있습니다.


# Presentation Layer
마지막 최상위 레이어인 프레젠테이션 레이어는 UI레벨에서의 처리이고 Android 의존성이 높습니다.

Mvp 구조를 사용한다면 presenter가 생성되는 시점에 유스 케이스를 주입받을수 있는 구조로 작성합니다.

이처럼 작성하게 될 시에 테스트하기에 좀더 편리하게 됩니다.

# AboutKotlin

실습을 통해 얻은 코틀린 지식 / 여러 안드로이드 팁을 공유하는 곳입니다.

# About ViewBinding 
 
 뷰 바인딩은 데이터 바인딩과 다르게 뷰 결합을 해주는 뷰이다. 굳이 따지자면 데이터 바인딩이 뷰 바인딩의 상위호환이다. ( 뷰 바인딩의 지원 기능을 포함하니까 .. )
 
```
 viewBinding {
    enabled = true
 }
```
  app 단위의 gradle 파일에 viewBinding 허용

```
 private lateinit var bindingExample : ActivityExampleBinding // 초기화 지연
 
 bindingExample = ActivityExampleBinding.inflate(layoutInflater) // viewBinding 세팅
 setContentView(bindingExample.root) // 해당 binding의 최상위 부모를 contentView로 
```
 Activity
 
 ```
  private lateinit var bindingExample : FragmentExampleBinding // 초기화 지연 
  bindingExample = FragmentExampleBinding.inflate(layoutInflater)
  
  return bindingExample.root
 ```
  Fragment ->  onCreate 메소드내에서 작성

# About Widget

위젯은 supportLibrary를 지원하지 않는다. 따라서 CardView, RecyclerView와 같이 태생이 supportLibrary인 뷰들은 예외처리된다. ( ... )
위젯 업데이트 주기는 xml 폴더 내에 widget 업데이트 주기 설정이 가능하다. ( 다만, 너무 많은 작업을 1초마다 실행시켰을때에 OOM이 발생할수도 .. )

```
<?xml version="1.0" encoding="utf-8"?>
<appwidget-provider
    android:initialLayout="@layout/example_init" // inital xml 
    android:minWidth="180dp" // 최소 크기
    android:minHeight="60dp" // 최소 크기 ( 3:1 비율 )
    android:updatePeriodMillis="86400000" // 업데이트 주기
    android:resizeMode="horizontal|vertical"
    xmlns:android="http://schemas.android.com/apk/res/android" />
```
xml -> provider.xml

# About MVVM with DataBinding

MVVM은 디자인패턴이다. 말 그대로 , Model View ViewModel로 나누어서 사용하는 디자인패턴인데, Model에서는 기본적으로 data class 혹은 enum과 같은 데이터 가공 용도로 기틀을 잡아두는 것이고,
View는 ViewModel의 값의 변화에 따라서, 동적으로 업데이트 해주는 역할을 하고, ViewModel에서는 Model에서의 데이터를 이용해서, CRUD와 같은 작업을 수행한다. 

위와 같은 이유로 ViewModel은 Model과 상호작용하고, View와 Model은 서로 알지 못한다. 또한 View와 ViewModel이 서로 상호작용, View - ViewModel - Model 처럼 다리 역할을 해준다. 
기존에 MVC 패턴과의 차이점은 Controller에서 무겁거나 하드한 작업을 처리함으로써, 유지보수에도 어렵고, Controller에 부담감이 많았는데 해당 디자인패턴을 이용하면서, 유지보수에도 편하고, 무리가 덜가는 서비스가 구현이 가능하다.

```
class MainViewModel(application: Application) : AndroidViewModel(application) {
    var liveData = MutableLiveData<String>()
    
    init { 
      liveData.value = "hello"
    }
}
```
ViewModel
```
  private lateinit var exampleBinding : ActivityExampleBinding // 초기화 지연
  
  exampleBinding.viewModel = MainViewModel(application) // AndroidViewModel(application) 단일 클래스 extends
  exampleBinding.viewModel.liveData.observe(this, t -> { 
    // UI 변경
  }) // observe를 통한 실시간 값 변경시, 메소드 실행 
 

```
Activity 

# About Coroutine

### Coroutine 기본 이용 방법

```
  GlobalScope.launch { // 기존 쓰레드
     withContext(Dispatchers.Main) { // 메인 쓰레드

     }
     // 기존 쓰레드
     withContext(Dispatchers.IO) { // IO 처리 쓰레드 ( 비동기 작업에 많이 이용됨. )

     }
     //기존 쓰레드
  }
```  

### funcA 메소드 호출 이후 funcB 메소드 호출 

```
  suspend fun initMembers() { // suspendCoroutine을 처리하기 위한 메소드 suspend 추가
        withContext(Dispatchers.Main) { // 메인 쓰레드
            membersNum.value = suspendCoroutine { // 서스펜드 코루틴 진입 
               CodeObject.getReference.child("example").addValueEventListener(object : ValueEventListener { // realtime db를 통한 valueEventListener
                   override fun onDataChange(snapshot: DataSnapshot) {
                       example.value = snapshot.value.toString() // 값 라이브데이터에 넣기
                       if(isActive) { // 여전히 실행중이라면,
                           it.resume(snapshot.value.toString()) // 값이 올때까지 수신 대기
                       }
                   }

                   override fun onCancelled(error: DatabaseError) {
                      Log.d("Crashed", error.message)
                   }

               })
            }
        }
    }
```    
ViewModel
```
     CoroutineScope(Dispatchers.IO).launch { // 해당 메소드는 비동기 작업이므로 코루틴스코프에 IO 처리 , 메인쓰레드 할당 X
            binding.mainViewModel?.initMembers() // funcA 실행
            withContext(Dispatchers.Main){ // 메인 쓰레드 진입
                binding?.mainViewModel?.increaseMembers() // funcB 실행
            }
        }
```        
Activity with DataBinding




