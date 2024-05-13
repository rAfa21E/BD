# BD
CREATE TABLE Caso (
    codigo CHAR(6),
    Vacuna VARCHAR(20) NOT NULL,
    Tratamiento VARCHAR(20) NOT NULL
);

CREATE TABLE Historial_Clinico (
    Cod_Historial_Clinico CHAR(6),
    Cod_Animal CHAR(6),
    Codigo CHAR(6),
    Cod_Veterinario CHAR(6),
    Descripcion VARCHAR(20) NOT NULL,
    Fecha TIMESTAMP
);

CREATE TABLE Animal (
    Cod_Animal CHAR(6),
    Cod_Cliente CHAR(6),
    Cod_Especie CHAR(6),
    Cod_Raza CHAR(6),
    Nombre VARCHAR(20) NOT NULL,
    Peso DECIMAL(6,2),
    Fecha_De_Nacimiento TIMESTAMP,
    Color VARCHAR(20)
);

CREATE TABLE Especie (
    Cod_Especie CHAR(6),
    Especie VARCHAR(20) NOT NULL
);

CREATE TABLE Raza (
    Cod_Raza CHAR(6),
    Raza VARCHAR(20) NOT NULL
);

CREATE TABLE Cliente (
    Cod_Cliente CHAR(6),
    Numero_De_Cedula CHAR(11) NOT NULL,
    Nombre VARCHAR(20),
    Apellido VARCHAR(20),
    Direccion VARCHAR(20) NOT NULL,
    Fecha_De_Nacimiento DATE,
    Telefono CHAR(11) NOT NULL,
    Correo_Electronico VARCHAR(20)
);

CREATE TABLE Factura (
    Cod_Factura CHAR(6),
    Cod_Cliente CHAR(6),
    Cod_Animal CHAR(6),
    Cod_Servicio CHAR(6),
    Numero_De_Pago CHAR(6) NOT NULL,
    Subtotal DECIMAL(6,2) NOT NULL,
    Descuento DECIMAL(6,2),
    Fecha TIMESTAMP
);

CREATE TABLE Factura_Servicio (
    Cod_Factura CHAR(6),
    Cod_Servicio CHAR(6)
);

CREATE TABLE Servicio (
    Cod_Servicio CHAR(6),
    Medicamento VARCHAR(20),
    Comida VARCHAR(20),
    Vacuna VARCHAR(20),
    Tarifa VARCHAR(20) NOT NULL
);

CREATE TABLE Veterinario (
    Cod_Veterinario CHAR(6),
    Numero_De_Cedula_V CHAR(11) NOT NULL,
    Nombre_V VARCHAR(20),
    Apellido_V VARCHAR(20),
    Telefono_V CHAR(11) NOT NULL,
    Fecha_De_labor DATE
);

CREATE TABLE Usuario (
    id_usuario CHAR(5) PRIMARY KEY,
    correo_E_U VARCHAR(20),
    u_contraseña VARCHAR(20)
);

ALTER TABLE Animal ADD CONSTRAINT PK_Cod_Animal PRIMARY KEY (Cod_Animal);
ALTER TABLE Caso ADD CONSTRAINT PK_Codigo PRIMARY KEY (codigo);
ALTER TABLE Especie ADD CONSTRAINT PK_Especie PRIMARY KEY (Cod_Especie);
ALTER TABLE Cliente ADD CONSTRAINT PK_Cod_Cliente PRIMARY KEY (Cod_Cliente);
ALTER TABLE Factura ADD CONSTRAINT PK_Cod_Factura PRIMARY KEY (Cod_Factura);
ALTER TABLE Historial_Clinico ADD CONSTRAINT PK_Cod_Historial_Clinico PRIMARY KEY (Cod_Historial_Clinico);
ALTER TABLE Raza ADD CONSTRAINT PK_Cod_Raza PRIMARY KEY (Cod_Raza);
ALTER TABLE Servicio ADD CONSTRAINT PK_Cod_Servicio PRIMARY KEY (Cod_Servicio);
ALTER TABLE Veterinario ADD CONSTRAINT PK_Cod_Veterinario PRIMARY KEY (Cod_Veterinario);

ALTER TABLE Historial_Clinico ADD CONSTRAINT FK_Cod_Animal FOREIGN KEY (Cod_Animal) REFERENCES Animal(Cod_Animal) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Historial_Clinico ADD CONSTRAINT FK_Codigo FOREIGN KEY (Codigo) REFERENCES Caso(codigo) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Historial_Clinico ADD CONSTRAINT FK_Cod_Veterinario FOREIGN KEY (Cod_Veterinario) REFERENCES Veterinario(Cod_Veterinario) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Animal ADD CONSTRAINT FK_Cod_Cliente FOREIGN KEY (Cod_Cliente) REFERENCES Cliente(Cod_Cliente) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Animal ADD CONSTRAINT FK_Cod_Especie FOREIGN KEY (Cod_Especie) REFERENCES Especie(Cod_Especie) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Animal ADD CONSTRAINT FK_Cod_Raza FOREIGN KEY (Cod_Raza) REFERENCES Raza(Cod_Raza) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Factura ADD CONSTRAINT FK_Cod_Cliente1 FOREIGN KEY (Cod_Cliente) REFERENCES Cliente(Cod_Cliente) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Factura ADD CONSTRAINT FK_Cod_Animal2 FOREIGN KEY (Cod_Animal) REFERENCES Animal(Cod_Animal) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Factura ADD CONSTRAINT FK_Cod_Servicio1 FOREIGN KEY (Cod_Servicio) REFERENCES Servicio(Cod_Servicio) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Factura_Servicio ADD CONSTRAINT FK_Cod_Factura FOREIGN KEY (Cod_Factura) REFERENCES Factura(Cod_Factura) ON DELETE CASCADE ON UPDATE CASCADE;
ALTER TABLE Factura_Servicio ADD CONSTRAINT FK_Cod_Servicio FOREIGN KEY (Cod_Servicio) REFERENCES Servicio(Cod_Servicio) ON DELETE CASCADE ON UPDATE CASCADE;
