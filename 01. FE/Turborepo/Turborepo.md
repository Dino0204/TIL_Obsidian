터보레포는 JS/TS 코드베이스를 위한 고성능 빌드 시스템이다.
[[Monorepo]] 구조를 빠르게 사용할 수 있으며 일반적으로 사용되는 [[Multirepo]] 구조 또한 사용할 수 있다. [[Vercel]]에서 개발 되었다.

## 터보레포 왜 사용할까?
---
터보레포를 왜 사용하는지 알려면 Monorepo 구조의 문제점부터 알아야 한다. 모노레포는 각 작업마다 자체 테스트, 린팅, 빌드 프로세스등이 존재하는데 이는 속도 저하의 원인이 된다. 따라서 터보레포는 이와 같은 문제점을 원격 캐시에 작업 결과를 저장하는 것으로해결하였다. [[CI/CD]]와 같은 작업을 여러번 반복해서 작업할 필요 없이 단 한번만 실행하여 작업을 완료할 수 있다.

## 시작하기
---
아래 단계를 따라서 터보레포를 시작해보자.

### 전역 설치
```bash
npm install turbo --global
```

### 템플릿 설치
아래 명령어를 실행하면 저장소가 설치가 될탠데 자세한 내용은 [깃허브](https://github.com/vercel/turborepo/blob/main/examples/basic/README.md)를 참고하자.
그리고 아래 내용이 이해가 안된다면 [예제](https://turborepo.com/docs/getting-started/examples)를 통해 확인 할 수도 있다.
```bash
pnpm dlx create-turbo@latest
```

