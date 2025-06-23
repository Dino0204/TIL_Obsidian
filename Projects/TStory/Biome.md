![[Pasted image 20250623181957.png]]

JavaScript, TypeScript, JSX, TSX, JSON을 위한 포매터
-> CI 및 개발자 시간을 절약해 준다.

JavaScript, TypeScript, JSX를 위한 린터
-> TypeScript ESLint, 써드파티 라이브러리에서 가져온 266개의 규칙으로 구성되어 있다.

즉, JS, TS를 개발할 때 사용되는 포매터 겸 린터이다.

## Biome 왜 사용해야 할까?
---
- Rust로 구축되어 속도가 빠르다.
- 초기 설정이 필요하지 않아 간단하다.
- 크기에 상관없이 모든 코드베이스를 처리할 수 있어서 확장성이 높다.
- 내부 통합이 잘 되어 있어서 이전 작업을 재사용할 수 있다.
- 모호한 오류 메시지를 피하고, 문제가 있을 때 문제 발생원인, 해결책을 제시해준다.
- 외부 지원 없이 표준 라이브러리만으로 지원한다.

![[Pasted image 20250623100532.png]]
최적의 환경에서 Prettier보다 대략 35배 정도 빠르다.

> eslint-plugin-prettier 이슈
> Prettier의 코드 포메팅 규칙을  ESLint의 린팅 과정에 포함하여 코드 스타일 문제를 Prettier의 규칙에 따라 검사 및 수정하는 플러그인.
> 
> ESLint, Prettier를 통해 2번 파싱하기 때문에 속도가 저하되는 문제가 있다.
> -> Biome을 사용하면 속도가 저하되지 않는다.

## Biome 사용하기
---
### Biome 라이브러리 설치
```node
npm i -D -E @biomejs/biome
```

### Biome 익스텐션 설치 및 프로젝트에 적용
Biome 익스텐션을 통해 린트 룰이 잘 적용되었는지 확인 할 수 있다.
![[Pasted image 20250623101150.png]]

` .vscode/settings.json `
```json
{
  // VSC 기본 포매터: 특정 프로젝트만 Biome을 사용하기 위해서 사용한다.
  "editor.defaultFormatter": "biomejs.biome",

  // 파일 저장 시 자동으로 실행할 코드 작업 정의
  "editor.codeActionsOnSave": {
	// Biome 익스텐션에서 지원하는 Quick Fix
    "quickfix.biome": "explicit",
    // Biome에서 제공하는 import 정리 기능
    "source.organizeImports.biome": "explicit"
  }
}
```

### Biome JSON 환경 설정
Biome은 초기 설정 없이 사용할 수 있지만 요구 사항에 맞게 일부 설정을 변경할 수 있다.
```node
npx @biomejs/biome init
```

`biome.json`
```json
{
  "$schema": "https://biomejs.dev/schemas/2.0.4/schema.json",
  "vcs": {
    "enabled": false,
    "clientKind": "git",
    "useIgnoreFile": false
  },
  "files": {
	// Biome에 정의되어 있지 않은 파일 형식, 규칙을 무시한다.
    "ignoreUnknown": false
  },
  "formatter": {
    "enabled": true,
    "indentStyle": "tab"
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true
    }
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "double"
    }
  },
  "assist": {
    "enabled": true,
    "actions": {
      "source": {
	    // import 정리 기능 활성화
        "organizeImports": "on"
      }
    }
  }
}
```

### Script 작성
Biome을 자동화 도구로 사용하기 위해서 규칙을 한번에 적용할 수 있는 실행 명령어를 작성한다.

`package.json`
```json 
{
  "scripts": {
    "lint": "biome lint --write",
    "format": "biome format --write",
	// linter, formater, import 규칙 한번에 적용 및 변경
    "check": "biome check --write",
    // 문제가 발생한 파일이 어떤 규칙을 위반 했는지 보고서 형태로 알려줌
    "reporter": "biome check --reporter=summary",
  },
}
```

### Biome Caching
변경된 부분만을 빠르게 처리할 수 있다.
```node
biome explain daemon-logs
```

## 참고 자료
---
https://po4tion.dev/biome#heading-prettier-biome
https://biomejs.dev
[[ESLint]]
[[Prettier]]



