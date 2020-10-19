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

