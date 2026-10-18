# 환경 설정
이 프로젝트의 환경은 uv로 관리됩니다. 

1. uv 설치(최초 1회)
    - macOS / Linux
        ```bash
        curl -LsSf https://astral.sh/uv/install.sh | sh          # macOS / Linux
        ```
    - Windows PowerShell
        ```powershell
        powershell ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
        ```

2. uv 설치 확인
    ```bash
    uv --version
    ```

3. 레포를 받은 뒤 환경 생성
    ```bash
    git pull origin main
    rm -rf .venv        # 기존 .venv(예: 3.14)가 있다면 삭제
    uv sync             # Python 3.12가 없으면 uv가 자동으로 받아서 설치함  
    ```

4. 의존성 추가 시
    ```bash
    uv add <패키지>
    ```
    | **NOTE**: `pip install`로 설치하지 않습니다. `uv.lock`에 기록되지 않아 다른 팀원 간 환경에 drfit 발생함. 

5. 팀 규칙
    1. `pyproject.toml`과 `uv.lock`은 항상 같이 커밋합니다.
    2. main을 pull한 뒤에는 uv sync를 실행합니다. 다른 팀원이 추가한 패키지가 반영됩니다.
    3. uv.lock에서 머지 충돌이 나면 직접 고치지 않습니다. pyproject.toml의 충돌만 해결한 뒤 `uv lock`으로 lock 파일을 다시 만듭니다.
    4. 스크립트는 `uv run python src/train.py`처럼 실행합니다. 가상환경을 따로 켤 필요가 없습니다.

# 미션 소개

이번 미션에서는  모델을 활용하여 FashionMNIST 데이터셋의 각 패션 아이템(예: 티셔츠, 바지, 스니커즈 등)을 조건부로 생성하는 작업을 수행합니다. 각 클래스에 해당하는 이미지를 생성하는 cGAN (Conditional GAN) 모델을 직접 설계하고 학습시켜 보세요.

# 데이터 소개
- **데이터 링크**: torchvision.datasets.FashionMNIST를 통해 바로 다운로드 가능합니다.
- **데이터 구성**:
    - 훈련 데이터: 60,000장의 이미지
    - 테스트 데이터: 10,000장의 이미지
    - 28×28 크기의 흑백 이미지 (10개 클래스)
- **클래스 목록**:
    - T-shirt/top
    - Trouser
    - Pullover
    - Dress
    - Coat
    - Sandal
    - Shirt
    - Sneaker
    - Bag
    - Ankle boot

# 제출 안내

다음 내용을 포함한 Colab Notebook 파일을 제출해 주세요.

파일 이름은 09_{팀명}_{성함}.ipynb 형태로 해 주세요.

1. 분석 과정과 결과
    - 데이터 로드, 전처리, cGAN 모델 설계, 학습, 생성 이미지 예측 및 평가 과정을 순차적으로 진행해 주세요.
    - 조건부 레이블을 활용해 각 패션 아이템 클래스별로 이미지를 생성하는 모델을 구현하세요.
2. 마크다운을 활용한 설명
    - 각 코드 셀이 수행하는 작업(의도, 알고리즘, 함수 설명 등)을 마크다운을 통해 자세히 기록해 주세요.
    - 노트북 내에서 코드와 결과를 한눈에 이해할 수 있도록 정리해 주세요.
3. 모델 성능 평가 및 제출
    - 생성된 이미지의 품질을 정성적(시각적 평가) 및 정량적(FID, IS 등, optional)으로 평가해 보세요.
    - 테스트 데이터셋에 대한 모델의 조건부 생성 성능을 확인할 수 있는 결과와 함께 Notebook 파일을 제출해 주세요.

# 참고 사항
- 미션을 시작할 때 도움이 필요하다면, Baseline 코드를 참고할 수 있습니다. 이 코드는 기본적인 코드로 제공되며, 여러분이 원하는 대로 자유롭게 변형할 수 있어요.
    - Baseline 코드: {project_root}/baseline/baseline_Image_Generation_FashionMNIST.ipynb
    - 주의 사항: Baseline 코드는 여러분이 모델을 시작하는 데 도움을 주기 위한 참고 자료일 뿐이며, Baseline 코드를 그대로 사용하는 것보다는 이를 기반으로 자신의 아이디어를 추가하고 발전시키는 것이 중요합니다. 가능하면 스스로 모델을 구축해보고 다양한 방법을 시도하여 성능을 향상시켜 보세요.    

