# GOD-ImageClassification
Google Open Data를 활용한 이미지 분류 모델

### 적용 가능 분야
- 분류: 이미지 라벨 예측
- 분류 라벨을 통해 트렌드 분석(실시간 라벨 빈도 분석 등), 사용자 프로파일링 등 관심사 파악
- 콘텐츠 분류

### turicreate을 이용한 이미지 분류
- 폴더를 sframe으로 로드 가능(추가적인 폴더 트리를 구성해줄 필요 없음)
- train, vaild, test 분할 함수 제공
- 파일명에서 텍스트를 추출해 데이터 라벨링 작업 가능
- 간단한 하이퍼 파라미터 튜닝(모델 아키텍처, iteration 등)
- simple prediction, top k predcition 가능 + probability, rank, margin 옵션 선택 가능

### 데이터 출처
- 출처: [Google Open Image Dataset V6](https://storage.googleapis.com/openimages/web/index.html)
- [awscli](https://aws.amazon.com/ko/cli/)를 이용한 다운로드 가능
```bash
aws s3 --no-sign-request sync s3://open-images-dataset/validation [target_dir/validation]
```

### 데이터 설명
- Image<br>
  이미지 데이터: train - 513GB, vaild - 12GB, test - 36GB
- ImageIDs<br>
  AuthorProfileURL, Author, Title, OriginalSize, OriginalMD5, Thumbnail300KURL, Rotation 등 정보 포함
- metadata<br>
  LabelName, DislayName 등 클래스명, 약 2만개의 클래스 보유
- Mlabel(머신), Hlabel(사람)<br>
  Source, LabelName, Confidence 등 라벨링 정보

### 데이터 처리 작업
- 데이터 로드: sframe reading
- 테이블 병합: concatenation
- 데이터 사전 구축: LabelName과 DisplayName 연결
- ImageID를 활용한 라벨링
- feature 추출
- 서브샘플링 등 카테고리 구성
- sframe 데이터셋 구축, 모델 러닝, 테스트 및 평가, 로그 기록
