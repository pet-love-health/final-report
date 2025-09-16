# Capítulo IV: Solution Software Design.
## 4.1. Strategic-Level Domain-Driven Design.
### 4.1.1. Design-Level EventStorming.
Se llevó a cabo un proceso de Event Storming para identificar los Bounded Contexts de nuestro sistema. Durante este
proceso, se siguieron los pasos que se describen a continuación:

Collect Domain Events 

Se plantean eventos importantes de todos los grupos funcionales en tiempo pasado y nomenclatura en inglés.
![Collect Domain Events](https://i.postimg.cc/hj83SGny/collect-domain-events.png)

Timeline

Se ordenan todos los eventos y se empieza con un “happy path” es decir, eventos exitosos.
![Timeline1](https://i.postimg.cc/28yTtG1X/timeline1.png)
![Timeline2](https://i.postimg.cc/Mpj56Gb7/timeline2.png)

Pain and Pivotal Points

En este paso se resaltan con un diamante los eventos por aclarar o que requieren de más conocimientos de especialistas.
Por otro lado, los pivotal points son puntos de cambios que se marcan con una barra vertical.
Por otro lado, los pivotal points son puntos de cambios que se marcan con una barra vertical.
![PainAndPivotalPoints1](https://i.ibb.co/3vSmC4W/pain-and-pivotal-points1.png)
![PainAndPivotalPoints2](https://i.postimg.cc/hvysjz5r/pain-and-pivotal-points2.png)

#### 4.1.1.1 Candidate Context Discovery

![Candidate1](https://i.postimg.cc/L8h7zRk5/candidate1.png)
![Candidate2](https://i.postimg.cc/QdPzmPSb/candidate2.png)

#### 4.1.1.2 Domain Message Flows Modeling.

Dado el diagrama de eventos de EventStorming que ya se ha presentado, el siguiente paso es modelar los flujos de
mensajes. Para esto, podemos identificar las interacciones clave que ocurren en el sistema, y cómo estos mensajes 
desencadenan acciones o actualizaciones en otros contextos.

Solicitud de inicio de sesión: En este escenario, un actor (Customer) crea una cuenta en nuestro sistema y, de inmediato, 
se suscribe al plan predeterminado para validar sus credenciales, gracias a una política establecida. Este evento se
registra en nuestro backend, lo que confirma la suscripción. Una vez verificada la suscripción dentro del bounded
context de *Access*, al cliente se le permitirá acceder al comando de solicitud de inicio de sesión (Sign in request).
![MessageFlow1](https://i.postimg.cc/GmZMGDhg/message-flow1.png)

**Búsqueda de una veterinaria:** En este escenario, un actor (Customer) interactúa con el frontend solicitando el 
ingreso a su cuenta mediante el comando (*Sign in request*). Tras realizar las validaciones de credenciales en *Account 
Access* y verificar la cuenta, se le permitirá al cliente buscar veterinarias usando el comando (*Search Vet*). Una vez 
que acceda a esta función a través del frontend, el evento de (*Results searched*) será activado en nuestro backend 
dentro del bounded context de *Research and appointment*. Finalmente, podrá seleccionar el perfil de una veterinaria
mediante (*Select Vet profile*).
![MessageFlow2](https://i.postimg.cc/9fZLpfDm/message-flow2.png)

**Agendar una cita con un veterinario:** En este escenario, tras verificar las credenciales del cliente al iniciar
sesión, se le permite elegir un perfil de veterinario. Una vez completada esta acción, nuestro backend activa el evento
(*Vet profile selected*) y el cliente puede solicitar una cita utilizando el comando (*Request appointment*).
![MessageFlow3](https://i.postimg.cc/sXzw0RWp/message-flow3.png)

**Manejar el historial médico de la mascota:** Para gestionar el historial médico, el actor (Customer) solicita una cita
con un veterinario. Luego, se le pedirá información relevante sobre diagnósticos de enfermedades y actualizaciones de
reportes. Este comando se ejecuta desde nuestro frontend mediante (*Collect medical information*). Si la información se 
completa, se envía a la plataforma a través de (*Send medical information to platform*). Finalmente, una vez que toda la
información esté en nuestro backend, el veterinario puede actualizar el historial médico de la mascota usando el 
comando (*Update medical history*).
![MessageFlow4](https://i.postimg.cc/66YYzgpv/message-flow4.png)

#### 4.1.1.3 Bounded Context Canvases.

Se crearon lienzos de Bounded Context para cada uno de los contextos identificados en el proceso de EventStorming.
Estos lienzos ayudan a definir los límites de cada contexto, sus responsabilidades y las interacciones
con otros contextos.

![BoundedContext1](https://i.postimg.cc/KcPyzZQy/bounded-context1.png)
![BoundedContext2](https://i.postimg.cc/V6X2dRqF/bounded-context2.png)
![BoundedContext3](https://i.postimg.cc/GpWZLNy2/bounded-context3.png)
![BoundedContext4](https://i.postimg.cc/qvZPYgB2/bounded-context4.png)
![BoundedContext5](https://i.postimg.cc/FKdMQm18/bounded-context5.png)

### 4.1.2. Context Mapping.
### 4.1.3.1 Software Architecture.

En esta sección, se describe la Arquitectura de Software de la solución utilizando el C4 Model para su representación visual, a través de la herramienta Structurizr. Se introducirá la estructura general del sistema, comenzando por una vista de alto nivel (Context Level Diagram) y detallando las interacciones y componentes clave (Container Level Diagrams), proporcionando así una visión clara y comprensible de la arquitectura propuesta.

#### 4.1.3.2. Software Architecture System Landscape Diagram.
#### 4.1.3.3. Software Architecture Context Level Diagrams.

A continuación mostramos el diagrama de contexto de la arquitectura de software de la solución propuesta. En este diagrama se presentan los actores externos que interactúan con el sistema y los sistemas externos con los que se comunica.

![c4-context-diagram](https://i.postimg.cc/gjDvmyvD/c4-upet-2.png)
![c4-context-diagram](https://i.postimg.cc/gjDvmyvD/c4-upet-2.png)
![c4-context-diagram](https://i.postimg.cc/gjDvmyvD/c4-upet-2.png)
![c4-context-diagram](https://i.postimg.cc/gjDvmyvD/c4-upet-2.png)

#### 4.1.3.4. Software Architecture Container Level Diagrams.

En esta sección se presenta el diagrama de contenedores de la solución propuesta. Este diagrama detalla los contenedores de software y sus interrelaciones, proporcionando una visión general de la estructura interna del sistema.

![c4-containers-diagram](https://i.postimg.cc/QMKNbVW8/containers-dise-oyexperimentos.png)

#### 4.1.3.5. Software Architecture Deployment Diagrams.
## 4.2. Tactical-Level Domain-Driven Design
### 4.2.1. Bounded Context:  Identity and Access Context
- [Domain Layer](#4211-domain-layer)
- [Interface Layer](#4212-interface-layer)
- [Application Layer](#4213-application-layer)
- [Infrastructure Layer](#4214-infrastructure-layer)
- [Bounded Context Software Architecture Component Level Diagrams](#4215-bounded-context-software-architecture-component-level-diagrams)
- [Bounded Context Software Architecture Code Level Diagrams](#4216-bounded-context-software-architecture-code-level-diagrams)

#### 4.2.1.1. Domain Layer
#### Models
| **Clase**        | **Descripción**                                                                                                                                                                                                |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **User**         | Representa la entidad de usuario con atributos como `id`, `name`, `email`, `password`, `userType`, etc. Relacionado con `PetOwner` y `Veterinarian`.                                                           |
| **PetOwner**     | Representa la entidad de propietario de mascotas con atributos como `id`, `userId`, `numberPhone`, `location`, `subscriptionType`, etc. Relacionado con `User`, `Pet`, y `Review`.                             |
| **Veterinarian** | Representa la entidad de veterinario con atributos como `id`, `user_id`, `description`, `experience`, `clinic_id`, etc. Relacionado con `User`, `VeterinaryClinic`, `Availability`, `Appointment`, y `Review`. |

#### Enums
| **Enum**             | **Descripción**                                                   |
|----------------------|-------------------------------------------------------------------|
| **UserType**         | Enum para los tipos de usuarios: `Vet`, `Owner`.                  |
| **SubscriptionType** | Enum para los tipos de suscripciones: `Basic`, `Advanced`, `Pro`. |

#### Validators
| **Clase**           | **Descripción**                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|
| **SchemaValidator** | Contiene métodos para validar esquemas, asegurando que los campos requeridos estén presentes en los datos de entrada. |


#### 4.2.1.2. Interface Layer
Description of the design and components of the interface layer for the Identity and Access Context.

#### Schemas
| **Esquema**                       | **Descripción**                                                                                                                                                                                                   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UserSchemaGet**                 | Esquema para la respuesta de la obtención de un usuario. Incluye `id`, `name`, `email`, `userType`, `image_url`, `registered`.                                                                                    |
| **UserSchemaPost**                | Esquema para la creación de un nuevo usuario. Incluye `name`, `email`, `password`, `userType`.                                                                                                                    |
| **UserChangeImage**               | Esquema para actualizar la imagen de un usuario. Incluye `image_url`, `role`.                                                                                                                                     |
| **VeterinarianSchemaPost**        | Esquema para la creación de un nuevo veterinario. Incluye `clinicName`, `otp_password`.                                                                                                                           |
| **VeterinarianUpdateInformation** | Esquema para la actualización de la información de un veterinario. Incluye `name`, `description`, `experience`.                                                                                                   |
| **VeterinarianSchemaGet**         | Esquema para la respuesta de la obtención de un veterinario. Incluye `id`, `name`, `clinicId`, `image_url`, `description`, `experience`, `user_id`.                                                               |
| **VeterinarianProfileSchemaGet**  | Esquema para la respuesta detallada del perfil de un veterinario. Incluye `id`, `name`, `image_url`, `description`, `experience`, `clinicName`, `workingHourStart`, `workingHourEnd`, `clinicAddress`, `reviews`. |

#### 4.2.1.3. Application Layer
Description of the design and components of the application layer for the Identity and Access Context.

#### Services

| **Servicio**            | **Método**                                                                                       | **Descripción**                                                                                                                                            |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UserService**         | `get_user_by_id(user_id: int, db: Session)`                                                      | Recupera un usuario por su ID. Lanza una excepción 404 si el usuario no existe.                                                                            |
|                         | `change_image(role_id: int, role, image: str, db: Session)`                                      | Cambia la imagen de perfil del usuario según su rol (Owner o Veterinarian). Actualiza la entidad `User` y guarda los cambios.                              |
| **PetOwnerService**     | `create_new_petowner(user_id: int, petowner: PetOwnerSchemaPost, db: Session = Depends(get_db))` | Crea un nuevo registro de propietario de mascotas. Verifica el tipo de usuario, si ya está registrado y el formato del teléfono. Emite un token de acceso. |
|                         | `get_petowners(db: Session = Depends(get_db))`                                                   | Recupera todos los propietarios de mascotas, incluyendo sus datos de usuario asociados.                                                                    |
|                         | `get_petowner_by_user_id(user_id: int, db: Session)`                                             | Recupera un propietario de mascotas por su ID de usuario.                                                                                                  |
|                         | `get_petOwner_by_id(petOwner_id: int, db: Session) -> PetOwnerSchemaGet`                         | Recupera un propietario de mascotas por su ID.                                                                                                             |
|                         | `change_Datapetowner(petowner_id: int, petowner: PetOwnerUpdateInformation, db: Session)`        | Actualiza los datos de un propietario de mascotas existente.                                                                                               |
| **VeterinarianService** | `create_new_veterinarian(user_id: int, veterinarian: VeterinarianSchemaPost, db: Session)`       | Crea un nuevo registro de veterinario. Verifica el tipo de usuario, si ya está registrado, y valida el OTP y la clínica. Emite un token de acceso.         |
|                         | `get_all_vets(db: Session = Depends(get_db)) -> List[VeterinarianSchemaGet]`                     | Recupera todos los veterinarios, incluyendo sus datos de usuario asociados.                                                                                |
|                         | `get_vet_by_user_id(user_id: int, db: Session) -> VeterinarianSchemaGet`                         | Recupera un veterinario por su ID de usuario.                                                                                                              |
|                         | `get_vet_by_id(vet_id: int, db: Session) -> VeterinarianSchemaGet`                               | Recupera un veterinario por su ID.                                                                                                                         |
|                         | `get_vet_by_id_details(vet_id: int, db: Session) -> VeterinarianProfileSchemaGet`                | Recupera información detallada sobre un veterinario, incluyendo reseñas.                                                                                   |
|                         | `get_vets_by_clinic_id(clinic_id: int, db: Session) -> List[VeterinarianSchemaGet]`              | Recupera veterinarios por ID de clínica.                                                                                                                   |
|                         | `get_available_times(vet_id: int, day: date, db: Session)`                                       | Recupera los horarios disponibles para un veterinario en un día específico.                                                                                |
|                         | `change_DataVet(vet_id: int, vet: VeterinarianUpdateInformation, db: Session)`                   | Actualiza los datos de un veterinario existente.                                                                                                           |

#### 4.2.1.4. Infrastructure Layer
Description of the design and components of the infrastructure layer for the Identity and Access Context.\

#### **Repositorios**

| Clase/Servicio             | Descripción                                                                                           |
|----------------------------|-------------------------------------------------------------------------------------------------------|
| **UserRepository**         | Maneja la interacción con la base de datos para la entidad `User`. Incluye operaciones como crear, leer, actualizar y eliminar usuarios. |
| **PetOwnerRepository**     | Maneja la interacción con la base de datos para la entidad `PetOwner`. Permite crear, leer, actualizar y eliminar propietarios de mascotas. |
| **VeterinarianRepository** | Maneja la interacción con la base de datos para la entidad `Veterinarian`. Incluye operaciones de gestión de veterinarios como crear, leer, actualizar y eliminar. |

#### **Mappers**

| Clase/Servicio             | Descripción                                                                                           |
|----------------------------|-------------------------------------------------------------------------------------------------------|
| **UserMapper**             | Mapea la entidad `User` a la base de datos usando SQLAlchemy. Define cómo se traducen las propiedades del modelo `User` en columnas de la tabla de base de datos. |
| **PetOwnerMapper**         | Mapea la entidad `PetOwner` a la base de datos usando SQLAlchemy. Define cómo se traducen las propiedades del modelo `PetOwner` en columnas de la tabla de base de datos. |
| **VeterinarianMapper**     | Mapea la entidad `Veterinarian` a la base de datos usando SQLAlchemy. Define cómo se traducen las propiedades del modelo `Veterinarian` en columnas de la tabla de base de datos. |

#### Routes

| **Ruta**                                                             | **Método**   | **Descripción**                                                                                                           |
|----------------------------------------------------------------------|--------------|---------------------------------------------------------------------------------------------------------------------------|
| **PetOwners**                                                         |              |                                                                                                                           |
| `/petowners/{user_id}`                                                | POST         | Crear un nuevo propietario de mascotas.                                                                                  |
| `/petowners`                                                          | GET          | Obtener todos los propietarios de mascotas.                                                                             |
| `/petowners/users/{user_id}`                                          | GET          | Obtener un propietario de mascotas por ID de usuario.                                                                    |
| `/petowners/{petOwner_id}`                                            | GET          | Obtener un propietario de mascotas por ID de propietario.                                                                |
| `/petowners/{petOwner_id}`                                            | PUT          | Actualizar la información de un propietario de mascotas.                                                                 |
| **Users**                                                             |              |                                                                                                                           |
| `/users`                                                              | GET          | Obtener todos los usuarios.                                                                                             |
| `/users/{user_id}`                                                    | GET          | Obtener un usuario por ID.                                                                                              |
| `/users/{role_id}`                                                    | PUT          | Cambiar la imagen de un usuario.                                                                                        |
| **Veterinarians**                                                     |              |                                                                                                                           |
| `/veterinarians/{user_id}`                                            | POST         | Crear un nuevo veterinario.                                                                                             |
| `/veterinarians`                                                      | GET          | Obtener todos los veterinarios.                                                                                         |
| `/veterinarians/users/{user_id}`                                      | GET          | Obtener un veterinario por ID de usuario.                                                                               |
| `/veterinarians/{vet_id}`                                             | GET          | Obtener un veterinario por ID.                                                                                          |
| `/veterinarians/vets/{clinic_id}`                                    | GET          | Obtener veterinarios por ID de clínica.                                                                                  |
| `/veterinarians/reviews/{vet_id}`                                    | GET          | Obtener detalles del perfil de un veterinario, incluyendo reseñas.                                                        |
| `/veterinarians/{vet_id}/available_times`                            | POST         | Obtener los horarios disponibles de un veterinario.                                                                     |
| `/veterinarians/{vet_id}`                                             | PUT          | Actualizar la información de un veterinario.                                                                            |

#### 4.2.1.5. Bounded Context Software Architecture Component Level Diagrams
Component-level diagrams for the Identity and Access Context, showing the internal structure of components.

![Identity and Access Context Code Level Diagrams](https://i.postimg.cc/X7smGXCt/boundend-Identity-and-Access-Context.png)

#### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams
##### 4.2.1.6.1. Bounded Context Domain Layer Class Diagrams
Class diagrams for the domain layer of the Identity and Access Context.

![Identity and Access Context class diagram](https://i.postimg.cc/tJXv7HCX/Identity-and-Access-Context-class-diagram.png)

##### 4.2.1.6.2. Bounded Context Database Design Diagram
Database design diagram for the Identity and Access Context.

![Identity and Access Context database diagram](https://i.postimg.cc/XN8DmXQX/Identity-and-Access-Context-database-diagram.png)


### 4.2.3. Bounded Context:  Identity and Access Context
- [Domain Layer](#4231-domain-layer)
- [Interface Layer](#4232-interface-layer)
- [Application Layer](#4233-application-layer)
- [Infrastructure Layer](#4234-infrastructure-layer)
- [Bounded Context Software Architecture Component Level Diagrams](#4235-bounded-context-software-architecture-component-level-diagrams)
- [Bounded Context Software Architecture Code Level Diagrams](#4236-bounded-context-software-architecture-code-level-diagrams)

#### 4.2.3.1. Domain Layer

#### Aggregates

| **Aggregates**               | **Descripción**                                                                                                                                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **AppointmentAggregate**     | Se asegura de la consistencia en la gestión de citas (programación, cancelación, finalización). Contiene las reglas de negocio como validación de horarios, cambios de estado. |
| **AvailabilityAggregate**    | Agrupa la lógica de los bloques de tiempo de los veterinarios. Se asegura de que no haya solapamiento y que los rangos horarios sean válidos.                                  |

#### Entities

| **Entities**     | **Descripción**                                                                                                           |
|------------------|---------------------------------------------------------------------------------------------------------------------------|
| **Appointment**  | Entidad raíz del agregado. Representa una cita con atributos: id, petId, veterinarianId, appointmentDate, status, notes.  |
| **Availability** | Entidad raíz para disponibilidad, con atributos: id, veterinarianId, dayOfWeek, startTime, endTime.                       | 
| **Review**       | Entidad dependiente, vinculada a Appointment. Contiene id, appointmentId, rating, comment, createdAt.                     |

#### Value Objects

| **Value Objects**    | **Descripción**                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------|
| **AppointmentData**  | Datos propios de la cita (fecha, estado, notas) que viajan entre capas a través de AppointmentService y AppointmentRepository. |
| **AvailabilityData** | Datos de disponibilidad (día, rango horario) gestionados por AvailabilityService y persistidos en AvailabilityRepository.      |

#### 4.2.3.2 Interface Layer

Description of the design and components of the interface layer for the Appointment Context.

#### Schemas

| Esquema                      | Descripción                                                                                                                           |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **AppointmentSchemaGet**     | Esquema para la respuesta de la obtención de una cita. Incluye `id`, `petId`, `veterinarianId`, `appointmentDate`, `status`, `notes`. |
| **AppointmentSchemaPost**    | Esquema para la creación de una cita. Incluye `petId`, `veterinarianId`, `appointmentDate`, `notes`.                                  |
| **AppointmentSchemaUpdate**  | Esquema para la actualización del estado o detalles de una cita. Incluye `appointmentId`, `status`, `notes`.                          |
| **AvailabilitySchemaGet**    | Esquema para la respuesta de la obtención de disponibilidad. Incluye `id`, `veterinarianId`, `dayOfWeek`, `startTime`, `endTime`.     |
| **AvailabilitySchemaPost**   | Esquema para la creación de disponibilidad de un veterinario. Incluye `veterinarianId`, `dayOfWeek`, `startTime`, `endTime`.          |
| **AvailabilitySchemaUpdate** | Esquema para la actualización de la disponibilidad existente. Incluye `id`, `dayOfWeek`, `startTime`, `endTime`.                      |

#### 4.2.3.3. Application Layer

Description of the design and components of the application layer for the Identity and Access Context.

#### Services

| **Servicio**              | **Método**                                                                                     | **Descripción**                                                                                          |
| ------------------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **AppointmentService**    | `get_appointment_by_id(appointment_id: int, db: Session)`                                      | Recupera una cita por su ID. Lanza una excepción 404 si no existe.                                       |
|                           | `create_new_appointment(appointment: AppointmentSchemaPost, db: Session)`                      | Crea una nueva cita, validando disponibilidad del veterinario y existencia de la mascota.                |
|                           | `update_appointment(appointment_id: int, appointment: AppointmentSchemaUpdate, db: Session)`   | Actualiza el estado o notas de una cita existente.                                                       |
|                           | `get_appointments_by_pet(pet_id: int, db: Session)`                                            | Recupera todas las citas asociadas a una mascota específica.                                             |
|                           | `get_appointments_by_vet(vet_id: int, db: Session)`                                            | Recupera todas las citas asociadas a un veterinario.                                                     |
| **AvailabilityService**   | `get_availability_by_vet(vet_id: int, db: Session)`                                            | Recupera la disponibilidad de un veterinario.                                                            |
|                           | `create_availability(availability: AvailabilitySchemaPost, db: Session)`                       | Crea un nuevo registro de disponibilidad para un veterinario.                                            |
|                           | `update_availability(availability_id: int, availability: AvailabilitySchemaUpdate, db: Session)` | Actualiza una disponibilidad existente.                                                                |
|                           | `get_available_times(vet_id: int, day: date, db: Session)`                                     | Recupera los horarios disponibles para un veterinario en un día específico.                              |

#### 4.2.3.4. Infrastructure Layer

Description of the design and components of the infrastructure layer for the Appointment Context.

#### **Repositorios**

| **Repositorio**             | **Descripción**                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------- |
| **AppointmentRepository**   | Implementa la interfaz definida en el Domain Layer para manejar operaciones CRUD sobre citas. Incluye métodos para crear, actualizar, eliminar y consultar citas en la base de datos. |
| **AvailabilityRepository**  | Implementa la interfaz definida en el Domain Layer para manejar la disponibilidad de los veterinarios. Permite registrar, modificar y consultar horarios en la base de datos.         |

### **Mappers**

| **Mapeador**     | **Descripción**                                                                                                                                                                                |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AppointmentMapper**   | Convierte entre modelos de base de datos, entidades de dominio y esquemas (`AppointmentSchemaGet`, `AppointmentSchemaPost`, `AppointmentSchemaUpdate`).                                 |
| **AvailabilityMapper**  | Maneja la conversión de disponibilidad entre modelos de base de datos, entidades de dominio y esquemas (`AvailabilitySchemaGet`, `AvailabilitySchemaPost`, `AvailabilitySchemaUpdate`). |

#### **Routes**

| **Ruta**                                | **Método HTTP** | **Descripción**                                                                 |
| --------------------------------------- | --------------- | ------------------------------------------------------------------------------- |
| `/appointments/{appointment_id}`        | **GET**         | Obtiene una cita por su ID.                                                     |
| `/appointments`                         | **POST**        | Crea una nueva cita validando disponibilidad del veterinario.                   |
| `/appointments/{appointment_id}`        | **PUT**         | Actualiza el estado o notas de una cita existente.                              |
| `/appointments/pet/{pet_id}`            | **GET**         | Obtiene todas las citas asociadas a una mascota.                                |
| `/appointments/vet/{vet_id}`            | **GET**         | Obtiene todas las citas asociadas a un veterinario.                             |
| `/availability/vet/{vet_id}`            | **GET**         | Recupera la disponibilidad de un veterinario.                                   |
| `/availability`                         | **POST**        | Crea un nuevo registro de disponibilidad para un veterinario.                   |
| `/availability/{availability_id}`       | **PUT**         | Actualiza la disponibilidad existente.                                          |
| `/availability/vet/{vet_id}/day/{day}`  | **GET**         | Recupera los horarios disponibles de un veterinario en un día específico.       |

#### 4.2.3.5. Bounded Context Software Architecture Component Level Diagrams

Component-level diagrams for the Appointment Context, showing the internal structure of components.

<img src="../assets/img/Appointment1.png" height="100%" alt="100%"> 

#### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.1.6.1. Bounded Context Domain Layer Class Diagrams

Class diagrams for the domain layer of the Appointment Context.

<img src="../assets/img/Appointment2.png" height="100%" alt="100%"> 

##### 4.2.1.6.2. Bounded Context Database Design Diagram

Database design diagram for the Appointment Context.

<img src="../assets/img/Appointment3.png" height="100%" alt="100%"> 

