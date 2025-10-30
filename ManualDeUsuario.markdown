# Manual de Usuario

## 1. Login | Inicio de Sesion

El sistema ofrece **dos métodos de inicio de sesión**
- **Active Directory (AD):** Utiliza la **cuenta de correo corporativa**, es decir, el mismo **usuario y contraseña** que se emplea para iniciar sesión en los equipos del trabajo (Laptop o PC).  

- **Unity:** Es el método de autenticación propio del sistema **Unity**, diseñado para usuarios con cuentas específicas del sistema.

![Pantalla de Login](./imagen/login.png)

El usuario debe seleccionar el método de inicio de sesión que desea utilizar e ingresar sus **credenciales correspondientes** (usuario y contraseña) para acceder al sistema.

### Sistema de seguridad

>Reglas de Bloqueo Automático, Por Equivocacion de Contraseña
Límite de intentos: 3 intentos fallidos consecutivos
Duración del bloqueo: 30 minutos
Alcance: Aplicable a ambos métodos de autenticación (AD y Unity)

## 2. Dashboard Del Sistema

El **Dashboard** (Tablero Principal) es la primera pantalla que se visualiza al ingresar al sistema. Está diseñado para ofrecer una **visión general y rápida** de lo que Ofrece el Sistema.

En el lado izquierdo de la pantalla se encuentra el menú de navegación, dividido en dos secciones:

![Pantalla De Dashboard](./imagen/Dashboard.png)

* **Gestición Principal:** Permite acceder a las funciones principales del sistema:
    >**Dashboard:** La vista actual.
    **Campañas:** Gestionar y ver todas las campañas.
    **+ Crear Campaña:** Iniciar el proceso de creación de una nueva campaña.
    **Cargas Masivas:** (Funcionalidad para cargar datos o campañas de forma masiva)
    **Lista Precio Artículo**
    **Campañas masivas**
    **Reportes:** Acceder a informes detallados.
    **Plantillas:** Gestionar las plantillas utilizadas en las campañas.
* **Herramientas:** Funciones de configuración y búsqueda.
    >**Configuración:** Acceder a los ajustes del sistema.

Al pie del menú también se encuentra la opción **Modo Oscuro** para cambiar la interfaz visual.

## 3. Gestión de Campañas

La sección de **Gestión de Campañas** es el centro de control donde se administran y monitorean todas las campañas promocionales del sistema. Se accede a esta vista haciendo clic en la opción **Campañas** del menú lateral izquierdo.

![Pantalla de Campaña](./imagen/campaña.png)

### Encabezado de Acciones

En la parte superior, encontrará las principales herramientas de gestión:

**Nueva Campaña:** Botón principal para iniciar el proceso de creación de una nueva promoción.

![Modal Nueva Campaña](./imagen/ModalAgregarCampaña.png)

Al hacer clic en **Nueva Campaña**, aparecerá un **modal** donde debe ingresar los detalles iniciales de la promoción:

> **Nombre de la Campaña.** (Ej. *Descuento Verano 2024*).
> **Prioridad:** Seleccione el nivel de importancia de la campaña a través de un desplegable con las opciones **Baja, Media, Alta o Muy Alta**. Esto ayuda a clasificar y priorizar la ejecución de la promoción dentro del sistema.
> **Descripción:** Resumen de los objetivos y características de la campaña.
> **Fecha de Inicio** y **Fecha de Fin:** Define el periodo de vigencia.
> **Tipo de Campaña:** Seleccione en el desplegable el Tipo de Campaña, eligiendo entre: **Cliente**, **Lista** o **Requisitos**.
>
> Una vez completados los campos, haga clic en **Crear Campaña** para guarda La camapaña.
>**Notificación de Éxito:** Al completar la creación, el sistema mostrará una notificación en la parte inferior derecha para confirmar que la campaña ha sido guardada.


**Agregar Cliente a Campaña:** Esta funcionalidad permite asociar uno o más clientes específicos a una campaña ya existente. Se accede haciendo clic en el botón **Agregar Cliente.**

![Modal Agregar Cliente1](./imagen/ModalAgregarCliente1.PNG)

