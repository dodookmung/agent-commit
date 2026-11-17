# agent-commit

AI 모델 제공사(Claude, OpenAI, Gemini, Grok)별 독립 폴더와 전용 Git 작성자 프로필(user.name/email)을 적용해 커밋을 관리하는 테스트 레포지토리

---

## >왜 폴더를 메인으로 빠져나갔는데 git cofnig가 global 상태로 push가 안됐지? 

`git config --local`은 현재 터미널이 위치한 하위 폴더(`google\test`)가 아니라 **레포지토리 전체(`agent-commit\.git\config`)에 저장되는 설정**이기 때문입니다.

상위 루트 폴더(`agent-commit`)로 빠져나와도 여전히 같은 레포지토리 안이므로, 아까 설정한 `gemini-test` 값이 `global` 설정을 계속 덮어쓰고 있습니다. (Git은 항상 `local` 설정을 `global` 설정보다 우선 적용하며, 직접 지우기 전까지 유지됩니다.)

---

### `global` 설정으로 되돌리는 방법

레포지토리에 저장된 `--local` 설정을 삭제(`--unset`)하면 즉시 컴퓨터의 `global` 설정을 따라갑니다.

```powershell
git config --local --unset user.name
git config --local --unset user.email

```

실행 후 `git config user.name`을 입력해 본인 계정 이름이 나오는지 확인하시면 됩니다.

---

### 폴더별 운영 팁 (PowerShell 기준)

* **루트 폴더용 초기화 파일 추가:** 최상위 `agent-commit` 폴더에도 `reset.bat` 같은 파일을 만들어 위 `--unset` 명령어 두 줄을 넣어두시면, `README.md` 등을 수정할 때 바로 본인(`global`) 계정으로 돌아올 수 있습니다.
* **`.bat` 확장자 활용:** 현재 Windows PowerShell을 사용 중이시므로 스크립트 파일 확장자를 `.sh` 대신 `.bat`으로 만드시면 별도 도구 없이 터미널에서 `.\set.bat` 입력만으로 바로 실행됩니다.

---

## unset해도 잘 안됨

.git에 저장되면 뭔가 꼬이는듯
그냥 git 레포지토리 폴더별로 관리하는게 나을거 같은데 

## license

MIT
