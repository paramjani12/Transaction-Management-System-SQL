create table account(act_no varchar2(10), act_name varchar2(10), act_balance number(10), act_dob date);
create table account_branch(act_no varchar2(10), act_name varchar2(10), act_branch varchar2(10));
create table account_city(act_no varchar2(10), act_name varchar2(10), act_city varchar2(10));
insert into account values('19DCS001','Rajesh','35000','12-JUL-2001');
insert into account values('19DCS002','Shyam','30000','05-NOV-1993');
insert into account values('19DCS003','Bimal','55000','12-DEC-1997');
insert into account values('19DCS004','Neel','46000','31-JAN-2000');
insert into account values('19DCS005','Tushar','37900','27-FEB-2002');
insert into account values('19DCS006','Falguni','35060','01-JUL-1998');
insert into account values('19DCS007','Parimal','12070','17-SEP-2001');
insert into account values('19DCS008','Apu','17800','14-JUN-1994');
insert into account values('19DCS009','Sheetal','65070','22-AUG-1995');
insert into account values('19DCS010','Shiv','35600','07-MAY-1999');
insert into account_branch values('19DCS001','Rajesh','Manjalpur');
insert into account_branch values('19DCS002','Shyam','MG Road');
insert into account_branch values('19DCS003','Bimal','Mayapuri');
insert into account_branch values('19DCS004','Neel','Borivali');
insert into account_branch values('19DCS005','Tushar','Ghogha');
insert into account_branch values('19DCS006','Falguni','Powai');
insert into account_branch values('19DCS007','Parimal','Dum Dum');
insert into account_branch values('19DCS008','Apu','Hinjewadi');
insert into account_branch values('19DCS009','Sheetal','Maninagar');
insert into account_branch values('19DCS010','Shiv','Gachibowli');
insert into account_city values('19DCS001','Rajesh','Vadodara');
insert into account_city values('19DCS002','Shyam','Bangalore');
insert into account_city values('19DCS003','Bimal','Delhi');
insert into account_city values('19DCS004','Neel','Mumbai');
insert into account_city values('19DCS005','Tushar','Bhavnagar');
insert into account_city values('19DCS006','Falguni','Mumbai');
insert into account_city values('19DCS007','Parimal','Kolkata');
insert into account_city values('19DCS008','Apu','Pune');
insert into account_city values('19DCS009','Sheetal','Ahmedabad');
insert into account_city values('19DCS010','Shiv','Hyderabad');

select * from account;
select * from account_branch;
select * from account_city;


DECLARE 
xact_no account.act_no%type;
xact_balance account.act_balance%type;
opt number(1); 
deposit number(10);
withdrawal number(10);

BEGIN
xact_no:= :Enter_Account_Number;
opt:= :1Deposit_2Withdrawal_3Balance;  
select act_balance into xact_balance 
from account
where act_no=xact_no ; 
  
IF( opt = 1 ) THEN
deposit:= :Enter_Deposit_Amount;
update account
 set act_balance=act_balance+deposit
where act_no=xact_no ; 

xact_balance :=xact_balance +deposit;
dbms_output.put_line('Rs. '||deposit||' has been creadited in your account');
dbms_output.put_line('Your final balance is Rs. '||xact_balance );
                          
ELSIF( opt = 2 ) THEN 
withdrawal:= :Enter_Withdrawal_Amount;
    IF ( withdrawal<=xact_balance ) THEN
    update account
     set act_balance=act_balance-withdrawal
    where act_no=xact_no ;
    
    xact_balance:=xact_balance -withdrawal;
    dbms_output.put_line('Rs. '||withdrawal||' has been debited in your account');
    dbms_output.put_line('Your final balance is Rs.'||xact_balance );
    
    ELSE
    dbms_output.put_line('Your withdrawal amount is greater than balance');
    dbms_output.put_line('Your transaction failed');
    dbms_output.put_line('Your final balance is Rs.'||xact_balance ); 
    END IF;
ELSE
dbms_output.put_line('Your balance is Rs. '||xact_balance );
END IF;
    
  
END;
