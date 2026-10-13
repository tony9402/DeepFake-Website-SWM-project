# DeepFake-Website-SWM-project 분석

## 목적과 현재 범위

소프트웨어 마에스트로 11기 딥페이크 프로젝트의 웹 관련 코드입니다.

아래 파일과 모듈에서 구현을 확인할 수 있습니다. 코드·실험 자료의 구성을 분석한 결과이며 현재 운영 여부나 실행 성공을 나타내는 설명은 아닙니다.

## 주요 구성과 역할

| 경로 | 역할 또는 확인한 내용 |
| --- | --- |
| [requirements.txt](requirements.txt) | Python 의존성 목록 |
| [Dockerfile](Dockerfile) | 컨테이너 빌드 설정 |
| [LICENSE](LICENSE) | 라이선스 |
| [api/](api/) | Python 4개 |
| [app/](app/) | HTML 9개, Python 4개 |
| [images/](images/) | 이미지 자료 |
| [migrations/](migrations/) | Python 2개 |
| [config.py](config.py) | 설정 코드 |
| [server.py](server.py) | Python 1개 |

파일 구성에서 확인되는 형식은 Python 12개, HTML 9개입니다. 헤더와 예제·보조 코드를 포함한 파일 수이며 기능 개수나 구현 완성도를 뜻하지 않습니다.

## 소스에서 확인한 인터페이스

| 파일 | 정적으로 확인한 정의 |
| --- | --- |
| [api/TrustNetAPI.py](api/TrustNetAPI.py) | `connectServer`, `Triton` |
| [api/classifiers.py](api/classifiers.py) | `setup_srm_weights`, `setup_srm_layer`, `DeepFakeClassifierSRM`, `GlobalWeightedAvgPool2d`, `DeepFakeClassifier`, `DeepFakeClassifierGWAP` |
| [api/deepfake_utils.py](api/deepfake_utils.py) | `VideoReader`, `FastFaceExtractor`, `FaceExtractor`, `confident_strategy`, `put_to_center`, `isotropically_resize_image` |
| [api/grad_cam.py](api/grad_cam.py) | `FeatureExtractor`, `ModelOutputs`, `preprocess_image`, `show_cam_on_image`, `GradCam`, `GuidedBackpropReLU` |
| [app/forms.py](app/forms.py) | `RegistrationForm`, `LoginForm`, `UpdateAccountForm`, `VideoUploadForm`, `UpdateVideoForm`, `CommentForm` |
| [app/models.py](app/models.py) | `User`, `load_user`, `Video`, `Likes`, `Comments` |

이 목록은 파일의 함수·클래스 이름과 라우트 정의를 정적으로 읽은 결과입니다. 모든 정의가 공개 API라는 뜻은 아니며 실제 호출 관계와 입력 형식은 각 구현을 함께 확인해야 합니다.

## 설치와 사용을 확인하는 방법

[requirements.txt](requirements.txt)에서 프로젝트 설정을 확인합니다. 의존성에는 `Flask`, `Flask-Login`, `Flask-Migrate`, `Flask-SQLAlchemy`, `Flask-WTF`, `Jinja2`, `Mako`, `MarkupSafe` 등이 있습니다.

Python 소스에서 환경 변수 조회에 사용되는 이름으로 `DATABASE_URL`, `SECRET_KEY`를 확인했습니다. 값은 자신의 실행 환경에서 설정해야 하며 이 문서에는 접속 정보나 인증 값을 싣지 않습니다.

## 근거와 분석 범위

분석일: 2026-10-13 (Asia/Seoul). 문서 변경 전 소스 기준 커밋: `7693a8a5a84dc50c29c76c7cada7ef7eec1e5650`.

근거는 해당 기본 브랜치의 파일 목록, [README.md](README.md) 및 위에 연결한 소스·설정입니다. Python 파일과 표에 명시한 Notebook은 코드를 실행하지 않고 정적으로 살펴봤습니다. 그 외 파일은 구성과 원래 문서를 기준으로 설명했습니다. 의존성 설치, 학습, 서버·하드웨어 실행과 외부 서비스 연결은 검증하지 않았으므로 운영 상태나 성능의 증거로 사용할 수는 없습니다.
