# Patrón de diseño COMMAND
 
 El **patrón de diseño Command** es una técnica utilizada en programación orientada a objetos. Su objetivo es permitir solicitar una operación a un objeto sin conocer los detalles de su implementación ni el receptor real de la misma. 

##Sus puntos clave son:

1.	**Intención:**
* Encapsula una petición como un objeto, lo que facilita la parametrización de los métodos; es decir, la capacidad de configurar o personalizar la petición antes de ejecutarla.
* Permite gestionar colas o registros de mensajes y deshacer operaciones.
* Ofrece una interfaz común para invocar acciones de forma uniforme y extender el sistema con nuevas acciones.


2.	**Aplicaciones:**
* Facilita la parametrización de acciones a realizar.
* Independiza el momento de petición de ejecución, abstrayendo estos elementos de la implementación de la orden.
* Implementa callbacks, donde un parámetro de una orden puede ser otra orden que ejecutar.
* Soporta el “deshacer”.
* Desarrolla sistemas utilizando órdenes de alto nivel construidas con operaciones sencillas.
3.	**Estructura:**
* El término “orden” puede ser ambiguo, pero el patrón maneja esta ambigüedad.
* Cada operación se implementa como una clase independiente (comando).
* Los comandos pueden recibir parámetros para realizar tareas específicas.

### Beneficios de la parametrización
 Entre los beneficios de la parametrización podemos mencionar algunas utilidades:

1.	Parámetros del comando:
* Cada comando concreto puede recibir parámetros específicos. Por ejemplo, un comando para crear un archivo podría necesitar el nombre del archivo y la ubicación donde se creará.
* Estos parámetros se proporcionan cuando se crea una instancia del comando.
2.	Flexibilidad:
* La parametrización permite que los comandos sean más flexibles y adaptables. Puedes reutilizar el mismo comando con diferentes valores de entrada.
Por ejemplo, si tienes un comando SendEmail para enviar correos electrónicos, puedes configurar los destinatarios, el asunto y el contenido como parámetros. 

La parametrización en el patrón Command te permite ajustar los detalles de un comando antes de ejecutarlo, lo que aumenta su versatilidad. 
### Ejemplo
Imaginemos que estamos construyendo una aplicación de consola con múltiples comandos. Cada comando realiza una acción específica, como crear un archivo, enviar un correo electrónico o procesar datos:

1.	Interfaz ICommand:
- Definimos una interfaz llamada _ICommand_ con un método _Execute()_. Todos los comandos concretos implementarán esta interfaz.
2.	Comandos concretos:
- Creamos clases para cada comando específico, como _CreateFileCommand_, _SendEmailCommand_ y _ProcessDataCommand_.
- Cada clase implementa el método _Execute()_ y realiza la acción correspondiente.
3.	Cliente y cola de comandos:
- El cliente (_nuestra aplicación_) crea instancias de comandos concretos y los agrega a una cola.
- La cola de comandos ejecuta los comandos en orden, uno tras otro.
- Podemos agregar, quitar o reorganizar comandos en la cola según nuestras necesidades.
4.	Beneficios:
- _Desacoplamiento_: Los comandos no necesitan conocer los detalles de implementación de otros comandos ni del cliente.
- _Reutilización_: Podemos reutilizar los comandos en diferentes partes de la aplicación.
- _Historial y deshacer_: Podemos registrar los comandos ejecutados para implementar funciones de deshacer o rehacer.
Para entender un poco más podemos hacer uso de la siguiente analogía:

## Analogía del Restaurante para el Patrón Command

Imagina que estamos en un restaurante y analizamos cómo se gestionan los pedidos desde que un cliente hace una solicitud hasta que recibe su comida. 

![Analogía de un restaurante](https://refactoring.guru/images/patterns/content/command/command-comic-1.png?id=551df832f445080976f3116e0dc120c9)

1. **Cliente (Client)**: El cliente es quien realiza el pedido. En nuestra aplicación, esto es similar al código que configura y emite los comandos.

2. **Menú (Command Interface)**: El menú del restaurante es una lista de posibles comandos que un cliente puede pedir, como "Agregar comida", "Eliminar comida", "Completar pedido", etc. En nuestra aplicación, esto es la interfaz `Command` que declara el método `execute()`.

3. **Pedido Específico (ConcreteCommand)**: Cada pedido específico, como una "Pizza" o "Ensalada", es una implementación concreta del menú. En nuestra aplicación, estos son los comandos concretos como `AddTaskCommand`, `RemoveTaskCommand`, `CompleteTaskCommand`, etc.

4. **Camarero (Invoker)**: El camarero es el que toma el pedido del cliente y lo entrega a la cocina. No sabe cómo se cocina, solo se asegura de que el pedido llegue a quien lo va a preparar. En nuestra aplicación, esto es el `Invoker` que almacena y ejecuta los comandos.

5. **Cocina (Receiver)**: La cocina es quien realmente sabe cómo preparar los pedidos. Recibe las instrucciones del camarero y ejecuta las acciones necesarias para preparar la comida. En nuestra aplicación, esto es el `Receiver`, como la clase `TaskList` que se implementó en la To_Do_List ,que tiene los métodos para agregar, eliminar, completar y listar tareas.

6. **Orden de Pedido (Historial)**: El camarero puede llevar un historial de los pedidos hechos por el cliente para poder revisar, cancelar o repetir pedidos si es necesario. En nuestra aplicación, esto es el historial de comandos ejecutados que se puede usar para deshacer o rehacer acciones.


### Resumen

- **Cliente (Client)**: Configura y emite los comandos (`index.ts`).
- **Menú (Command Interface)**: Define la interfaz de los comandos (`Command.ts`).
- **Pedidos Específicos (ConcreteCommand)**: Implementaciones concretas de comandos (`AddTaskCommand.ts`, `RemoveTaskCommand.ts`, etc.).
- **Camarero (Invoker)**: Ejecuta los comandos y puede almacenar un historial (`TaskManager.ts`).
- **Cocina (Receiver)**: Ejecuta las acciones solicitadas por los comandos (`TaskList.ts`).

En resumen, el patrón Command es versátil y útil para abstraer detalles de implementación y gestionar operaciones de manera flexible.
