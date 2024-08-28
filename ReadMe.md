## 기본 Git 명령어

1. `git branch`: 현재 저장소의 브랜치 목록을 보여줍니다.
   - 사용법: `git branch`

2. `git checkout [브랜치명]`: 해당 브랜치로 이동합니다.
   - 사용법: `git checkout jryu`

1. `git status`: 현재 작업 디렉토리의 상태를 확인합니다. 변경된 파일, 스테이징된 파일 등을 보여줍니다.
   출력 결과에서 초록색은 `add`된 파일, 빨간색은 `add`되지 않은 파일입니다.
   - 사용법: `git status`

1. `git add [파일명]`: 변경된 파일을 스테이징 영역에 추가합니다.
   - 사용법: `git add README.md`
   - 전체를 넣고 싶다면 `git add .`

1. `git commit -m ""`: 스테이징된 변경사항을 커밋합니다. 따옴표 안에 커밋 메시지를 작성합니다.
   - 사용법: `git commit -m "README file added"`

6. `git push origin jryu`: 로컬의 커밋을 원격 저장소의 jryu 브랜치로 push합니다. 실행 이후 github 홈페이지에 push된 것을 확인할 수 있습니다.
   - 사용법: `git push origin jryu`

7. `git pull`: 원격 저장소의 변경사항을 현재 브랜치로 가져와 병합합니다. 항상 작업 시작 전에 `git pull`을 실행하여 최신 변경사항을 가져오는 것이 좋습니다.
   - 사용법: `git pull`

## 일반적인 작업 순서

1. 브랜치 확인 및 생성:
   ```
   git branch
   git checkout jryu
   ```

2. 작업 전 최신 변경사항 가져오기:
   ```
   git pull
   ```

3. 파일 수정 후 상태 확인:
   ```
   git status
   ```

4. 변경된 파일 스테이징:
   ```
   git add README.md
   ```

5. 변경사항 커밋:
   ```
   git commit -m "README file updated"
   ```

6. 변경사항 원격 저장소에 푸시:
   ```
   git push origin jryu
   ```

