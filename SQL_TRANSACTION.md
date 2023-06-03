/*
	TRANSACTION => ciclo de vida da info(dml)
	insert/update/delete
	commit/rollback/savepoint 
	DDL  / DML INSERT  / DQL = SELECT
*/

```
CREATE database BANCAO_TRANSACAO;
USE BANCAO_TRANSACAO;

CREATE TABLE PES_PESSOAS
(
	PES_CODIGO INT PRIMARY KEY AUTO_INCREMENT,
    PES_NOME VARCHAR(50) NOT NULL, 
    PES_CADASTRO DATETIME 
);

CREATE table ALU_ALUNOS(
	ALU_RA INT PRIMARY KEY AUTO_INCREMENT,
    ALU_CURSO VARCHAR(50) NOT NULL, 
    PES_CODIGO INT NOT NULL, 
    foreign key(PES_CODIGO) references PES_PESSOAS(PES_CODIGO)
);

insert into PES_PESSOAS VALUES(0, 'Matheus',now());
insert into pes_pessoas VALUES(0, 'Matheus',now());

select * from pes_pessoas;
```

/**
	COMMIT EM MYSQL É TRUE POR PADRÃO 
	TODA AÇÃO DML É GRAVADA AUTOMATICAMENTE, 
	OU SEJA, PARA DESFAZER UMA AÇÃO DML, 
	VOCÊ PRECISA DE OUTRA AÇÃO DML
*/

START transaction; -- commit is false (buffer)

insert into PES_PESSOAS VALUES(0, 'Davi',now());
savepoint aposdavi;

insert into PES_PESSOAS VALUES(0, 'Marcela',now());
savepoint aposmarcela;

insert into PES_PESSOAS VALUES(0, 'Isabel',now());

select * from pes_pessoas;
rollback to aposmarcela;
rollback to aposdavi;

rollback;-- rolback volta para o inicio da transaction 
commit;













