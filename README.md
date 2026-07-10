# Git으로 협업하기

## Github에서 Organization 만들기

1. GitHub 우측 상단 프로필 아이콘 클릭 → **Your organizations** 이동
2. **New organization** 클릭
3. 무료 플랜(**Free**) 선택
4. Organization 이름, 연락 이메일, 소유자(개인/팀) 여부 입력 후 생성
5. 생성 후 **People** 탭에서 팀원을 초대 (GitHub 아이디 또는 이메일로 검색 후 Invite)
   - 팀원은 초대 메일 또는 알림을 통해 수락해야 Organization 멤버로 등록됨
6. 팀 전용 저장소를 만들 경우 **Repositories → New repository**에서 Owner를 Organization으로 지정하여 생성

<br/>
<br/>

## Organization의 레포지토리 내 저장소로 fork하기

1. Organization 저장소 페이지 우측 상단 **Fork** 버튼 클릭
2. Fork 대상(Owner)을 **본인 개인 계정**으로 선택 (Organization 계정 권한이 있다면 그쪽으로 선택도 가능)
3. **Create fork** 클릭 → 본인 계정 아래에 동일한 저장소가 복사됨
4. 로컬로 클론

   ```bash
   git clone https://github.com/{내 계정}/{저장소명}.git
   cd {저장소명}
   ```

5. 원본(Organization) 저장소를 upstream으로 등록 (이후 원본의 최신 변경사항을 받아오기 위함)

   ```bash
   git remote add upstream https://github.com/{organization}/{저장소명}.git
   git remote -v   # origin(내 fork), upstream(원본) 확인
   ```

<br/>
<br/>

## (로컬) 수정사항 Push & Pull Request

1. 작업 전 최신 상태로 동기화

   ```bash
   git checkout main
   git pull upstream main
   ```

2. 작업용 브랜치 생성

   ```bash
   git checkout -b feature/{작업-내용}
   ```

3. 코드 수정 후 커밋

   ```bash
   git add .
   git commit -m "커밋 메시지"
   ```

4. 내 fork(origin)로 push

   ```bash
   git push origin feature/{작업-내용}
   ```

5. GitHub에서 내 fork 저장소로 이동 → **Compare & pull request** 버튼 클릭
6. base repository는 **Organization 저장소 / main**, head repository는 **내 fork / feature 브랜치**로 설정되어 있는지 확인
7. 제목과 변경 내용을 작성한 뒤 **Create pull request**
8. 리뷰어 지정 및 코드 리뷰 진행 → 승인(Approve) 후 **Merge pull request**

<br/>
<br/>

## (원격) 수정사항 Pull

다른 팀원이 merge한 최신 변경사항을 내 로컬/포크에 반영하는 과정

1. 원본(upstream) 저장소의 최신 변경사항 가져오기

   ```bash
   git checkout main
   git fetch upstream
   git merge upstream/main
   ```

2. 내 fork(origin)에도 최신 상태 반영

   ```bash
   git push origin main
   ```

3. 이후 새로운 작업을 시작할 때는 이 최신 main에서 브랜치를 분기하여 진행
