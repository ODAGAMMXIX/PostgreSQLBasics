# PostgreSQLBasics
PostgreSQL Exercises
![image](https://github.com/user-attachments/assets/f13e8b94-ff2a-4c2a-b5e2-b3d7e534e408)

No modelo relacional ilustrado na figura acima, a tabela viagem deverá armazenar informações sobre as viagens realizadas a serviço, incluindo o carro utilizado, o motorista responsável e a pessoa a ser transportada. Devem ser ainda registrados detalhes como o destino, data e hora do início e do fim da viagem, preservando a consistência temporal dos valores referentes ao início e ao fim da viagem.

Diante do exposto, pede-se:

a) especifique atributos, tipos e restrições da tabela viagem;

#### a) Especificação de atributos, tipos e restrições da tabela viagem
- **ID_Viagem**: INT, PRIMARY KEY, AUTO_INCREMENT
- **Carro_ID**: INT, NOT NULL (Foreign Key que referencia a tabela **carro**)
- **Motorista_ID**: INT, NOT NULL (Foreign Key que referencia a tabela **motorista**)
- **Passageiro_ID**: INT, NOT NULL (Foreign Key que referencia a tabela **passageiro**)
- **Destino**: VARCHAR(255), NOT NULL
- **Data_Inicio**: DATETIME, NOT NULL
- **Data_Fim**: DATETIME, NOT NULL
- **Consistência_Temporal**: CHECK (Data_Fim > Data_Inicio)

b) especifique restrições no relacionamento entre as tabelas;

#### b) Especificação de restrições no relacionamento entre as tabelas
- **Foreign Keys**:
  - **Carro_ID**: Referencia o **ID** da tabela **carro**.
  - **Motorista_ID**: Referencia o **ID** da tabela **motorista**.
  - **Passageiro_ID**: Referencia o **ID** da tabela **passageiro**.

c) Elabore consulta SQL para inserir valores ao iniciar a viagem

#### c) Elaboração de consulta SQL para inserir valores ao iniciar a viagem
```sql
INSERT INTO viagem (Carro_ID, Motorista_ID, Passageiro_ID, Destino, Data_Inicio, Data_Fim)
VALUES (1, 2, 3, 'Centro de São Paulo', '2025-03-13 09:00:00', '2025-03-13 11:00:00');
```

### SQL (regular)
```sql
-- Criação do banco de dados
CREATE DATABASE IF NOT EXISTS viagens_db;
USE viagens_db;

-- Criação da tabela carro
CREATE TABLE carro (
    Carro_ID INT PRIMARY KEY AUTO_INCREMENT,
    Modelo VARCHAR(100) NOT NULL,
    Placa VARCHAR(10) NOT NULL
);

-- Criação da tabela motorista
CREATE TABLE motorista (
    Motorista_ID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    CNH VARCHAR(20) NOT NULL
);

-- Criação da tabela passageiro
CREATE TABLE passageiro (
    Passageiro_ID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    RG VARCHAR(20) NOT NULL
);

-- Criação da tabela viagem
CREATE TABLE viagem (
    ID_Viagem INT PRIMARY KEY AUTO_INCREMENT,
    Carro_ID INT NOT NULL,
    Motorista_ID INT NOT NULL,
    Passageiro_ID INT NOT NULL,
    Destino VARCHAR(255) NOT NULL,
    Data_Inicio DATETIME NOT NULL,
    Data_Fim DATETIME NOT NULL,
    CHECK (Data_Fim > Data_Inicio), -- preservando a consistência temporal dos valores referentes ao início e ao fim da viagem.
    FOREIGN KEY (Carro_ID) REFERENCES carro(Carro_ID),
    FOREIGN KEY (Motorista_ID) REFERENCES motorista(Motorista_ID),
    FOREIGN KEY (Passageiro_ID) REFERENCES passageiro(Passageiro_ID)
);

-- Inserção de dados de exemplo
INSERT INTO carro (Modelo, Placa) VALUES ('Toyota Corolla', 'ABC1234');
INSERT INTO motorista (Nome, CNH) VALUES ('João Silva', '1234567890');
INSERT INTO passageiro (Nome, RG) VALUES ('Maria Souza', 'MG1234567');

-- Inserção de um valor inicial na tabela viagem
INSERT INTO viagem (Carro_ID, Motorista_ID, Passageiro_ID, Destino, Data_Inicio, Data_Fim)
VALUES (1, 1, 1, 'Centro de São Paulo', '2025-03-13 09:00:00', '2025-03-13 11:00:00');
```
### POSTGRESQL
```sql
-- Criação do banco de dados
CREATE DATABASE viagens_db;
\c viagens_db

-- Criação da tabela carro
CREATE TABLE carro (
    Carro_ID SERIAL PRIMARY KEY,
    Modelo VARCHAR(100) NOT NULL,
    Placa VARCHAR(10) NOT NULL
);

-- Criação da tabela motorista
CREATE TABLE motorista (
    Motorista_ID SERIAL PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    CNH VARCHAR(20) NOT NULL
);

-- Criação da tabela passageiro
CREATE TABLE passageiro (
    Passageiro_ID SERIAL PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    RG VARCHAR(20) NOT NULL
);

-- Criação da tabela viagem
CREATE TABLE viagem (
    ID_Viagem SERIAL PRIMARY KEY,
    Carro_ID INT NOT NULL,
    Motorista_ID INT NOT NULL,
    Passageiro_ID INT NOT NULL,
    Destino VARCHAR(255) NOT NULL,
    Data_Inicio TIMESTAMP NOT NULL,
    Data_Fim TIMESTAMP NOT NULL,
    CHECK (Data_Fim > Data_Inicio), --  preservando a consistência temporal dos valores referentes ao início e ao fim da viagem.
    FOREIGN KEY (Carro_ID) REFERENCES carro(Carro_ID),
    FOREIGN KEY (Motorista_ID) REFERENCES motorista(Motorista_ID),
    FOREIGN KEY (Passageiro_ID) REFERENCES passageiro(Passageiro_ID)
);

-- Inserção de dados de exemplo
INSERT INTO carro (Modelo, Placa) VALUES ('Toyota Corolla', 'ABC1234');
INSERT INTO motorista (Nome, CNH) VALUES ('João Silva', '1234567890');
INSERT INTO passageiro (Nome, RG) VALUES ('Maria Souza', 'MG1234567');

-- Inserção de um valor inicial na tabela viagem
INSERT INTO viagem (Carro_ID, Motorista_ID, Passageiro_ID, Destino, Data_Inicio, Data_Fim)
VALUES (1, 1, 1, 'Centro de São Paulo', '2025-03-13 09:00:00', '2025-03-13 11:00:00');
```
