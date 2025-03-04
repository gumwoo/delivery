/*
 * README
 * 
 * 본 프로젝트는 Java(안드로이드) 기반으로 개발되었으며, 배달 음식을 공동으로 주문하는 과정을
 * 지도와 마커, 실시간 채팅 등을 통해 손쉽게 관리할 수 있도록 설계되었습니다.
 * 
 * 아래 내용을 참고하시어 앱의 기능과 기술 스택을 이해하시기 바랍니다.
 */

/**
 * 프로젝트 명: 배달조각 (가칭)
 *
 * 1. 개요
 *    - 공동 배달 주문을 원하는 사용자들이 지도 상에서 위치를 지정하고,
 *      해당 위치(마커)에 대한 정보(식당 이름, 음식 종류, 모집 인원 등)를 공유합니다.
 *    - 실시간 채팅 기능을 통해 참여자들이 주문 세부 사항을 협의할 수 있습니다.
 *    - 멤버십 등급(무료, 실버, 프리미엄)에 따라 생성할 수 있는 마커 수가 달라지며,
 *      광고 시청을 통해 추가 마커 생성 기회도 얻을 수 있습니다.
 *
 * 2. 주요 기능
 *    A. 지도 및 위치 마커 생성/관리
 *       - 구글 지도(Google Maps) API를 사용하여 지도를 띄우고, 확대/축소 및 내 위치 추적이 가능합니다.
 *       - 마커 생성 시 입력 정보:
 *         * 채팅방 이름, 식당 이름, 음식 종류, 파티(모집) 설명, 모집 인원, 비밀번호 등
 *         * 생성된 마커의 위치 확인 후 사용자가 원하는 위치에 마커를 배치합니다.
 *       - 모집 시간 전 미리 마커를 생성해놓고, 해당 시간에 함께 주문할 사람을 모집할 수 있습니다.
 *       - 내가 만든 마커는 설정해 둔 비밀번호를 통해서만 삭제할 수 있어, 타인의 임의 삭제를 방지합니다.
 *
 *    B. 실시간 채팅(Firebase)
 *       - 파이어베이스(Firebase)를 통해 실시간 채팅 기능을 구현하였습니다.
 *       - 마커별로 독립된 채팅방이 생성되며, 상단에 해당 마커(채팅방)의 제목이 표시됩니다.
 *       - 채팅방 입장 시 닉네임을 설정할 수 있고, 현재 참여 인원 / 모집 인원이 상단에 표시됩니다.
 *       - 모집 인원이 다 차면 더 이상 참여할 수 없습니다.
 *       - 메시지에 전송 시각이 함께 표시되며, 송/수신자에 따라 말풍선 색상과 위치(좌우)가 구분됩니다.
 *
 *    C. 멤버십 등급 및 광고 시청 보상
 *       - 무료(Free): 마커 1개 생성 가능
 *       - 실버(Silver): 마커 5개 생성 가능
 *       - 프리미엄(Premium): 마커 무제한 생성 + 스페셜 홍보용 마커 생성 가능
 *       - 광고 시청 시, 추가 마커를 1회 더 생성할 수 있는 권한을 획득합니다.
 *         (사이드바 하단의 ‘광고보기’ 클릭 시 광고 재생)
 *
 *    D. 목록(LIST) 기능
 *       - 마커 정보를 리스트 형태로 표시하고, 필터링 옵션(내 위치와 마커 거리, 음식 메뉴, 모집 인원 등)을 제공합니다.
 *       - 상단에는 현재 사용자 위치가 표시되고, 각 마커까지의 거리도 함께 표시됩니다.
 *       - 리스트 화면에서도 플로팅 액션 버튼을 통해 지도 확인 및 마커 생성이 가능합니다.
 *
 *    E. 추천(RECOMMEND) 기능
 *       - 간단한 선호도 검사를 통해 오늘 먹을 메뉴를 추천해주는 웹 페이지를 제작하였습니다.
 *       - 사용자가 메뉴 선택에 어려움을 겪을 때 도움을 주는 간단한 설문/검사 형식입니다.
 *
 *    F. 사용자 피드백 수집(SURVEY)
 *       - 앱 내 ‘조사(SURVEY)’ 섹션에서 사용자들의 배달 음식 소비 패턴, 배달비 영향 등을 조사합니다.
 *       - 수집된 피드백은 서비스 개선 및 이벤트 기획 등에 활용할 수 있습니다.
 *
 *    G. 배달조각 웹 사이트
 *       - 앱 사이드바의 HOME 버튼을 통해 ‘배달조각’ 웹 사이트로 이동합니다.
 *       - 웹 페이지에서 프로젝트의 특징, 장점 등을 소개하고 홍보 자료로 사용할 수 있습니다.
 *
 *    H. 카카오 로그인 API
 *       - 카카오 계정으로 간편 로그인을 지원하며, 카카오 프로필 사진과 닉네임을 가져올 수 있습니다.
 *       - 로그아웃 기능도 제공합니다.
 *
 * 3. 기술 스택
 *    - 언어: Java (안드로이드 앱)
 *    - 서버/호스팅: Google Cloud Platform (GCP)
 *    - 데이터베이스: MySQL
 *      * 안드로이드 앱에서 직접 DB에 접근하기 어려우므로, Node.js 서버를 통해 통신
 *    - 서버 사이드 프로그래밍: Node.js
 *      * 안드로이드 <-> Node.js <-> MySQL 간 데이터 송수신
 *    - 지도: Google Maps API
 *    - 실시간 채팅: Firebase (Realtime Database)
 *    - 로그인: 카카오 로그인 API
 *
 * 4. 설치 및 실행 가이드 (개략)
 *    A. 사전 준비
 *       - 안드로이드 스튜디오(최신 버전) 설치
 *       - Google Cloud, Firebase, Kakao 개발자 콘솔에서 앱 키/토큰 발급
 *    B. 환경 변수 및 설정
 *       - google_maps_api.xml 파일에 Google Maps API 키 설정
 *       - Firebase 프로젝트 생성 후 google-services.json 파일 등록
 *       - 카카오 개발자 콘솔에서 패키지명, 해시키 등록 후 네이티브 앱 키 확인
 *       - Node.js 서버와의 통신을 위해 서버 URL, 포트 설정
 *    C. 실행
 *       - 안드로이드 스튜디오에서 프로젝트를 열고, 빌드(Gradle Sync)
 *       - 에뮬레이터 또는 실기기(USB 연결)에서 앱 실행
 *       - 서버(Node.js) 및 DB(MySQL) 구동 상태 확인
 *
 * 6. 기여 방법
 *    - GitHub 저장소를 통해 프로젝트를 공유하고 이슈/PR(Pull Request)을 통해 협업합니다.
 *    - 버그 제보, 기능 제안 등은 GitHub Issues 탭 활용
 *    - 로컬에서 작업 후, 커밋 & 푸시 → Pull Request
 *
 * 7. 라이선스
 *    - 본 프로젝트는 개인/학습용 시연을 목적으로 하며, 상업적 이용 시 라이선스 확인이 필요할 수 있습니다.
 *    - 사용된 외부 라이브러리(구글 지도, 파이어베이스, 카카오 API 등)는 각각의 라이선스 조항을 따릅니다.
 */
