user defined function
without parameter
create function fn_mail()
returns nvarchar(50)
as
begin
return 'Hello'
end
with parameter
create function fn_mail(@name nvarchar(50))
returns nvarchar(50)
as
begin
return 'Hello' + @name
end
--------------------------------------------------------------------------------
Cursor
declare @employeeid int;
declare @employeename varchar(50);
declare @cityid int;
declare @cityname varchar(50);
Declare cur_city Cursor for select employeeid, employeename, cityid from employee
open cur_city;
fetch next from cur_city into @employeeid, @employeename, @cityid;
while @@FETCH_STATUS=0
 begin
   select @cityname = cityname from city where cityid = @cityid
   print @employeename +' from '+ @cityname
   fetch next from cur_city into @employeeid, @employeename, @cityid;
 end
close cur_city;
deallocate cur_city;
--------------------------------------------------------------------------------
Triggers
disable trigger  employee_trigger on employee
create trigger employee_trigger on employee after insert
as
begin
 insert into employee_log select employeeid,'Inserted',getdate() from Inserted
end
--------------------------------------------------------------------------------
string functions
declare @string varchar(250)
set @string = 'Welcome to string'
select @string
--------------------------------------------------------------------------------
declare @string varchar(250)
set @string = 'Welcome to string'
select Replace(@string, 'string','hana')
--------------------------------------------------------------------------------
declare @string1 varchar(250) , @string2 varchar(250)
set @string1 = 'Welcome'
set @string2 = ' to string'
select @string1+' '+@string2
select concat(@string1, @string2)
--
declare @string1 varchar(250) , @string2 varchar(250)
set @string1 = 'Welcome to sql sql'
select substring(@string1, 12, 3)
--------------------------------------------------------------------------------
declare @string1 varchar(250) , @string2 varchar(250)
set @string1 = '       Welcome to sql sql'
select @string1, LTRIM(@string1)
--------------------------------------------------------------------------------
declare @string1 varchar(250)
set @string1 = '20102020'
select stuff(stuff(@string1, 3,0,'-'),6,0,'-')
