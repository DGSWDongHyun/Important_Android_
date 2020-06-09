# Important_Android_
안드로이드를 배우면서 중요한 것들을 공유하는 레포지트리입니다.

- 1. Android에서 Mysql을 쓰면 안되는 이유.

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
The same arguments actually apply to ANY client-side use of MySQL, it's just that they get even stronger on a mobile platform.
MySQL 을 사용하는 어떠한 클라이언트 라도 동일한 논쟁이 발생합니다. 단지 모바일 플랫폼 상에서는 더욱 강력하게 발생할 뿐이죠.

출처: https://ggoreb.tistory.com/110?category=381975 [나는 초보다]

-

- 2. 추가 예정.