>**Buscar Campaña:** Utilice la barra de búsqueda para encontrar la promoción deseada, escribiendo parte del **ID** o **nombre** de la campaña.
>**Selección:** Haga clic en la tarjeta de la campaña (ej. *normal osboter, ID: 13708*) para seleccionarla. El sistema resaltará la campaña elegida, habilitando el siguiente paso.

![Modal Agregar Cliente2](./imagen/ModalAgregarCliente2.PNG)

Una vez seleccionada la campaña, se habilita la búsqueda y adición individual de clientes:

>**Buscar Cliente por ID:** Ingrese el **ID** único del cliente que desea agregar al campo correspondiente (ej. *20144*).
>**Botón Buscar:** Presione el botón verde **Buscar**.
>**Resultado de la Búsqueda:** El sistema mostrará el nombre completo del cliente, su ID y su NIT (ej. *ROIDER MILLARES MANO*).
>**Botón Agregar:** Haga clic en el botón **+ Agregar** para añadir al cliente a una lista de espera temporal. Puede repetir este proceso para agregar múltiples clientes, buscando uno por uno.

![Modal Agregar Cliente3](./imagen/ModalAgregarCliente3.PNG)

>**Clientes Seleccionados:** A medida que agrega clientes, estos aparecerán listados en este apartado (ej. *Clientes Seleccionados (2)*), donde puede ver su nombre y su ID, y tiene la opción de removerlos (botón 'x') si cometió un error.
>**Agregar X Cliente(s):** Una vez que la lista de clientes seleccionados esté completa, haga clic en este botón para confirmar y guardar la asociación.
>
>**Cancelar:** Cierra el modal sin guardar los clientes agregados.

> **Notificaciones de Resultado:**
> **Éxito:** Si el cliente se inserta correctamente, aparecerá una notificación de **Éxito**.
> **Error:** Si el cliente ya existe en la campaña, el sistema mostrará una notificación de **Error** indicando que el cliente no puede ser agregado nuevamente.


**Agregar Artículo a Campaña:** Esta funcionalidad permite asociar productos específicos a una campaña promocional, definiendo sus condiciones de cantidad y precio. Se accede haciendo clic en el botón **Agregar Artículo** en el encabezado de la **Gestión de Campañas**.

![Modal Agregar Articulo 1](./imagen/ModalAgregarArticulo1.PNG)

> * **Buscar Campaña:** Utilice la barra de búsqueda para encontrar la promoción deseada, escribiendo parte del **ID** o **nombre** de la campaña.
> * **Selección de Campaña:** Haga clic en la tarjeta de la campaña (ej. *CAMP-000, ID: 13704*) para seleccionarla. El sistema resaltará la campaña elegida, habilitando el siguiente paso.

Una vez seleccionada la campaña, se habilita la búsqueda y adición del artículo:

>**Buscar Artículo:** Ingrese el **ID**, **nombre** o **descripción** del producto en el campo de búsqueda.
**Selección de Artículo:** Haga clic en la tarjeta del artículo deseado (ej. *AGUA CON GAS 1 LITRO OW, ID: 30-0-11-1*) para seleccionarlo.

![Modal Agregar Articulo 2](./imagen/ModalAgregarArticulo2.PNG)

Una vez seleccionado el artículo, debe configurar las condiciones promocionales:

>**Cantidad Mínima:** Ingrese la **cantidad mínima** de unidades que el cliente debe comprar para que aplique el precio promocional (ej. *1*).
>**Cantidad Máxima:** Ingrese la **cantidad máxima** de unidades a las que se puede aplicar el precio promocional (ej. *100*).
>**Precio Promocional:** Defina el **precio especial** que se aplicará al artículo (ej. *120*).

**Finalización de la Adición**

>**Agregar Artículo:** Una vez que todos los campos y selecciones estén correctos, haga clic en este botón para asociar el producto y sus condiciones a la campaña.
>**Cancelar:** Cierra el modal sin guardar el artículo ni las condiciones definidas.

> **Notificaciones de Resultado:**
> **Éxito:** Si el artículo se inserta correctamente, aparecerá una notificación de **Éxito**.
> **Error:** Si el artículo ya está asociado a esa campaña, el sistema mostrará una notificación de **Error** indicando que la inserción no se completó.


