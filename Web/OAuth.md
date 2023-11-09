## 1. OAuth 란?
`OAuth("Open Authorization")`는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, `접근 위임을 위한 개방형 표준`이다.

#### 즉, 애플리케이션이 사용자가 사용하는 타사 애플리케이션 정보에 접근하기 위해 권한을 타사에게 받는 것

---

## 2. 등장 배경
가장 간단 한 방법은 **사용자**가 **A Service**를 통해 **B service**의 기능을 사용하고 싶을 때, 사용자는 **A Service**에게 **B Service**의 ID/PW 를 알려주는 것이지만, 이는 **사용자**와 **B Service** 모두 불만족스러운 방식이다.

이후, 구글은 AuthSub, 야후는 BBAuth 등 각각 기업에서 개발한 인증 방법을 사용했지만, 표준화 되어있지 않았기 때문에 구글이나 야후 등과 연동하려면 개별적으로 개발하고 유지보수 해야했다

이를 위해 등장한 것이 바로 **OAuth** 이다. 최초 1.0 버전은 2006년 트위터와 Ma.gnolia 가 주도적으로 개발하였다. 이후 1.0버전이 개선된 1.0a 버전이 출시되었으나 모바일 어플리케이션 등에서 안전하게 사용될 수 없는 사례가 존재했다. 이런 사례를 보완하고 기존 버전보다 조금 더 단순화한 **OAuth 2.0** 버전이 **2012**년에 등장하게 되었다


> 용어정리 :  
> 사용자 : Resource Owner  
> B Service : Client  
> A Service : Resource Server, Authorization Server  
> Access Token : A Service가 필요로 하는 부분적인 기능만 허가  
 
 ---

## 3. 동작원리

#### 1. Client가 Resource Server에 사전 허가(등록)를 받는다.
- Client ID : 애플리케이션 식별자, 외부에 공개해도 됨
- Client Secret : ID에 대한 비밀번호, 절대 노출되면 안됨
- Authorized redirect URIs : 권한을 부여하는 과정에서 Authorized Code를 전달 받는 주소
- ![](https://velog.velcdn.com/images/k-minsik/post/de840de8-16bb-4cec-b4fb-caadb60afac7/image.png)


#### 2. Resource Owner가 Resource Server의 기능을 원하면 Client는 Owner에게 인증을 받는다(로그인 등)
- https://url/?client_id=1&scope=A&redirect_uri="..." 으로 로그인 유도
- Server가 위 주소의 Client ID를 확인하고 있으면 진행, 없으면 무시
- ![](https://velog.velcdn.com/images/k-minsik/post/c77fdec3-767d-442e-a0ba-79705c0ab953/image.png)


#### 3. Server가 Owner에게 Client에게 권한 위임 할 것인지 묻고 저장  
- ![](https://velog.velcdn.com/images/k-minsik/post/1b81d9c2-5253-41d4-bf73-d0cfdb2be58f/image.png)


#### 4. Resource Server가 Owner에게 redirect uri를 통해 Authorization code를 전달한다
- Owner는 redirect uri로 옮겨지고 Client에게 Code를 전달한다
- ![](https://velog.velcdn.com/images/k-minsik/post/3b6f7bef-945f-4fb0-81ec-95b7d03a4610/image.png)


#### 5. Client가 Code, ID, Secret, redirect_uri의 조합으로 Resource Server에게 인증하고 Access Token을 발급받는다
- ![](https://velog.velcdn.com/images/k-minsik/post/97e69e27-0b3a-410d-bdcc-5d71fdc831b1/image.png)

#### 6. Client가 발급받은 Access Token으로 Resource Server의 API를 사용하여 기능을 사용한다

#### 7. Client는 Access Token을 발급 받을 때, Refresh Tokendmf 함께 발급 받고, 모두 저장 해둔다
- 이후 Access Token이 만료되어 401 에러가 발생하면, Refresh Token을 보내 새로운 Access Token을 발급 받는다




---


> 참조 :
> https://ko.wikipedia.org/wiki/OAuth  
> 생활코딩 Youtube
