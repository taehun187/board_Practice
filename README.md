### README.md

```markdown
# 게시판 프로젝트

이 프로젝트는 Java와 Spring Boot를 사용하여 간단한 **게시판 기능**을 구현한 연습 프로젝트입니다. 주요 기능으로는 **게시글 작성**, **삭제**, **수정**, **파일 업로드**, **검색** 기능이 포함되어 있습니다.

---

## 🛠️ 사용된 기술 스택

- **Java 17**
- **Spring Boot**
- **Spring Data JPA**
- **Thymeleaf**: 서버 사이드 템플릿 엔진
- **Lombok**: 코드 간소화를 위한 라이브러리
- **HTML & CSS**: 프론트엔드 디자인
- **Bootstrap** (옵션, 필요시 UI 개선)

---

## 📂 프로젝트 구조

```
src
├── main
│   ├── java
│   │   └── com.taehun.board
│   │       ├── controller        # 컨트롤러 계층
│   │       │   └── BoardController.java
│   │       ├── entity            # JPA 엔티티
│   │       │   └── Board.java
│   │       ├── repository        # 데이터베이스 레이어
│   │       │   └── BoardRepository.java
│   │       └── service           # 비즈니스 로직 계층
│   │           └── BoardService.java
│   ├── resources
│   │   ├── static                # 정적 파일 (업로드된 파일 저장)
│   │   └── templates             # Thymeleaf 템플릿 파일
│   │       ├── boardlist.html
│   │       ├── boardview.html
│   │       ├── boardwrite.html
│   │       ├── boardmodify.html
│   │       └── message.html
│   └── application.yml           # 애플리케이션 설정 파일
```

---

## 🌟 구현 기능

### 1. **게시글 작성**
- 사용자는 제목, 내용을 입력하고 파일을 업로드할 수 있습니다.
- 업로드된 파일은 서버의 `/src/main/resources/static/files` 경로에 저장됩니다.
- 업로드된 파일 이름은 UUID를 사용하여 중복을 방지합니다.

### 2. **게시글 목록 조회**
- 게시글 목록은 **페이징 처리**가 적용되어 있으며, 최신 게시글이 상단에 표시됩니다.
- 페이지 번호는 하단에 표시됩니다.

### 3. **게시글 상세 조회**
- 게시글 제목, 내용, 업로드된 파일(다운로드 링크 포함)을 확인할 수 있습니다.

### 4. **게시글 수정**
- 기존 게시글의 제목과 내용을 수정할 수 있습니다.
- 새로운 파일을 업로드하면 기존 파일을 대체합니다.

### 5. **게시글 삭제**
- 선택한 게시글을 삭제할 수 있습니다.

### 6. **게시글 검색**
- 제목을 기준으로 게시글을 검색할 수 있습니다.
- 검색 키워드는 페이징과 함께 동작합니다.

---

## 📋 주요 코드 설명

### 1. BoardController
- 사용자 요청을 처리하는 컨트롤러 계층입니다.
- 주요 매핑:
  - `GET /board/write`: 게시글 작성 폼.
  - `POST /board/writepro`: 게시글 저장.
  - `GET /board/list`: 게시글 목록 조회.
  - `GET /board/view`: 특정 게시글 조회.
  - `GET /board/modify/{id}`: 게시글 수정 폼.
  - `POST /board/update/{id}`: 게시글 수정 처리.
  - `GET /board/delete`: 게시글 삭제.

### 2. BoardService
- 비즈니스 로직을 처리하는 계층입니다.
- 주요 기능:
  - 게시글 저장(`write`): 파일 업로드 포함.
  - 게시글 목록 조회(`boardList`).
  - 특정 게시글 조회(`boardView`).
  - 게시글 삭제(`boardDelete`).
  - 제목 기반 검색(`boardSearchList`).

### 3. BoardRepository
- 데이터베이스와 통신하는 레이어입니다.
- JPA를 사용하여 `Board` 엔티티를 관리합니다.
- 제목 검색을 위한 메서드:
  ```java
  Page<Board> findByTitleContaining(String searchKeyword, Pageable pageable);
  ```

### 4. Board 엔티티
- 게시글 정보를 저장하는 데이터베이스 테이블과 매핑됩니다.
- 주요 필드:
  - `id`: 게시글 ID (자동 증가).
  - `title`: 게시글 제목.
  - `content`: 게시글 내용.
  - `filename`: 업로드된 파일 이름.
  - `filepath`: 업로드된 파일의 저장 경로.

---

## 🖥️ 실행 방법

1. **프로젝트 클론**
   ```bash
   git clone <레포지토리 URL>
   cd 프로젝트_폴더명
   ```

2. **필요한 라이브러리 설치**
   - `Lombok`이 IDE에서 제대로 작동하도록 설정합니다.
   - Spring Boot와 H2 Database가 자동으로 설정됩니다.

3. **프로젝트 실행**
   ```bash
   ./mvnw spring-boot:run
   ```

4. **애플리케이션 접근**
   - 브라우저에서 `http://localhost:8090/board/list`로 접속하여 게시판 기능을 확인합니다.

---

## 📷 주요 화면

### 게시글 목록
- 페이징과 검색 기능 포함.

### 게시글 작성
- 제목, 내용, 파일 업로드 가능.

### 게시글 상세 조회
- 제목, 내용, 파일 다운로드 가능.





