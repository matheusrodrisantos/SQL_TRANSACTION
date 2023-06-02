# criando procedures 
delimiter | 
create procedure prc_cadastrar_aluno(
IN vnome  varchar(50),
in vcurso varchar(50)
) 
begin 
	declare codigopessoa int;
    declare erro tinyint default 0;
    
    declare continue handler for 
    sqlexception set erro =1;
    
    start transaction;
    insert into pes_pessoas values(0,vnome, now());
	select last_insert_id() into codigopessoa;
    
    if(erro=0)then 
		insert into alu_alunos values
        (0, vcurso,codigopessoa);
        if(erro=0)then
			select 0 as msg;
			commit;
        else
			select 2 as msg;
			rollback;
		end if;
	else 	
		select 1 as msg;
		rollback;
    end if;
end;
|
