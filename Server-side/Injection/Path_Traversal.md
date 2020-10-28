# Path Traversal
Path가 사용되는 대푲거인 로직으로는
URL/File이 있습니다.

URL/File의 Path에는 Parent Directory를 의미하는 구분자 `..`가 있습니다.
예를 들어 `/tmp/test/../a` 경로가 해석되면
`/tmp/test/`의 상위 폴더인
`/tmp/`폴더의 하위에 있는 `a` 즉 `/tmp/a`를 나타낸다.

사용자의 입력 데이터가 검증 없이
URL/File Path에 직접적으로 사용되면
설계 및 개발 당시에 의도치않은
임의의 경로에 접근할 수 있는
해당 취약점이 발생합니다. 