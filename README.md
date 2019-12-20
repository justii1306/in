#in
```
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
 
CREATE TABLE statistcs
( player_id number NOT NULL,
match_id number not null,
  serve_sum number(10) NOT NULL,
  serve_ace number(10) NOT NULL,
  serve_error number(10) NOT NULL,
  serve_ace_on_set number(10) NOT NULL,
  receive_sum number(10) NOT NULL,
  receive_error number(10) NOT NULL,
  receive_positive number(10) NOT NULL,
  receive_positive_percentage number(10) NOT NULL,
  receive_perfect number(10) NOT NULL,
  receive_perfect_percentagee number(10) NOT NULL,
  spike_sum number(10) NOT NULL,
  spike_error number(10) NOT NULL,
  spike_blocked number(10) not null,
  spike_perfect number(10) not null,
  spike_perfect_percentage number(10) not null,
  block_sum number(10) not null,
  block_on_set number(10) not null,
  constraint player_fk foreign key (player_id) references player(player_id),
  constraint match_fk foreign key (match_id) references match(match_id)
);


create table match(
match_id NUMBER GENERATED ALWAYS AS IDENTITY,
match_date date NOT NULL,
match_city varchar2(20) not null,
match_city_host varchar(1) not null,
set_lost number not null,
set_won number not null,
result varchar(1) not null,
constraint match_pk primary key (match_id)) 

create or replace trigger trg_bi_test
before insert on match
for each row
begin
if :new.set_lost > :new.set_won
then
:new.result := 'l';
else 
:new.result := 'w';
end if;
end;

create or replace trigger positive_receive
before insert on statistcs
for each row
begin
:new.receive_positive_percentage := ((:new.receive_positive + :new.receive_perfect) * 100 / :new.receive_sum);
end;

create or replace trigger perfect_receive
before insert on statistcs
for each row
begin
:new.receive_perfect_percentagee := ( :new.receive_perfect * 100 / :new.receive_sum);
end;


ALTER TABLE player
ADD (
    player_weight number(10) not null,
    player_height number(10) not null
);

INSERT INTO match
(match_date, match_city, match_city_host,set_lost,set_won )
VALUES
(to_date('03-02-2019', 'dd-mm-yyyy'),'Lodz','h',2,3)


ALTER TABLE player
ADD (
    player_weight number(10) not null,
    player_height number(10) not null
);

insert  into player values (123456, 'Fabian Drzyzga', 95, 196)
```

create or replace trigger positive_spike
before insert on statistcs
for each row
begin
:new.spike_perfect_percentage := (:new.spike_perfect * 100 / :new.spike_sum);
end;
