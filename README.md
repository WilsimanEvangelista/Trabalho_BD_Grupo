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

A farmácia "WLD" conterá as informações aqui detalhadas. Do FABRICANTE será registrado CNPJ, nome, telefone, email. Do PRODUTO será registrado código, nome, preço. Do PEDIDO será registrado código, valor_total. Do CLIENTE  será registrado data_nascimento e herdará os dados cpf, nome e telefone de PESSOA. Do ENTREGADOR será registrado salario e herdará os dados cpf, nome e telefone de PESSOA. Da ENTREGA será registrado código e data de entrega. Do ENDERECO será registrado codigo, tipo_logradouro, numero, municipio, bairro, cep, estado e nome_logradouro.
Ao produto ser adicionado a um pedido, deve-se informar a quantidade de produtos de uma mesma classe que foi adicionado. Pedido possui de um a vários produtos e um produto deve estar inserido em um ou vários pedidos. O fabricante deve possuir um ou vários produtos e um produto deve possuir apenas um fabricante. Um cliente deve realizar um ou vários pedidos e um pedido pode ter sido realizado por apenas um cliente. Um entregador realiza nenhuma ou várias entregas e uma entrega pode ser realizada por apenas um entregador. Um pedido possui apenas um endereco e um endereco pode possuir um ou vários pedidos. Por fim, um fabricante possui um ou vários enderecos e um endereco possui apenas um fabricante.

### 4.PERGUNTAS A SEREM RESPONDIDAS E TABELA DE DADOS
   #### 4.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?    
   - Nesse sistema é possível gerar relatórios com a quantidade de cada produto que está sendo adicionado aos pedidos. 
   - Nesse sistema é possível saber a quantidade de produtos de cada fabricante que estão sendo adicionados aos pedidos.
   - Nesse sistema é possível saber em qual ano ou época do ano está tendo mais vendas.
   - Nesse sistema é possível gerar relatórios sobre o valor total dos produtos, sabendo assim em qual período houve mais lucro.
   - Nesse sistema é possível gerar relatórios sobre quantos pedidos estão sendo entregues por cada entregador.
    
### 5. MODELO CONCEITUAL