**Asociar Lista de Precios:** Esta funcionalidad permite vincular una lista de precios existente a una campaña promocional. Se accede haciendo clic en el botón **$ Lista Precios** en el encabezado de la **Gestión de Campañas**.

Al hacer clic, se abre el modal **"Asociar Lista de Precios"**:

![Modal Asociar Lista Precios 1](./imagen/ModalAsociarListaPrecios1.PNG)

>**Buscar Campaña:** Utilice la barra de búsqueda para encontrar la promoción deseada, escribiendo parte del **ID** o **nombre** de la campaña.
>**Selección de Campaña:** Haga clic en la tarjeta de la campaña (ej. *CAMP-000, ID: 13704*) para seleccionarla. El sistema resaltará la campaña elegida, habilitando el siguiente paso.

Una vez seleccionada la campaña, se habilita la búsqueda y selección de la lista de precios:

>**Buscar Lista de Precios:** Ingrese el **ID**, **nombre** o **categoría** de la lista de precios que desea asociar.
>**Selección de Lista:** Haga clic en la tarjeta de la lista de precios (ej. *AIDISA BENI - AGENCIAS, ID: 217*) para seleccionarla. El sistema resaltará la lista elegida.

![Modal Asociar Lista Precios 2](./imagen/ModalAsociarListaPrecios2.PNG)

**Finalización de la Asociación**

>**Asociar Lista:** Una vez que la campaña y la lista de precios han sido seleccionadas, haga clic en este botón verde para confirmar y guardar la asociación.
>**Cancelar:** Cierra el modal sin guardar la asociación.

> **Notificaciones de Resultado:**
> **Éxito:** Si la lista de precios se asocia correctamente a la campaña, aparecerá una notificación de **Éxito**.
> **Error:** Si la lista de precios ya está asociada a la campaña, el sistema mostrará una notificación de **Error** indicando que la asociación no se completó.


**Agregar Requisito:** Esta funcionalidad permite establecer las condiciones mínimas de compra de un artículo que un cliente debe cumplir para poder acceder a una promoción. Se accede haciendo clic en el botón **Requisitos** en el encabezado de la **Gestión de Campañas**.

Al hacer clic, se abre el modal **"Agregar Requisito"**:

![Modal Agregar Requisito 1](./imagen/ModalAgregarRequisito1.PNG)

>**Buscar Campaña:** Utilice la barra de búsqueda para encontrar la promoción a la que se vinculará el requisito, escribiendo parte del **ID** o **nombre** de la campaña.
> **Selección de Campaña:** Haga clic en la tarjeta de la campaña (ej. *CAMP-000, ID: 13704*) para seleccionarla. El sistema resaltará la campaña elegida.

Una vez seleccionada la campaña, se procede a definir el artículo y sus condiciones de requisito:

> **Buscar Artículo:** Ingrese el **ID**, **nombre** o **descripción** del producto que será el requisito en el campo de búsqueda.
> **Selección de Artículo:** Haga clic en la tarjeta del artículo deseado (ej. *AGUA CON GAS 1 LITRO OW*) para seleccionarlo.

![Modal Agregar Requisito 2](./imagen/ModalAgregarRequisito2.PNG)

Una vez seleccionado el artículo, debe configurar las condiciones que el cliente debe cumplir:

>**Cantidad Requerida:** Ingrese la **cantidad mínima** de unidades de este artículo que el cliente debe poseer o comprar para aplicar a la promoción (ej. *1*).
>**Cantidad Mínima / Máxima:** Estos campos definen el rango de unidades al cual se aplicarán las condiciones del requisito.
>**Precio Promocional:** El precio especial o valor asociado a la condición del requisito.

**Finalización de la Adición**

>**Agregar Requisito:** Una vez que todos los campos de condición estén definidos, haga clic en este botón verde para guardar el requisito y asociarlo a la campaña.
>**Cancelar:** Cierra el modal sin guardar el requisito.

> **Notificaciones de Resultado:**
> **Éxito:** Si el requisito se inserta correctamente en la campaña, aparecerá una notificación de **Éxito**.
> **Error:** Si el artículo ya ha sido definido como requisito para esa campaña, el sistema mostrará una notificación de **Error** indicando que la operación no se completó.

