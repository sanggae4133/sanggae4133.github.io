---
title: Github Pages 블로그 제작 (1) (with Chirpy theme for Jekyll)
date: 2024-11-16 01:43:00 +09:00
categories: [Blog, Github_Pages]
tags:
  [
    blog,
    github_pages,
    chripy,
    jekyll  
]
---
> 참고링크:
>
> [Chirpy 테마 커스터마이징](https://www.irgroup.org/posts/Chirpy-%ED%85%8C%EB%A7%88-%EC%BB%A4%EC%8A%A4%ED%84%B0%EB%A7%88%EC%9D%B4%EC%A7%95/)
>
> [Gihub 블로그 만들기](https://chirpy.cotes.page/posts/getting-started/)

# 서문

블로그를 시작하기 앞서, 사실 tistory, velog, naver blog 셋 다 사용을 해봤었다. 음... 근데 뭔가 셋 다 살짝 애매한 느낌이랄까? 세 플랫폼 전부 깊게 사용한 건 아니지만, 그리고 길게 사용한 것도 아니지만 일단 tistory는 기본 허여멀건 디자인이 맘에 들지 않아서 패스였고, 블로그 목적이 애드 센스는 아니지만 그래도 velog는 애드센스를 못 붙이고, naver blog는 그냥 뭔가 거부감이 들고...

그러다 얼마 전에는 따로 넷북으로 구축한 개인용 홈서버에서 nginx를 커스터마이징해서 블로그 서버를 만들거나 netlify와 같은 무료 호스팅 서비스를 이용해서 블로그를 만들거나 하는 선택지도 여러 번 찾아 봤던 것 같다.

뭐 어떤 방법이든 시간을 들여 사용법을 익히고 꾸준히 포스팅을 진행한다면야 다 좋은 방법인 것 같으나, 결국 이번에 본격적으로 Github Pages를 이용해서 블로그를 개설하기로 마음 먹은 큰 이유는 아래인 느낌이랄까

1. 개발자스러운가
   - 즉, vs code와 같은 텍스트 에디터나 IDE 등을 이용해 편집이 가능한가
   - 개발에 어느 정도 익숙해야 입문할 수 있는가
   - 많은 노력을 들이지 않고 크로스 OS로 포스팅이 가능한가
2. md를 지원하는가? (노트앱을 협업은 노션, 개인용은 옵시디언을 이용하다 보니 은근 이게 컸다)
3. 애드센스 부착이 가능한가?
4. 레퍼런스가 많은가?

사실 다른 플렛폼도 이를 충족할테지만, 어찌됐든 한 번 의지가 충만할 때 시작하고 끝을 보는 타입이라 내 의지가 구글링을 하며 사라지지 않도록 더 길게 찾아보지 않고 Github Pages를 선택했다.

[Gitbug 블로그 테마 모음 사이트](https://jekyll-themes.com/)

테마는 위 사이트에서 둘러보다 마음에 드는 [테마](https://github.com/cotes2020/jekyll-theme-chirpy) "Chirpy"로 정했고, 테마를 정하는 기준은 깊게 생각하진 않았고

1. 적당히 예쁘고 심플한가(꾸미는데 품이 적당히 드는 가성비 좋은 테마인가)
   - 결국 BE, Infra 쪽이 주력이라 FE 개발 쪽은 아직 덜 익숙해서인 탓이다..
2. 레퍼런스가 많은가

로 정했다.

여튼 서론이 길었다. 앞으로도 그러겠지만, 포스트는 해당 분야를 A to Z 상세히 설명하기 보단 독자가 어느 정도 백그라운드 지식이 있다는 가정 하에, 그리고 내가 다시 보기 위한 기록용도 느낌으로 작성하고자 한다.

# 시작하기

> [Jekylll(지킬)](https://jekyllrb-ko.github.io/) 이란?
>
> Ruby 언어로 작성된 static site generator이다.
>
> 쉽게 생각하면 현재 Web/App에서 Reverse Proxy 등으로 많이 사용되는 WS인 NginX와 비슷하다고 생각하면 될 것이다.
>
> 다만, 도드라지는 특징이 있다면 MD 파일을 작성하면 이를 html로 바꿔줘, 간단히 블로그나 복잡한 로직이 없는 개인 웹 사이트를 제작하기 간편하다.

사실 FE 개발을 주력으로 하는 지인들은 그냥 React가 익숙하기에 React로 개인 포트폴리오 사이트나 블로그를 운영하는 것을 봤다. 하지만... 블로그를 운영하기에 글의 퀄리티를 높이는데 집중하지 못하고 html, css, js를 심층적으로 다루기엔 이런 MD 자동 변환이 정말 좋은 기능이라 생각된다.

따라서 기본적으로 Jekyll과 Github Pages를 이용해 블로그를 구축하는 건

- Jekyll: WS
- Github Pages: Hosting

이런 방식으로 역할을 나누는 것이다. Github Repo 같은 경우 한 Repo 당 일반적으로 1GB의 용량제한이 있으므로, 블로그 규모가 커지면 그냥 간단하게 내가 이제까지 작성했던 소스코드를 가지고 AWS든, 개인 서버에 도메인을 붙여 호스팅하면 그만이다(이는 본인은 개인서버를 이미 운영 중이기 때문에, 우선 블로그 포스트 규모가 좀 커진 후에 추후에 다뤄볼 예정이다.)

하지만! 테마를 처음부터 만들기엔 배보다 배꼽인 큰 건 사실이다. 따라서 이미 잘 만들어진 여러 테마를 이용하자 본인은 위에서 말했듯 Chirpy를 사용하기로 했다.

# Ruby, Jekyll 설치

mac, window 환경을 모두 사용하기에 둘 다 세팅 방법이 살짝 다르나 Chripy 테마 개발자가 친절하게 어떻게 설치하는지 알려주고 있다. ([Chripy Starter](https://chirpy.cotes.page/posts/getting-started/))

## Window

wsl을 사용했다. docker를 이용한 컨테이너 방식을 통해 버전 관리가 용이하게 진행하는 방법도 있으나, 어차피 Ruby를 평소 개발환경에서 사용하지 않기 때문에 굳이..? 어차피 wsl(ubuntu)를 사용해도 rvm을 통해 ruby 버전 관리는 크게 문제가 없다.

### RVM(Ruby Version Manager), Ruby 설치

window wsl이 설치가 안 됐다면 설치하고 오자..! 참고로 wsl2 환경이다.

```bash
$ \curl -sSL https://get.rvm.io | bash -s stable	# RVM curl로 최신 stable 버전 받아오기
$ source ~/.rvm/scripts/rvm	# rvm 활성화
$ rvm install 3.3.5	# 최신 stable 버전이 공식 홈페이지를 찾아보니 현재 기준으로는 3.3.5인 듯 하다. 현재 기준으로 조금 있다 사용할 bundle은 Ruby 3.1.0 이상의 환경만 지원하기 때문에 참고할 것
$ rvm use 3.3.5 --default	# ruby 디폴트 사용 버전 설정
```

여기까지 하면 ruby 설치 완료다. 당연히 버전 확인을 통해 제대로 설치됐는지 확인한다.

```bash
$ rvm list	# rvm에 현재 설치되어 있는 ruby 버전들 확인
=* ruby-3.3.5 [ x86_64 ]

# => - current
# =* - current && default
#  * - default

$ ruby -v	# ruby가 환경변수에 제대로 등록되어 있는지와 버전 체크
ruby 3.3.5 (2024-09-03 revision ef084cc8f4) [x86_64-linux]
```

### Gem 설치

```bash
$ bundle install	# 시간이 좀 걸린다
```

## Mac

우선 당연하게도 homebrew를 설치해놔야 한다.

### chruby, ruby-install 설치 및 Ruby 설치

```bash
$ brew install chruby ruby-install
$ ruby-install ruby 3.3.5	# 시간이 좀 걸린다.
```

이후 환경 변수에 등록해준다.

```bash
$ echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
$ echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
$ echo "chruby ruby-3.3.5" >> ~/.zshrc # run 'chruby' to see actual version
```

이후 ruby 버전 확인

```bash
$ ruby -v	# ruby가 환경변수에 제대로 등록되어 있는지와 버전 체크
ruby 3.3.5 (2024-09-03 revision ef084cc8f4) [arm64-darwin24]
```

### Jekyll 설치

```bash
$ gem install jekyll
$ bundle install
$ bundle update
$ bundle install
```

이후 아래 페이지에 들어가 Node.js를 설치해주면 된다.

https://nodejs.org/en

# 첫 시도: [Chripy Starter](https://chirpy.cotes.page/posts/getting-started/)

스타터를 사용해 처음 시도를 했다. 웬진 모르겠지만 `tools/test.sh`를 실행하는 과정에서 검사를 통과를 못해 배포가 안 되는 문제가 발생했다. 각 html 링크가 내부적으로 제대로 링킹이 안 되는 듯하다.. 아직 Ruby 코드를 뜯어볼 정도로 Ruby를 많이 접한 건 아니라 디버깅을 하기 보다는 그냥 깔끔하게 다른 방법을 택했다.

# 두번째 시도: [테마 레포 코드 fork](https://github.com/cotes2020/jekyll-theme-chirpy)

위 링크를에 들어가 repo를 fork한다. 뭐 사실 그냥 zip파일로 다운 받아서 바로 따로 repo를 만들어도 되지만, fork를 한다면 혹시라도 테마 변경 사항이 있을 때 이를 원본 repo에서 받아올 수 있는 장점이 있다.

당연히 개인 도메인이 있다면 그렇게 하지 않아도 되나, ``<github username>.githbu.io``형식으로 repo 이름을 만들어야 한다.

이 repo를 로컬에 받아 이제부터 본격적으로 테마 커스터마이징을 들어가면 되겠다.

repo의 root dir에서 아래 명령어로 테마 커스터마이징을 위한 초기화 스크립트를 실행시켜 준다.

```bash
$ ./tools/init.sh
```

이후 바로 WS 실행!

```bash
# 둘 중 아무거나
$ bundle execjekyll serve
$ TZ='Asia/Seoul' bundle exec jekyll serve
```

위로 해도 되나, timezone 이슈로 로컬 실행 시 제대로 포스트가 노출이 안되는 이슈가 있을 경우 아래로 하면 될 것 같다. 참고로 위 명령어를 통해 정식으로 내 repo에 push해서 github actions 트리거가 발동되기 전에 로컬에서 어떻게 글이 보일지 확인할 수 있다.

이후 `_config.yml`을 수정하면 되는데, 음 테마 개발자가 누가봐도 쉽게 알 수 있도록 주석을 제공해놔서 설명은 패스하겠다. 다만 `lang`설정의 경우 ko가 아니 ko-KR을 하면 개발자가 제공해논 기본 한국어 언어셋을 사용할 수 있다는 점, 그리고 `timezone`설정의 경우 `Asia/Seoul`이 아닌 `"Asia/Seoul"`로 적어야 적용이 된다는 점은 유의하면 좋겠다.

---

이제 여기까지 해서 기본적인 Chripy를 통한 Github Pages 블로그 호스팅을 할 수 있도록 알아봤다. 다음 포스팅에서는 기본적으로 많이 사용하는 커스터마이징, 그리고 디테일한 글 작성 방법을 한 번 다뤄볼 예정이다.


*fin.*
