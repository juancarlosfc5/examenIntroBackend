# examenIntroBackend

# 🚗 Sistema de Gestión de Concesionarios

## 📌 Descripción
Este proyecto implementa una base de datos en **MySQL** para la gestión de un concesionario de vehículos. El sistema permite el almacenamiento y administración de información clave como clientes, vendedores, vehículos, ventas, mantenimientos y facturación.

## 📊 Modelo Entidad-Relación
El diseño de la base de datos se basa en el siguiente modelo entidad-relación:

## Modelo Conceptual
![Modelo conceptual](https://github.com/user-attachments/assets/6f1d6f41-dfe4-4b08-ae49-93f15011b6bb)

## Modelo Fisico
![Modelo fisico](https://github.com/user-attachments/assets/0759e8d8-0341-4602-a931-bfc2aa57b793)

## Script MySQL
CREATE DATABASE IF NOT EXISTS concesionario;
USE concesionario;

CREATE TABLE CONCESIONARIO (
    id_concesionario INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    direccion VARCHAR(255) NOT NULL,
    telefono VARCHAR(20) NOT NULL,
    correo VARCHAR(100) NOT NULL
);

CREATE TABLE VEHICULO (
    VIN VARCHAR(50) PRIMARY KEY,
    marca VARCHAR(50) NOT NULL,
    referencia VARCHAR(50) NOT NULL,
    modelo INT NOT NULL,
    precio DECIMAL(10,2) NOT NULL,
    color VARCHAR(30) NOT NULL,
    tipo_combustible VARCHAR(30) NOT NULL,
    tipo_transmision VARCHAR(30) NOT NULL,
    estado VARCHAR(30) NOT NULL,
    disponibilidad BOOLEAN NOT NULL,
    id_concesionario INT,
    FOREIGN KEY (id_concesionario) REFERENCES CONCESIONARIO(id_concesionario)
);

CREATE TABLE CLIENTE (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    telefono VARCHAR(20) NOT NULL,
    correo VARCHAR(100) NOT NULL,
    direccion VARCHAR(255) NOT NULL
);

CREATE TABLE VENDEDOR (
    id_vendedor INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    num_empleado INT NOT NULL,
    fecha_contratacion DATE NOT NULL
);

CREATE TABLE VENTA (
    id_venta INT PRIMARY KEY AUTO_INCREMENT,
    fecha_venta DATE NOT NULL,
    total DECIMAL(10,2) NOT NULL,
    metodo_pago VARCHAR(50) NOT NULL,
    id_cliente INT,
    id_vendedor INT,
    FOREIGN KEY (id_cliente) REFERENCES CLIENTE(id_cliente),
    FOREIGN KEY (id_vendedor) REFERENCES VENDEDOR(id_vendedor)
);

CREATE TABLE DETALLE_VENTA (
    id_venta INT,
    VIN VARCHAR(50),
    PRIMARY KEY (id_venta, VIN),
    FOREIGN KEY (id_venta) REFERENCES VENTA(id_venta),
    FOREIGN KEY (VIN) REFERENCES VEHICULO(VIN)
);

CREATE TABLE ORDEN_MANTENIMIENTO (
    id_orden_mantenimiento INT PRIMARY KEY AUTO_INCREMENT,
    fecha_orden DATE NOT NULL,
    id_cliente INT,
    id_concesionario INT,
    FOREIGN KEY (id_cliente) REFERENCES CLIENTE(id_cliente),
    FOREIGN KEY (id_concesionario) REFERENCES CONCESIONARIO(id_concesionario)
);

CREATE TABLE MANTENIMIENTO (
    id_mantenimiento INT PRIMARY KEY AUTO_INCREMENT,
    id_orden_mantenimiento INT,
    FOREIGN KEY (id_orden_mantenimiento) REFERENCES ORDEN_MANTENIMIENTO(id_orden_mantenimiento)
);

CREATE TABLE DETALLE_MANTENIMIENTO (
    id_detalle_mantenimiento INT PRIMARY KEY AUTO_INCREMENT,
    id_mantenimiento INT,
    VIN VARCHAR(50),
    tipo_servicio VARCHAR(100) NOT NULL,
    costo DECIMAL(10,2) NOT NULL,
    fecha_servicio DATE NOT NULL,
    FOREIGN KEY (id_mantenimiento) REFERENCES MANTENIMIENTO(id_mantenimiento),
    FOREIGN KEY (VIN) REFERENCES VEHICULO(VIN)
);

CREATE TABLE FACTURA (
    id_factura INT PRIMARY KEY AUTO_INCREMENT,
    fecha_factura DATE NOT NULL,
    total DECIMAL(10,2) NOT NULL
);

ALTER TABLE DETALLE_MANTENIMIENTO ADD FOREIGN KEY (id_detalle_mantenimiento) REFERENCES FACTURA(id_factura);
ALTER TABLE DETALLE_VENTA ADD FOREIGN KEY (id_venta) REFERENCES FACTURA(id_factura);

## 🛠️ Tecnologías Utilizadas
- **MySQL** – Sistema de gestión de bases de datos relacional.
- **Mermaid.js** – Para la representación visual del modelo ER.
- **Git/GitHub** – Control de versiones y colaboración.

## 🎯 Funcionalidades
✅ Gestión de concesionarios y su inventario de vehículos.  
✅ Registro de clientes y vendedores.  
✅ Administración de ventas y facturación.  
✅ Control de órdenes y detalles de mantenimiento.