## 4. Crear Nueva Campaña

Al seleccionar la opción **Crear Campaña** en el menú de **Gestión Principal**, se accede a una vista detallada para configurar la promoción desde cero. Esta vista se divide en dos pestañas principales: **General** y **Artículos**.

### Pestaña General

Esta pestaña permite configurar los datos básicos y las condiciones principales de la campaña.

![Modal CrearCampaña](./imagen/crearCampaña1.PNG)

#### Información General

>**Nombre de la Campaña:** Ingrese un nombre descriptivo para la promoción (Ej. *Promoción Verano 2024*).
**Prioridad:** Utilice el desplegable para seleccionar el nivel de importancia: **Baja**, **Media**, **Alta** o **Muy Alta**.
**Tipo de Campaña:** Seleccione en el desplegable la modalidad:
    * Si elige **Por Cliente**, se habilitará la pestaña **Clientes**.
    * Si elige **Por Lista**, se habilitará la pestaña **Listas**.
**Requiere Requisito:** Es un campo **opcional**. Marque esta casilla (**check**) si desea que la promoción solo aplique a clientes que cumplan una condición previa (ej. comprar un artículo mínimo). Al marcarlo, se habilita la pestaña **Requisitos**.
**Descripción, Fecha de Inicio / Fin, y Estado:** Defina los demás detalles de la campaña.


### Pestaña Artículos

Esta pestaña está siempre disponible y se utiliza para configurar los productos que forman parte de la promoción.

![Modal CrearCampañaArticulo](./imagen/crearCampañaArticulo.PNG)

Agregar Nuevos Productos

>**Acción:** Haga clic en el botón verde **Agregar Artículo** ubicado en la esquina superior derecha del panel.
**Resultado:** Cada clic agrega un nuevo bloque de campos vacío, lo que le permite configurar un producto promocional adicional, como se muestra a continuación:

![Modal CrearCampañaArticulo](./imagen/crearCampañaArticulo1.PNG)

Configurar los Parámetros del Artículo

Por cada bloque de artículo agregado, debe configurar los siguientes campos:

>**ID Artículo:** Seleccione el producto que formará parte de la promoción. Al hacer clic en el campo de selección, se desplegará un **buscador** que permite encontrar el artículo.
    **Búsqueda:** Puede buscar productos tanto por **ID (código)** como por **Nombre**.
    **Selección:** Al hacer scroll o escribir las primeras letras, el sistema filtra y muestra la lista de artículos disponibles. Simplemente haga clic en el artículo Requerido para seleccionarlo.

![Modal CrearCampañaArticulo](./imagen/crearCampañaArticulo2.PNG)

>**Cantidad Mínima / Cantidad Máxima:** Defina el rango de unidades que el cliente debe comprar para que se aplique el precio promocional.
**Precio Promocional:** Introduzca el precio especial que tendrá el producto dentro de esta campaña.
**Eliminar:** Utilice el ícono del basurero (papelera) rojo al final del bloque para eliminar ese producto específico de la campaña.

![Modal CrearCampañaArticulo](./imagen/crearCampañaArticulo3.PNG)

Una vez que haya configurado todos los artículos, puede proceder a las pestañas **Listas** o **Requisitos** para finalizar la creación de la campaña.

### Pestañas Clientes / Listas

Una de estas pestañas se habilitará automáticamente según el **Tipo de Campaña** seleccionado en la Pestaña General:

#### A. Pestaña Clientes (Si Tipo de Campaña = Por Cliente)

>**Buscar Cliente por ID:** Permite buscar clientes de forma individual, ingresando su ID (clíid).
**Clientes Seleccionados:** Muestra una lista temporal de clientes agregados. Al hacer clic en **+ Agregar X Cliente(s)**, estos se asocian permanentemente a la campaña, apareciendo en **Clientes de la Campaña**.

![Pestaña Clientes en Crear Campaña](./imagen/crearCampañaCliente.PNG)

