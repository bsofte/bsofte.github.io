---
layout: single
title: "mysql 테이블의 json 컬럼에 json 값 생성, 수정, 삭제하는 방법"
---
# 공통사항
* json_str: JSON 값을 {}로 정리한 텍스트 형식의 값을 뜻한다. 해보면 알겠지만 mysql 테이블의 json 컬럼에서 json 값 처리할 때 json_str는 쓰면 안 된다.
  * 예시
  ```json
  {'2022-1-1': {'wds': 10, 'dmd': 1.0}}
  ```
* json_obj: json 값을 JSON_OBJECT(key1, val1, key2, val2, ...) 형식으로 정의한 객체를 뜻한다. mysql에서 json값 처리할 때는 이 형식으로 써야 한다.
  * 예시
  ```json
  JSON_OBJECT('2022-1-1', JSON_OBJECT('wds', 10, 'dmd', 1.0))
  JSON_OBJECT('2022-1-1', JSON_ARRAY(JSON_OBJECT('wds', 10, 'dmd', 1.0)))
  ```

# 리셋
### 함수: JSON_OBJECT()
### 쿼리
```mysql
UPDATE tbl_name SET col_name = JSON_OBJECT();
```

# 최초 입력
### 시도 1
- 함수: JSON_OBJECT(json_str)
- 결과: X. json_value를 그냥 문자열로 인식한다.
### 시도 2
- 함수: JSON_OBJECT(json_str)
- 결과: X. 최초 입력한 키/값 페어의 첫번째 값을 배열로 인식하지 못한다.
### 시도 3
- 함수: JSON_MERGE_PATCH(col_name, JSON_OBJECT(key1, val1, key2, val2, ...))
- 결과: X. 상동.
### 시도 4
- 함수: JSON_MERGE_PRESERVE(...)
- 결과: X. 상동.
### 시도 5
- 함수: JSON_OBJECTMERGE_PRESERVE(...)
- 결과: X. 상동.

# 키/값 추가

# 특정 키에 값 추가 (기존 값 있는 상태)

#

