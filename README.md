
## Funcionamiento 

- Ruta principal 

```text
http://${hostname}:${port}/
```

- Generar token de sesion

```text
GET => /generar/:categoria 
``` 


## En categoria puedes escoger entre:
 
> - acudientes
> - pacientes
> - citas
> - medicos 

- En otro caso daremos excepciones:

- No es necesario enviar datos

- la categoria debe ir en MINUSCULA

- Retornamos un token con la estructura de la categoria que se selecciono

- El token debe ir en el Bearer de las otras rutas

## Listar pacientes

```txt
GET => /pacientes => pacientes
```
### Descripcion de la consulta:
```txt
- Obtener todos los pacientes alfabéticamente
```

- No necesita datos de entrada
- El token debe ir, en caso contrario mostrara excepciones o errores


## Listar citas

```txt
GET => /citas => citas
```
### Descripcion de la consulta:
```txt
- Obtener todas las citas alfabéticamente
```
- No necesita datos de entrada
- El token debe ir, en caso contrario mostrara excepciones o errores


## Lista medicos por especialidad
```txt
GET => /medicos/:especialidad => medicos
```

### Descripcion de la consulta:
```txt
- Obtener todos los médicos de una especialidad específica (por ejemplo, **'Cardiología'**)
```

- debes mandar un ***id*** de la especialidad
- Debe ser un dato ***numerico***
- ***ningun*** caracter en letras
- en caso contrario  mostrara excepciones o errores



## Proxima cita
```txt
GET => /citas/:paciente => citas
```

### Descripcion de la consulta
```txt
- Encontrar la próxima cita para un paciente específico (por ejemplo, el paciente con **usu_id 1**):
```

- debes manda un ***id*** del paciente
- Debe ser un dato ***numerico***
- ***ningun*** caracter en letras
- en caso contrario mostrara excepciones o errores


## Listar citas con medicos especificos

```txt
GET => /citas/medico/:medico => citas
```

### Descripcion de la consulta
```txt
- Encontrar todos los pacientes que tienen citas con un médico específico (por ejemplo, el médico con **id= 1**)
```

- debes enviar un  ***id*** del medico
- Debe ser un dato ***numerico***
- ***ningun*** caracter en letras
- en caso contrario mostrara excepciones o errores


## Listar las citas de un paciente
```txt
- GET => /citas/consultorio/:paciente => citas
```
### Descripcion de la consulta 

```txt
Obtener las citas para un paciente especifico y el numero del consultorio
```

- debes enviar un  ***id*** del medico
- Debe ser un dato ***numerico***
- ***ningun*** caracter en letras
- en caso contrario mostrara excepciones o errores


## Listar citas por fecha especifica

```txt
GET => /fecha/cita => citas
``` 

### Descripcion de la consulta
```txt 
- Encontrar todas las citas para un día específico (por ejemplo, **'2023-07-12'**)
```

- Datos de entrada 
```json
{
    "fecha": "..."
}
```

- El nombre del parametro debe ser "fecha"
- la fecha tiene que estar en formato **`` yy/mm/dd ``**
- Debe ser una ***cadena de texto***
- en caso contrario mostrara excepciones o errores


## listar medicos y sus especialidades

```txt
GET => /doctores/obtener/especializacion => medicos
```

### Descripcion de la consulta 
```txt
- Obtener los médicos y sus consultorios
```
- No necesita datos de entrada
- El token debe ir, en caso contrario recibiras excepciones


## listar cantidad de citas por medico y fecha

```txt
GET => /cantidad/citas => citas
```

### Descripcion de la consulta 
```txt
- Contar el número de citas que un médico tiene en un día específico (por ejemplo, el médico con **id 1 en '2023-07-12'**)
```

- Datos de entrada: 
```json
{
    "fecha": "...",
    "medico": 0
}
``` 
- los nombres de los parametros deben ser "fecha" y "medico"
- la fecha tiene que estar en formato **`` yy/mm/dd ``**
- deberas mandar la ***id*** del medico
- En caso contrario no recibiras informacion. 

## listar consultorios donde han habido citas 
```txt
GET => /consultorios/citas => citas
```

### Descripcion de la consulta 
```txt
- Obtener los consultorio donde se aplicó las citas de un paciente
```
- No necesita datos de entrada
- El token debe ir, en caso contrario recibiras excepciones

## Listar citas por genero
```txt
GET => /genero/citas/:genero => citas
```

### Descripcion de la consulta
```txt
- Obtener todas las citas realizadas por los pacientes de un genero si su estado de la cita fue atendidad
```

- Deberas mandar el genero -> **Masculino** o **Femenino**
- En caso contrario no recibiras informacion. 


## Paciente nuevo 
```txt
POST => /pacientes => pacientes
```

### Descripcion de la consulta
```txt
- Insertar un paciente a la tabla usuario pero si es menor de edad solicitar primero que ingrese el acudiente y validar si ya estaba registrado el acudiente.
```

- Datos de entrada: 
```json
{
  "nombres": "...",
  "apellidos": "...",
  "telefono": "...",
  "direccion": "...",
  "email": "...",
  "tipo_documento": 0,
  "genero": 0,
  "acudiente": parametro opcional 
}
```
- nombres => deben estar separados **"[cadena cadena]** ejemplo "Stiven "
- apellidos => deben estar separados **"[cadena cadena]** ejemplo "Carvajal"
- telefono => una cadena de numeros 
- direccion => una cadena de texto
- email => formato email **asdsadsa@asdada.extension**
- tipo_documento => dato numerico
- genero => dato numerico
- acudiente => parametro opcional, el parametro debe ponerse en caso que el paciente que este registrando sea menor de edad
- En caso de que sea menor de edad, deberas llenar el campo **"acudiente"** con un dato Numerico
- en caso contrario recibiras ***excepciones***


## Listar citas rechazadas 

```txt
GET => /fechaCitas/:año/:mes => citas
```

### Descripcion de la consulta 
```txt
- Mostrar todas las citas que fueron rechazadas y en un mes específico, mostrar la fecha de la cita, el nombre del usuario y el médico.
```

- deberas mandar el año y el mes de la siguiente manera
```txt
/fechaCitas/23/08 || /fechaCitas/22/01
```