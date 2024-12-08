
# Back Over MongoDB

## 1. Iniciar la lambda de start replication

Pre condiciones:
- Tareas de replicacion del DMS pausadas
- MongoDB caído o fuera de servicio,
- Existe el usuario en DocumentDB que usan los microservicios

Procedimiento:
- Input de la lambda:
  - ```
    {
      "DOCDB_USER_APLICATION_USERNAME" : "<Username del usuario de DocumentDB que usan los microservicios>"
    }
    ```

- Flujo de la lambda:
  - Inicia una instancia EC2 y espera que esté lista.

  - Actualiza el usuario de documentDB que usarán los microservicios con permisos para insertar, actualizar y leer documentos en todas las bases de datos especificadas en el archivo dmsReplicationTasks.json

  - Inicializa el servicio de replication.service, este servicio se encarga de subir a S3 las operaciones (inserciones, actualizaciones, eliminaciones) que se aplican a los documentos de las diferentes colecciones y bases de datos del DocumentDB, puede ver su estado y sus logs con los siguientes comandos:
    ```
    sudo systemctl status replication.service
    sudo journalctl -u replication.service -n 50
    ```

Post condiciones:
- Servicio de replicación iniciado y subiendo las operaciones del DocumentDb al bucket de S3.

## 2. Inicar la lambda de restore replication
Pre condiciones:
- La lambda start replication fue ejecutada
- Servicio de replication iniciado y corriendo
- MongoDB operativo y permite acceso del EC2
- Existe usuario en mongoDB con permisos de lectura y escritura

Proceimiento:
- Input de la lambda
  - ```
    {
      "DOCDB_USER_APLICATION_USERNAME" : "<Username del usuario que usan los microservicios para escribir en documentDB>",
      "MONGODB_USERNAME":"<Username del usuario de MongoDB on-premise>",
      "MONGODB_PASSWORD":"<Password del usuario de MongoDB on-premise>",
      "MONGODB_ENDPOINT":"<Endpoint | ip | dominio del servidor de MongoDB>",
      "MONGODB_PORT":"<Puerto del MongoDB>"
    }
    ```
    EJemplo:
  - ```
    {
      "DOCDB_USER_APLICATION_USERNAME" : "user-test",
      "MONGODB_USERNAME":"test",
      "MONGODB_PASSWORD":"testtest",
      "MONGODB_ENDPOINT":"testqa-mongodb01.losandes.pe",
      "MONGODB_PORT":"27017"
    }
    ```
  *Nota: El usuario de MongoDB que se vaya a ingresar debe tener permisos de lectura y escritura en las bases de datos que se están replicando*


- Flujo de la lambda:
  - Actualiza el usuario "DOCDB_USER_APLICATION_USERNAME" a permisos de solo lectura en todas las bases de datos y colecciones del documentDB.
  - Aprovisiona estos 3 servicios:
    - restore.service: Se encarga de restaurar el contenido del S3 (las operaciones registrados mientras el mongoDB estaba fuera de servicio) hacia el mongoDB
    - monitor_replication.service: Se encarga de monitorear que el servicio de replication haya acabado para empezar la restauración del S3 hacia el mongoDB, verifica en un intervalo de 5 minutos de forma constante si es que hay cambios en el S3, cuando ya no detecta cambios, después de 5 minutos activa el servicio de restore.
    - backup.service: Se encarga de generar un dump del mongoDB y documentDB  y subirlo al S3.
  - Inicializa primero el servicio monitor_replication y backup, el servicio restore es iniciado por el servicio monitor_replication caundo se cumpla la condición de que el servicio de replication haya acabado.
  -
Post condiciones:
- Servicio de monitor_replication corriendo
- Servicio de restore a la espera de ser iniciado por el servicio de monitor_replication
- Servicio de backup corriendo


## 3. Inicar la lambda de clean replication

Pre condiciones:
- Lambda restore replication fue ejecutada

Procedimiento:
- Input:
  - No hay input
- Flujo de la lambda:
    - Aprovisionar estos 3 servicios:
      - clean.service: Servicio de borrar el resumeTokenJSON que usa el servicio de replication para asegurar la consistencia en el procesamiento de operaciones del documentDB, borrar la carpeta replication/ del S3.
      - monitor_restore.service: Servicio que monitorea que el servicio de restore.service haya finalizado para ejecutar el servicio de clean.service.
      - monitor_clean.service: Servicio que monitorea que el servicio clean.service y backup.service hayan terminado para apagar el EC2 donde se están ejecutando todos los servicios.
  - Inicializa el serivcio de monitor_restore y los otros dos se ejecutan automaticamente de acuerdo al servicio monitor_restore

Post condiciones:
  - Carpeta replication/ del S3 siendo limpiada
  - Ec2 apagado

## 4. Reactivar las tareas
Reactivar las tareas cambiando el valor de dms_start_replication a true y correrlo



## Notas importantes

- El EC2 debe estar prendido todo el tiempo que el MongoDB esté fuera de servicio, es decir, todo el tiempo que los microservicios estén usando a DocumentDB para realizar sus operaciones.
- Asegurarse que ninguna lambda programada apague el EC2.