![image](https://user-images.githubusercontent.com/116188500/202016087-dde6659d-4451-4a73-9a61-e41aa4c0f6dd.png)

 #### 5.1 Validação do Modelo Conceitual
 #### 5.2 Descrição dos dados
 
 PESSOA: Tabela que armazena informações sobre as pessoas presentes no modelo. </br>
 CLIENTE: Tabela que armazena informações referentes ao cliente. </br>
 ENTREGADOR: Tabela que armazena informações referentes ao entregador. </br>
 ENTREGA: Tabela que armazena informações sobre a entrega que será realizada pelo entregador. </br>
 FABRICANTE: Tabela que armazena informações referentes ao fabricante. </br>
 PRODUTO: Tabela que armazena informações referentes ao produto. </br>
 PEDIDO: Tabela que armazena informações referentes ao pedido. </br>
 ENDERECO: Tabela que armazena informações sobre os endereços necessários. </br>
 Fabricante_Telefone: Tabela que relaciona o fabricante a seu(s) telefone(s). </br>
 Fabricante_Email: Tabela que relaciona o fabricante a seu(s) email(s). </br>
 Pessoa_Telefone: Tabela que relaciona a Pessoa a seu(s) telefone(s). </br>
 Cliente_Pedido: Tabela que relaciona o cliente a seu pedido. </br>
 Pedido_Produto: Tabela que relaciona o pedido ao produto que foi inserido nele. </br>
 Fabricante_Produto: Tabela que relaciona o Fabricante ao(s) produto(s) que ele possui. </br>
 Entregador_Entrega: Tabela que relaciona o Entregador a Entrega que ele realizará. </br>
 Pedido_Endereco: Tabela que relaciona o pedido ao endereço requerido nele. </br>
 Fabricante_Endereco: Tabela que relaciona o fabricante a seu endereço. </br>
 
### 6. MODELO LÓGICO

![image](https://user-images.githubusercontent.com/116188500/202015959-7f0b538e-8e11-47dc-80b4-2623dcf3f16b.png)

### 7. MODELO FÍSICO

      DROP TABLE IF EXISTS FABRICANTE CASCADE;
      CREATE TABLE FABRICANTE (
          CNPJ BIGINT PRIMARY KEY,
          nome VARCHAR
      );

      DROP TABLE IF EXISTS PRODUTO CASCADE;
      CREATE TABLE PRODUTO (
          codigo INT PRIMARY KEY,
          preco DOUBLE PRECISION,
          nome VARCHAR
      );


      DROP TABLE IF EXISTS PEDIDO CASCADE;
      CREATE TABLE PEDIDO (
          codigo INT PRIMARY KEY,
          valor_total DOUBLE PRECISION
      );

      DROP TABLE IF EXISTS PESSOA CASCADE;
      CREATE TABLE PESSOA (
          cpf BIGINT PRIMARY KEY,
          nome VARCHAR
      );

      DROP TABLE IF EXISTS CLIENTE CASCADE;
      CREATE TABLE CLIENTE (
          FK_PESSOA_cpf BIGINT PRIMARY KEY REFERENCES PESSOA (CPF),
          data_nascimento DATE
      );

      DROP TABLE IF EXISTS ENTREGADOR CASCADE;
      CREATE TABLE ENTREGADOR (
          FK_PESSOA_cpf BIGINT PRIMARY KEY REFERENCES PESSOA (CPF),
          salario DOUBLE PRECISION
      );

      DROP TABLE IF EXISTS ENTREGA CASCADE;
      CREATE TABLE ENTREGA (
          codigo INT PRIMARY KEY,
          data DATE
      );

      DROP TABLE IF EXISTS ENDERECO CASCADE;
      CREATE TABLE ENDERECO (
          codigo INT PRIMARY KEY,
          nome_logradouro VARCHAR,
          bairro VARCHAR,
          estado VARCHAR,
          cep BIGINT,
          numero INT,
          tipo_logradouro VARCHAR,
          municipio VARCHAR    
      );

      DROP TABLE IF EXISTS FABRICANTE_TELEFONE CASCADE;
      CREATE TABLE FABRICANTE_TELEFONE (
          fk_FABRICANTE_cnpj BIGINT REFERENCES FABRICANTE (CNPJ),
          telefone BIGINT
      );

      DROP TABLE IF EXISTS FABRICANTE_EMAIL CASCADE;
      CREATE TABLE FABRICANTE_EMAIL (
          fk_FABRICANTE_cnpj BIGINT REFERENCES FABRICANTE (CNPJ),
          email VARCHAR
      );

      DROP TABLE IF EXISTS PESSOA_TELEFONE CASCADE;
      CREATE TABLE PESSOA_TELEFONE (
          fk_PESSOA_cpf BIGINT NOT NULL REFERENCES PESSOA (CPF),
          telefone BIGINT
      );

      DROP TABLE IF EXISTS CLIENTE_PEDIDO CASCADE;
      CREATE TABLE CLIENTE_PEDIDO (
          fk_CLIENTE_FK_PESSOA_cpf BIGINT REFERENCES CLIENTE (FK_PESSOA_cpf),
          fk_PEDIDO_codigo INT REFERENCES PEDIDO (codigo)
      );

      DROP TABLE IF EXISTS PEDIDO_PRODUTO CASCADE;
      CREATE TABLE PEDIDO_PRODUTO (
          fk_PEDIDO_codigo INT REFERENCES PEDIDO (codigo),
          fk_PRODUTO_codigo INT REFERENCES PRODUTO (codigo),
          quantidade INT
      );

      DROP TABLE IF EXISTS FABRICANTE_PRODUTO CASCADE;
      CREATE TABLE FABRICANTE_PRODUTO (
          fk_FABRICANTE_CNPJ BIGINT REFERENCES FABRICANTE (CNPJ),
          fk_PRODUTO_codigo INT REFERENCES PRODUTO (codigo)
      );

      DROP TABLE IF EXISTS ENTREGADOR_ENTREGA CASCADE;
      CREATE TABLE ENTREGADOR_ENTREGA (
          fk_ENTREGADOR_FK_PESSOA_cpf BIGINT REFERENCES ENTREGADOR (FK_PESSOA_cpf),
          fk_ENTREGA_codigo INT REFERENCES ENTREGA (codigo)
      );

      DROP TABLE IF EXISTS PEDIDO_ENDERECO CASCADE;
      CREATE TABLE PEDIDO_ENDERECO (
          fk_ENDERECO_codigo INT REFERENCES ENDERECO (codigo),
          fk_PEDIDO_codigo INT REFERENCES PEDIDO (codigo)
      );

      DROP TABLE IF EXISTS FABRICANTE_ENDERECO CASCADE;
      CREATE TABLE FABRICANTE_ENDERECO (
          fk_FABRICANTE_CNPJ BIGINT REFERENCES FABRICANTE (CNPJ),
          fk_ENDERECO_codigo INT REFERENCES ENDERECO (codigo)
      );


### 8. INSERT APLICADO NAS TABELAS DO BANCO DE DADOS

      INSERT INTO FABRICANTE (cnpj,nome)
      VALUES
          (05161069000110, 'Neo Química'),
          (57507378000608, 'EMS'),
          (02814497000700, 'Cimed'),
          (61190096000869, 'Eurofarma'),
          (60665981000207, 'União Química');

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

      INSERT INTO PESSOA (cpf,nome)
      VALUES
          /*Cliente*/
          (54690831916, 'Imelda Wong'),
          (92077224684, 'Scarlett Weber'),
          (34633306292, 'Emi Hunter'),
          (58596061431, 'Rana Riddle'),
          (61142416604, 'Cruz Farley'),
          (60202318666, 'Ria Montoya'),
          (96116796203, 'Patricia Pruitt'),
          (76299908511, 'Anastasia Stanton'),
          (59600170651, 'Keefe Atkinson'),
          (65782808488, 'Uriel Dickson'),
          /*Entregador*/
          (13756003437, 'Hillary Shepherd'),
          (32368942621, 'Lacota Barnes'),
          (51292729755, 'Ima Nixon'),
          (96104491844, 'Hiroko Whitney'),
          (53327782904, 'Carlos Barrett');

      INSERT INTO CLIENTE (fk_PESSOA_cpf,data_nascimento)
      VALUES
          (54690831916, '1980-01-13'),
          (92077224684, '2005-11-13'),
          (34633306292, '2000-10-27'),
          (58596061431, '1965-01-25'),
          (61142416604, '1997-05-17'),
          (60202318666, '1995-10-30'),
          (96116796203, '1960-07-28'),
          (76299908511, '1981-06-13'),
          (59600170651, '1950-03-27'),
          (65782808488, '1973-04-20');

      INSERT INTO ENTREGADOR (fk_PESSOA_cpf,salario)
      VALUES
          (13756003437, 1132.23),
          (32368942621, 906.55),
          (51292729755, 2754.12),
          (96104491844, 1546.41),
          (53327782904, 2123.89);

      INSERT INTO ENTREGA (codigo,data)
      VALUES
          (435323,'2020-01-20'),
          (658745,'2020-02-13'),
          (585678,'2021-03-12'),
          (234567,'2021-04-30'),
          (876544,'2022-05-27'),
          (487865,'2022-06-17'),
          (137866,'2020-07-28'),
          (341893,'2021-08-15'),
          (976543,'2022-09-11'),
          (179356,'2022-10-03');

      INSERT INTO ENDERECO (codigo,nome_logradouro,bairro,estado,cep,numero,tipo_logradouro,municipio)
      VALUES
          /*Fabricante*/
          (98, 'Vp-R3', 'DISTRITO AGROINDUSTRIAL DE ANAPOLIS', 'Goiás', 75132015, 1283, 'Rua', 'Anapolis'),
          (83, 'Polo de Desenvolvimento Juscelino Kubitschek Trech', 'SANTA MARIA', 'Distrito Federal', 72549550, 5304, 'Loteamento', 'Brasília'),
          (71, 'Amg 1920', 'Galpao1', 'Minas Gerais', 37567000, 3943, 'Rodovia', 'São Sebastião da Bela Vista'),
          (33, 'Presidente Castelo Branco', 'INGAHI', 'São Paulo', 06696000, 3565, 'Rodovia', 'Itapevi'),
          (59, 'Magalhaes de Castro', 'Cidade Jardim', 'São Paulo', 05676120, 4800, 'Avenida', 'São Paulo'),
          /*Pedido*/
          (55337, 'Tuiuti', 'Vila Esperança', 'Goiás', 75133460, 579, 'Rua', 'Anápolis'),
          (42555, 'Guararapes', 'Vila Esperança', 'Goiás', 75133540, 321, 'Rua', 'Anápolis'),
          (20945, 'QR 100', 'Conjunto Y', 'Distrito Federal', 72500432, 968, 'Rua', 'Santa Maria'),
          (84632, 'AC 101', 'Conjunto AC', 'Distrito Federal', 72501104, 234, 'Rua', 'Santa Maria'),
          (30396, 'São José', 'Centro', 'Minas Gerais', 37210000, 138, 'Rua', 'Itumirim'),
          (21162, 'Dom Inocêncio', 'A Definir', 'Minas Gerais', 37210000, 180, 'Avenida', 'Itumirim'),
          (62295, 'Luso', 'Condomínio Refúgio dos Pinheiros', 'São Paulo', 06690520, 502, 'Rua', 'Itapevi'),
          (62465, 'Diego Dias', 'Jardim Nova Itapevi', 'São Paulo', 06690120, 529, 'Estrada', 'Itapevi'),
          (82017, 'Goivos', 'Cidade Jardim', 'São Paulo', 05675080, 301, 'Rua', 'São Paulo'),
          (30928, 'Malvas', 'Cidade Jardim', 'São Paulo', 05673000, 153, 'Rua', 'São Paulo');

      INSERT INTO FABRICANTE_TELEFONE (fk_fabricante_cnpj,telefone)
      VALUES
          (05161069000110, 6238788150),
          (05161069000110, 6238788234),
          (57507378000608, 1938879800),
          (02814497000700, 1135447350),
          (61190096000869, 1150908600),
          (60665981000207, 1155862000),
          (60665981000207, 1155862120);

      INSERT INTO FABRICANTE_EMAIL (fk_fabricante_cnpj,email)
      VALUES
          (05161069000110, 'fiscal@brainfarma.ind.br'),
          (57507378000608, 'wagner@gruponc.net.br'),
          (57507378000608, 'programadevisitas@ems.com.br'),
          (02814497000700, 'tributario@grupocimed.com.br'),
          (61190096000869, 'contencioso.fiscal@eurofarma.com.br'),
          (60665981000207, 'ca-fiscal@uniaoquimica.com.br');

      INSERT INTO PESSOA_TELEFONE (fk_PESSOA_cpf,telefone)
      VALUES
          /*Cliente*/
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
          (65782808488, 987125117),
          /*Entregador*/
          (13756003437, 994974686),
          (13756003437, 913301515),
          (32368942621, 939204786),
          (51292729755, 977216975),
          (51292729755, 951993534),
          (96104491844, 991308985),
          (53327782904, 955491364);

      INSERT INTO CLIENTE_PEDIDO (fk_CLIENTE_FK_PESSOA_cpf,fk_pedido_codigo)
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

      INSERT INTO FABRICANTE_PRODUTO (fk_fabricante_cnpj,fk_produto_codigo)
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

      INSERT INTO ENTREGADOR_ENTREGA (fk_ENTREGADOR_FK_PESSOA_cpf,fk_ENTREGA_codigo)
      VALUES
          (13756003437, 435323),
          (13756003437, 658745),
          (32368942621, 585678),
          (32368942621, 234567),
          (51292729755, 876544),
          (51292729755, 487865),
          (96104491844, 137866),
          (96104491844, 341893),
          (53327782904, 976543),
          (53327782904, 179356);

      INSERT INTO PEDIDO_ENDERECO (fk_ENDERECO_codigo,fk_pedido_codigo)
      VALUES
          (55337, 626),
          (42555, 179),
          (20945, 406),
          (84632, 271),
          (30396, 500),
          (21162, 389),
          (62295, 745),
          (62465, 578),
          (82017, 674),
          (30928, 300);

      INSERT INTO FABRICANTE_ENDERECO (fk_fabricante_cnpj,fk_ENDERECO_codigo)
      VALUES
          (05161069000110, 98),
          (57507378000608, 83),
          (02814497000700, 71),
          (61190096000869, 33),
          (60665981000207, 59);

### 9. TABELAS E PRINCIPAIS CONSULTAS
   #### 9.1 CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas)

      select * from cliente;
      
      
      select * from cliente_pedido;
      
      
      select * from endereco;
      
      
      select * from entrega;
      
      
      select * from entregador;
      
      
      select * from entregador_entrega;
      
      
      select * from fabricante;
      
      
      select * from fabricante_email;
      
      
      select * from fabricante_endereco;
      
      
      select * from fabricante_produto;
      
      
      select * from fabricante_telefone;
      
      
      select * from pedido;
      
      
      select * from pedido_endereco;
      
      
      select * from pedido_produto;
      
      
      select * from pessoa;
      
      
      select * from pessoa_telefone;
      
      
      select * from produto;
      
      

   #### 9.2 CONSULTAS DAS TABELAS COM FILTROS WHERE
   #### 9.3 CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
   #### 9.4 CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12)
   #### 9.5 INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)
   #### 9.6 CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)
   #### 9.7 CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)
   #### 9.8 CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)
   #### 9.9 CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)
   #### 9.10 SUBCONSULTAS (Mínimo 4)
   
   ### 10 RELATÓRIOS E GRÁFICOS
   
   ### 11 SLIDES E VÍDEO PARA APRESENTAÇAO FINAL
   
   
