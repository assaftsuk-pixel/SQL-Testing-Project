# SQL-Testing-Project- Finding an active client who's name doesnt show at the 'account_warning' table and he is from the club 'solider'
select c.client_id, c.name_heb, car.branch_number, car.account_number
from clients as c
join client_account_relation as car on c.client_serial_number = car.client_serial_number
where c.client_active= 1
and exists
(select 1
from clubs as clu
where clu.client_serial_number = c.client_serial_number
and clu.club_name = 'solider')
 and not exists
(select 1
from account_warnings as accw
where accw.account_number = car.account_number)
