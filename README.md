# OCR with Gemini API, Cloud Vision AI, or Document AI

Gemini API:
<a href="https://colab.research.google.com/github/cjk0604/ocr-with-gemini/blob/main/ocr_with_gemini.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Gemini In Colab">
</a>
<a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2Fcjk0604%2Focr-with-gemini%2Fmain%2Focr_with_gemini.ipynb">
  <img src="https://img.shields.io/badge/Colab_Enterprise-Open-blue?logo=google-cloud" alt="Open In Colab Enterprise">
</a>
<a href="https://github.com/cjk0604/ocr-with-gemini/blob/main/ocr_with_gemini.ipynb">
  <img src="https://img.shields.io/badge/GitHub-View_Source-black?logo=github" alt="View on GitHub">
</a>
<br>
Cloud Vision AI: 
<a href="https://colab.research.google.com/github/cjk0604/ocr-with-gemini/blob/main/ocr_with_cloud_vision.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Cloud Vision In Colab">
</a>
<a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2Fcjk0604%2Focr-with-gemini%2Fmain%2Focr_with_cloud_vision.ipynb">
  <img src="https://img.shields.io/badge/Colab_Enterprise-Open-blue?logo=google-cloud" alt="Open In Colab Enterprise">
</a>
<a href="https://github.com/cjk0604/ocr-with-gemini/blob/main/ocr_with_cloud_vision.ipynb">
  <img src="https://img.shields.io/badge/GitHub-View_Source-black?logo=github" alt="View on GitHub">
</a>
<br>
Document AI: 
<a href="https://colab.research.google.com/github/cjk0604/ocr-with-gemini/blob/main/ocr_with_document_ai.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Document AI In Colab">
</a>
<a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2Fcjk0604%2Focr-with-gemini%2Fmain%2Focr_with_document_ai.ipynb">
  <img src="https://img.shields.io/badge/Colab_Enterprise-Open-blue?logo=google-cloud" alt="Open In Colab Enterprise">
</a>
<a href="https://github.com/cjk0604/ocr-with-gemini/blob/main/ocr_with_document_ai.ipynb">
  <img src="https://img.shields.io/badge/GitHub-View_Source-black?logo=github" alt="View on GitHub">
</a>

Gemini API, Cloud Vision AI, 또는 Document AI를 활용하여 상품 이미지에서 바코드(GTIN, UPC, EAN 등)를 인식하고, 상품명/상세 정보를 자동으로 추출하는 핸즈온 노트북 모음입니다.

## 노트북 목록

| 노트북 | 사용 API | 설명 |
|--------|----------|------|
| `ocr_with_gemini.ipynb` | Gemini (Vertex AI) | 생성형 AI 기반 OCR — 프롬프트로 바코드 해석 및 상품 정보 추론 |
| `ocr_with_cloud_vision.ipynb` | Cloud Vision API | 전통적 CV/ML 기반 OCR — TEXT/LABEL/LOGO/OBJECT Detection |
| `ocr_with_document_ai.ipynb` | Document AI | 문서 특화 OCR — 바코드 네이티브 감지 + Layout Parser Chunking |

## 주요 기능

- **Image Captioning / Label Detection** — 상품 이미지의 내용을 자연어로 설명하거나 라벨로 분류
- **OCR** — 바코드 영역 감지 및 bounding box 시각화
- **GTIN/UPC 추출** — 바코드 값을 기반으로 상품명, 브랜드, 카테고리 등 구조화된 정보 추출
- **Logo / Object Detection** — 브랜드 로고 및 객체 감지 (Cloud Vision)
- **바코드 네이티브 감지** — 바코드 형식/값 직접 반환, 정규식 불필요 (Document AI)
- **Layout Parser + Chunking** — 문서 구조 분석 및 의미 단위 분할, RAG 파이프라인에 활용 (Document AI)
- **Batch 처리** — 여러 이미지를 한 번의 API 호출로 일괄 분석 (Cloud Vision)

## 노트북 비교

| 항목 | Gemini OCR | Cloud Vision AI | **Document AI** |
|------|-----------|-----------------|-----------------|
| 방식 | 생성형 AI (LLM) | 전통적 CV + ML 파이프라인 | **문서 특화 AI 파이프라인** |
| OCR | 프롬프트 기반 자유 형식 | `TEXT_DETECTION` / `DOCUMENT_TEXT_DETECTION` | **OCR Processor** |
| 객체 감지 | 프롬프트로 bounding box 요청 | `OBJECT_LOCALIZATION`, `LABEL_DETECTION` | — |
| 로고/브랜드 | 프롬프트로 추론 | `LOGO_DETECTION` 전용 기능 | — |
| 바코드 값 | LLM이 직접 해석 | OCR 텍스트에서 정규식으로 파싱 | **`detected_barcodes` 네이티브 지원** |
| 문서 구조 | 프롬프트로 추론 | 미지원 | **Layout Parser + Chunking** |
| 입력 형식 | 이미지 | 이미지 | **이미지 + PDF + TIFF 등** |
| 비용 | 토큰 기반 과금 | 요청 건수 기반 과금 (월 1,000건 무료) | 페이지 수 기반 과금 |

## 사전 준비

### 1. Google Cloud 프로젝트 설정

