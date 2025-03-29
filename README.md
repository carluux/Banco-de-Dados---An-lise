# Banco-de-Dados---An-lise
atividades de sala de aula de banco de dados

-- Criando o banco de dados 
CREATE DATABASE Empresa; 
USE Empresa;

-- Criando a tabela de Departamentos primeiro 
CREATE TABLE Departamentos ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    nome VARCHAR(100) NOT NULL 
);

-- Criando a tabela de Cargos primeiro 
CREATE TABLE Cargos ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    nome VARCHAR(100) NOT NULL, 
    nivel VARCHAR(50) NOT NULL 
);

-- Criando a tabela de Funcionários depois que as tabelas referenciadas existem 
CREATE TABLE Funcionarios ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    nome VARCHAR(100) NOT NULL, 
    data_nascimento DATE NOT NULL, 
    salario DECIMAL(10,2) NOT NULL, 
    departamento_id INT NOT NULL, 
    cargo_id INT NOT NULL, 
    FOREIGN KEY (departamento_id) REFERENCES Departamentos(id), 
    FOREIGN KEY (cargo_id) REFERENCES Cargos(id) 
);

-- Inserindo dados na tabela Departamentos 
INSERT INTO Departamentos (nome) VALUES 
('TI'), 
('RH'), 
('Financeiro'), 
('Marketing'), 
('Vendas');

-- Inserindo dados na tabela Cargos 
INSERT INTO Cargos (nome, nivel) VALUES 
('Analista', 'Pleno'), 
('Gerente', 'Sênior'), 
('Assistente', 'Júnior'), 
('Coordenador', 'Sênior'), 
('Desenvolvedor', 'Pleno');

-- Inserindo dados na tabela Funcionarios 
INSERT INTO Funcionarios (nome, data_nascimento, salario, departamento_id, cargo_id) VALUES 
('Ana Silva', '1985-06-15', 5500.00, 1, 5), 
('Carlos Santos', '1990-03-22', 4800.00, 2, 1), 
('Bruna Costa', '1987-12-10', 6000.00, 3, 2), 
('Daniel Oliveira', '1992-08-05', 5200.00, 1, 5), 
('Fernanda Lima', '1995-09-30', 4500.00, 2, 3), 
('Gustavo Souza', '1980-01-25', 7000.00, 3, 2), 
('Helena Martins', '1983-11-17', 5300.00, 1, 4), 
('Igor Ferreira', '1991-07-08', 4900.00, 2, 1), 
('Juliana Rocha', '1989-04-19', 5600.00, 3, 2), 
('Lucas Mendes', '1993-06-23', 5100.00, 1, 5);


aqui estão as respostas das alternativas 

-- Funcionário com o maior salário
SELECT * 
FROM Funcionarios 
ORDER BY salario DESC 
LIMIT 1;

-- Funcionário com o menor salário
SELECT * 
FROM Funcionarios 
WHERE salario = (SELECT MIN(salario) FROM Funcionarios);

-- Contagem total de funcionários
SELECT COUNT(*) AS total_funcionarios FROM Funcionarios;

-- Funcionários nascidos a partir de 1990
SELECT * 
FROM Funcionarios 
WHERE data_nascimento >= '1990-01-01';

-- Média salarial dos funcionários, arredondada para 2 casas decimais
SELECT ROUND(AVG(salario), 2) AS media_salarial FROM Funcionarios;

-- Extrair os 3 primeiros caracteres do nome do funcionário
SELECT nome, SUBSTRING(nome, 1, 3) AS iniciais FROM Funcionarios;

-- Contagem de funcionários por departamento
SELECT d.nome AS departamento, COUNT(f.id) AS total_funcionarios
FROM Funcionarios f
JOIN Departamentos d ON f.departamento_id = d.id
GROUP BY d.nome;

