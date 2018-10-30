# 서버연동을 위한 HTTP 공부


앱에서 기록된 정보를 서버에 저장하고 싶은데 거기까지 가는 길은 비개발자에게 멀고도 험난하다. 약간의 위로가 되는 점은 무슨 말인지는 모르더라도 대개 들어보거나, 본적이 있는 단어가 많이 나온다는 점이다.


## HTTP란
HyperText Transfer Protocol.
초본문전송규약, 하이퍼본문전송규약이라고도 하며 WWW 상에서 정보를 주고받을 수 있는 프로토콜이다. 보통 80번 포트를 사용한다.


(초본문전송규약이라니... 영어보다 한글이 더 어렵다 ㄷㄷㄷ)


## 리소스 불러오기
GET 이라는 명령어를 써준다. 네이버 웹툰 링크에 나오는 /index.nhn 같은 것으로 시도해 봤지만 https만 제공하고 있어서 telnet 으로 테스트는 불가능했다.

telnet 은 원격 서버에 접속해서 그 서버를 조작할 수 있는 프로그램이다. 보통 포트 번호를 사용해서 접속하게 되면 포트 번호에서 제공하는 서버의 프로토콜을 TCP로 전송할 수 있다.


## TCP란
전송 제어 프로토콜. Transmission Control Protocol.


## URL 이란
Uniform Resource Locator. 하나의 서버에서 여러 리소스를 제공할 수 있는데, 리소스 간에 어떤 것을 가져올지 구분할 수 있게 해주는 규약이다.

URL은 리소스의 위치를 표시하는데 폴더는 /로 구분하고, 한글을 쓸 수 없다.
? 뒤에 쿼리스트링이라는 요소가 있어서 &를 기준으로 나눠서 볼 수 있다.

e.g. https://search.daum.net/search?w=tot&DA=YZR&t__nil_searchbox=btn&sug=&sugo=&q=%ED%95%9C%EB%B9%84%EC%9E%90 에서 ? 뒤에 쿼리스트링을
W=tot / DA = YZR 등으로 &를 기준으로 나눠서 볼 수 있다.


## homebrew
앱스토어 같은 개념으로 생각하면 된다. UI는 대체로 없고 주로 터미널에서 사용하기 위한 프로그램을 설치하는 곳이다. 오늘은 telnet 을 실행하기 위해서 [홈브루](https://brew.sh)를 설치했다.


## HTTP 요청 메시지 구조

HTTP 메시지 구조를 보면 요청라인, 요청헤더, 본문으로 구성되어 있다.
요청라인은 대체로 GET 이나 POST로 시작한다. 그리고 리소스 위치인 URL이 들어가게 된다.


## swift에서 GET 실습
버튼을 하나 만들어서 <신비한 동물사전2> 영화 url의 페이지를 불러와 보았다.

```swift
@IBAction func button01(_ sender: Any) {
    print("까꿍")
    do {
        let url = URL(string: "https://movie.daum.net/moviedb/main?movieId=111490")
        let response = try String(contentsOf: url!)
        print(response)
    } catch let e as NSError {
        print(e.localizedDescription)
    }
}
```