>**Búsqueda Exitosa** | Al ingresar el ID y hacer clic en **Buscar**, el sistema muestra el cliente encontrado con su ID, NIT y nombre. Un botón **+ Agregar** aparece al lado derecho. |
| **Cliente Encontrado y Agregado a Selección Temporal** | Al hacer clic en **+ Agregar**, el cliente se mueve inmediatamente al campo **Clientes Seleccionados** como un tag (`Roider Millares Mano (201444)`). |
| **Búsqueda Fallida** | Si el ID ingresado no existe, se muestra un mensaje de "No hay cliente" o similar en el área de resultados.

![Pestaña Clientes en Crear Campaña](./imagen/crearCampañaCliente1.PNG)

**Clientes Seleccionados:** Muestra una lista temporal de clientes. Para asociarlos a la campaña, debe finalizar el proceso.

![Pestaña Clientes en Crear Campaña](./imagen/crearCampañaCliente2.PNG)

**Confirmar Adición** | Se hace clic en el botón **+ Agregar X Cliente(s)** (donde X es el número de clientes seleccionados). 
**Clientes de la Campaña** | El cliente se asocia de forma permanente y se lista en la sección **Clientes de la Campaña (X)**, mostrando su ID y nombre (`201444 - Roider Millares Mano`). Se incluye un ícono de eliminación Para Eliminar el Cliente.

![Pestaña Clientes en Crear Campaña](./imagen/crearCampañaCliente3.PNG)

#### B. Pestaña Listas (Si Tipo de Campaña = Por Lista)

>**Listas de Precios:** Permite asociar una o varias listas de precios específicas a la campaña.
**Buscar Lista:** Utilice el campo para buscar y agregar listas de precios, las cuales aparecerán en **Listas Agregadas**.

![Pestaña Listas en Crear Campaña](./imagen/crearCampañaLista1.PNG)

>**Buscar/Seleccionar** Al hacer clic en el campo **Buscar lista...**, se despliega una lista de todas las listas de precios disponibles, las cuales pueden ser filtradas por ID o nombre. Ejemplo: `217 - AIDISA BENI - AGENCIAS`.
**Selección Múltiple**  Puedes seleccionar una lista a la vez. Cada vez que seleccionas una, esta se agrega a la sección **Listas Agregadas** y puedes volver a hacer clic en el campo **Buscar lista...** para seleccionar otra.

![Pestaña Listas en Crear Campaña](./imagen/crearCampañaLista2.PNG)

**Listas Agregadas (X):** Muestra el listado de todas las listas de precios que han sido seleccionadas y asociadas a la campaña.

>**Visualización:** Cada lista se muestra con su ID y nombre (Ejemplo: `48 - AIDISA BENI`).
**Eliminación:** Cada lista cuenta con un ícono (papelera) para poder eliminarla de la lista de asociación antes de guardar la campaña.
**Guardar Campaña:** Una vez que todas las listas deseadas están agregadas, se hace clic en el botón **Guardar Campaña** ubicado en la parte inferior derecha para finalizar la creación o edición de la campaña con las listas asociadas.

![Pestaña Listas en Crear Campaña](./imagen/crearCampañaLista3.PNG)

### Pestaña Requisitos (Condicional)

Esta pestaña solo se habilita si se marca la opción **Requiere Requisito** en la Pestaña General.

>**Requisitos de la Campaña:** Permite configurar los artículos y las cantidades mínimas que el cliente debe comprar o poseer para calificar a la promoción.
**+ Agregar Requisito:** Utilice este botón para añadir una nueva fila de requisitos, donde podrá seleccionar el artículo y definir la **Cantidad Requerida**, **Cantidad Mínima/Máxima** y el **Precio Promocional** asociado a la condición.

![Pestaña Requisitos en Crear Campaña](./imagen/crearCampañaRequisito.PNG)


### Guardar Campaña

* **Guardar Campaña:** Haga clic en este botón verde para registrar la campaña con toda la configuración definida en las pestañas.
* **Cancelar:** Descarta todos los cambios y regresa a la vista anterior.

## 5. Carga Masiva (Lista Precio Articulo)


La funcionalidad de **Carga Masiva** guía al usuario a través de un asistente de **5 Pasos** para importar listas de precios por artículo de manera eficiente, asegurando la **validación de los datos antes de la inserción**.


