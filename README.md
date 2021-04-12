# AI_CCTV
- 얼굴인식이 가능한 cctv
- 딥러닝 학습을 통해 얼굴인식 모델 개발
- 해당 레포지토리는 라즈베리 파이의 코드, 모델 학습 코드, 파이어베이스와 라즈베리파이와의 연동 코드를 포함
- 3명의 얼굴을 분리하는데, 각 50장의 사진을 사용. 70%는 Training, 30%는 validation에 이용 
- 안드로이드 앱 : https://github.com/SuyeonKim1702/AI_CCTV
- 라즈베리 카메라에 녹화된 영상을 프레임 단위로 나누어 사진을 얻음 

### CNN 모델
<img src = "https://user-images.githubusercontent.com/46915174/114360215-be58ba00-9baf-11eb-9f28-d7fef6e32e22.png" width = 600>

- Convolutional Layer #1: 3x3크기의 필터, 16x16 크기의 layer
- Convolutional Layer #2: 3x3크기의 필터, 32x32 크기의 layer
- Convolutional Layer #3: 3x3크기의 필터, 64x64 크기의 layer
- Convolutional Layer #4: 5x5크기의 필터, 128x128 크기의 layer
- FC Layer #1: 512
- FC Layer #2: 256
- Drop Out Layer : Keep_prob값을 0.7로 주어 30%의 뉴런을 drop out
- 3명의 얼굴을 분리 시, 3200 스텝의 과정을 거쳐 90%이상의 정확도 산출
- 위 모델은, 학습된 얼굴이 '누구'인지를 판단해주지만, 카메라에 포착된 얼굴이 학습된 사람인지 여부를 알려줄 수는 없음
    - 영상 속, 얼굴이 검출된 프레임 개수중 85% 이상을 일관된 사람으로 인식하면, 모델에 등록된 사람으로 판단
- face_recognition.ipynb

### Image Augmentation 
- 3명의 얼굴을 분리할 때, 각 50장의 사진을 넣었는데도 overfitting 현상이 나타나 Training Accuracy는 95%를 육박했으나, Validation Accuracy는 30%에서 오르지 않았음
- Image Augmentation 기법을 이용해 데이터셋을 8배로 늘림
- SheerX, Affine, CropAndPad, DropOut, Sharpen, ElasticTransformation 
- image Augmentation의 예시 
<img src = "https://user-images.githubusercontent.com/46915174/114366191-2a3e2100-9bb6-11eb-97b8-fb561d47a21b.png" width = 500>
- imageAugmentation.py


### 전체 프로젝트의 구조
<img src = "https://user-images.githubusercontent.com/46915174/114355657-afbbd400-9baa-11eb-8126-aeca1386cee0.png" width = 600>

