# hanul-project

<b> 가상의 기업 <우산써조>의 홈페이지를 제작하였습니다. </b><br><br>
Java 언어를 기반으로 Spring Framework를 이용하여 제작된 웹사이트입니다.<br>
Spring MVC 패턴으로 JSP를 제작하여 Web Page의 기능 등을 구현하였습니다.<br>
데이터베이스는 Oracle XE를 이용하여 구현하였고, MyBatis를 이용해 연동하였습니다.<br><br>
<b> 자세한 사항은 강수진_web.pptx파일을 내려받아 참고하시기 바랍니다. </b>

<hr>

### 개발환경
```
Windows 10 / 64bit
Spring Tool Suite4 Version: 4.7.1
Oracle Database 11g Express Edition
JAVA Version 8u251 ver
Apache Tomcat v8.5
GitHub & GitHub Desktop
```

### DataBase Table
```
가입회원 테이블

create table bUser (
	user_email	 varchar2(30)	 primary key,
	user_pw		 varchar2(30)	 not null,
	user_nickname	 varchar2(30)	 not null,
	user_phone	 varchar2(15),
	user_zipcode	 number,
	user_address	 varchar2(1024),
	detail_address	 varchar2(1024),
	user_birth	 date,
	user_key	 varchar2(30),
	user_image	 varchar2(300),
	user_imagepath	 varchar2(300)
);

-- 컬럼 추가됨 (user_image)
alter table bUser add user_image varchar2(300) default 'default_profile.png';
alter table bUser add user_imagepath varchar2(200) default '';

게시판

create table bBoard (
	board_num	number	primary key,
	board_category	number	not null,
	board_email	varchar2(30),
	board_nickname	varchar2(30),
	board_date	date,
	board_title	varchar2(1024),
	board_content	varchar2(2048) 		default '글 내용이 없습니다.',
	board_file	varchar2(1024),
	board_recommend	varchar2(30),
	constraint email
	foreign key (board_email)
	references bUser (user_email)
);

-- 카테고리 => 공지사항:0 / 사용후기:1

-- 글 번호 시퀀스 생성
create sequence board_seq increment by 1;

-- 파일컬럼 변경 및 조회수 컬럼추가
alter table bBoard add	board_readcnt number default 0;
alter table bBoard add	board_filename varchar2(1024);
alter table bBoard add	board_filepath varchar2(1024);

주문

create table bOrder (
	order_num	number	primary key,
	order_email	varchar2(30)	not null,
	order_nickname	varchar2(30),
	order_phone	varchar2(50)	not null,
	order_date	date	not null,
	order_option	varchar2(50),
	order_color	varchar2(30),
	order_count	number,
 	order_amount	number,
 	order_pay	varchar2(30),
 	deliv_name	varchar2(30)	not null,
 	deliv_phone	varchar2(50)	not null,
	deliv_zipcode	number	not null,
	deliv_address	varchar2(1024)	not null,
	deliv_detailaddress	varchar2(1024)	not null,
 	deliv_memo	varchar2(1024)	

);

문의

create table bQna (
	qna_num			number			primary key,
	qna_email		varchar2(30) 	not null,
	qna_nickname		varchar2(30),
	qna_category		varchar2(30),
	qna_content		varchar2(1024) 	not null,
);

판매제품 테이블

create table tmerchandise (
	M_NUM		VARCHAR2(50)		constraint m_num_pk primary key,
	M_NAME		VARCHAR2(50),
	M_PRICE		NUMBER				not null,
	M_DATE		DATE
);
```