**Paso 1: Descargar Plantilla**

>**Al darle a descargar Plantilla:**  
Obtiene la plantilla oficial **`.XLSX`** que define las columnas requeridas por el sistema.
**Acción:**  
Haga clic en el botón **"Descargar Plantilla .XLSX"**.
**Avanzar:**  
Haga clic en **"Siguiente"** para continuar.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio1.PNG)

**Paso 2: Cargar Archivo**

Subir el archivo Excel con los datos de precios actualizados. Arrastrando el Archivo o Dando Click Para seleccionar el Archivo.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio2.PNG)

>**Objetivo:**  
Subir el archivo **Excel** llenado con los datos de Lista Precio Articulo
**Acción:**  
Arrastre o haga clic en el área de carga para seleccionar su archivo.
**Vista Previa:**  
El archivo subido (por ejemplo: `CargaLISTAPRECIOMASIVA(1).xlsx`) aparecerá listado con el estado **Pendiente**.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio3.PNG)
**Avanzar:**  
Haga clic en **"Siguiente"**.


**Paso 3: Validar Datos**


Verificar la integridad y estructura de los datos antes de insertarlos en la base de datos.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio4.PNG)

>**Acción:**  
Haga clic en **"Validar Todos"** para iniciar la verificación de los archivos pendientes.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio5.PNG)

>**Resultado:**  
Si es exitoso, el estado cambia a **Validado** y se confirma que los registros están listos para insertar.
si es Error Se listan errores de validación por fila.

**Avanzar:**  
Haga clic en **"Siguiente"** una vez que el archivo esté validado.


**Paso 4: Editar Datos**

Revisar y realizar **correcciones manuales** a los datos validados antes de la inserción.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio6.PNG)

>**Acción:**  
Despliegue el archivo haciendo clic en su nombre. Se mostrará una **tabla con los datos cargados**.

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio7.PNG)

>**Corrección:**  
Puede **editar los valores directamente** en la tabla y luego hacer clic en **"Guardar Cambios"**.

**Avanzar:**  
Haga clic en **"Siguiente"**.



**Paso 5: Insertar en BD**

Ejecutar la **carga de los registros validados y corregidos** a la Base de Datos (BD).

![Pestaña ListaPrecioArticulo](./imagen/CargaMasivaListaPrecio8.PNG)

**Resumen:**  
Se muestra el **total de registros listos para insertar**.

**Acción Final:**  
Haga clic en el botón **"Insertar X registros"** para iniciar el proceso.

**Control:**  
Use el botón **"Cancelar"** para detener la inserción si es necesario.

## 6. Carga Masiva (Campaña Masiva)

La funcionalidad de **Carga Masiva** permite crear campañas de manera eficiente, utilizando plantillas de Excel(.xlsx) para importar grandes volúmenes de datos. Se accede seleccionando **Carga Masiva** en el menú de Gestión Principal. El proceso está guiado por Pasos de **1 a 5 pasos**.

elegimos Que Tipo de Carga Vamos a Realizar


![Pestaña Requisitos en Crear Campaña](./imagen/CargaMasiva1.png)

**Paso 1: Seleccionar Tipo de Carga (Por Cliente)**

Este primer paso define la estructura de los datos que se importarán.

![Pestaña Requisitos en Crear Campaña](./imagen/CargaMasivaPorCliente1.png)

>**Configuración de Carga:** Utilice el menú desplegable **Tipo de Carga** para seleccionar la modalidad de importación.
**Opción seleccionada:** **Campaña por Cliente** (Crea campañas asociadas a clientes específicos con artículos y requisitos).
**Detalles del Tipo Seleccionado:** El sistema le indica los archivos y hojas esperados.
    **Archivo esperado:** `CampañaPorCliente.xlsx`
    **Hoja requerida:** `PorCliente`
**Acción:** Confirme la selección y haga clic en **Siguiente**

**Paso 2: Cargar Archivos**

Este paso se enfoca en proporcionar el archivo de datos.

![Pantalla paso 2.1](./imagen/CargaMasivaPorCliente2.png)

