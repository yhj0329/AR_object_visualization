# AR_object_visualization
OpenCV를 이용해서 카메라의 영상을 Calibration하고 AR Object를 시각화하는 프로그램이다.

## ar_object_visualization.py
chessboard에 AR object를 시각화하는 기능이다.

#### 설명
Calibration 해서 얻은 값을 아래 코드처럼 K와 dis_coeff에 집어넣는다.
```python
# The given video and calibration data
video_file = './chessboard.mov'
K = np.array([[1427.03710, 0, 523.923472],
              [0, 1434.21618, 920.961584],
              [0, 0, 1]]) # Derived from `calibrate_camera.py`
dist_coeff = np.array([ 0.01215035, -0.0346861, -0.01021252, -0.0050372, 0.03557859])
```
아래 코드의 좌표를 수정하면 AR object를 바꿀 수 있다.
```python
# Prepare a 3D box for simple AR
box_lower = board_cellsize * np.array([[5, 0, 0], [6, 2, 0], [8, 3, 0], [6, 4, 0], [5, 6, 0], [4, 4, 0], [2, 3, 0], [4, 2, 0]])
box_upper = board_cellsize * np.array([[5, 0, -1], [6, 2, -1], [8, 3, -1], [6, 4, -1], [5, 6, -1], [4, 4, -1], [2, 3, -1], [4, 2, -1]])
```

#### 주의사항
- 영상에서 체스판의 좌표 (10, 7)이 전부 보여야 한다.

#### 조작키
- SPACE BAR : 정지
- ESC : 종료

#### 결과


## camera_calibration.py
카메라의 영상을 Calibration 하는 기능이다.

#### 기능
카메라는 우리가 실제로 보는 3차원 세상을 2차원 이미지로 변환한다.  
이때 3차원의 점들이 이미지 상에서 어디에 맺히는지 기하학적으로 생각하면,  
실제 이미지는 사용된 렌즈, 렌즈와 이미지 센서와의 거리, 렌즈와 이미지 센서가 이루는 각 등  
카메라 내부의 기구적인 부분에 의해서 크게 영향을 받는 것을 알 수 있다.  
그러므로, 3차원 점들이 영상에 투영된 위치를 구하거나, 역으로 영상 좌표로부터 3차원 공간좌표를 복원할 때에는  
내부 요인을 제거해야하만 정확한 계산이 가능하다.  
이러한 내부의 매개변수(Parameter) 값을 구하는 과정을 Camera Calibration이라고 합니다.

#### 조작키
- SPACE BAR : 정지하고 꼭짓점을 보여준다
- ENTER after pause : calibration 할 이미지 선택
- ESC : 종료

#### 결과


