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

A farmácia "WLD" conterá as informações aqui detalhadas. Da PESSOA, será registrado codigo e nome. Do CONTATO, será registrado codigo, tipo_contato e contato. Do CLIENTE, será registrado data_nascimento e cpf. Do ENTREGADOR, será registrado salario e cpf. Do FABRICANTE, será registrado cnpj. Do PEDIDO, será registrado codigo e valor_total. Do PRODUTO, será registrado codigo, nome e preco. Do ENDERECO, será registrado codigo, tipo_logradouro, numero, municipio, bairro, cep, estado e nome_logradouro. Por fim, na entrega do PEDIDO pelo ENTREGADOR é registrada a data. Uma PESSOA possui um ou vários contatos e um CONTATO pertence a apenas uma PESSOA. Um CLIENTE realiza  um ou vários pedidos e um PEDIDO é realizado por apenas um CLIENTE. Um ENTREGADOR entrega um ou vários pedidos e um PEDIDO é entregue por apenas um entregador. Um FABEBRICANTE possui um ou vários produtos e um PRODUTO possui apenas um fabricante. Um PEDIDO possui um ou vários produtos e um PRODUTO pode estar inserido em nenhum ou vários pedidos. Um FABRICANTE possui um ou vários endereços e um ENDERECO só pode pertencer a um fabricante. Um PEDIDO pode possuir apenas um endereço e um ENDERECO pode pertencer a um ou vários pedidos.

### 4.PERGUNTAS A SEREM RESPONDIDAS E TABELA DE DADOS
   #### 4.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?    
   - Nesse sistema é possível gerar relatórios com a quantidade de cada produto que está sendo adicionado aos pedidos. 
   - Nesse sistema é possível saber a quantidade de produtos de cada fabricante que estão sendo adicionados aos pedidos.
   - Nesse sistema é possível saber em qual ano ou época do ano está tendo mais vendas.
   - Nesse sistema é possível gerar relatórios sobre o valor total dos produtos, sabendo assim em qual período houve mais lucro.
   - Nesse sistema é possível gerar relatórios sobre quantos pedidos estão sendo entregues por cada entregador.
    
### 5. MODELO CONCEITUAL

