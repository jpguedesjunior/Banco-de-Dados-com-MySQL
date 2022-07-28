# Banco-de-Dados-com-MySQL
/*Este Projeto tem o intuito de desenvolver um script de Banco de Dados. /db_faculdade/*

CREATE DATABASE db_faculdade
DEFAULT CHARACTER SET utf8mb4
DEFAULT COLLATE utf8mb4_0900_ai_ci;

USE db_faculdade;

CREATE TABLE departamento (
    departamento INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_departamento CHAR (20) NOT NULL
);

CREATE TABLE professor (
    cod_professor INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_professor CHAR (20) NOT NULL,
    sobrenome_professor CHAR (50) NOT NULL,
    status BOOLEAN,
    fk_cod_departamento INTEGER (4),
FOREIGN KEY (fk_cond_departamento) REFERENCES departamento
    (cod_departamento)
);

CREATE TABLE curso (
    cod_curso INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_curso CHAR (20),
    fk_cod_departamento INTEGER (4),
FOREIGN KEY (fk_cod_departamento) REFERENCES  departamento
(cod_departamento)
);

CREATE TABLE turma (
    cod_turma INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    periodo CHAR (8),
    num_aluno INTEGER (4),
    dt_inicio DATE,
    dt_fim DATE,
    fk_cod_curso INTEGER (4),
FOREIGN KEY (fk_cod_curso) REFERENCES curso (cod_curso)
); 

CREATE TABLE disciplina (
    cod_disciplina INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_disciplina CHAR (20),
    carga_horaria INTEGER (4) NOT NULL,
    descricao CHAR (50),
    num_alunos INTEGER (4) NOT NULL,
    fk_cod_departamento INTEGER (4) NOT NULL,
FOREIGN KEY (fk_cod_departamento) REFERENCES departamento
(cod_departamento)
);

CREATE TABLE tipo_telefone (
    cod_tipo_telefone INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    tipo_telefone CHAR (8)
);

CREATE TABLE telefone (
    cod_telefone INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    num_telefone CHAR (20),
    fk_cod_tipo INTEGER (4),
FOREIGN KEY (fk_cod_tipo) REFERENCES tipo_telefone (cod)
);

CREATE TABLE tipo_logradouro (
    cod_logradouro INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    tipo_logradouro CHAR (11)
);

CREATE TABLE endereco (
    cod_endereco INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_rua CHAR (50) NOT NULL,
    numero_rua INTEGER (4) NOT NULL,
    complemento CHAR (20) NULL,
    CEP CHAR (8) NOT NULL,
    fk_cod_tipo_logradouro INTEGER (4) REFERENCES tipo_logradouro
    (cod_tipo_logradouro)
);

CREATE TABLE aluno (
    RA INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    nome_aluno CHAR (20),
    sobrenome_aluno CHAR (20),
    CPF CHAR (11),
    status BOOLEAN,
    sexo CHAR (1),
    nome_pai CHAR (50),
    nome_mae CHAR (50),
    email CHAR (50),
    whatsapp CHAR (20),
    fk_cod_curso INTEGER (4),
FOREIGN KEY (fk_cod_endereco) REFERENCES endereco (cod_endereco),
FOREIGN KEY (fk_cod_curso) REFERENCES curso (cod_curso),
FOREIGN KEY (fk_cod_turma) REFERENCES turma (cod_turma)
);

CREATE TABLE telefone_aluno (
    cod_tel_aluno INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    fk_RA_ INTEGER (4) NOT NULL,
    fk_cod_telefone INTEGER (4) NOT NULL,
FOREIGN KEY (fk_cod_telefone) REFERENCES telefone (cod_telefone),
FOREIGN KEY (fk_RA) REFERENCES aluno (RA)
);

CREATE TABLE historico (
    cod_historico INTEGER (4) PRIMARY KEY AUTO_INCREMENT,
    dt_inicio DATE,
    dt_fim DATE,
    fk_RA INTEGER (4) NOT NULL,
FOREIGN KEY (fk_RA) REFERENCES aluno (RA)
);

CREATE TABLE professor_disciplina (
    fk_cod_professor INTEGER (4) NOT NULL,
    fk_cod_disciplina INTEGER (4) NOT NULL,
    PRIMARY KEY (fk_cod_professor, fk_cod_disciplina),
FOREIGN KEY (fk_cod_professor) REFERENCES professor (cod_professor),
FOREIGN KEY (fk_cod_disciplina) REFERENCES disciplina (cod_disciplina)
);

CREATE TABLE curso_disciplina (
    fk_cod_curso INTEGER (4) NOT NULL,
    fk_cod_disciplina INTEGER (4) NOT NULL,
    PRIMARY KEY (fk_cod_curso, fk_cod_disciplina),
FOREIGN KEY (fk_cod_dicsciplina) REFERENCES disciplina (cod_disciplina),
FOREIGN KEY (fk_cod_curso) REFERENCES curso (cod_curso)
);

CREATE TABLE disciplina_historico (
    fk_cod_historico INTEGER (4) NOT NULL,
    fk_cod_disciplina INTEGER (4) NOT NULL,
    nota FLOAT (4,2),
    frequencia INTEGER (4),
    PRIMARY KEY (fk_cod_historico, fk_cod_disciplina),
FOREIGN KEY (fk_cod_historico) REFERENCES historico (cod_historico),
FOREIGN KEY (fk_cod_disciplina) REFERENCES disciplina (cod_disciplina)
);

CREATE TABLE aluno_disciplina (
    fk_RA INTEGER (4) NOT NULL,
    fk_cod_disciplina INTEGER (4) NOT NULL,
    PRIMARY KEY (fk_RA, fk_cod_disciplina),
FOREIGN KEY (fk_RA) REFERENCES aluno (RA),
FOREIGN KEY (fk_cod_disciplina) REFERENCES disciplina (cod_disciplina)
);


INSERT INTO tipo_logradoura                                                       
	(tipo_logradoura)                 
VALUES                                                               
	('rua'),
    ('alameda'),
    ('avenida'),
    ('campo'),
    ('chácara');  
        
INSERT INTO endereco                                                     
	(nome_rua, numero_rua, complemento, CEP, fk_cod_tipo_logradoura)                 
VALUES                                                               
	('QNL','5','perto daqui','12345678','1'),
    ('QNJ','15','perto dali','87654321','1'),
    ('QNQ','3','perto dila','23415783','2'),
    ('QNR','1','perto daquilo','95639324','3'),
    ('Ceilandia','43','perto dacula','74256548','4'),
    ('Rute','2','perto disso','75836481','1'),
    ('Don joão','21','longe daqui','22462864','2'),
    ('Pinheiros','12','padaria pão bom','87463281','3'),
    ('EPTG','32','perto da estatua','86774245','3'),
    ('Alameda','7','condominio aiai','75638356','4'),
    ('Comencial','31','pedio grande','75278431','5'),
    ('Itapu','35','dinossauro','12345643','5'),
    ('Tokyo','38','rugido','66677788','2'),
    ('Elio','32','balão','23465498','1'),
    ('Capitapuaba','53','bomba','44239863','3'),
    ('Capivarinha','47','cocorico','11234631','3'),
    ('Coqueiro','42','galo','67381263','2'),
    ('Roberto piris','4','festa','68235317','2'),
    ('Agusto lima','7','ebaa','74827646','1');
    
INSERT INTO tipo_telefone                                                      
	(tipo_telefone)                 
VALUES                                                               
	('celular'),
    ('residen'),
    ('comercio');
    

    
INSERT INTO telefone                                                      
	(num_telefone,fk_cod_tipo)                 
VALUES                                                               
	('222222222','10'),
    ('121212121','10'),
    ('141414141','10'),
    ('181818181','10'),
    ('765213456','12'),
    ('124356578','11'),
    ('234654634','12'),
    ('876342355','11'),
    ('134556467','10'),
    ('857625484','12'),
    ('123321231','11'),
    ('456654564','10'),
    ('789987897','11'),
    ('680086806','12'),
    ('579975795','10'),
    ('357753573','10'),
    ('246642462','11'),
    ('135531351','12'),
    ('485632348','10'),
    ('094642360','11'),
    ('054387521','12'),
    ('435476547','10'),
    ('846728124','11'),
    ('813764513','12'),
    ('131313131','10');
    
INSERT INTO departamento                                                      
	(nome_departamento)                 
VALUES                                                               
	('Ciencias Humanas'),
    ('Matematica'),
    ('Biologicas'),
    ('Estagio'),
    ('Tecnologia Informação');  
    
    
INSERT INTO curso                                                     
	(nome_curso,fk_cod_departamento)                 
VALUES                                                               
	('Enge de softwarer','5'),
    ('Analise de sistemas','5'),
    ('Biologia','3'),
    ('Historia','1'),
    ('Matematica','2'),
    ('Engenharia eletrica','4'),
    ('Pscicologia','1'),
    ('Medicina','3'),
    ('Farmacia','3'),
    ('Direito','1');
    
    
INSERT INTO turma                                                     
	(periodo,num_alunos,dt_inicio,dt_fim,fk_cod_curso)                 
VALUES                                                               
	('Matutino','25','2020-03-01','2020-06-01','11'),
    ('Vesper','31','2020-06-01','2020-12-01','12'),
    ('Matutino','27','2020-03-01','2020-06-01','13'),
    ('Vesper','29','2020-06-01','2020-12-01','14'),
    ('Matutino','25','2020-03-01','2020-06-01','15'),
    ('Vesper','23','2020-06-01','2020-12-01','16'),
    ('Noturno','30','2020-03-01','2020-06-01','17'),
    ('Noturno','20','2020-06-01','2020-12-01','18');
    
INSERT INTO aluno                                                    
	(nome_aluno,sobrenome_aluno,CPF,status,sexo,nome_mae,nome_pai,email,whatsapp,fk_cod_curso,fk_cod_turma,fk_cod_endereco)                 
VALUES                                                               
	('Emerson','Caetano','07182674190','1','M','Claudia','Emerson','emerson@gmail.com','183647283','12','9','1'),
    ('Antonio','Martins','03826219382','2','M','Maria','Roberto','antonio@gmail.com','222222222',NULL,NULL,'2'),
    ('Thais','Lima','84637285935','1','F','Lurdes','Carlos','thais@gmail.com','548309139','12','10','3'),
    ('Andreia','Martins','27489235471','1','F','Leticia','João','andreia@gmail.com','994827362','11','11','4'),
    ('Ala','Pamela','96745388473','2','F','Civirina','Roberto','ala@gmail.com','884627351',NULL,NULL,'5'),
    ('Maria','Neve','66472849373','1','F','Simone',NULL,'maria@gmail.com','463748593',11,'12','7'),
    ('João','Pimentel','00773232503','1','M','Rute','Davi','jãozinho@gmail.com','948572904','13','13','7'),
    ('Arthur','Dultra','94503629591','1','M','Esther','Tião','chaulinmatadodeporco@gmail.com','746283648','14','14','6'),
    ('Pedro','Cabral','04759274196','1','M','Adriana',NULL,'pedro@gmail.com','12346743','15','15','8'),
    ('Igor','Figueredo','82648925376','1','M','Rosane','Ramon','igor@gmail.com','860741578','16','16','9'),
    ('Ivonete','Cardoso','64826385851','1','F','Cristina','Ricardo','ivonete@gmail.com','456654564','15','9','10'),
    ('Roberto','Silva','56403781309','1','M','Barbara','Bruno','roberto@gmail.com','121212121','17','10','11'),
    ('Arthur','Lima','94716390254','1','M','Rita','Flavio','arthur@gmail.com','131313131','13','11','12'),
    ('Rodrigo','Fernandes','95782109441','1','M','Rosaria','Antonio','rodrigo@gmail.com','141414141','14','12','13'),
    ('Esther','Costa','04947313804','1','F','Maria','Thiago','esther@gmail.com','123321231','12','13','14'),
    ('Juliana','Caetano','40284395325','2','F','Claudia','Emerson','juliana@gmail.com','789987897',NULL,NULL,'15'),
    ('Juvenal','Ribeiro','24234582376','1','M','Barbara','Breno','juvenal@gmail.com','680086806','18','14','16'),
    ('Brunna','Pinheiro','12341516545','1','F','Simaria',NULL,'bruninha@gmail.com','181818181','13','15','17'),
    ('Flavio','Cardoso','12364356456','1','M','Damares','Roberto','flavioDaXJ@gmail.com','579975795','16','16','18'),
    ('Vinicios','Roriz','54345474546','1','M','Divina','Lucas','Dinossalro@gmail.com','357753573','18','9','19');
    

    
INSERT INTO telefone_aluno                                                    
	(fk_RA,fk_cod_telefone)                 
VALUES                                                               
	('1','5'),
    ('2','1'),
    ('4','6'),
    ('5','7'),
    ('6','8'),
    ('7','9'),
    ('9','10'),
    ('10','11'),
    ('12','2'),
    ('13','12'),
    ('14','3'),
    ('16','14'),
    ('17','15'),
    ('18','16'),
    ('19','4'),
    ('20','17'),
    ('1','18'),
    ('1','19'),
    ('1','20'),
    ('5','21'),
    ('5','22'),
    ('5','23'),
    ('9','24'),
    ('9','25'),
    ('9','13');
     
INSERT INTO disciplina                                                     
	(nome_disciplina,carga_horaria,descricao,num_alunos,fk_cod_departamento)                 
VALUES                                                               
	('Raciocinio logico','150','Estudar logica','20','2'),
    ('Pscicologia cogni','100','Estudar a mente','27','1'),
    ('Eletronica digital','125','Estudar os computadores','30','2'),
    ('Programação em C','200','Estudar codigo C','15','5'),
    ('Sociologia','112','Estudar as pessoas','60','1'),
    ('Calculo','140','Estudar matematica','17','2'),
    ('Historia','100','Estudar livros infantis','37','3'),
    ('Geografia','111','Estudar as pedras','35','1'),
    ('Direito civil','293','Estudar os crimes','21','3'),
    ('Portugues','190','ler tirinha da Mafalda','29','1'),
    ('Balela','50','fazer nada','50','4'),
    ('Banco de dados','200','como ser um DBA','30','5'),
    ('Culinaria','135','fazer comida','26','4'),
    ('quimica','170','virar o walter white','32','3'),
    ('Corpo humano','220','estudar o corpo','12','1'),
    ('Ninjitsu','400','virar um ninja','5','4'),
    ('Roubo','99','não pode, é feio','7','4'),
    ('Biologia','225','virus e umas coisas','28','2'),
    ('fisica','200','acho pior que matematica','25','2'),
    ('matematida descreta','200','tipo matematica, so que introvertida','18','2'),
    ('literatura','150','ler livro','23','1'),
    ('Mecanica','150','montar carro','28','4'),
    ('Artesanato','90','fazer porta lapis','10','4'),
    ('PHP','175','eu gosto','36','5'),
    ('Java','175','eu não gosto','32','5'),
    ('Patinhos','100','quack','20','3'),
    ('Logica','200','pensar','21','2'),
    ('estrategia','210','como dominar o mundo?','35','2'),
    ('Box','100','dar porrada','24','4'),
    ('xadres','100','os cambito da rainha','13','2');
    
INSERT INTO curso_disciplina                                                    
	(fk_cod_curso,fk_cod_disciplina)                 
VALUES                                                               
	('11','31'),
    ('12','32'),
    ('13','33'),
    ('14','34'),
    ('15','35'),
    ('16','36'),
    ('17','37'),
    ('18','38'),
    ('19','39'),
    ('20','40'),
    ('11','41'),
    ('12','42'),
    ('13','43'),
    ('14','44'),
    ('15','45'),
    ('16','46'),
    ('17','47'),
    ('18','48'),
    ('19','49'),
    ('20','50'),
    ('11','51'),
    ('12','52'),
    ('13','53'),
    ('14','54'),
    ('15','55'),
    ('16','56'),
    ('17','57'),
    ('18','58'),
    ('19','59'),
    ('20','60');
    
INSERT INTO professor                                                     
	(nome_professor, sobrenome_professor, status, fk_cod_departamento)                 
VALUES                                                               
	('Luciano','Martins','1','1'),
    ('Antonio','Lopes','1','2'),
    ('Flavia','Pires','1','3'),
    ('Bruno','Pinheiro','0','4'),
    ('Pedro','Whegner','0','5'),
    ('Julia','Matos','1','1'),
    ('Ivonete','Cardoso','1','2'),
    ('Rebeca','Solsa','0','3'),
    ('Valdernei','Diney','1','4'),
    ('Leandro','Lima','1','5');
    
INSERT INTO disciplina_professor                                                   
	(fk_cod_professor,fk_cod_disciplina)                 
VALUES                                                               
	('1','31'),
    ('2','32'),
    ('3','33'),
    ('6','34'),
    ('7','35'),
    ('9','36'),
    ('10','37'),
    ('1','38'),
    ('2','39'),
    ('3','40'),
    ('6','41'),
    ('7','42'),
    ('9','43'),
    ('10','44'),
    ('1','45'),
    ('2','46'),
    ('3','47'),
    ('6','48'),
    ('7','49'),
    ('9','50'),
    ('10','51'),
    ('1','52'),
    ('2','53'),
    ('3','54'),
    ('6','55'),
    ('7','56'),
    ('9','57'),
    ('10','58'),
    ('1','59'),
    ('2','60');
    
INSERT INTO aluno_disciplina                                                   
	(fk_RA,fk_cod_disciplina)                 
VALUES                                                               
	('1','31'),
    ('3','32'),
    ('4','33'),
    ('6','34'),
    ('7','35'),
    ('8','36'),
    ('9','37'),
    ('10','38'),
    ('11','39'),
    ('12','40'),
    ('13','41'),
    ('14','42'),
    ('15','43'),
    ('17','44'),
    ('18','45'),
    ('19','46'),
    ('20','47'),
    ('1','48'),
    ('3','49'),
    ('4','50'),
    ('6','51'),
    ('7','52'),
    ('8','53'),
    ('9','54'),
    ('10','55'),
    ('11','56'),
    ('12','57'),
    ('13','58'),
    ('14','59'),
    ('15','60');

INSERT INTO historico                                                 
	(dt_inicio,dt_fim,fk_RA)                 
VALUES                                                               
	('2020-02-01','2021-08-29','1'),
    ('2020-03-02','2021-07-28','2'),
    ('2020-01-03','2021-06-27','3'),
    ('2020-06-04','2021-05-26','4'),
    ('2020-07-05','2021-04-25','5'),
    ('2020-04-06','2021-03-24','6'),
    ('2020-12-07','2021-02-23','7'),
    ('2020-04-08','2021-01-22','8'),
    ('2020-08-09','2021-12-21','9'),
    ('2020-11-10','2021-11-20','10'),
    ('2020-03-11','2021-10-19','11'),
    ('2020-07-12','2021-09-18','12'),
    ('2020-04-13','2021-08-17','13'),
    ('2020-03-14','2021-07-16','14'),
    ('2020-09-15','2021-06-15','15'),
    ('2020-10-16','2021-05-14','16'),
    ('2020-11-17','2021-04-13','17'),
    ('2020-06-18','2021-03-12','18'),
    ('2020-07-19','2021-02-11','19'),
    ('2020-08-20','2021-01-10','20');
    
INSERT INTO historico_disciplina                                                     
	(fk_cod_disciplina, fk_cod_historico, nota, frequencia)                 
VALUES                                                               
	('31','1','6.2','3'),
    ('32','2','6.5','0'),
    ('33','3','7.1','6'),
    ('34','4','10.0','5'),
    ('35','5','3.5','5'),
    ('36','6','5.5','1'),
    ('37','7','7.0','2'),
    ('38','8','6.0','3'),
    ('39','9','10.0','0'),
    ('40','10','9.5','0'),
    ('41','11','4.1','4'),
    ('42','12','1.3','0'),
    ('43','13','5.4','7'),
    ('44','14','8.4','0'),
    ('45','15','8.9','3'),
    ('46','16','9.9','4'),
    ('47','17','10.0','5'),
    ('48','18','6.0','10'),
    ('49','19','7.4','2'),
    ('50','20','6.9','1'),
    ('51','1','2.0','1'),
    ('52','2','0.0','4'),
    ('53','3','7.6','4'),
    ('54','4','8.5','0'),
    ('55','5','9.1','4'),
    ('56','6','4.9','0'),
    ('57','7','6.5','6'),
    ('58','8','6.8','8'),
    ('59','9','7.5','1'),
    ('60','10','8.3','5');
    
    INSERT INTO tipo_logradouro                                                       
	(tipo_logradouro)                 
VALUES                                                               
    ('rua'),
    ('alameda'),
    ('avenida'),
    ('campo'),
    ('chácara');  
        
INSERT INTO endereco                                                     
	(nome_rua, numero_rua, complemento, CEP, fk_cod_tipo_logradouro)                 
VALUES                                                               
    ('QNN','5','conjunto','12345678','1'),
    ('QNJ','55','perto dali','87654321','1'),
    ('QNQ','3','perto dila','23415783','2'),
    ('QNR','6','perto daquilo','95639324','3'),
    ('Ceilandia','43','perto dacula','74256548','4'),
    ('Rute','2','perto disso','75836481','1'),
    ('Don joão','21','longe daqui','22462864','2'),
    ('Pinheiros','12','padaria pão bom','87463281','3'),
    ('EPTG','32','perto da estatua','86774245','3'),
    ('Alameda','7','condominio aiai','75638356','4'),
    ('Comencial','31','pedio grande','75278431','5'),
    ('Itapu','35','dinossauro','12345643','5'),
    ('Tokyo','38','rugido','66677788','2'),
    ('Elio','32','balão','23465498','1'),
    ('Capitapuaba','53','bomba','44239863','3'),
    ('Capivarinha','47','cocorico','11234631','3'),
    ('Coqueiro','42','galo','67381263','2'),
    ('Roberto piris','4','festa','68235317','2'),
    ('Agusto lima','7','ebaa','74827646','1');
    
INSERT INTO tipo_telefone                                                      
	(tipo_telefone)                 
VALUES                                                               
    ('celular'),
    ('residen'),
    ('comercio');
    

    
INSERT INTO telefone                                                      
	(num_telefone,fk_cod_tipo)                 
VALUES                                                               
    ('324222222','10'),
    ('521212121','10'),
    ('141414141','10'),
    ('181818181','10'),
    ('765213456','12'),
    ('124356578','11'),
    ('234654634','12'),
    ('876342355','11'),
    ('134556467','10'),
    ('857625484','12'),
    ('123321231','11'),
    ('456654564','10'),
    ('789987897','11'),
    ('680086806','12'),
    ('579975795','10'),
    ('357753573','10'),
    ('246642462','11'),
    ('135531351','12'),
    ('485632348','10'),
    ('094642360','11'),
    ('054387521','12'),
    ('435476547','10'),
    ('846728124','11'),
    ('813764513','12'),
    ('731313131','10');
    
INSERT INTO departamento                                                      
	(nome_departamento)                 
VALUES                                                               
    ('Ciencias Biológicas'),
    ('Matematica'),
    ('Biologicas'),
    ('Estagio'),
    ('Tecnologia Informação');  
    
    
INSERT INTO curso                                                     
	(nome_curso,fk_cod_departamento)                 
VALUES                                                               
    ('Engenharia de softwarer','5'),
    ('Analise de sistemas','5'),
    ('Biologia','3'),
    ('Historia','1'),
    ('Matematica','2'),
    ('Engenharia eletrica','4'),
    ('Pscicologia','1'),
    ('Medicina','3'),
    ('Farmacia','3'),
    ('Enfermagem','1');
    
    
INSERT INTO turma                                                     
	(periodo,num_alunos,dt_inicio,dt_fim,fk_cod_curso)                 
VALUES                                                               
    ('Matutino','25','2020-03-01','2020-06-01','11'),
    ('Vesper','31','2020-06-01','2020-12-01','12'),
    ('Matutino','27','2020-03-01','2020-06-01','13'),
    ('Vesper','29','2020-06-01','2020-12-01','14'),
    ('Matutino','25','2020-03-01','2020-06-01','15'),
    ('Vesper','23','2020-06-01','2020-12-01','16'),
    ('Noturno','30','2020-03-01','2020-06-01','17'),
    ('Noturno','20','2020-06-01','2020-12-01','18');
    
INSERT INTO aluno                                                    
	(nome_aluno,sobrenome_aluno,CPF,status,sexo,nome_mae,nome_pai,email,whatsapp,fk_cod_curso,fk_cod_turma,fk_cod_endereco)                 
VALUES                                                               
    ('Arthur','Guedes','08182674190','1','M','Claudia','Emerson','emerson@gmail.com','183647283','12','9','1'),
    ('Maurilio','Mello','08826219382','2','M','Maria','Roberto','antonio@gmail.com','222222222',NULL,NULL,'2'),
    ('Renata','Lima','84637285935','1','F','Lurdes','Carlos','thais@gmail.com','548309139','12','10','3'),
    ('Andreia','Martins','27489235471','1','F','Leticia','João','andreia@gmail.com','994827362','11','11','4'),
    ('Ana','Pamela','96745388473','2','F','Civirina','Roberto','ala@gmail.com','884627351',NULL,NULL,'5'),
    ('Maria','Neiva','66472849373','1','F','Simone',NULL,'maria@gmail.com','463748593',11,'12','7'),
    ('João','Pimentel','00773232503','1','M','Rute','Davi','jãozinho@gmail.com','948572904','13','13','7'),
    ('Arthur','Dultra','94503629591','1','M','Esther','Tião','chaulinmatadodeporco@gmail.com','746283648','14','14','6'),
    ('Pedro','Cabral','04759274196','1','M','Adriana',NULL,'pedro@gmail.com','12346743','15','15','8'),
    ('Itamar','Figueredo','82648925376','1','M','Rosane','Ramon','igor@gmail.com','860741578','16','16','9'),
    ('Ivonete','Cardoso','64826385851','1','F','Cristina','Ricardo','ivonete@gmail.com','456654564','15','9','10'),
    ('Roberto','Silva','56403781309','1','M','Barbara','Bruno','roberto@gmail.com','121212121','17','10','11'),
    ('Arthur','Lima','94716390254','1','M','Rita','Flavio','arthur@gmail.com','131313131','13','11','12'),
    ('Rodrigo','Fernandes','95782109441','1','M','Rosaria','Antonio','rodrigo@gmail.com','141414141','14','12','13'),
    ('Esther','Costa','04947313804','1','F','Maria','Thiago','esther@gmail.com','123321231','12','13','14'),
    ('Juliana','Caetano','40284395325','2','F','Claudia','Emerson','juliana@gmail.com','789987897',NULL,NULL,'15'),
    ('Juvenal','Ribeiro','24234582376','1','M','Barbara','Breno','juvenal@gmail.com','680086806','18','14','16'),
    ('Brunna','Pinheiro','12341516545','1','F','Simaria',NULL,'bruninha@gmail.com','181818181','13','15','17'),
    ('Flavio','Cardoso','12364356456','1','M','Damares','Roberto','flavioDaXJ@gmail.com','579975795','16','16','18'),
    ('Feliciano','Ramirez','54345474546','1','M','Divina','Lucas','Dinossalro@gmail.com','357753573','18','9','19');
    

    
INSERT INTO telefone_aluno                                                    
	(fk_RA,fk_cod_telefone)                 
VALUES                                                               
	('1','5'),
    ('2','1'),
    ('4','6'),
    ('5','7'),
    ('6','8'),
    ('7','9'),
    ('9','10'),
    ('10','11'),
    ('12','2'),
    ('13','12'),
    ('14','3'),
    ('16','14'),
    ('17','15'),
    ('18','16'),
    ('19','4'),
    ('20','17'),
    ('1','18'),
    ('1','19'),
    ('1','20'),
    ('5','21'),
    ('5','22'),
    ('5','23'),
    ('9','24'),
    ('9','25'),
    ('9','13');
     
INSERT INTO disciplina                                                     
	(nome_disciplina,carga_horaria,descricao,num_alunos,fk_cod_departamento)                 
VALUES                                                               
    ('Enfermagem','150','Estudar logica','20','2'),
    ('Pedagogiagia cognitiva','100','Estudar a mente','27','1'),
    ('Eletronica digital','125','Estudar os computadores','30','2'),
    ('Programação em C','200','Estudar codigo C','15','5'),
    ('Sociologia','112','Estudar as pessoas','60','1'),
    ('Calculo','140','Estudar matematica','17','2'),
    ('Historia','100','Estudar livros infantis','37','3'),
    ('Geografia','111','Estudar as pedras','35','1'),
    ('Direito civil','293','Estudar os crimes','21','3'),
    ('Portugues','190','ler tirinha da Mafalda','29','1'),
    ('Balela','50','fazer nada','50','4'),
    ('Banco de dados','200','como ser um DBA','30','5'),
    ('Culinaria','135','fazer comida','26','4'),
    ('quimica','170','virar o walter white','32','3'),
    ('Corpo humano','220','estudar o corpo','12','1'),
    ('Ninjitsu','400','virar um ninja','5','4'),
    ('Roubo','99','não pode, é feio','7','4'),
    ('Biologia','225','virus e umas coisas','28','2'),
    ('fisica','200','acho pior que matematica','25','2'),
    ('matematida descreta','200','tipo matematica, so que introvertida','18','2'),
    ('literatura','150','ler livro','23','1'),
    ('Mecanica','150','montar carro','28','4'),
    ('Artesanato','90','fazer porta lapis','10','4'),
    ('PHP','175','eu gosto','36','5'),
    ('Java','175','eu não gosto','32','5'),
    ('Patinhos','100','quack','20','3'),
    ('Logica','200','pensar','21','2'),
    ('estrategia','210','como dominar o mundo?','35','2'),
    ('Box','100','dar porrada','24','4'),
    ('xadres','100','os cambito da rainha','13','2');
    
INSERT INTO curso_disciplina                                                    
	(fk_cod_curso,fk_cod_disciplina)                 
VALUES                                                               
	('11','31'),
    ('12','32'),
    ('13','33'),
    ('14','34'),
    ('15','35'),
    ('16','36'),
    ('17','37'),
    ('18','38'),
    ('19','39'),
    ('20','40'),
    ('11','41'),
    ('12','42'),
    ('13','43'),
    ('14','44'),
    ('15','45'),
    ('16','46'),
    ('17','47'),
    ('18','48'),
    ('19','49'),
    ('20','50'),
    ('11','51'),
    ('12','52'),
    ('13','53'),
    ('14','54'),
    ('15','55'),
    ('16','56'),
    ('17','57'),
    ('18','58'),
    ('19','59'),
    ('20','60');
    
INSERT INTO professor                                                     
	(nome_professor, sobrenome_professor, status, fk_cod_departamento)                 
VALUES                                                               
	('Luciano','Martins','1','1'),
    ('Paulo','Pereira','1','2'),
    ('Flavia','Pires','1','3'),
    ('Bruno','Pinheiro','0','4'),
    ('Pedro','Whegner','0','5'),
    ('Julia','Matos','1','1'),
    ('Ivonete','Cardoso','1','2'),
    ('Rebeca','Solsa','0','3'),
    ('Valdernei','Diney','1','4'),
    ('Leandro','Lima','1','5');
    
INSERT INTO disciplina_professor                                                   
	(fk_cod_professor,fk_cod_disciplina)                 
VALUES                                                               
	('1','31'),
    ('2','32'),
    ('3','33'),
    ('6','34'),
    ('7','35'),
    ('9','36'),
    ('10','37'),
    ('1','38'),
    ('2','39'),
    ('3','40'),
    ('6','41'),
    ('7','42'),
    ('9','43'),
    ('10','44'),
    ('1','45'),
    ('2','46'),
    ('3','47'),
    ('6','48'),
    ('7','49'),
    ('9','50'),
    ('10','51'),
    ('1','52'),
    ('2','53'),
    ('3','54'),
    ('6','55'),
    ('7','56'),
    ('9','57'),
    ('10','58'),
    ('1','59'),
    ('2','60');
    
INSERT INTO aluno_disciplina                                                   
	(fk_RA,fk_cod_disciplina)                 
VALUES                                                               
	('1','31'),
    ('3','32'),
    ('4','33'),
    ('6','34'),
    ('7','35'),
    ('8','36'),
    ('9','37'),
    ('10','38'),
    ('11','39'),
    ('12','40'),
    ('13','41'),
    ('14','42'),
    ('15','43'),
    ('17','44'),
    ('18','45'),
    ('19','46'),
    ('20','47'),
    ('1','48'),
    ('3','49'),
    ('4','50'),
    ('6','51'),
    ('7','52'),
    ('8','53'),
    ('9','54'),
    ('10','55'),
    ('11','56'),
    ('12','57'),
    ('13','58'),
    ('14','59'),
    ('15','60');

INSERT INTO historico                                                 
	(dt_inicio,dt_fim,fk_RA)                 
VALUES                                                               
	('2020-02-01','2021-08-29','1'),
    ('2020-03-02','2021-07-28','2'),
    ('2020-01-03','2021-06-27','3'),
    ('2020-06-04','2021-05-26','4'),
    ('2020-07-05','2021-04-25','5'),
    ('2020-04-06','2021-03-24','6'),
    ('2020-12-07','2021-02-23','7'),
    ('2020-04-08','2021-01-22','8'),
    ('2020-08-09','2021-12-21','9'),
    ('2020-11-10','2021-11-20','10'),
    ('2020-03-11','2021-10-19','11'),
    ('2020-07-12','2021-09-18','12'),
    ('2020-04-13','2021-08-17','13'),
    ('2020-03-14','2021-07-16','14'),
    ('2020-09-15','2021-06-15','15'),
    ('2020-10-16','2021-05-14','16'),
    ('2020-11-17','2021-04-13','17'),
    ('2020-06-18','2021-03-12','18'),
    ('2020-07-19','2021-02-11','19'),
    ('2020-08-20','2021-01-10','20');
    
INSERT INTO historico_disciplina                                                     
	(fk_cod_disciplina, fk_cod_historico, nota, frequencia)                 
VALUES                                                               
    ('31','1','6.2','3'),
    ('33','2','6.5','0'),
    ('33','3','7.1','6'),
    ('34','4','10.0','5'),
    ('35','5','3.5','5'),
    ('36','6','5.5','1'),
    ('37','7','7.0','2'),
    ('38','8','6.0','3'),
    ('39','9','10.0','0'),
    ('40','10','9.5','0'),
    ('41','11','4.1','4'),
    ('42','12','1.3','0'),
    ('43','13','5.4','7'),
    ('44','14','8.4','0'),
    ('45','15','8.9','3'),
    ('46','16','9.9','4'),
    ('47','17','10.0','5'),
    ('48','18','6.0','10'),
    ('49','19','7.4','2'),
    ('50','20','6.9','1'),
    ('51','1','2.0','1'),
    ('52','2','0.0','4'),
    ('53','3','7.6','4'),
    ('54','4','8.5','0'),
    ('55','5','9.1','4'),
    ('56','6','4.9','0'),
    ('57','7','6.5','6'),
    ('58','8','6.8','8'),
    ('59','9','7.5','1'),
    ('60','10','8.3','5');
    
     
/////////////////////
USE db_faculdade;

CREATE USER professor@localhost 
IDENTIFIED BY '1234';

GRANT SELECT ON db_faculdade.disciplina 
TO professor@localhost;

GRANT SELECT ON db_faculdade.turma 
TO professor@localhost;

GRANT SELECT ON db_faculdade.departamento 
TO professor@localhost;

GRANT SELECT, INSERT, UPDATE (nome_professor, sobrenome_professor, status, fk_cod_departamento) 
ON db_faculdade.professor 
TO professor@localhost;


2.
creat user aluno@localhost
identifyed bt '1234';

graant select, update, select,
on db_faculdade.aluno
to aluno@localhost;

graant select, insert, select,
on db_faculdade.endereco
to aluno@localhost;

grant select, insert on db_faculdade.telefone
to aluno@localhost;

grant select, insert on db_faculdade.turma
to aluno@localhost;

grant select, insert on db_faculdade.disciplina
to aluno@localhost;

3.
creat user diretor@l'%'   (@localhost)
identifyed by;

grant all on db_faculdade.*
to diretor@'%' with grant options;

creat user secretaria@localhost;

grant select, insert
on db_faculdade.*
to secretaria@localhost;

grant update on db_faculdade.professor
to secretaria@localhost;


grant update on db_faculdade.departamento
to secretaria@localhost;


grant update on db_faculdade.disciplina
to secretaria@localhost;
////////////
1
insert

select ra, concat(a.nome_aluno,' ', a.sobrenome_aluno) as nome ,
  c.nome_curso, t.periodo
from aluno a
join curso c
  on a.fk_codcurso = c.cod_curso
join turma t
  on a.fk_cod_turma = t.cod_turma
order by a.nome_aluno;

2
select a.ra, a.nome_aluno, a.sobrenome_aluno,
   d.nome_disciplina, dh.nota
from aluno a
join aluno_disciplina ad
   on ad.fk_ra = a.ra
join disciplina d
   on d.cod_disciplina = ad.fk_cod_disciplina
join historico h
   on a.ra = h.fk_ra
join disciplina_historico dh
   on dh.fk_cod_disciplina = d.cod_disciplina
where a.ra = '1'
order by dh.nota desc;

3
select concat(p.nome_professor, ' ', p.sobrenome_professor) as nome,
     d.nome_disciplina, d.crga_horaria
from professor p 
join professor_disciplina pd
   on pd.fk_cod_professor = p.cod_professor
join disciplina d
   on pd.fk_cod_disciplina = d.cod_disciplina;

4
 select a.ra, a.nome_aluno, a.sobrenome_aluno, a.cpf,a.status,
        a.sexo, a.nome_pai, a.nome_mae, a.email, a.whatsapp,
        tl.tipo_logradouro, e.nome_rua,
        e.numero_rua, e.complemento, e.CEP, t.num_telefone,
from aluno a
join endereco e
   on a.fk_cod_endereco = e.cod_endereco
join tipo_logradouro tl
   on e.fk+cod_tipo_logradouro - tl.cod_tipo_logradouro
join telefone t
   on ta.fk_cod_telefone = t.cod_telefone
join tipo_telefone tt
   on t.fk_cod_tipo = tt.cod_tipo
order by a.nome_aluno;

5
select d.nome_disciplina, dep.nome_departamento,
   c.nome_curso
from disciplina d
join departamento dep
   on d.fk_cod_departamento = dep.cod_departamento
join curso_disciplina
   on cd.fk_cod_disciplina = d.cod_disciplina
join curso c 
   on cd.fk_cod_curso = c.cod_curso
join professor_disciplina pd
   on pd.fk_cod_disciplina = d.cod_disciplina
join professor_disciplina pd
   on pd.fk_cod_disciplina = d.cod_disciplina
join professor p
   on pd.fk_cod_professor = p.cod_professor
order by d.nome_disciplina;

 





 






    
    
    
