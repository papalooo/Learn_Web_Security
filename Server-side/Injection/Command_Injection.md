# Command Injection

## 목차
1. [개요](#개요)
2. [특수문자](#특수문자)

## 개요
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

일반적으로 웹 어플리케이션에서 OS Command를 사용하는 이유는 이미 기능을 구현한
OS 실행파일이 존재할 때
코드 상에서 다시 구현하지 않고
`OS Commnad`로 실행하면 더 편리하기 때문이다.

`OS Commnad`는 내부적으로
쉘을 이용해 실행하는데,
쉘에는 한 줄에 여러 명령어를 실행하는 등의
쉘 사용자 편의성을 위해 제공하는
특수 문자들이 존재합니다.

`OS Command`를 사용할 때
만약 사용자의 입력이 검증되지 않고,
그대로 `OS Command` 함수에 들어가게된다면
오른쪽 탭의 특수 문자를 이용해
사용자가 원하는 명령어를 함께 실행하게 될 수도 있습니다.

## 특수문자

### `&&`
**명령어 연속 실행**
한 줄에 여러 명령어를
사용하고 싶을 때 사용합니다.
앞 명령어에서 에러가 발생하지 않아야
뒷 명령어를 실행합니다.(Logical And)

> $ echo hello &&
> echo theori
> hello
> theori
-----
### `||`
**명령어 연속 실행**
한 줄에 여러 명령어를
사용하고 싶을 때 사용합니다.
앞 명령어에서 에러가 발생해야
뒷 명령어를 실행합니다.

> 1 : $ cat / || echo theori
> 2 : cat: /: Is a directory
> 3 : theori
-----
### `;`
**명령어 구분자**
한 줄에 여러 명령어를
사용하고 싶을 떄 사용합니다.
`;`은 단순히 명령어를
구분하기 위해 사용하며,
앞 명령어의 에러 유무와 관계 없이
뒷 명령어를 실행합니다.

> 1 $ echo hello;
> echo theori
> hello
> theori
-----
### `|`
**파이프**
앞 명령어의 결과가
뒷 명령어의 입력으로 들어갑니다.

> $ echo id | \bin\sh
> uid=1001(theori)
> gid=1001(theori)
> groups=1001(theori)
-----
### ``
**명령어 치환**
``안에 들어있는 명령어를 실행한 결과로
치환됩니다.

> echo \`echo theori\` theori
-----
### `$()`
명령어 치환
`$()`안에 들어있는 명령어를
실행한 결과로 치환됩니다.
이 문자는 ``와 다르게 중복 사용이 가능합니다.

> \$ echo $(echo
> theori)
> theori

## Command_Injection
`Command Injection` 취약점을 막기 위해서는
사용자의 입력 데이터가
Command 인자가 아닌 다른 값으로
해석되는 것을 막아야 합니다.

가장 좋은 방법은 웹 어플리케이션에서
`OS Command`를 사용하지 않는 것입니다.
웹 어플리케이션에서 필요한 `OS Command`가
라이브러리 형태로 구현되어 있으면
해당 라이브러리를 사용하고,
아니면 직접 짜는 것이 좋습니다.

> OS Command는 사용할 경우,
> 다른 취약점이 발생하는 등의 잠재적인
> 위협이 될 수 있습니다.