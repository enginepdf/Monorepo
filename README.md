// reference : https://velog.io/@kdydesign/Lerna%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Mono-Repo-%EA%B5%AC%EC%B6%95-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC
// https://y0c.github.io/2019/06/14/monorepo-tutorial/

Mono-Repo를 사용하기 좋은 경우

1. 서로 다른 패키지가 연관 관계를 가질 때
2. 첫번째 항목이 고려된 상황에서 N개의 패키지의 형태와 목적이 유사한 경우
3. 두번째 항목이 고려된 상황에서 N개의 패키지 중 배포되어야 할 패키지의 비중이 큰 경우


Lerna : Mono-Repo를 위한 CLI 도구, git, npm을 사용하여 mono-repo 관리와 workflow를 최적화하는 도구

Lerna의 기본 구조 : Root 경로 아래 packages 폴더가 있고 그 하위에 각 package 별 폴더 생성
                 Root 경로의 package.json에는 모든 package가 공통으로 사용되는 dependencies가 명시

Yarn Workspace

Hoisting



lerna clean

lerna bootstrap

lerna run

lerna publish

lerna exec

