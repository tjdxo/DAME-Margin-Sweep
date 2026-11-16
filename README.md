# DAME Margin Sweep — GitHub Pages

DAME 96D/192D Margin Sweep 결과를 정적 페이지로 공개하는 저장소입니다.

## 파일 구조

- `index.html` : 반응형 히트맵·순위표·W&B JSON/CSV 입력 UI
- `data/experiments.json` : **공식 실험 데이터** (GitHub에서 버전 관리)
- `.nojekyll` : GitHub Pages 정적 파일 배포 설정

## GitHub Pages 배포

1. GitHub에 새 저장소를 만들고 이 폴더의 **내용물**(index.html, data/, README.md, .nojekyll)을 저장소 루트에 업로드합니다.
2. 저장소 **Settings → Pages → Build and deployment → Deploy from a branch**를 선택합니다.
3. Branch를 `main`, 폴더를 `/(root)`로 정하고 저장합니다.
4. Pages에 표시된 공개 URL로 접속합니다.

저장소가 Public이면 누구든지 페이지를 볼 수 있지만, **쓰기 권한 없는 방문자는 GitHub 저장소의 데이터를 수정할 수 없습니다.**

## 새 실험 결과 업데이트

**방법 A — 편집 UI 사용**

1. GitHub Pages URL 뒤에 `?edit=1`을 붙여 개인 브라우저 편집 모드에 진입합니다.
2. 실험명(`01_0225` 등)을 입력하고 W&B Summary JSON 또는 평가 CSV를 붙여넣어 **결과 등록 / 덮어쓰기**를 누릅니다.
3. **JSON 백업** 버튼을 눌러 `experiments.json`을 다운로드합니다.
4. 로컬 저장소의 `data/experiments.json`을 다운로드한 파일로 교체한 다음 GitHub에 커밋·푸시합니다.
5. 사이트 새로고침 시 모든 방문자에게 공식 데이터가 반영됩니다.

편집 화면의 데이터는 **브라우저 localStorage에만 임시 저장**됩니다. `?edit=1`은 **비밀번호/접근통제가 아닙니다.** 누구든 열 수 있지만, GitHub 공식 데이터를 바꾸려면 해당 저장소에 쓰기 권한이 필요합니다. 공식 데이터는 일반 방문자에게 별도의 입력 없이 읽기 전용으로 보입니다.

**방법 B — GitHub에서 JSON 바로 수정**

- GitHub 웹에서 `data/experiments.json`의 연필 아이콘으로 JSON 배열에 새 실험 객체를 추가하거나 수정하고 커밋합니다.
- 객체 예시:

```json
{
  "id": "01_0225",
  "source": "W&B 재실험 원본",
  "metrics": {
    "EER/O/both/full": 2.2,
    "EER/O/enroll_5s/1s": 5.8
  }
}
```

`01_0225`는 **기존 잘못된 결과를 삭제**했으며 정확한 재실험값을 받은 후에만 다시 등록합니다. (위 수치는 JSON 구조 예시일 뿐 실제 결과가 아닙니다.)

## 기존 v2와 데이터 주의사항

- 기존 `01_0225`는 `0075_0225` 설정을 잘못 등록한 결과이므로 공식 데이터에서 삭제하였습니다.
- 96D/192D Margin의 이름 규칙: `01_0225` → `0.1`, `0.225`.
- `요약값` 배지는 원본 17개 EER이 아닌 과거 이미지에서 옮긴 반올림 데이터입니다.
- 기존 v2 HTML의 `localStorage`와 새 Pages 편집 모드는 분리되어 있습니다. 잘못된 `01_0225` 결과가 이전 저장값에서 자동 복원되지 않습니다.
- 게시된 JSON 파일과 편집 초안은 별도입니다. 게시된 JSON이 업데이트되어도 **편집 모드의 오래된 로컬 초안**은 자동 갱신되지 않으므로, 공식 JSON으로 초기화하기 전 초안을 백업하세요.

## 로컬 미리보기

브라우저에서 `index.html`을 더블클릭해 `file://`로 실행하면 JSON fetch가 차단될 수 있습니다. 저장소 폴더에서 실행하세요.

```bash
python -m http.server 8000
```

그 후 http://localhost:8000 으로 접속합니다.