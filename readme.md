# 깃 플로우 적용 테스트
테스트 브랜치 테스트 중

## 개발 및 개발자테스트
master			$ git pull
				$ git switch develop
develop 		$ git flow feature start < branch name > // branch name 브랜치로 자동 이동
feature/name	$ git commit	// 개발 작업 후 커밋
				$ git flow feature finish simulation	// feature/name 브랜치 develop 브랜치로 병합 -> feature/name 브랜치 삭제 -> develop 브랜치 이동
develop			$ git pull		// origin/develop 과 동기화
				$ git push		// origin/develop 에 push

				$ git branch -r		// remote 에 support 브랜치 있는지 확인
				-	$ git pull origin 	// origin 에 있는 support branch pull
					or
				-	$ git flow support start -F < version > master		// remote에 support 브랜치 없다면, master 베이스로 test용 support 브랜치 생성 후 이동

support/version	$ git log develop	// 테스트 할 브랜치 커밋 복사하기
				$ git merge < commit hash >		// 테스트할 커밋 병합 후 테스트
				$ git push origin support/version	// 테스트 통과시 remote 에 support 브랜치 푸쉬
				// 이후 기능단위로 releases/<version> 에 머지 리퀘스트

## 사용자 테스트
(git flow init 시 next release branch 명을 develop 대신 release, prefix 중 release/ 를 releases/  로 명명)
master			$ git pull
				$ git switch -c origin/support/<version>
				$ git pull origin support/<version>
				$ git flow release start <version>
releases/version	$ git log support/<version>	// release 할 기능에 대한 커밋 확인
					$ git merge < commit hash >
					$ git flow release finish <version> // editor 에서 master 태그 작성
					$ git push origin release
gitlab		merge request release -> master