- 모델 성능 개선해 보기
    - 데이터 증강(Data Augmentation): 이미지 회전, 크롭, 밝기/대비 조절 등으로 모델의 일반화 성능을 높여보세요.
    - 하이퍼파라미터 튜닝: 학습률, 배치 크기, 에폭 수 등을 조정하여 최적의 성능을 도출해 보세요.
    - 모델 구조 개선: 조건부 생성 네트워크에 추가적인 레이어 등을 도입하여 성능 개선을 시도해 보세요.

# 협업 방식
## general rule
- 절대로 main 브랜치에는 push하지 않습니다. 
- 각 팀원은 작업 브랜치를 만들어서 작업하고, main에 병합하기 위해서는 PR을 발행합니다. 
    
## branch naming rule
- **브랜치 이름은 반드시 영어로 작성합니다.** 
- **브랜치 이름에서 띄어쓰기는 '-' 하이픈을 사용합니다.** 

| 목적 | 이름 규칙 | 
| -- | -- | 
| EDA | eda/{your name} | 
| 모델링 및 실험 | exp/{실험 목적을 나타내는 소개} | 
| 잡업(환경설정, README 수정 등) | chore/{브랜치 목적을 나타내는 소개} |

## commit convention
- 일정 작업 단위가 완성되면 커밋을 진행합니다.
- **커밋 메시지는 한국어로 작성해도 좋습니다.**
- 커밋 메시지에는 작업 내용을 포괄할 수 있는 묘사(description)을 작성합니다. 팀원이 커밋 메시지만 보고 무슨 일을 했는 지 확인할 수 있어야 합니다. 
- 커밋 메시지의 구성
    ```text
    <type>: <subject>

    <body>
    ```

    | type | 정의 | 비고 | 
    | -- | -- | -- |
    | code | 코드 작업 | .py, .ipynb 작업. <br>eda 코드 작성, 수정, 모델링/실험 코드 작성, 수정</br> | 
    | docs | 문서 작업 | READEME.md, CLAUDE.md, AGENTS.md 등 코드파일이 아닌 파일을 생성 및 수정 |
    | chore | 설정 작업 | 환경변수 추가, 가상환경에 패키지 추가 등 환경설정 작업 |

    > 이번 미션에서는 너무 세부적인 커밋 타입을 지정하지는 않고, 커밋 메시지 작성에 익숙해지는 것을 목적으로 아래 두 작업유형(type)만 지정했습니다. 추후 추가가 필요하면 여기에 추가하면 됩니다.

# Git Cheat sheet
> `<...>`로 표시된 부분은 각자 상황에 맞게 바꿔서 입력합니다. (`<`, `>` 기호는 지우고 입력)

0. 최초 1회 설정
    - 커밋에 기록될 내 이름과 이메일을 등록합니다. GitHub 계정의 이메일을 사용하세요.
        ```bash
        git config --global user.name "<내 이름>"
        git config --global user.email "<GitHub 계정 이메일>"
        ```
    - Github 웹사이트에서 Personal Access Token을 발급받아 로컬 환경에 저장하세요.

1. 레포지토리 클론
    - 원격 레포지토리를 내 컴퓨터로 복사합니다. 클론은 처음 한 번만 하면 됩니다.
        ```bash
        git clone <원격 레포지토리 URL>
        cd <레포지토리 폴더 이름>
        ```
    - 원격 레포지토리 URL은 GitHub 레포지토리 페이지의 초록색 `<> Code` 버튼에서 복사할 수 있습니다.

2. 브랜치 생성 및 체크아웃
    - 작업을 시작하기 전에 항상 main 브랜치를 최신 상태로 맞춘 뒤, 거기서 새 브랜치를 만듭니다.
        ```bash
        git switch main          # main 브랜치로 이동
        git pull origin main     # 원격의 최신 main 내용을 받아오기
        git switch -c <브랜치 이름>   # 새 브랜치를 만들고 그 브랜치로 이동
        ```
    - 브랜치 이름은 위의 branch naming rule을 따릅니다. 예) `git switch -c eda/raewoo`, `git switch -c exp/add-dropout`
    - 이미 만들어 둔 브랜치로 이동할 때는 `-c` 없이 `git switch <브랜치 이름>`을 사용합니다.
    - 현재 내가 어느 브랜치에 있는지 확인하기
        ```bash
        git branch       # * 표시가 붙은 것이 현재 브랜치
        ```

