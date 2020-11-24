# Git_Study

# 기존 folder를 git repo에 연동시키려고 했는데, 자꾸 .gitignore만 생성되고 폴더 전체 mapping이 안됨..
# 그나마 이를 해결할 수 있는 방법

> rm -rf .git # 이를 통해 local의 폴더를 git해제시킬 수 있다.
> echo "# DT" > README.md # 순서가 중요한가 싶지만, 아무튼 이와 같은 README.md를 먼저 생성해준다.
> git init # 현재 있는 위치에서 폴더를 git화 시킨다.
> git add README.md # stage에 올리는 절차?
> git commit -m "First commit"
> git branch -M main # 이렇게 하면 현재 위치한 폴더의 git:(master)가 git:(main)으로 바뀐다.
> git remote add origin https://github.com/zoshs2/DT.git # 본격적으로 원격저장소 repository에 연동하는 절차일 듯. 
> git push -u origin main # main 브랜치를 origin에다가 push하라 라는 뜻인가보다.

## 이렇게하면 우선은 README.md만 repo에 등록된다. 
## 그 이후로 나머지 파일들을 업로드 시키려면, 
> git add . # . 는 현재 위치한 곳에서 모든 파일 및 폴더를 일컫는다.
> git commit -m "나머지 파일 및 폴더 커밋"
> git push -u origin main # 원격저장소(repo)에 푸쉬푸쉬!! 

# 아무튼 절차는 add -> commit -> push

Git streaming은 보통 세 가지 영역의 상호작용으로 일어난다.
공간적으로 
1. Work Space 2. Local Repository 3. Remote Repository 로 나뉜다.
Work Space는 내가 작업하는 로컬 공간이다.
여기서 작업한 추가내용 또는 생성내용, 변경내용, 삭제내용등에 관한 사항을
> git add . 
를 통해 Staging Area로 올린다.
이 명령어를 통해 .git/hooks에 먼가가 생성됨을 알 수 있다.
이게 바로 Staging Area에 올라온 index 파일이라고 말한다. (* .git : 이 폴더가 바로 Local Repository이다.)

이를 다시 커밋(commit)한다면,
> git commit -m "First commit"
Staging Area에 있던 변경내용이 commit history 공간에 기록된다.

요약하자면, Local Repository 는 Staging Area와 Commit History 공간으로 나뉜다.
이를 원격저장소(Remote Repository)에 반영하려면 push를 해주면 된다.
> git push -u origin(# 원격저장소 alias) main(branch 이름)
( * 최초로 remote repository에 연동할 때, 별칭을 origin으로 설정했었다. 
     > git remote add origin https://github.com/zoshs2/DT.git )
     
     
## Remote Repo.를 Local Workplace에 반영하는 방법.
만약 멀티유저 개발환경에서 누군가가 내가 마지막으로 보관해놨던 커밋이후로 신규커밋을 추가했다면, 
나의 로컬 Workplace에 그 신규 커밋을 반영하는 방법은 무엇일까?
기존에는 로컬 환경에서
> git add . (local repo의 staging area에 올림)
> git commit -m "blah blah" (local repo의 commit history에 기록함)
> git push -u origin main (remote repo의 main branch로 반영시킴)
와 같은 흐름을 통해 나만의 작업을 remote repo. 에 반영하는 작업만 수행했다.
즉, 눈감고 귀닫고 내 일만 하는 것..ㅋ

그래서 멀티유저끼리의 공동 개발환경에선 당연히 
remote repo.에서 신규 커밋 및 변경사항을 
내 local 작업공간에도 반영해야 할 필요가 생긴다.
기본적인 흐름은 다음과 같다.
> git fetch  ( remote repo.와 나만의 local workplace(또는 local repo.)를 서로 비교하면서, remote repo.로부터 상이한 변동사항을 끌어온다.
> git merge origin/main ( git fetch 명령은 상이한 변동사항을 끌어올 뿐, 아직 반영하지 않은 상황인데, staging area에 머무는 index파일들과 유사한 상태이다.
                          따라서, 이러한 변동사항을 이제 직접 반영시켜주기 위해서는 merge(병합)을 사용한다. origin/main은 HEAD(중심이 되는 브랜치포인터)의 목표를 가리킨다.
                          브랜치(branch)는 후술하겠지만, 일종의 포인터 개념이다. HEAD라는 화살표를 특정 브랜치 포인터로 가리키며 작업을 수행하는 매커니즘이다. 자세한 내용은 나중에 더...)
