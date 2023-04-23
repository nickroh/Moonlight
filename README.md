# Moonlight
 
군대에서 [A50](https://namu.wiki/w/%EA%B0%A4%EB%9F%AD%EC%8B%9C%20A50?from=A50)을 가지고 원신을 하다 빡쳐서 시작한 프로젝트

### 현 문제

A50은 너무 구리다 그냥 구리다 원신을 최저옵으로 해도 얼마안가 내가 게임을 하는것인지 게임이 나를 하는것인지 구분을 할 수 없다

물론 그냥 좋은 폰을 사면 해결이 되긴하지만 이건 너무 비싸다. 최소한 스냅드래곤 855 이상급의 모델을 사야하나 중고가가 15만원이고 그마져도 

번인등의 하자들이 있다.

그렇기에 그럴바에는 A50으로 집 노트북을 [Moonlight](https://moonlight-stream.org/)를 이용해 원격 조종하여 원신을 하자는 계획을 세우게 되었다

## 준비과정

* WOL
컴퓨터를 24시간 켜두기는 좀 그렇다 그렇기에 컴퓨터를 내가 원할떄 생활관에 누워서 킬 수 있어야 한다

집의 인터넷 구조는 이와같다

<광랜> -- <GNT 2400 모뎀> -- <IPTIME 1004a 공유기> -- <원격조종할 노트북>

IPTIME 에서는 기본적으로 DDNS 와 WOL을 지원하기에 이를 이용하기로 한다 허나 GNT2400 모뎀이 NAT 모드로 되어있었기에 

IPTIME 외부접속주소가 내부망으로 뜨는 현상이 있어 GNT2400 모뎀을 bridge 모드로 수정후 다시 시도하였고 성공적으로 DDNS를 통해 공유기에 접속

그리고 WOL기능을 사용할 수 있었다

보통을 이정도면 되겠지만 나는 컴퓨터가 켜진다면 뭔가 확실한 알림을 받고싶다

1. WOL로 컴퓨터 전원 on
2. 메일로 전원이 켜졌음을 알림
3. 전원이 켜진걸 확인하는 나

이러한 구조를 원한다

고로

sender.ps1
```shell
$Username = "yourusername"
$Password = "yourpassword"
$From = "sender@example.com"
$To = "recipient@example.com"
$Subject = "Subject of the email"
$Body = "Body of the email."

$SMTPServer = "smtp.example.com" 
$SMTPPort = 587

$SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
$SMTPClient.EnableSsl = $true
$SMTPClient.Credentials = New-Object System.Net.NetworkCredential($Username, $Password)

$Message = New-Object System.Net.Mail.MailMessage($From, $To, $Subject, $Body)

$SMTPClient.Send($Message)
```

다음과같이 배치파일을 만들어 시작프로그램에 넣어둔다
```bat
powershell.exe -ExecutionPolicy Bypass -File "C:\ .... \sender.ps1"
```

* Moonlight

컴퓨터를 켰다면 이제 휴대폰으로 원격조종을 해야한다

내 폰이 A50인 관계로 Android 기준으로 설명할것이며 아이폰은 알바가아니다

일단 앱을 [다운받는다](https://play.google.com/store/apps/details?id=com.limelight&pli=1)

게임을 돌릴 PC가 Nvidia 그래픽 카드를 이용한다면 Nvidia Shield 를 이용할수 있지만 왜인지 모르게 Error 521을 계속 토하므로

우리는 Sunshine을 이용해 볼것이다 [다운로드](https://play.google.com/store/apps/details?id=com.limelight&pli=1)

위의 준비과정이 끝났다면

1. 게임을 돌리 PC에 [Moonlight Hosting Tool](https://play.google.com/store/apps/details?id=com.limelight&pli=1)을 다운받는다
2. Moonlight Hosting Tool 을 실행한다 
3. 이놈이 지가 알아서 검사를 한다음에 문제가 있다면 알려줄테니 알아서 해결한다
4. [이걸 보고 Sunshine을 잘 설치한다](http://syanoe.com/game/g-util/7834.htm)

다했다면 잘 원격조종이 되는지 확인해보자

* 게임패드

문라이트 앱내에서도 어느정도의 터치스크린 기반 게임 패드를 제공하지만 이건 구리다 고로 [이런걸](https://www.joytron.co.kr/product_view.php3?kind=13&skind=28&f_num=1399) 사는걸 추천한다

* 문라이트 세부 설정

사실 직접 이것저것 해보는게 좋겠지만 자잘한 팁을 적어보면 

이앱은 데이터를 퍼먹는다 만약 진짜 무제한 요금제를 쓰는게 아니라면 어느정도 제한을 걸고 사용해야한다

문라이트 앱내에서 설정에 들어가면 Video Frame Rate, Video Bitrate, Video Resolution을 설정할수 있는데 만약 본인이 

데이터가 완전 무제한이 아니라 100GB + 5Mbps 와 같은 요금제라면 1080p 에 30FPS 정도나 720p 에 30FPS를 사용하고 너무 불편하지 않을정도로 Video Bitrate를 줄이는것을 추천한다


* ETC

만약 게임 콘솔만을 원격제어를 위해 사용한다면 키보드 사용은 불가능 하기에 바탕화면에 윈도우 화상 키보드 바로가기를 추가해두는것이 좋다









