# A.i-ChatRoom
 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
index 379c869cb5703313d1a211d1f1ff51bcd00b7b5b..a697386477aefe074d0b30bfbf84ec85a23b0435 100644
--- a/README.md
+++ b/README.md
@@ -41,25 +41,53 @@ MetaCore CLI:
 unzip MEDUSA_V2_1_RESOURCE_AWARE_METACORE.zip
 cd MEDUSA_V2_1
 
 python -m venv .venv
 .venv\Scripts\activate
 pip install -r requirements.txt
 
 # (권장) 세션/작업 시작 (UID 발급 + active 설정)
 python -m metacore start MED BLD "MEDUSA V2.1 session" "resource accounting + advanced scheduling + hardening"
 
 # (선택) 서버에서 hardgate 강제
 $env:MEDUSA_METACORE_HARDGATE = "1"
 
 python -m medusa.server
 ```
 
 ## 테스트
 ```bash
 pytest -q
 ```
 
 ---
 
 ## Monitoring
 See: `monitoring/README_MONITORING.md`
+
+---
+
+## GitHub 업로드 준비 체크리스트
+
+현재 구조로도 GitHub 업로드는 가능하지만, 아래 항목을 먼저 점검하면 "바로 실행 가능한 결과물"에 더 가깝습니다.
+
+1. **환경 고정**
+   - `requirements.txt` 최신화 및 버전 고정
+   - Python 실행 버전(`3.10+` 등) 명시
+
+2. **실행 진입점 검증**
+   - 로컬에서 `python -m medusa.server` 정상 부팅 확인
+   - `python -m metacore index` 등 핵심 CLI 동작 확인
+
+3. **기본 테스트 확인**
+   - `pytest -q` 통과 상태 확인
+   - 최소 smoke test 결과를 README 또는 PR 본문에 첨부
+
+4. **시크릿 분리**
+   - 토큰/키/로컬 경로는 `.env`로 분리
+   - 저장소에는 `.env.example`만 커밋
+
+5. **배포 문서화**
+   - 설치 → 실행 → 검증 순서로 Quickstart 유지
+   - 선택 옵션(예: `MEDUSA_METACORE_HARDGATE=1`)의 영향 설명
+
+위 체크가 끝나면, 브랜치에 커밋 후 GitHub 원격 저장소로 `push`하고 PR을 생성하면 팀 단위 검증/배포 흐름으로 바로 연결할 수 있습니다.
 
EOF
)