>**Preparación de la Plantilla:** Consulte la pestaña **Instrucciones** para ver la estructura requerida para la carga por cliente.
    * **Columnas Clave:** Se esperan grupos de columnas como `campaigns/*`, `articles/*`, `clients/*`, y `requirements/*` (opcional).
**Validaciones:** Se realizan verificaciones sobre la prioridad, rangos de cantidad y precios correctos.
**Subida de Archivo:** Utilice la zona de carga para subir su archivo **Excel** (`.xlsx`) ya preparado.
**Archivos Cargados:** Los archivos subidos aparecerán listados con estado '**pending**' (pendiente).
**Acción:** Suba el archivo y haga clic en **Siguiente**.

![Pantalla paso 2.2](./imagen/CargaMasivaPorCliente3.png)

**Paso 3: Validar Archivos**

En este paso se inicia la verificación de los datos.

![Pantalla paso 3](./imagen/CargaMasivaPorCliente4.png)
>**Botón Validar Todos:** Haga clic en este botón para que el sistema inicie el proceso de lectura, validación de estructura y validación de datos de todos los archivos en estado 'pending'.
**Progreso:** El estado de cada archivo se actualiza, mostrando el progreso de la validación.
**Resultados de la Validación:**
    * Estado '**validated**' (Validado): Indica que el archivo es correcto y está listo para ser revisado y guardado. Se muestra una notificación de **Éxito** (ej. "X registros listos para revisar").
    * Estado '**error**' (Error): Se encontraron errores de datos o formato. El sistema proporciona un mensaje de **Error** detallando los fallos (ej. "Fila X: Campo Y - Mensaje de error").
**Acción:** Asegúrese de que todos los archivos estén en estado '**validated**'. Si hay errores, debe corregir el archivo Excel original y volver a subirlo. Haga clic en **Siguiente**.

**Validado**
![Pantalla paso 3](./imagen/CargaMasivaPorCliente7.png)

**Error**
![Pantalla paso 3](./imagen/CargaMasivaPorCliente6.png)

**Paso 4: Previsualizar y Editar Datos**

Este paso permite una revisión de los datos validados y la corrección manual antes de la inserción final.

>**Acordeón de Archivos:** Los archivos validados se agrupan. Al desplegar cada uno, se muestra una **tabla de datos** donde puede previsualizar y editar los registros cargados. **Haciendo Click Al Nombre Del Archivo** Muestra todos Los Datos Que Contiene

![Pantalla paso 4](./imagen/CargaMasivaPorCliente8.png)

>**Edición de Datos:** Puede modificar los valores de las celdas **directamente en la tabla**.
**Guardar Cambios:** Las modificaciones se guardan internamente en el sistema antes de la inserción a la base de datos, lo cual se confirma con una notificación de **Éxito** (ej. "X registros actualizados").
**Acción:** Revise los registros y haga los ajustes finales. Haga clic en **Siguiente**.


![Pantalla paso 4](./imagen/CargaMasivaPorCliente9.png)

**Paso 5: Revisar y Acciones Finales**

El último paso confirma la cantidad de datos a insertar y ejecuta la acción final.

![Pantalla paso 5](./imagen/CargaMasivaPorCliente10.png)

**Resumen:** Muestra la cantidad de archivos validados y el total de registros listos para la inserción en la **Base de Datos (BD)**.
**Acciones:**
    **Insertar en BD:** Ejecuta la Carga Masiva. Al hacer clic, el sistema procesa los datos validados.
        **Éxito:** Muestra una notificación indicando cuántos archivos se insertaron correctamente (ej. "X archivo(s) insertado(s) correctamente").
        **Error:** Si hay fallas al comunicarse con el servidor o al insertar datos, se mostrará un mensaje de **Error al insertar datos**.
    **Descargar JSON:** Permite descargar todos los registros validados en formato `.json` para uso externo.
**Acción:** Haga clic en **Insertar en BD** para finalizar la Carga Masiva.

![Pantalla paso 5](./imagen/CargaMasivaPorCliente11.png)

## 7 Configuraciones.


**Configuración General:**: Personalización de apariencia y preferencias
**Perfil de Usuario:**  Información personal y gestión de seguridad

![Pantalla configuraciones](./imagen/configuracion.PNG)