![image](https://user-images.githubusercontent.com/116188500/205468090-bf92ec0a-e507-4575-95b8-59ae4cddd479.png)

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

![image](https://user-images.githubusercontent.com/116188500/205468111-f9c65cc4-844f-4af9-93f6-4d96619b03a1.png)

### 7. MODELO FÍSICO

      DROP TABLE IF EXISTS PESSOA CASCADE;
      CREATE TABLE PESSOA (
          codigo INT PRIMARY KEY,
          nome VARCHAR
      );

      DROP TABLE IF EXISTS CLIENTE CASCADE;
      CREATE TABLE CLIENTE (
          FK_PESSOA_codigo INT PRIMARY KEY REFERENCES PESSOA (codigo),
          cpf BIGINT,
          data_nascimento DATE
      );

      DROP TABLE IF EXISTS ENTREGADOR CASCADE;
      CREATE TABLE ENTREGADOR (
          FK_PESSOA_codigo INT PRIMARY KEY REFERENCES PESSOA (codigo),
          salario DOUBLE PRECISION,
          cpf BIGINT
      );

      DROP TABLE IF EXISTS ENDERECO CASCADE;
      CREATE TABLE ENDERECO (
          codigo INT PRIMARY KEY,
          tipo_logradouro VARCHAR,
          numero INT,
          municipio VARCHAR,
          nome_logradouro VARCHAR,
          bairro VARCHAR,
          cep BIGINT,
          estado VARCHAR
      );

      DROP TABLE IF EXISTS CONTATO CASCADE;
      CREATE TABLE CONTATO (
          codigo INT PRIMARY KEY,
          FK_PESSOA_codigo INT REFERENCES PESSOA (codigo),
          tipo_contato VARCHAR,
          contato VARCHAR
      );

      DROP TABLE IF EXISTS FABRICANTE CASCADE;
      CREATE TABLE FABRICANTE (
          FK_PESSOA_codigo INT PRIMARY KEY REFERENCES PESSOA (codigo),
          FK_ENDERECO_codigo INT REFERENCES ENDERECO (codigo),
          cnpj BIGINT
      );

      DROP TABLE IF EXISTS PRODUTO CASCADE;
      CREATE TABLE PRODUTO (
          codigo INT PRIMARY KEY,
          FK_FABRICANTE_FK_PESSOA_codigo INT REFERENCES FABRICANTE (FK_PESSOA_codigo),
          preco DOUBLE PRECISION,
          nome VARCHAR
      );

      DROP TABLE IF EXISTS PEDIDO CASCADE;
      CREATE TABLE PEDIDO (
          codigo INT PRIMARY KEY,
          FK_CLIENTE_FK_PESSOA_codigo INT REFERENCES CLIENTE (FK_PESSOA_codigo),
          FK_ENDERECO_codigo INT REFERENCES ENDERECO (codigo),
          FK_ENTREGADOR_FK_PESSOA_codigo INT REFERENCES ENTREGADOR (FK_PESSOA_codigo),
          valor_total DOUBLE PRECISION,
          data DATE
      );

      DROP TABLE IF EXISTS Pedido_Produto CASCADE;
      CREATE TABLE Pedido_Produto (
          fk_PRODUTO_codigo INT REFERENCES PRODUTO (codigo),
          fk_PEDIDO_codigo INT REFERENCES PEDIDO (codigo),
          quantidade INT
      );


### 8. INSERT APLICADO NAS TABELAS DO BANCO DE DADOS

      INSERT INTO PESSOA (CODIGO, NOME)
      VALUES
          /*Cliente*/
          (10, 'Imelda Wong'),
          (11, 'Scarlett Weber'),
          (12, 'Emi Hunter'),
          (13, 'Rana Riddle'),
          (14, 'Cruz Farley'),
          (15, 'Ria Montoya'),
          (16, 'Patricia Pruitt'),
          (17, 'Anastasia Stanton'),
          (18, 'Keefe Atkinson'),
          (19, 'Uriel Dickson'),
          /*Entregador*/
          (20, 'Hillary Shepherd'),
          (21, 'Lacota Barnes'),
          (22, 'Ima Nixon'),
          (23, 'Hiroko Whitney'),
          (24, 'Carlos Barrett'),
          /*Fabricante*/
          (25, 'Neo Química'),
          (26, 'EMS'),
          (27, 'Cimed'),
          (28, 'Eurofarma'),
          (29, 'União Química');

      INSERT INTO CLIENTE (FK_PESSOA_codigo, CPF, data_nascimento)
      VALUES
          (10, 54690831916, '1980-01-13'),
          (11, 92077224684, '2005-11-13'),
          (12, 34633306292, '2000-10-27'),
          (13, 58596061431, '1965-01-25'),
          (14, 61142416604, '1997-05-17'),
          (15, 60202318666, '1995-10-30'),
          (16, 96116796203, '1960-07-28'),
          (17, 76299908511, '1981-06-13'),
          (18, 59600170651, '1950-03-27'),
          (19, 65782808488, '1973-04-20');

      INSERT INTO ENTREGADOR (FK_PESSOA_codigo, salario, CPF)
      VALUES
          (20, 1132.23, 13756003437),
          (21, 906.55, 32368942621),
          (22, 2754.12, 51292729755),
          (23, 1546.41, 96104491844),
          (24, 2123.89, 53327782904);

      INSERT INTO ENDERECO (CODIGO, nome_logradouro, bairro, estado, cep, numero, tipo_logradouro, municipio)
      VALUES
          (981560, 'Vp-R3', 'DISTRITO AGROINDUSTRIAL DE ANAPOLIS', 'Goiás', 75132015, 1283, 'Rua', 'Anapolis'),
          (832479, 'Polo de Desenvolvimento Juscelino Kubitschek Trech', 'SANTA MARIA', 'Distrito Federal', 72549550, 5304, 'Loteamento', 'Brasília'),
          (713388, 'Amg 1920', 'Galpao1', 'Minas Gerais', 37567000, 3943, 'Rodovia', 'São Sebastião da Bela Vista'),
          (334297, 'Presidente Castelo Branco', 'INGAHI', 'São Paulo', 16696000, 3565, 'Rodovia', 'Itapevi'),
          (595106, 'Magalhaes de Castro', 'Cidade Jardim', 'São Paulo', 15676120, 4800, 'Avenida', 'São Paulo'),

          (553371, 'Tuiuti', 'Vila Esperança', 'Goiás', 75133460, 579, 'Rua', 'Anápolis'),
          (425552, 'Guararapes', 'Vila Esperança', 'Goiás', 75133540, 321, 'Rua', 'Anápolis'),
          (209453, 'QR 100', 'Conjunto Y', 'Distrito Federal', 72500432, 968, 'Rua', 'Santa Maria'),
          (846324, 'AC 101', 'Conjunto AC', 'Distrito Federal', 72501104, 234, 'Rua', 'Santa Maria'),
          (303965, 'São José', 'Centro', 'Minas Gerais', 37210000, 138, 'Rua', 'Itumirim'),
          (211626, 'Dom Inocêncio', 'A Definir', 'Minas Gerais', 37210000, 180, 'Avenida', 'Itumirim'),
          (622957, 'Luso', 'Condomínio Refúgio dos Pinheiros', 'São Paulo', 16690520, 502, 'Rua', 'Itapevi'),
          (624658, 'Diego Dias', 'Jardim Nova Itapevi', 'São Paulo', 16690120, 529, 'Estrada', 'Itapevi'),
          (820179, 'Goivos', 'Cidade Jardim', 'São Paulo', 15675080, 301, 'Rua', 'São Paulo'),
          (309280, 'Malvas', 'Cidade Jardim', 'São Paulo', 15673000, 153, 'Rua', 'São Paulo')



      INSERT INTO CONTATO (CODIGO, FK_PESSOA_codigo, tipo_contato, CONTATO)
      VALUES
          /*Fabricante_Telefone*/
          (3731, 25, 'Telefone', '6238788150'),
          (9193, 25, 'Telefone', '6238788234'),
          (6240, 26, 'Telefone', '1938879800'),
          (9393, 27, 'Telefone', '1135447350'),
          (4576, 28, 'Telefone', '1150908600'),
          (6806, 29, 'Telefone', '1155862000'),
          (6142, 29, 'Telefone', '1155862120'),
          /*Fabricante_Email*/
          (4654, 25, 'Email', 'fiscal@brainfarma.ind.br'),
          (3372, 26, 'Email', 'wagner@gruponc.net.br'),
          (5793, 26, 'Email', 'programadevisitas@ems.com.br'),
          (9364, 27, 'Email', 'tributario@grupocimed.com.br'),
          (8290, 28, 'Email', 'contencioso.fiscal@eurofarma.com.br'),
          (4151, 29, 'Email', 'ca-fiscal@uniaoquimica.com.br'),
          /*Cliente_Telefone*/
          (7510, 10, 'Telefone', '970190276'),
          (8633, 10, 'Telefone', '980300504'),
          (8632, 11, 'Telefone', '949138088'),
          (8815, 12, 'Telefone', '999945176'),
          (5668, 12, 'Telefone', '925680861'),
          (3103, 13, 'Telefone', '974209776'),
          (9896, 14, 'Telefone', '957793668'),
          (5935, 15, 'Telefone', '956902521'),
          (4836, 15, 'Telefone', '958740237'),
          (8451, 16, 'Telefone', '977235674'),
          (2160, 16, 'Telefone', '957818092'),
          (8879, 17, 'Telefone', '937623463'),
          (9454, 18, 'Telefone', '929855588'),
          (9202, 18, 'Telefone', '990437656'),
          (9544, 19, 'Telefone', '987125117'),
          /*Entregador_Telefone*/
          (1469, 20, 'Telefone', '994974686'),
          (4149, 20, 'Telefone', '913301515'),
          (4823, 21, 'Telefone', '939204786'),
          (4280, 22, 'Telefone', '977216975'),
          (4952, 22, 'Telefone', '951993534'),
          (6315, 23, 'Telefone', '991308985'),
          (6993, 24, 'Telefone', '955491364');

      INSERT INTO FABRICANTE (FK_PESSOA_codigo, FK_ENDERECO_codigo, CNPJ)
      VALUES
          (25, 981560, 15161069000110),
          (26, 832479, 57507378000608),
          (27, 713388, 12814497000700),
          (28, 334297, 61190096000869),
          (29, 595106, 60665981000207);

      INSERT INTO PRODUTO (CODIGO, FK_FABRICANTE_FK_PESSOA_codigo, PRECO, NOME)
      VALUES
          (694, 25, 6.49, 'Paracetamol'),
          (720, 25, 19.90, 'Vitamina A-Z'),
          (145, 26, 8.99, 'Losartana Potássica'),
          (909, 26, 36.42, 'Somalgin Cardio'),
          (266, 27, 47.90, 'Ômega 3'),
          (247, 27, 38.90, 'Cálcio MDK'),
          (920, 28, 43.20, 'Aciclovir'),
          (523, 28, 84.24, 'Azitromicina'),
          (740, 29, 16.00, 'Bromazepam'),
          (280, 29, 29.90, 'Cloridrato de Tramadol');

      INSERT INTO PEDIDO (CODIGO, FK_CLIENTE_FK_PESSOA_codigo, FK_ENDERECO_codigo, FK_ENTREGADOR_FK_PESSOA_codigo, valor_total, DATA)
      VALUES
          (20053, 10, 553371, 20, 25.96, '2020-01-20'),
          (29962, 11, 425552, 20, 39.80, '2020-02-13'),
          (63240, 12, 209453, 21, 26.97, '2021-03-12'),
          (17778, 13, 846324, 21, 36.42, '2021-04-30'),
          (11580, 14, 303965, 22, 95.80, '2022-05-27'),
          (30645, 15, 211626, 22, 116.70, '2022-06-17'),
          (70175, 16, 622957, 23, 43.20, '2020-07-28'),
          (81603, 17, 624658, 23, 168.48, '2021-08-15'),
          (63886, 18, 820179, 24, 80.00, '2022-09-11'),
          (79646, 19, 309280, 24, 59.80, '2022-10-03');


      INSERT INTO Pedido_Produto (fk_PRODUTO_codigo, fk_PEDIDO_codigo, quantidade)
      VALUES
          (694, 20053, 4),
          (720, 29962, 3),
          (145, 63240, 2),
          (909, 17778, 1),
          (266, 11580, 2),
          (247, 30645, 3),
          (920, 70175, 1),
          (523, 81603, 2),
          (740, 63886, 5),
          (280, 79646, 2);

### 9. TABELAS E PRINCIPAIS CONSULTAS
   #### 9.1 CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas)

      select * from PRODUTO;
      
      select * from PEDIDO;
      
      select * from PESSOA;
      
      select * from CLIENTE;
      
      select * from ENTREGADOR;
      
      select * from ENDERECO;
      
      select * from CONTATO;
      
      select * from FABRICANTE;
      
      select * from Pedido_Produto;
      
      

   #### 9.2 CONSULTAS DAS TABELAS COM FILTROS WHERE
   
   #### 9.3 CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS
   
   #### 9.4 CONSULTAS QUE USAM OPERADORES LIKE E DATAS
   #### 9.5 INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS
   #### 9.6 CONSULTAS COM INNER JOIN E ORDER BY 
   #### 9.7 CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO 
   #### 9.8 CONSULTAS COM LEFT, RIGHT E FULL JOIN 
   #### 9.9 CONSULTAS COM SELF JOIN E VIEW 
   #### 9.10 SUBCONSULTAS 
   
   ### 10 RELATÓRIOS E GRÁFICOS
   
   ### 11 SLIDES E VÍDEO PARA APRESENTAÇAO FINAL
   
   
