#in

CREATE TABLE player
( player_id number(10) NOT NULL,
  player_name varchar2(50) NOT NULL,
  discipline_id number(10) NOT NULL,
  CONSTRAINT player_pk PRIMARY KEY (player_id),
  constraint discipline_fk foreign key (discipline_id) references discipline(discipline_id)
);

create table discipline
( discipline_id number(10) NOT NULL,
  discipline_name varchar2(50),
  constraint discipline_pk primary key (discipline_id)
 );
