# OCR with Gemini

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cjk0604/ocr-with-gemini/blob/main/ocr_with_gemini.ipynb)
[![Open In Colab Enterprise](https://img.shields.io/badge/Colab_Enterprise-Open-blue?logo=google-cloud)](https://console.cloud.google.com/vertex-ai/colab/import/github/cjk0604/ocr-with-gemini/blob/main/ocr_with_gemini.ipynb)
[![View on GitHub](https://img.shields.io/badge/GitHub-View_Source-black?logo=github)](https://github.com/cjk0604/ocr-with-gemini/blob/main/ocr_with_gemini.ipynb)

Google Gemini 모델을 활용하여 상품 이미지에서 바코드(GTIN, UPC, EAN 등)를 인식하고, 상품명/상세 정보를 자동으로 추출하는 핸즈온 노트북입니다.

## 주요 기능

- **Image Captioning** — 상품 이미지의 내용을 자연어(영문/한국어)로 설명
- **OCR** — 바코드 영역 감지 및 bounding box 시각화
- **GTIN/UPC 추출** — 바코드 값을 기반으로 상품명, 브랜드, 카테고리 등 구조화된 정보 추출

## 사용 모델

- `gemini-3-flash-preview` (Vertex AI)

## 사전 준비

### 1. Google Cloud 프로젝트 설정

1. [Google Cloud Console](https://console.cloud.google.com/)에서 프로젝트를 생성하거나 기존 프로젝트를 선택합니다.
2. **Vertex AI API**를 활성화합니다.
   - Cloud Console > API 및 서비스 > 라이브러리 > "Vertex AI API" 검색 > 사용 설정

### 2. API 키 발급

1. Cloud Console > **API 및 서비스** > **사용자 인증 정보**로 이동합니다.
2. **+ 사용자 인증 정보 만들기** > **API 키**를 클릭합니다.
3. 생성된 API 키를 복사합니다.
4. (권장) 키 제한사항에서 **Vertex AI API**만 허용하도록 설정합니다.

### 3. 노트북에 API 키 입력

```python
client = genai.Client(
    vertexai=True,
    api_key="YOUR_API_KEY",  # 발급받은 API 키 입력
)
```

> **주의:** API 키를 코드에 직접 하드코딩하지 말고 환경 변수나 `.env` 파일을 사용하는 것을 권장합니다. `.env` 파일은 `.gitignore`에 포함되어 있어 git에 커밋되지 않습니다.

## 설치 및 실행

```bash
pip install google-genai opencv-python Pillow
```

| 패키지 | 역할 |
|--------|------|
| `google-genai` | Google Gemini API 클라이언트. Vertex AI를 통해 Gemini 모델에 텍스트/이미지를 전송하고 추론 결과를 받아옵니다. |
| `opencv-python` | 이미지 읽기, 색상 변환, bounding box 그리기 등 컴퓨터 비전 처리에 사용합니다. |
| `Pillow` | Python 이미지 처리 라이브러리(PIL). 이미지를 열고, 변환하고, 노트북에서 출력하는 데 사용합니다. |

`ocr_with_gemini.ipynb` 노트북을 Jupyter 또는 Google Colab에서 열어 셀을 순서대로 실행합니다.

## 노트북 구성

| 섹션 | 내용 |
|------|------|
| 1. Setup | 라이브러리 설치, Gemini 클라이언트 초기화 |
| 2. 공통 함수 | `inference`, `read_image`, `clean_results` |
| 3. Image Captioning | 이미지 캡션 생성 (영문 + 한국어 상품 설명) |
| 4. OCR | 바코드 감지/시각화, GTIN/UPC 기반 상품 정보 추출 |

## 프로젝트 구조

```
ocr_with_gemini/
├── ocr_with_gemini.ipynb   # 메인 핸즈온 노트북
├── README.md
└── .gitignore
```
