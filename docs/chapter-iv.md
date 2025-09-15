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
### 4.2.1. Bounded Context:
#### 4.2.1.1. Domain Layer.
#### 4.2.1.2. Interface Layer.
#### 4.2.1.3. Application Layer.
#### 4.2.1.4. Infrastructure Layer.
#### 4.2.1.5. Bounded Context Software Architecture Component Level Diagrams.
#### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams.
##### 4.2.1.6.1. Bounded Context Domain Layer Class Diagrams.
##### 4.2.1.6.2. Bounded Context Database Design Diagram.
