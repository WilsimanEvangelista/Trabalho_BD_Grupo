# Trabalho_BD: 
Trabalho desenvolvido durante a disciplina de Banco de Dados no semestre 2022/2 - IFES Campus Serra

---

# 🧬 **Farmácia WLD** 💊
---

# Sumário:

### 1. Componentes

#### Integrantes do grupo

Wilsiman Evangelista - wilsiman.evangelista.ifes@gmail.com

Lorena Toraes - lorenatoraessantos@gmail.com

Davi Salles - cardososallesdavi@gmail.com

### 2. INTRODUÇÃO E MOTIVAÇÃO

Em 2019 iniciou-se a pandemia de Covid-19 e por conta dela o consumo de produtos farmacêuticos aumentou exponencialmente. Contudo as pessoas, em sua maioria, estavam em isolamento social e com isso as entregas foram de suma importância, neste contexto surge a farmácia "WLD" com objetivo de suprir esta necessidade. A farmácia "WLD" tem como maior objetivo aproximar a comunidade do comércio e a motivação para sua criação se deu pois mesmo após a amenização da pandemia (atualmente, 3 anos após seu início) há a grande necessidade de delivery, pois o mundo se tornou muito mais digital, o home office é cada vez mais comum e a necessidade de sair de casa para comprar qualquer coisa passa a ser cada vez mais remota.

### 3. MINI-MUNDO

A farmácia "WLD" conterá as informações aqui detalhadas. Do FABRICANTE será registrado CNPJ, nome, telefone, email, endereço. Do PRODUTO será registrado código, nome, preço. Do PEDIDO será registrado código, valor_total. Do CLIENTE será registrado CPF, nome, telefone. Do ENTREGADOR será registrado cpf, telefone, nome.
Ao produto ser adicionado a um pedido, deve-se informar a quantidade de produtos de uma mesma classe que foi adicionado. Para o entregador entregar um produto, deve-se informar o codigo, endereco e data da entrega. Pedido possui de um a vários produtos e um produto deve estar inserido em um ou vários pedidos. O fabricante deve possuir um ou vários produtos e um produto deve possuir apenas um fabricante. Um cliente deve realizar um ou vários pedidos e um pedido pode ter sido realizado por um ou vários cliente. Por fim, um entregador entrega nenhum ou vários pedidos e um pedido deve ser entregue por apenas um entregador.

### 4.PERGUNTAS A SEREM RESPONDIDAS E TABELA DE DADOS
   #### 4.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?    
   - Nesse sistema é possível gerar relatórios com a quantidade de cada produto que está sendo adicionado aos pedidos. 
   - Nesse sistema é possível saber a quantidade de produtos de cada fabricante que estão sendo adicionados aos pedidos.
   - Nesse sistema é possível saber em qual ano ou época do ano está tendo mais vendas.
   - Nesse sistema é possível gerar relatórios sobre o valor total dos produtos, sabendo assim em qual período houve mais lucro.
   - Nesse sistema é possível gerar relatórios sobre quantos pedidos estão sendo entregues por cada entregador.
    
### 5. MODELO CONCEITUAL

