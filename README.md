# LAB 02a - Manage Governance via Azure Policy

Enero 17 de 2023*, Ramón Peinado Ruiz

Se nos ha encargado la implementacion de las siguientes funcionalidades

Etiquetar grupos de recursos que incluyan sólo recursos de infraestructura (como cuentas de almacenamiento Cloud Shell)

-Garantizar que sólo los recursos de infraestructura etiquetados correctamente puedan añadirse a los grupos de recursos de infraestructura

-Remediar cualquier recurso no conforme

**Objetivos:**

------

• Task 1: Crear y Asignar tags mediante el portal

• Task 2: Forzar Tagging via Policy

• Task 3: Aplicar Policy via tagging

• Task 4: Eliminacion de recursos

**Diagrama:**

------

<img src="/img/1ºimagenn.png" alt="6ºimagenn" style="zoom:80%;" />

### TASK 1:

------

Identificamos el nombre de nuestra cuenta de almacenamiento vía PowerShell con el comando

**df**

<img src="/img/2ºimagenn.png" alt="2ºimagenn" style="zoom:80%;" />

gruposhelrpr en nuestro caso

Accedemos al grupo de recurso donde este esa cuenta 

***Home>ResourceGroups>grupocloudhshelrpr>tags>add tag**

<img src="/img/3ºimagenn.png" alt="3ºimagenn" style="zoom:80%;" />

Creamos un tag con los siguientes valores:



| Setting | Value |
| ------- | ----- |
| Name    | Role  |
| Value   | Infra |

Este tag solo se encontrara dentro del grupo de recursos y no dentro de la cuenta de almacenamiento

<img src="/img/4ºimagenn.png" alt="4ºimagenn" style="zoom:80%;" />

<img src="/img/5ºimagenn.png" alt="5ºimagenn" style="zoom:80%;" />

### TASK 2:

------

Vamos a forzar el tagging desde Policy

***Home>Buscar>Policy>Authoring>Definitions***

<img src="/img/6ºimagenn.png" alt="6ºimagenn" style="zoom:80%;" />

Asignamos con los siguientes valores

| Setting        | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Subscription   | the name of the Azure subscription you are using in this lab |
| Resource Group | the name of the resource group containing the Cloud Shell account you identified in the previous task |

<img src="/img/7ºimagenn.png" alt="7ºimagenn" style="zoom:80%;" />

Volvemos al grupo de recursos e intentamos crear una nueva cuenta de almacenamiento

<img src="/img/8ºimagenn.png" alt="8ºimagenn" style="zoom:80%;" />

Obtenemos el siguiente error por no introducir los taggins correspondientes

{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"RequestDisallowedByPolicy","message":"Resource 'raimostorage' was disallowed by policy. Policy identifiers: '... (Code: RequestDisallowedByPolicy)","policyDetails":[]}]}

### TASK 3:

------

A continuacion vamos aplicar los tagings mediante directivas

***Home>Buscar>Policy>Authoring>Assignments***

Borramos el assignment que hay

<img src="/img/9ºimagenn.png" alt="8ºimagenn" style="zoom:80%;" />

Tras esto asignamos otra 

<img src="/img/10ºimagenn.png" alt="8ºimagenn" style="zoom:80%;" />

Dentro de parametros asignamos el tagname Role

<img src="/img/11ºimagenn.png" alt="11ºimagenn" style="zoom:80%;" />

A continuacion volvemos al grupo de recursos y creamos una cuenta de nuevo para ver como la directiva se aplica directamente y los tags aparecen automáticamente sin nosotros añadirlos manualmente

<img src="/img/12ºimagenn.png" alt="12ºimagenn" style="zoom:80%;" />

### TASK 3:

------