3. 작업 단위 스테이징 및 커밋
    - 변경 사항 확인
        ```bash
        git status       # 어떤 파일이 바뀌었는지 확인
        git diff         # 바뀐 내용을 줄 단위로 확인
        ```
    - 스테이징: 이번 커밋에 포함할 파일을 고릅니다.
        ```bash
        git add <파일 경로>     # 특정 파일만 추가 (권장)
        git add .              # 현재 폴더의 모든 변경 사항 추가
        ```
    - 커밋: 위의 commit convention에 맞춰 메시지를 작성합니다. `-m`을 두 번 쓰면 첫 번째는 subject, 두 번째는 body가 됩니다.
        ```bash
        git commit -m "code: FashionMNIST 클래스별 분포 EDA 추가" -m "클래스별 샘플 수와 평균 이미지를 시각화함"
        ```
    - 커밋 기록 확인
        ```bash
        git log --oneline
        ```

4. 푸쉬
    - 내 브랜치의 커밋을 원격 레포지토리에 올립니다. **main이 아닌 내 작업 브랜치로 push 하는지 반드시 확인하세요.**
        ```bash
        git push -u origin <브랜치 이름>   # 해당 브랜치를 처음 push할 때
        git push                         # 이후부터는 이것만 입력해도 됨
        ```

5. PR
    - push 후 GitHub 레포지토리 페이지에 들어가면 `Compare & pull request` 버튼이 보입니다. 이 버튼을 누릅니다.
        - 버튼이 보이지 않으면 `Pull requests` 탭 → `New pull request` → `base: main`, `compare: <내 브랜치>`를 선택합니다.
    - PR 제목과 설명에 무슨 작업을 했는지 작성하고 `Create pull request`를 누릅니다.
    - 팀원의 리뷰를 받은 뒤 main에 병합(Merge)합니다.
    - 리뷰 반영으로 수정할 내용이 생기면, 같은 브랜치에서 3~4번(커밋, 푸쉬)을 반복하면 PR에 자동으로 반영됩니다.

6. PR 병합 후 정리
    - 병합이 끝나면 main을 최신화하고, 다 쓴 브랜치는 삭제합니다. 다음 작업은 다시 2번부터 시작합니다.
        ```bash
        git switch main
        git pull origin main
        git branch -d <브랜치 이름>   # 로컬 브랜치 삭제
        ```

7. Tips
    - 항상 main에 최근 변경사항이 있는 지 확인하는 습관을 들이세요. origin과 local의 drift가 있지 않도록 항상 로컬 환경을 최신화 해주세요. 


# 추가 실습(심화)

심화 문제는 채점에 포함되지 않습니다. 편한 마음으로 도전해 보세요.

## 미션 소개
- 목표: 조건부 GAN(cGAN)을 활용하여 다양한 모자 이미지를 생성하는 모델을 구축합니다.
1. 데이터셋:
    - 해당 데이터셋은 20개 클래스(각기 다른 스타일의 모자, 캡, 헬멧 등)로 구성되어 있습니다.
    - 이미지의 해상도와 다양성이 FashionMNIST보다 높으므로, 모델 구조나 학습 전략을 조금 더 세밀하게 조정해야 할 수 있습니다.
2. 실습 내용
    - 데이터 로드 및 전처리
    - ImageFolder 등으로 데이터를 불러오고, 적절한 크기로 리사이즈합니다.
    - 데이터 증강 기법(예: Random Crop, Horizontal Flip, Color Jitter 등)을 적용해 데이터 다양성을 확보합니다.
    - 모델 설계 및 학습
    - 기존의 FashionMNIST cGAN 모델을 베이스로 하되, 이미지 해상도와 데이터 복잡성을 고려하여 Generator와 Discriminator의 네트워크 구조를 조정해 보세요.
    - 조건부 레이블을 사용하여 각 모자 클래스에 따른 이미지를 생성하도록 학습시키세요.
3. 평가 및 결과 시각화
    - 학습 도중 및 학습 후에 각 클래스별로 생성된 이미지를 시각화하여, 모델의 성능을 평가해 보세요.
    - 다양한 평가 지표를 활용해 모델의 개선 방향을 모색해 보세요.
4. 마크다운 설명
    - 각 단계의 의도와 알고리즘, 구현 방법 등을 상세히 기록해 주세요.
    - 실험 결과 및 개선 방안에 대한 해설이나 인사이트를 포함해도 좋습니다.
## 제출 안내 (추가 실습)
- 추가 실습에 대한 결과도 포함된 Notebook 파일을 제출해 주세요.
- 미션을 시작할 때 도움이 필요하다면, Baseline 코드를 참고할 수 있습니다. 이 코드는 기본적인 코드로 제공되며, 여러분이 원하는 대로 자유롭게 변형할 수 있어요.
    - Baseline 코드: {project_root}/baseline/baseline_Image_Generation_Headgear.ipynb
- 파일 이름은 기본 미션 파일과 별도로 09_{팀명}_{성함}_advanced.ipynb 형태로 제출해 주세요.