1. [Google Cloud Console](https://console.cloud.google.com/)에서 프로젝트를 생성하거나 기존 프로젝트를 선택합니다.
2. 사용할 API를 활성화합니다:
   - **Gemini 노트북**: Vertex AI API 활성화
   - **Cloud Vision 노트북**: Cloud Vision API 활성화
   - **Document AI 노트북**: Document AI API 활성화
   - Cloud Console > API 및 서비스 > 라이브러리에서 검색 후 사용 설정

### 2. 인증 설정

#### Gemini 노트북 — API 키

1. Cloud Console > **API 및 서비스** > **사용자 인증 정보**로 이동합니다.
2. **+ 사용자 인증 정보 만들기** > **API 키**를 클릭합니다.
3. 생성된 API 키를 복사합니다.
4. (권장) 키 제한사항에서 **Vertex AI API**만 허용하도록 설정합니다.

```python
client = genai.Client(
    vertexai=True,
    api_key="YOUR_API_KEY",  # 발급받은 API 키 입력
)
```

#### Cloud Vision 노트북 — 서비스 계정 또는 ADC

**방법 A: 서비스 계정 키 파일**
1. Cloud Console > **IAM 및 관리자** > **서비스 계정**에서 키를 생성합니다.
2. 노트북에서 키 파일 경로를 지정합니다.

```python
credentials = service_account.Credentials.from_service_account_file("key.json")
client = vision.ImageAnnotatorClient(credentials=credentials)
```

**방법 B: ADC (Application Default Credentials)**
- Colab/Vertex AI Workbench 등에서는 별도 설정 없이 자동 인증됩니다.

```python
client = vision.ImageAnnotatorClient()
```

#### Document AI 노트북 — 프로세서 생성 + ADC

1. [Document AI Console](https://console.cloud.google.com/ai/document-ai)에서 **OCR** 및 **Layout Parser** 프로세서를 생성합니다.
2. 생성된 프로세서 ID를 노트북에 입력합니다.

```python
PROJECT_ID = "your-project-id"
LOCATION = "us"
OCR_PROCESSOR_ID = "your-ocr-processor-id"
LAYOUT_PROCESSOR_ID = "your-layout-parser-id"

opts = ClientOptions(api_endpoint=f"{LOCATION}-documentai.googleapis.com")
client = documentai.DocumentProcessorServiceClient(client_options=opts)
```

> **주의:** API 키나 서비스 계정 키를 코드에 직접 하드코딩하지 말고 환경 변수나 `.env` 파일을 사용하는 것을 권장합니다. `.env` 파일은 `.gitignore`에 포함되어 있어 git에 커밋되지 않습니다.

## 설치 및 실행

```bash
# Gemini 노트북
pip install google-genai opencv-python Pillow

# Cloud Vision 노트북
pip install google-cloud-vision opencv-python Pillow

# Document AI 노트북
pip install google-cloud-documentai opencv-python Pillow
```

| 패키지 | 역할 |
|--------|------|
| `google-genai` | Google Gemini API 클라이언트. Vertex AI를 통해 Gemini 모델에 텍스트/이미지를 전송하고 추론 결과를 받아옵니다. |
| `google-cloud-vision` | Google Cloud Vision API 클라이언트. 이미지에서 텍스트, 라벨, 로고, 객체 등을 감지합니다. |
| `google-cloud-documentai` | Google Cloud Document AI 클라이언트. OCR, 바코드 감지, Layout Parser, Chunking 등 문서 처리 기능을 제공합니다. |
| `opencv-python` | 이미지 읽기, 색상 변환, bounding box 그리기 등 컴퓨터 비전 처리에 사용합니다. |
| `Pillow` | Python 이미지 처리 라이브러리(PIL). 이미지를 열고, 변환하고, 노트북에서 출력하는 데 사용합니다. |

노트북을 Jupyter 또는 Google Colab에서 열어 셀을 순서대로 실행합니다.

## 노트북 구성

### `ocr_with_gemini.ipynb`

| 섹션 | 내용 |
|------|------|
| 1. Setup | 라이브러리 설치, Gemini 클라이언트 초기화 |
| 2. 공통 함수 | `inference`, `read_image`, `clean_results` |
| 3. Image Captioning | 이미지 캡션 생성 (영문 + 한국어 상품 설명) |
| 4. OCR | 바코드 감지/시각화, GTIN/UPC 기반 상품 정보 추출 |

### `ocr_with_cloud_vision.ipynb`

| 섹션 | 내용 |
|------|------|
| 1. Setup | 라이브러리 설치, Cloud Vision 클라이언트 초기화 |
| 2. 공통 함수 | `load_vision_image`, `draw_poly_boxes`, `extract_gtin_codes` |
| 3. Label / Logo / Object Detection | 라벨 분류, 로고 감지, 객체 위치 표시 |
| 4. OCR | TEXT_DETECTION으로 텍스트 추출, 정규식 GTIN 파싱, 종합 JSON 기록, 배치 처리 |

### `ocr_with_document_ai.ipynb`

| 섹션 | 내용 |
|------|------|
| 1. Setup | 라이브러리 설치, Document AI 클라이언트 및 프로세서 초기화 |
| 2. 공통 함수 | `process_document`, `get_text_from_layout`, `draw_doc_boxes` |
| 3. OCR Processor | 텍스트 추출, 줄 단위 시각화, 바코드 네이티브 감지 |
| 4. Layout Parser | 문서 구조 분석, Chunking으로 의미 단위 분할, PDF 처리 |
| 5. GTIN/UPC 추출 | 바코드 + OCR 텍스트 결합, 구조화된 JSON 상품 정보 기록 |

## 프로젝트 구조

```
ocr_with_gemini/
├── ocr_with_gemini.ipynb         # Gemini 기반 핸즈온 노트북
├── ocr_with_cloud_vision.ipynb   # Cloud Vision 기반 핸즈온 노트북
├── ocr_with_document_ai.ipynb    # Document AI 기반 핸즈온 노트북
├── README.md
└── .gitignore
```