#### Tema
>- **Propósito**: Seleccionar el esquema de colores del sistema
>- **Opciones disponibles**:
>   `Claro`: Interfaz con colores claros
>   `Oscuro`: Interfaz con colores oscuros
>   `Sistema`: Se adapta automáticamente a la configuración del dispositivo del usuario

#### Tamaño de Fuente
>- **Propósito**: Ajustar el tamaño del texto en toda la interfaz
>- **Opciones disponibles**:
   `Pequeño`: Texto de tamaño reducido
   `Mediano`: Texto de tamaño estándar (recomendado)
   `Grande`: Texto de tamaño ampliado para mejor legibilidad


#### Notificaciones del Sistema
>- **Propósito**: Activar/desactivar notificaciones en tiempo real dentro de la aplicación
>- **Funcionalidad**: Muestra alertas y mensajes emergentes durante el uso

#### Botón "Guardar Cambios"
>- **Propósito**: Aplicar todas las configuraciones modificadas
>- **Comportamiento**:
   Muestra spinner de carga durante el proceso
   Emite mensaje de confirmación al completar
   Las preferencias se aplican inmediatamente

#### Botón "Restablecer"
>- **Propósito**: Volver a la configuración predeterminada del sistema
>- **Efecto**:
   Restaura todos los valores por defecto
   Cambia el tema a "Sistema"
   Emite mensaje de confirmación



### Información Personal

#### Cabecera de Perfil
> **Avatar**: Imagen o iniciales basadas en el nombre de usuario
 **Nombre completo**: Muestra el nombre real del usuario
 **Correo electrónico**: Dirección de email institucional
 **Departamento**: Área o departamento asignado

![Pantalla configuraciones](./imagen/configuracion1.PNG)

#### Datos de Solo Lectura


>**Nombre de usuario**: Identificador único en el sistema
**Nombre completo**: Nombre y apellidos
**Correo electrónico**: Dirección corporativa
**Departamento**: Unidad organizativa
**Roles**: Lista de permisos y niveles de acceso asignados

### Cambio de Contraseña


![Pantalla configuraciones](./imagen/configuracion2.PNG)
#### Políticas de Seguridad
> **Longitud mínima:** 8 caracteres
 **Requisito de Contraseña:** Al menos una letra mayúscula (A-Z), Al menos un número (0-9) O un carácter especial
 **Restricción histórica:** No se pueden reutilizar contraseñas anteriores.
 **Cambio obligatorio**: El sistema solicita cambio automáticamente cada 60 días por políticas de seguridad

#### Proceso Paso a Paso

##### Campo "Contraseña actual"
>**Propósito**: Verificar la identidad del usuario
 **Requisito**: Debe coincidir con la contraseña vigente

##### Campo "Nueva contraseña"
> **Propósito**: Establecer la nueva credencial
> **Validaciones**:
>  - Mínimo 8 caracteres
>  - Al menos una letra mayúscula (A-Z) 
>  - Al menos un número (0-9) O un carácter especial
>  - No puede ser igual a contraseñas anteriores (últimos 60 días)

##### Campo "Confirmar nueva contraseña"
> **Propósito**: Verificar que la nueva contraseña se haya escrito correctamente
 **Validación**: Debe coincidir exactamente con el campo "Nueva contraseña"

##### Botón "Cambiar contraseña"
- **Acción**: Envía la solicitud de cambio al servidor
- **Indicador visual**: Muestra spinner de carga durante el proceso
- **Comportamiento post-cambio**:
  - Limpia automáticamente todos los campos
  - Muestra mensaje de confirmación
  - Registra el cambio para el historial de contraseñas

#### Mensajes de Error y Validación

| Error | Mensaje | Causa |
|-------|---------|-------|
| Contraseñas no coinciden | "Las contraseñas no coinciden" | Los campos nueva y confirmación son diferentes |
| Contraseña muy corta | "La contraseña debe tener al menos 8 caracteres" | No cumple longitud mínima |
| Error de servidor | Mensaje específico del sistema | Problemas de conexión o validación en backend |
| Contraseña anterior | "No puede utilizar contraseñas anteriores" | Intento de reutilizar contraseña histórica |
