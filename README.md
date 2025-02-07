# -SQL-Server

-- Eliminar la base de datos si ya existe
DROP DATABASE IF EXISTS NVIDIA_Education;

-- Crear la base de datos
CREATE DATABASE NVIDIA_Education;

-- Usar la base de datos
USE NVIDIA_Education;

-- Crear la tabla Instructores
CREATE TABLE Instructores (
    instructor_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    especialidad VARCHAR(100),
    email VARCHAR(100) UNIQUE NOT NULL
);

-- Insertar 3 instructores
INSERT INTO Instructores (nombre, especialidad, email)
VALUES 
    ('Carlos Pérez', 'Inteligencia Artificial', 'carlos@example.com'),
    ('María Gómez', 'Desarrollo de Videojuegos', 'maria@example.com'),
    ('Luis Ramírez', 'Ciencia de Datos', 'luis@example.com');

-- Crear la tabla Cursos
CREATE TABLE Cursos (
    curso_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    descripción TEXT,
    duración VARCHAR(50),
    nivel VARCHAR(50),
    instructor_id INT,
    FOREIGN KEY (instructor_id) REFERENCES Instructores(instructor_id)
);

-- Insertar 3 cursos
INSERT INTO Cursos (nombre, descripción, duración, nivel, instructor_id)
VALUES 
    ('Introducción a la IA', 'Curso básico de inteligencia artificial.', '10 horas', 'Básico', 1),
    ('Desarrollo de Juegos con Unity', 'Aprende a crear videojuegos con Unity.', '20 horas', 'Intermedio', 2),
    ('Análisis de Datos con Python', 'Curso avanzado de ciencia de datos.', '15 horas', 'Avanzado', 3);

-- Crear la tabla Usuarios
CREATE TABLE Usuarios (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    contraseña VARCHAR(255) NOT NULL,
    rol VARCHAR(50) NOT NULL
);

-- Insertar 3 usuarios
INSERT INTO Usuarios (nombre, email, contraseña, rol)
VALUES 
    ('Juan López', 'juan@example.com', 'hashedpassword123', 'Estudiante'),
    ('Ana Martínez', 'ana@example.com', 'hashedpassword456', 'Desarrollador'),
    ('Pedro Sánchez', 'pedro@example.com', 'hashedpassword789', 'Profesional');

-- Crear la tabla Certificaciones
CREATE TABLE Certificaciones (
    certificacion_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    descripción TEXT,
    requisitos TEXT
);

-- Insertar 3 certificaciones
INSERT INTO Certificaciones (nombre, descripción, requisitos)
VALUES 
    ('Certificación en IA', 'Certificación en inteligencia artificial.', 'Completar curso de IA y aprobar el examen.'),
    ('Certificación en Unity', 'Certificación en desarrollo de videojuegos.', 'Completar curso de Unity y presentar un proyecto.'),
    ('Certificación en Ciencia de Datos', 'Certificación en análisis de datos.', 'Completar curso de ciencia de datos y aprobar el examen.');

-- Crear la tabla Progreso_Usuario
CREATE TABLE Progreso_Usuario (
    progreso_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    curso_id INT,
    certificacion_id INT,
    progreso DECIMAL(5,2),
    fecha_inicio DATE,
    fecha_fin DATE,
    FOREIGN KEY (user_id) REFERENCES Usuarios(user_id),
    FOREIGN KEY (curso_id) REFERENCES Cursos(curso_id),
    FOREIGN KEY (certificacion_id) REFERENCES Certificaciones(certificacion_id)
);

-- Insertar 3 registros de progreso
INSERT INTO Progreso_Usuario (user_id, curso_id, certificacion_id, progreso, fecha_inicio, fecha_fin)
VALUES 
    (1, 1, 1, 50.0, '2023-10-01', NULL),
    (2, 2, 2, 75.0, '2023-09-15', '2023-10-15'),
    (3, 3, 3, 100.0, '2023-08-01', '2023-09-01');

-- Crear la tabla Recursos
CREATE TABLE Recursos (
    recurso_id INT PRIMARY KEY AUTO_INCREMENT,
    curso_id INT,
    tipo VARCHAR(50),
    url VARCHAR(255),
    FOREIGN KEY (curso_id) REFERENCES Cursos(curso_id)
);

-- Insertar 3 recursos
INSERT INTO Recursos (curso_id, tipo, url)
VALUES 
    (1, 'Video', 'https://example.com/video-ia'),
    (2, 'PDF', 'https://example.com/pdf-unity'),
    (3, 'Enlace', 'https://example.com/enlace-datos');


SHOW TABLES;
SELECT * FROM Instructores;
SELECT * FROM Cursos;
SELECT * FROM Usuarios;
SELECT * FROM Certificaciones;
SELECT * FROM Progreso_Usuario;
SELECT * FROM Recursos;
