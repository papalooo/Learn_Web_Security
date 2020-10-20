# Open Direct

`Redirect`는 사용자의 Location을
이동시키기 위한 기능 중 하나입니다.

Redirect가 사용되는 코드는
아래와 같이 HTTP Response의 300번대
영역을 통해 이동되고나,
JS를 통해 이동하는 경우가 대부분이며

이때 이동하는 주소가
공격자에 의해 변경될 경우
Open Redirect 취약점이 발생ㅎ나다.

```python
from flask import Flask, request, redirect
app = Flask(__name__)
@app.route('/redirect')
def index():
	return redirect(request.args.get('url'))
```

`Open Redirect` 취약점은 사용자가
접속한 도메인 사이트에 대한 신뢰를
무너뜨릴 수 있는 공격으로,

`Open Redirect` 취약점을 통해
피싱 사이트로 접속을 유도하거나,
다른 취약점을 연계하여, 사용자를 공격 가능합니다.

## 공격방법

공격방법은 `Redirect`가 발생하는 경로에서
공격자의 입력 값에 의해 주소가 변경 될 경우,
해당 경로와 공격자의 값이
함께 전달되도록 사용자를 유도하여
`Redirect`가 실행되도록 하는 방법이 있습니다.

url 데이터를 https://example.com과 같이
주소를 유도하거나,
javascript: \<JS Code>의 형태로 JS를 실행 할 수 있습니다.

    Ex javascript:alert(1)