![image](https://user-images.githubusercontent.com/116188500/198857102-cd034569-23af-4bb3-9304-06497ba13f5c.png)

 #### 5.1 Validação do Modelo Conceitual
 #### 5.2 Descrição dos dados
 
 CLIENTE: Tabela que armazena informações referentes ao cliente. </br>
 ENTREGADOR: Tabela que armazena informações referentes ao entregador. </br>
 FABRICANTE: Tabela que armazena informações referentes ao fabricante. </br>
 PEDIDO: Tabela que armazena informações referentes ao pedido. </br>
 PRODUTO: Tabela que armazena informações referentes ao produto. </br>
 Cliente_Pedido: Tabela que relaciona o cliente a seu pedido. </br>
 Cliente_Telefone: Tabela que relaciona o cliente a seu(s) telefone(s). </br>
 Entregador_Pedido: Tabela que relaciona o entregador ao pedido que ele terá de entregar. </br>
 Entregador_Pedido_Endereco: Tabela que relaciona a entrega a seu endereço de entrega. </br>
 Entregador_Telefone: Tabela que relaciona o entregador a seu(s) telefone(s). </br>
 Fabricante_Email: Tabela que relaciona o fabricante a seu(s) email(s). </br>
 Fabricante_Endereco: Tabela que relaciona o fabricante a seu endereço. </br>
 Fabricante_Telefone: Tabela que relaciona o fabricante a seu(s) telefone(s). </br>
 Pedido_Produto: Tabela que relaciona o pedido ao produto que foi inserido nele. </br>
 Produto_Fabricante: Tabela que relaciona o produto ao fabricante que o produziu. </br>
 
### 6. MODELO LÓGICO

![image](https://user-images.githubusercontent.com/116188500/198857119-2eb9fb20-7d19-4338-919c-0bf22f89cfb9.png)

### 7. MODELO FÍSICO

    drop table if exists cliente cascade; 
    CREATE TABLE CLIENTE ( 
        CPF BIGINT PRIMARY KEY, 
        nome VARCHAR 
    ); 

    drop table if exists fabricante_endereco cascade; 
    CREATE TABLE Fabricante_Endereco ( 
        endereco_PK INT NOT NULL PRIMARY KEY, 
        nome_logradouro VARCHAR, 
        bairro VARCHAR, 
        estado VARCHAR,
        cep BIGINT, 
        numero INT, 
        tipo_logradouro VARCHAR, 
        municipio VARCHAR 
    ); 

    drop table if exists fabricante cascade; 
    CREATE TABLE FABRICANTE (
        CNPJ BIGINT PRIMARY KEY,
        FK_endereco_endereco_PK INT REFERENCES fabricante_endereco (endereco_pk),
        nome VARCHAR
    );

    drop table if exists entregador cascade;
    CREATE TABLE ENTREGADOR (
        CPF BIGINT PRIMARY KEY,
        nome VARCHAR
    );

    drop table if exists produto cascade;
    CREATE TABLE PRODUTO (
        codigo INT PRIMARY KEY,
        preco DOUBLE PRECISION,
        nome VARCHAR
    );

    drop table if exists pedido cascade;
    CREATE TABLE PEDIDO (
        codigo INT PRIMARY KEY,
        valor_total DOUBLE PRECISION
    );

    drop table if exists cliente_telefone cascade;
    CREATE TABLE Cliente_Telefone (
        fk_CLIENTE_CPF BIGINT REFERENCES cliente (cpf),
        telefone BIGINT
    );

    drop table if exists fabricante_telefone cascade;
    CREATE TABLE Fabricante_Telefone (
        fk_FABRICANTE_CNPJ BIGINT REFERENCES fabricante (cnpj),
        telefone BIGINT
    );

    drop table if exists fabricante_email cascade;
    CREATE TABLE Fabricante_Email (
        fk_FABRICANTE_CNPJ BIGINT references fabricante (cnpj),
        email VARCHAR
    );

    drop table if exists entregador_telefone cascade;
    CREATE TABLE Entregador_Telefone (
        fk_ENTREGADOR_CPF BIGINT references entregador (cpf),
        telefone BIGINT
    );

    drop table if exists cliente_pedido cascade;
    CREATE TABLE Cliente_Pedido (
        fk_CLIENTE_CPF BIGINT references cliente (cpf),
        fk_PEDIDO_codigo INT references pedido (codigo)
    );

    drop table if exists pedido_produto cascade;
    CREATE TABLE Pedido_Produto (
        fk_PEDIDO_codigo INT references pedido (codigo),
        fk_PRODUTO_codigo INT references  produto (codigo),
        quantidade INT
    );

    drop table if exists Entregador_Pedido_Endereco cascade;
    CREATE TABLE Entregador_Pedido_Endereco (
        endereco_PK INT NOT NULL PRIMARY KEY,
        tipo_logradouro VARCHAR,
        numero INT,
        municipio VARCHAR,
        nome_logradouro VARCHAR,
        bairro VARCHAR,
        cep BIGINT,
        estado VARCHAR
    );

    drop table if exists entregador_pedido cascade;
    CREATE TABLE Entregador_Pedido (
        fk_ENTREGADOR_CPF BIGINT references entregador (cpf),
        fk_PEDIDO_codigo INT references pedido (codigo),
        data DATE,
        codigo INT PRIMARY KEY,
        fk_endereco_endereco_PK INT references Entregador_Pedido_Endereco (endereco_pk)
    );

    drop table if exists produto_fabricante cascade;
    CREATE TABLE Produto_Fabricante (
        fk_FABRICANTE_CNPJ BIGINT references fabricante (cnpj),
        fk_PRODUTO_codigo INT references produto (codigo)
    );


### 8. INSERT APLICADO NAS TABELAS DO BANCO DE DADOS

    INSERT INTO CLIENTE (cpf,nome)
    VALUES
    (54690831916, 'Imelda Wong'),
    (92077224684, 'Scarlett Weber'),
    (34633306292, 'Emi Hunter'),
    (58596061431, 'Rana Riddle'),
    (61142416604, 'Cruz Farley'),
    (60202318666, 'Ria Montoya'),
    (96116796203, 'Patricia Pruitt'),
    (76299908511, 'Anastasia Stanton'),
    (59600170651, 'Keefe Atkinson'),
    (65782808488, 'Uriel Dickson');

    INSERT INTO FABRICANTE_ENDERECO (endereco_pk,nome_logradouro,bairro,estado,cep,numero,tipo_logradouro,municipio)
    VALUES
    (98, 'Vp-R3', 'DISTRITO AGROINDUSTRIAL DE ANAPOLIS', 'Goiás', 75132015, 1283, 'Rua', 'Anapolis'),
    (83, 'Polo de Desenvolvimento Juscelino Kubitschek Trech', 'SANTA MARIA', 'Distrito Federal', 72549550, 5304, 'Loteamento', 'Brasília'),
    (71, 'Amg 1920', 'Galpao1', 'Minas Gerais', 37567000, 3943, 'Rodovia', 'São Sebastião da Bela Vista'),
    (33, 'Presidente Castelo Branco', 'INGAHI', 'São Paulo', 06696000, 3565, 'Rodovia', 'Itapevi'),
    (59, 'Magalhaes de Castro', 'Cidade Jardim', 'São Paulo', 05676120, 4800, 'Avenida', 'São Paulo');

    INSERT INTO FABRICANTE (cnpj,fk_endereco_endereco_pk,nome)
    VALUES
    (05161069000110, 98, 'Neo Química'),
    (57507378000608, 83, 'EMS'),
    (02814497000700, 71, 'Cimed'),
    (61190096000869, 33, 'Eurofarma'),
    (60665981000207, 59, 'União Química');

    INSERT INTO ENTREGADOR (cpf,nome)
    VALUES
    (13756003437, 'Hillary Shepherd'),
    (32368942621, 'Lacota Barnes'),
    (51292729755, 'Ima Nixon'),
    (96104491844, 'Hiroko Whitney'),
    (53327782904, 'Carlos Barrett');

    INSERT INTO PRODUTO (codigo,preco,nome)
    VALUES
    (694, 6.49, 'Paracetamol'),
    (720, 19.90, 'Vitamina A-Z'),
    (145, 8.99, 'Losartana Potássica'),
    (909, 36.42, 'Somalgin Cardio'),
    (266, 47.90, 'Ômega 3'),
    (247, 38.90, 'Cálcio MDK'),
    (920, 43.20, 'Aciclovir'),
    (523, 84.24, 'Azitromicina'),
    (740, 16.00, 'Bromazepam'),
    (280, 29.90, 'Cloridrato de Tramadol');

    INSERT INTO PEDIDO (codigo,valor_total)
    VALUES
    (626, 25.96),
    (179, 39.80),
    (406, 26.97),
    (271, 36.42),
    (500, 95.80),
    (389, 116.70),
    (745, 43.20),
    (578, 168.48),
    (674, 80.00),
    (300, 59.80);

    INSERT INTO CLIENTE_TELEFONE (fk_CLIENTE_CPF,telefone)
    VALUES
    (54690831916, 970190276),
    (54690831916, 980300504),
    (92077224684, 949138088),
    (34633306292, 999945176),
    (34633306292, 925680861),
    (58596061431, 974209776),
    (61142416604, 957793668),
    (60202318666, 956902521),
    (60202318666, 958740237),
    (96116796203, 977235674),
    (96116796203, 957818092),
    (76299908511, 937623463),
    (59600170651, 929855588),
    (59600170651, 990437656),
    (65782808488, 987125117);

    INSERT INTO FABRICANTE_TELEFONE (FK_fabricante_cnpj,telefone)
    VALUES
    (05161069000110, 6238788150),
    (05161069000110, 6238788234),
    (57507378000608, 1938879800),
    (02814497000700, 1135447350),
    (61190096000869, 1150908600),
    (60665981000207, 1155862000),
    (60665981000207, 1155862120);

    INSERT INTO FABRICANTE_EMAIL (FK_fabricante_cnpj,email)
    VALUES
    (05161069000110, 'fiscal@brainfarma.ind.br'),
    (57507378000608, 'wagner@gruponc.net.br'),
    (57507378000608, 'programadevisitas@ems.com.br'),
    (02814497000700, 'tributario@grupocimed.com.br'),
    (61190096000869, 'contencioso.fiscal@eurofarma.com.br'),
    (60665981000207, 'ca-fiscal@uniaoquimica.com.br');

    INSERT INTO ENTREGADOR_TELEFONE (FK_entregador_cpf,telefone)
    VALUES
    (13756003437, 994974686),
    (13756003437, 913301515),
    (32368942621, 939204786),
    (51292729755, 977216975),
    (51292729755, 951993534),
    (96104491844, 991308985),
    (53327782904, 955491364);

    INSERT INTO CLIENTE_PEDIDO (fk_CLIENTE_CPF,fk_PEDIDO_codigo)
    VALUES
    (54690831916, 626),
    (92077224684, 179),
    (34633306292, 406),
    (58596061431, 271),
    (61142416604, 500),
    (60202318666, 389),
    (96116796203, 745),
    (76299908511, 578),
    (59600170651, 674),
    (65782808488, 300);

    INSERT INTO PEDIDO_PRODUTO (fk_pedido_codigo,fk_produto_codigo,quantidade)
    VALUES
    (626, 694, 4),
    (179, 720, 2),
    (406, 145, 3),
    (271, 909, 1),
    (500, 266, 2),
    (389, 247, 3),
    (745, 920, 1),
    (578, 523, 2),
    (674, 740, 5),
    (300, 280, 2);

    INSERT INTO Entregador_Pedido_Endereco (endereco_PK,tipo_logradouro,numero,municipio,nome_logradouro,bairro,cep,estado)
    VALUES
    (55337, 'Rua', 579, 'Anápolis', 'Tuiuti', 'Vila Esperança', 75133460, 'Goiás'),
    (42555, 'Rua', 321, 'Anápolis', 'Guararapes', 'Vila Esperança', 75133540, 'Goiás'),
    (20945, 'Rua', 968, 'Santa Maria', 'QR 100', 'Conjunto Y', 72500432, 'Distrito Federal'),
    (84632, 'Rua', 234, 'Santa Maria', 'AC 101', 'Conjunto AC', 72501104, 'Distrito Federal'),
    (30396, 'Rua', 138, 'Itumirim', 'São José', 'Centro', 37210000, 'Minas Gerais'),
    (21162, 'Avenida', 180, 'Itumirim', 'Dom Inocêncio', 'A Definir', 37210000, 'Minas Gerais'),
    (62295, 'Rua', 502, 'Itapevi', 'Luso', 'Condomínio Refúgio dos Pinheiros', 06690520, 'São Paulo'),
    (62465, 'Estrada', 529, 'Itapevi', 'Diego Dias', 'Jardim Nova Itapevi', 06690120, 'São Paulo'),
    (82017, 'Rua', 301, 'São Paulo', 'Goivos', 'Cidade Jardim', 05675080, 'São Paulo'),
    (30928, 'Rua', 153, 'São Paulo', 'Malvas', 'Cidade Jardim', 05673000, 'São Paulo');

    INSERT INTO ENTREGADOR_PEDIDO (fk_entregador_cpf,fk_pedido_codigo,data,codigo,fk_endereco_endereco_PK)
    VALUES
    (13756003437, 626, '2021-10-27', 4143, 55337),
    (32368942621, 179, '2020-12-22', 4376, 42555),
    (32368942621, 406, '2021-02-22', 4375, 20945),
    (51292729755, 271, '2020-03-28', 6978, 84632),
    (51292729755, 500, '2019-11-28', 6973, 30396),
    (96104491844, 389, '2020-11-13', 2532, 21162),
    (53327782904, 745, '2020-01-16', 9395, 62295),
    (32368942621, 578, '2021-05-03', 8304, 62465),
    (96104491844, 674, '2021-07-20', 6377, 82017),
    (13756003437, 300, '2020-06-14', 8125, 30928);

    INSERT INTO PRODUTO_FABRICANTE (fk_fabricante_cnpj,fk_produto_codigo)
    VALUES
    (05161069000110 ,694),
    (05161069000110 ,720),
    (57507378000608 ,145),
    (57507378000608 ,909),
    (02814497000700 ,266),
    (02814497000700 ,247),
    (61190096000869 ,920),
    (61190096000869 ,523),
    (60665981000207 ,740),
    (60665981000207 ,280);

### 9. TABELAS E PRINCIPAIS CONSULTAS
   #### 9.1 CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas)

    Select * from cliente;


![Image](https://user-images.githubusercontent.com/116188500/198843989-196f5589-74dc-4585-b16a-5374bf7e65da.png)


    Select * from cliente_pedido;


![Image](https://user-images.githubusercontent.com/116188500/198844026-eece567d-6ebb-4151-8ce3-8a0ed52780df.png)


    Select * from cliente_telefone;


![Image](https://user-images.githubusercontent.com/116188500/198844046-6dcc947c-a1b3-4a99-a0a8-11b101c5ada4.png)


    Select * from entregador;


![Image](https://user-images.githubusercontent.com/116188500/198844103-bb90df0b-b10c-449a-85a1-1720a092088d.png)


    Select * from entregador_pedido;


![Image](https://user-images.githubusercontent.com/116188500/198844112-8abb3702-2683-42bc-8601-940985050dcc.png)


    Select * from Entregador_Pedido_Endereco;


![Image](https://user-images.githubusercontent.com/116188500/198844152-5589e4ab-09ec-4231-a0fe-554e7fa759cf.png)


    Select * from entregador_telefone;


![Image](https://user-images.githubusercontent.com/116188500/198844165-4cc6e126-7758-4e87-8d36-097bacc8d061.png)


    Select * from fabricante;


![Image](https://user-images.githubusercontent.com/116188500/198844524-bf9f957b-1f42-4bbe-9222-cea76576fbe5.png)


    Select * from fabricante_email;


![Image](https://user-images.githubusercontent.com/116188500/198844553-e4a423ef-9fca-40f9-8fd7-7431c63684de.png)


    Select * from Fabricante_Endereco;


![Image](https://user-images.githubusercontent.com/116188500/198854990-8f39846e-5806-49b6-a1ab-2ed7fcde5189.png)


    Select * from fabricante_telefone;


![Image](https://user-images.githubusercontent.com/116188500/198855000-ae958901-e8a0-4c27-accd-486e265df65b.png)


    Select * from pedido;


![Image](https://user-images.githubusercontent.com/116188500/198855010-cd6f3a3c-3ba6-466d-9b9d-5caadf02724e.png)


    Select * from pedido_produto;


![Image](https://user-images.githubusercontent.com/116188500/198855018-647e4a87-fa93-49de-b59c-823ab63c86a4.png)


    Select * from produto;


![Image](https://user-images.githubusercontent.com/116188500/198855030-49d0b2b5-f6ca-4abd-aa9c-7fd2422c3950.png)


    Select * from produto_fabricante;


![Image](https://user-images.githubusercontent.com/116188500/198855042-a97864a7-ca18-4cd8-8795-1ea0d400dc73.png)

   #### 9.2 CONSULTAS DAS TABELAS COM FILTROS WHERE
   #### 9.3 CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
   #### 9.4 CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12)
   #### 9.5 INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)
   #### 9.6 CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)
   #### 9.7 CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)
   #### 9.8 CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)
   #### 9.9 CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)
   #### 9.10 SUBCONSULTAS (Mínimo 4)
