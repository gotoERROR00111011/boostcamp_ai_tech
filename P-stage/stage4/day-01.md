# Stage 4 - Day 01

## Opinion

수식인식기 프로젝트 EDA, 주로 image 의 특징 중심으로 dataset 분석을 한다.  
text image의 특성을 잘 활용하면 간단한 preprocessing으로 좋은 결과를 얻을 것이라 생각한다.

## Reason

text는 상하좌우 뒷면 처럼 다른 측면을 고려하지 않아도 된다. (일부 기울기는 존재한다)  
또한 대체로 색의 영향이 적어서 grayscale으로 충분하다.  
위와 같은 특징을 활용하면 특화된 preprocessing, augmentation이 가능하다.

## Example

dataset은 대체로 검은색 문자, 흰색 배경 으로 구성되어 있었다.  
일부 rgb문자, 형광펜 표시 등의 경우도 있었으나 grayscale로 변환할 경우 명암 정도의 차이였다.

## Opinion / Offer

dataset은 예상대로 단순한 구성(어두운 문자, 밝은 배경)임을 확인했다.  
계획대로 첫번째 주는 data 처리에 집중하도록 한다.
