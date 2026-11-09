# Biblioteca

Base de datos de ejemplo para la gestión de una biblioteca. Contiene autores, libros, usuarios y préstamos.

## Motor y esquema

- **MySQL**: base de datos `biblioteca`
- **Supabase (PostgreSQL)**: esquema `biblioteca`

Ambas implementaciones son equivalentes y contienen 10 registros por tabla.

## Tablas

### `autores`
| Campo | Tipo | Restricciones |
|---|---|---|
| id_autor | INT | PK, autoincremental |
| nombre | VARCHAR(100) | NOT NULL |
| nacionalidad | VARCHAR(50) | NOT NULL |

### `libros`
| Campo | Tipo | Restricciones |
|---|---|---|
| id_libro | INT | PK, autoincremental |
| titulo | VARCHAR(200) | NOT NULL |
| id_autor | INT | FK -> autores(id_autor) |
| anio | INT | NOT NULL |
| genero | VARCHAR(50) | NOT NULL |
| disponible | BOOLEAN | DEFAULT TRUE |

### `usuarios`
| Campo | Tipo | Restricciones |
|---|---|---|
| id_usuario | INT | PK, autoincremental |
| nombre | VARCHAR(100) | NOT NULL |
| email | VARCHAR(100) | NOT NULL, UNIQUE |
| telefono | VARCHAR(20) | |

### `prestamos`
| Campo | Tipo | Restricciones |
|---|---|---|
| id_prestamo | INT | PK, autoincremental |
| id_libro | INT | FK -> libros(id_libro) |
| id_usuario | INT | FK -> usuarios(id_usuario) |
| fecha_prestamo | DATE | NOT NULL |
| fecha_devolucion | DATE | |

## Datos de ejemplo

### autores
| id_autor | nombre | nacionalidad |
|---|---|---|
| 1 | Gabriel Garcia Marquez | Colombiana |
| 2 | Jorge Luis Borges | Argentina |
| 3 | Isabel Allende | Chilena |
| 4 | Julio Cortazar | Argentina |
| 5 | Mario Vargas Llosa | Peruana |
| 6 | Octavio Paz | Mexicana |
| 7 | Carlos Fuentes | Mexicana |
| 8 | Laura Esquivel | Mexicana |
| 9 | Pablo Neruda | Chilena |
| 10 | Juan Rulfo | Mexicana |

### libros
| id_libro | titulo | id_autor | anio | genero | disponible |
|---|---|---|---|---|---|
| 1 | Cien anios de soledad | 1 | 1967 | Novela | 1 |
| 2 | El amor en los tiempos del colera | 1 | 1985 | Novela | 1 |
| 3 | Ficciones | 2 | 1944 | Cuento | 0 |
| 4 | El aleph | 2 | 1949 | Cuento | 1 |
| 5 | La casa de los espiritus | 3 | 1982 | Novela | 1 |
| 6 | Rayuela | 4 | 1963 | Novela | 1 |
| 7 | La ciudad y los perros | 5 | 1963 | Novela | 0 |
| 8 | El laberinto de la soledad | 6 | 1950 | Ensayo | 1 |
| 9 | Aura | 7 | 1962 | Novela | 1 |
| 10 | Pedro Paramo | 10 | 1955 | Novela | 0 |

### usuarios
| id_usuario | nombre | email | telefono |
|---|---|---|---|
| 1 | Suri Escobar | suri@example.com | 555-1001 |
| 2 | Henry Moguel | henry@example.com | 555-1002 |
| 3 | David Ortiz | david@example.com | 555-1003 |
| 4 | Ana Lopez | ana@example.com | 555-1004 |
| 5 | Luis Ramirez | luis@example.com | 555-1005 |
| 6 | Maria Torres | maria@example.com | 555-1006 |
| 7 | Carlos Mendez | carlos@example.com | 555-1007 |
| 8 | Sofia Herrera | sofia@example.com | 555-1008 |
| 9 | Diego Castro | diego@example.com | 555-1009 |
| 10 | Elena Ruiz | elena@example.com | 555-1010 |

### prestamos
| id_prestamo | id_libro | id_usuario | fecha_prestamo | fecha_devolucion |
|---|---|---|---|---|
| 1 | 3 | 1 | 2026-10-01 | 2026-10-15 |
| 2 | 7 | 2 | 2026-10-03 | 2026-10-17 |
| 3 | 10 | 3 | 2026-10-05 | 2026-10-19 |
| 4 | 1 | 4 | 2026-10-08 | NULL |
| 5 | 2 | 5 | 2026-10-10 | 2026-10-24 |
| 6 | 4 | 6 | 2026-10-12 | NULL |
| 7 | 5 | 7 | 2026-10-14 | 2026-10-28 |
| 8 | 6 | 8 | 2026-10-16 | NULL |
| 9 | 8 | 9 | 2026-10-18 | 2026-11-01 |
| 10 | 9 | 10 | 2026-10-20 | NULL |

## DDL (MySQL)

```sql
CREATE TABLE autores (
  id_autor INT NOT NULL AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  nacionalidad VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_autor)
);

CREATE TABLE libros (
  id_libro INT NOT NULL AUTO_INCREMENT,
  titulo VARCHAR(200) NOT NULL,
  id_autor INT NOT NULL,
  anio INT NOT NULL,
  genero VARCHAR(50) NOT NULL,
  disponible BOOLEAN NOT NULL DEFAULT TRUE,
  PRIMARY KEY (id_libro),
  FOREIGN KEY (id_autor) REFERENCES autores (id_autor)
);

CREATE TABLE usuarios (
  id_usuario INT NOT NULL AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL UNIQUE,
  telefono VARCHAR(20),
  PRIMARY KEY (id_usuario)
);

CREATE TABLE prestamos (
  id_prestamo INT NOT NULL AUTO_INCREMENT,
  id_libro INT NOT NULL,
  id_usuario INT NOT NULL,
  fecha_prestamo DATE NOT NULL,
  fecha_devolucion DATE,
  PRIMARY KEY (id_prestamo),
  FOREIGN KEY (id_libro) REFERENCES libros (id_libro),
  FOREIGN KEY (id_usuario) REFERENCES usuarios (id_usuario)
);
```
