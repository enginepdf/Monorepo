
# Monorepo

- 하나의 저장소에서 test, build, release 한 번에 진행 가능
- 모듈별 개별적 버전 관리
- 패키지 매니저 등록 없이 코드 공유 쉬워짐


## Mono-Repo를 사용하기 좋은 경우

1. 서로 다른 패키지가 연관 관계를 가질 때(동일 모듈을 다른 프로젝트에도 같이 사용해야 될 때 등)
2. 첫번째 항목이 고려된 상황에서 N개의 패키지의 형태와 목적이 유사한 경우
3. 두번째 항목이 고려된 상황에서 N개의 패키지 중 배포되어야 할 패키지의 비중이 큰 경우


Module resolving(search the module inside of node_modules if not go to parent one)

require('specific-module') instead of require('../specific-module') then find the module under node_module folder


## Yarn Workspace

1. yarn init  (for root package.json)

root/package.json
``` 
{
  "private": true,   
  "workspaces": [
    "packages/*"
  ]	
}
```

2. 패키지별 package.json 생성

cd packages/functions && yarn init -y
cd packages/server && yarn init -y

server/package.json
``` 
{
  "name": "@project/server",   // npm에서 가지고 온 모듈과 구분 위해 @포함한 prefix 사용 
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT"
}
```

3. root 디렉토리에서 yarn install

4. server 패키지에서 functions 모듈을 참조

packages/functions/index.js
```
module.exports = () => {
  console.log('this works!');
};
```

yarn workspace @project/server add @project/functions@1.0.0  // server 패키지에 functions 의존성 추가

packages/server/index.js
``` 
const check=require('@project/functions');
check()
```

5. server/index.js 실행

node packages/server/index

6. npm 모듈 추가

packages/server/package.json
``` 
"dependencies": {
  "@project/functions": "1.0.0",
  ...
}
```

packages/functions/package.json
```
"dependencies": {
  ...
}
```

Hoist : root에서 yarn install 시에 공통된 모듈에 같은 버전이면 hoist 되어 root 폴더의 node_modules에 설치


## Lerna

Lerna : Mono-Repo를 위한 CLI 도구, git, npm을 사용하여 mono-repo 관리와 workflow를 최적화하는 도구

Lerna의 기본 구조 : Root 경로 아래 packages 폴더가 있고 그 하위에 각 package 별 폴더 생성
                 Root 경로의 package.json에는 모든 package가 공통으로 사용되는 dependencies가 명시


lerna clean

lerna bootstrap

lerna run

lerna publish

lerna exec


### reference  
https://velog.io/@kdydesign/Lerna%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Mono-Repo-%EA%B5%AC%EC%B6%95-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC

https://y0c.github.io/2019/06/14/monorepo-tutorial/
