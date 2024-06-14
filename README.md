# Banco-Plano-de-saúde(Doctor Find)-SQL




-- Criação do banco de dados
CREATE DATABASE IF NOT EXISTS PlanoSaude;
USE PlanoSaude;

-- Tabela de Clientes
CREATE TABLE IF NOT EXISTS Clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    endereco VARCHAR(255),
    telefone VARCHAR(15),
    email VARCHAR(255) UNIQUE
);

-- Tabela de Usuários
CREATE TABLE IF NOT EXISTS Usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    tipo ENUM('ADMINISTRADOR', 'RECEPCIONISTA', 'VENDEDOR') NOT NULL
);

-- Tabela de Médicos
CREATE TABLE IF NOT EXISTS Medicos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    especialidade VARCHAR(255) NOT NULL,
    crm VARCHAR(20) NOT NULL UNIQUE,
    telefone VARCHAR(15),
    email VARCHAR(255) UNIQUE
);

-- Tabela de Pacientes
CREATE TABLE IF NOT EXISTS Pacientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    endereco VARCHAR(255),
    telefone VARCHAR(15),
    email VARCHAR(255) UNIQUE,
    data_nascimento DATE
);

-- Tabela de Funcionários
CREATE TABLE IF NOT EXISTS Funcionarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    endereco VARCHAR(255),
    telefone VARCHAR(15),
    email VARCHAR(255) UNIQUE,
    cargo VARCHAR(255)
);

-- Tabela de Planos de Saúde
CREATE TABLE IF NOT EXISTS PlanosSaude (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome_plano VARCHAR(255) NOT NULL,
    descricao TEXT,
    preco DECIMAL(10, 2) NOT NULL
);

-- Tabela de Vendas
CREATE TABLE IF NOT EXISTS Vendas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    id_plano INT NOT NULL,
    data_venda DATE NOT NULL,
    valor DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id),
    FOREIGN KEY (id_plano) REFERENCES PlanosSaude(id)
);

-- Inserção de Clientes
INSERT INTO Clientes (nome, cpf, endereco, telefone, email) VALUES 
('João da Silva', '111.222.333-44', 'Rua A, 123', '(11) 98765-4321', 'joao.silva@example.com'),
('Maria de Souza', '222.333.444-55', 'Avenida B, 456', '(11) 97654-3210', 'maria.souza@example.com'),
('Carlos Oliveira', '333.444.555-66', 'Praça C, 789', '(11) 96543-2109', 'carlos.oliveira@example.com');

-- Inserção de Usuários
INSERT INTO Usuarios (username, password, tipo) VALUES
('admin1', 'password123', 'ADMINISTRADOR'),
('recepcionista1', 'password123', 'RECEPCIONISTA'),
('vendedor1', 'password123', 'VENDEDOR');

-- Inserção de Médicos
INSERT INTO Medicos (nome, especialidade, crm, telefone, email) VALUES
('Dr. João Pereira', 'Cardiologia', 'CRM123456', '(11) 98765-4321', 'joao.pereira@example.com'),
('Dra. Maria Santos', 'Dermatologia', 'CRM654321', '(11) 97654-3210', 'maria.santos@example.com');

-- Inserção de Pacientes
INSERT INTO Pacientes (nome, cpf, endereco, telefone, email, data_nascimento) VALUES 
('Ana Maria da Silva', '123.456.789-01', 'Rua das Flores, 123', '(11) 91234-5678', 'ana.silva@example.com', '1980-05-10'),
('Carlos Eduardo Souza', '234.567.890-12', 'Avenida Central, 456', '(11) 92345-6789', 'carlos.souza@example.com', '1975-08-20'),
('Maria Fernanda Oliveira', '345.678.901-23', 'Praça da Liberdade, 789', '(11) 93456-7890', 'maria.oliveira@example.com', '1990-03-15');

-- Inserção de Funcionários
INSERT INTO Funcionarios (nome, cpf, endereco, telefone, email, cargo) VALUES
('José da Silva', '456.789.012-34', 'Rua Nova, 100', '(11) 91234-5678', 'jose.silva@example.com', 'Atendente'),
('Fernanda Lima', '567.890.123-45', 'Avenida Paulista, 2000', '(11) 92345-6789', 'fernanda.lima@example.com', 'Gerente');

-- Inserção de Planos de Saúde
INSERT INTO PlanosSaude (nome_plano, descricao, preco) VALUES
('Plano Básico', 'Cobertura básica de consultas e exames.', 199.90),
('Plano Intermediário', 'Cobertura intermediária de consultas, exames e alguns procedimentos.', 299.90),
('Plano Completo', 'Cobertura completa de consultas, exames, procedimentos e internações.', 499.90);

-- Inserção de Vendas
INSERT INTO Vendas (id_cliente, id_plano, data_venda, valor) VALUES
(1, 1, '2024-06-01', 199.90),
(2, 2, '2024-06-02', 299.90),
(3, 3, '2024-06-03', 499.90);