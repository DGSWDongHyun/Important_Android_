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
](url)

위 그림을 보면 알 수 있듯이 ViewModel은 Model은 알지만 View를 모르고 View는 Model을 모르지만 ViewModel을 알 수 있습니다. 이제 AAC JetPack을 사용하여 보다 쉽게 MVVM 패턴을 프로젝트에 적용해보도록 하겠습니다.







