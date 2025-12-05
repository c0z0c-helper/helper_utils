# helper-utils

[![PyPI version](https://badge.fury.io/py/helper-utils.svg)](https://badge.fury.io/py/helper-utils)
[![Python](https://img.shields.io/pypi/pyversions/helper-utils.svg)](https://pypi.org/project/helper-utils/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Python 개발 시 자주 사용하는 유틸리티 모음 라이브러리

## 주요 기능

- **🔍 helper_logger**: 로깅 유틸리티 (콘솔/파일 핸들러, 환경변수 기반 설정, KST 타임존)
- **📊 helper_pandas**: Pandas 확장 기능 (한글 컬럼 설명, 데이터 출력, HTML/콘솔 지원)
- **🌲 helper_utils_print**: 출력 유틸리티 (디렉토리/JSON/딕셔너리 트리 구조 출력)
- **📁 helper_utils_colab**: 경로 관리 유틸리티 (로컬/Colab 환경 경로 자동 탐색)

## 설치

### 기본 설치
```bash
pip install helper-utils

# 테스트 서버
pip install --index-url https://test.pypi.org/simple/ helper-utils
```

### 선택적 의존성 설치
```bash
# .env 파일 지원
pip install helper-utils[dotenv]

# Jupyter/Colab 지원
pip install helper-utils[jupyter]

# PyTorch Tensor 지원
pip install helper-utils[torch]

# 모든 선택적 의존성 설치
pip install helper-utils[all]
```

## 사용법

### 1. Logger (helper_logger)

환경변수 또는 코드 기반으로 로깅을 쉽게 설정할 수 있습니다.

```python
from helper_utils import get_auto_logger, sample_logger_env

# .env.example_logger 샘플 파일 생성
sample_logger_env()

# 자동으로 호출자 모듈명을 로거 이름으로 사용
logger = get_auto_logger()
logger.info("Hello World")
logger.debug("디버그 메시지")
logger.warning("경고 메시지")
logger.error("에러 메시지")
```

**환경변수 설정 예시 (`.env` 파일)**:
```env
LOG_LEVEL=INFO
LOG_CONSOLE=True
LOG_FILE=True
LOG_FILE_PATH=./logs/app.log
LOG_FILE_MAX_BYTES=10485760
LOG_FILE_BACKUP_COUNT=5
```

### 2. Pandas Extension (helper_pandas)

DataFrame과 Series에 한글 컬럼 설명 기능을 추가합니다.

```python
from helper_utils import set_pandas_extension
import pandas as pd

# Pandas 확장 등록
set_pandas_extension()

# DataFrame 생성
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35],
    'city': ['Seoul', 'Busan', 'Incheon']
})

# 컬럼 설명 추가
df.set_col_description('name', '사용자 이름')
df.set_col_description('age', '나이')
df.set_col_description('city', '거주 도시')

# 한글 컬럼명과 함께 출력
df.show()
# 출력:
# name (사용자 이름)  age (나이)  city (거주 도시)
# Alice               25          Seoul
# Bob                 30          Busan
# Charlie             35          Incheon

# 컬럼 설명 조회
print(df.get_col_description('name'))  # 출력: 사용자 이름
```

### 3. Print Utilities (helper_utils_print)

디렉토리, JSON, 딕셔너리를 트리 구조로 출력합니다.

```python
from helper_utils import print_dir_tree, print_json_tree, print_dic_tree

# 디렉토리 트리 출력
print_dir_tree('/path/to/directory', max_depth=3)

# JSON/딕셔너리 트리 출력 (파이프 스타일)
data = {
    'users': [
        {'name': 'Alice', 'age': 25},
        {'name': 'Bob', 'age': 30}
    ],
    'config': {'debug': True}
}
print_json_tree(data, max_depth=5, max_list_items=10)

# 딕셔너리 트리 출력 (박스 드로잉 스타일)
print_dic_tree(data, max_depth=5, show_values=True)
```

### 4. Colab/Path Utilities (helper_utils_colab)

로컬 및 Google Colab 환경에서 경로를 자동으로 관리합니다.

```python
from helper_utils import my_driver, my_cache

# Google Drive 경로 가져오기 (Colab에서 자동 마운트)
drive_path = my_driver()
print(drive_path)  # /content/drive/MyDrive (Colab) 또는 로컬 경로

# 캐시 디렉토리 가져오기 (OS별 자동 탐색)
cache_path = my_cache()
print(cache_path)  # ~/.cache (Linux/Mac) 또는 로컬 경로

# 하위 경로 지정
model_cache = my_cache('models/bert')
data_drive = my_driver('datasets/images')
```

**환경변수 우선 지원**:
```env
MY_DRIVER_PATH=/custom/drive/path
MY_CACHE_PATH=/custom/cache/path
```

## 의존성

### 필수 의존성
- `matplotlib >= 3.2.0`
- `numpy >= 1.16.0`
- `pandas >= 1.0.0`
- `pytz >= 2021.1`

### 선택적 의존성
- `python-dotenv >= 0.19.0` - `.env` 파일 지원
- `IPython >= 7.0.0` - Jupyter/Colab 지원
- `torch >= 1.0.0` - PyTorch Tensor 지원

## 라이선스

MIT License - 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 기여

이슈 리포트 및 풀 리퀘스트는 [GitHub Repository](https://github.com/c0z0c-helper/helper_utils)에서 환영합니다!

## 작성자

**c0z0c** - [c0z0c.dev@gmail.com](mailto:c0z0c.dev@gmail.com)

## 관련 라이브러리

- [helper-plot-hangul](https://github.com/c0z0c-helper/helper_plot_hangul) - Matplotlib 한글 폰트 자동 설정
- [helper-hwp](https://github.com/c0z0c-helper/helper_hwp) - HWP 파일 파싱 라이브러리
