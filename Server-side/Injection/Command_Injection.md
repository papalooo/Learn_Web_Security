# Command Injection

웹 앱에서 OS Command를 사용하기 위해
> PHP(System)
> NodeJS(child_process)
> Python(os.system)
이 셋과 같이 OS Command를 실행하는 함수가
구현되어있습니다.

OS Command란
1. `linux(ls, pwd, ping, zip)`
2. `windows(dir, pwd, ping)`
이 처럼 OS에서 사용되는 Command입니다.

일반적으로 웹 어플리케이션에서 OS Command를 사용하는 이유는 이미 기능을 구현한 OS 실행파일이 존재할 때
