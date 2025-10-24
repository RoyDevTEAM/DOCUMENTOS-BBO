# Manual de Usuario

## 1. Login | Inicio de Sesion

El sistema ofrece **dos métodos de inicio de sesión**
- **Active Directory (AD):** Utiliza la **cuenta de correo corporativa**, es decir, el mismo **usuario y contraseña** que se emplea para iniciar sesión en los equipos del trabajo (Laptop o PC).  

- **Unity:** Es el método de autenticación propio del sistema **Unity**, diseñado para usuarios con cuentas específicas del sistema.

![Pantalla de Login](./imagen/login.png)

El usuario debe seleccionar el método de inicio de sesión que desea utilizar e ingresar sus **credenciales correspondientes** (usuario y contraseña) para acceder al sistema.

## 2. Dashboard Del Sistema

El **Dashboard** (Tablero Principal) es la primera pantalla que se visualiza al ingresar al sistema. Está diseñado para ofrecer una **visión general y rápida** de lo que Ofrece el Sistema.

En el lado izquierdo de la pantalla se encuentra el menú de navegación, dividido en dos secciones:

![Pantalla De Dashboard](./imagen/Dashboard.png)
* **Gestición Principal:** Permite acceder a las funciones principales del sistema:
    * **Dashboard:** La vista actual.
    * **Campañas:** Gestionar y ver todas las campañas.
    * **+ Crear Campaña:** Iniciar el proceso de creación de una nueva campaña.
    * **Carga Masiva:** Funcionalidad para cargar datos o campañas de forma masiva.
    * **Reportes:** Acceder a informes detallados.
    * **Plantillas:** Gestionar las plantillas utilizadas en las campañas.
* **Herramientas:** Funciones de configuración y búsqueda.
    * **Buscar:** Para encontrar elementos dentro del sistema.
    * **Configuración:** Acceder a los ajustes del sistema.

Al pie del menú también se encuentra la opción **Modo Oscuro** para cambiar la interfaz visual.

## 3. Gestión de Campañas

La sección de **Gestión de Campañas** es el centro de control donde se administran y monitorean todas las campañas promocionales del sistema. Se accede a esta vista haciendo clic en la opción **Campañas** del menú lateral izquierdo.

![Pantalla de Campaña](./imagen/campaña.png)

### Encabezado de Acciones

En la parte superior, encontrará las principales herramientas de gestión:

**Nueva Campaña:** Botón principal para iniciar el proceso de creación de una nueva promoción.

![Modal Nueva Campaña](./imagen/ModalAgregarCampaña.png)

Al hacer clic en **Nueva Campaña**, aparecerá un **modal** donde debe ingresar los detalles iniciales de la promoción:

> * **Nombre de la Campaña.** (Ej. *Descuento Verano 2024*).
> * **Prioridad:** Seleccione el nivel de importancia de la campaña a través de un desplegable con las opciones **Baja, Media, Alta o Muy Alta**. Esto ayuda a clasificar y priorizar la ejecución de la promoción dentro del sistema.
> * **Descripción:** Resumen de los objetivos y características de la campaña.
> * **Fecha de Inicio** y **Fecha de Fin:** Define el periodo de vigencia.
> * **Tipo de Campaña:** Seleccione en el desplegable el Tipo de Campaña, eligiendo entre: **Cliente**, **Lista** o **Requisitos**.
>
> Una vez completados los campos, haga clic en **Crear Campaña** para guarda La camapaña.
>**Notificación de Éxito:** Al completar la creación, el sistema mostrará una notificación en la parte inferior derecha para confirmar que la campaña ha sido guardada.
>

**Agregar Cliente a Campaña:** Esta funcionalidad permite asociar uno o más clientes específicos a una campaña ya existente. Se accede haciendo clic en el botón **Agregar Cliente.**

![Modal Agregar Cliente1](./imagen/ModalAgregarCliente1.PNG)

>* **Buscar Campaña:** Utilice la barra de búsqueda para encontrar la promoción deseada, escribiendo parte del **ID** o **nombre** de la campaña.
>* **Selección:** Haga clic en la tarjeta de la campaña (ej. *normal osboter, ID: 13708*) para seleccionarla. El sistema resaltará la campaña elegida, habilitando el siguiente paso.

![Modal Agregar Cliente2](./imagen/ModalAgregarCliente2.PNG)

Una vez seleccionada la campaña, se habilita la búsqueda y adición individual de clientes:

>* **Buscar Cliente por ID:** Ingrese el **ID** único del cliente que desea agregar al campo correspondiente (ej. *20144*).
>* **Botón Buscar:** Presione el botón verde **Buscar**.
>* **Resultado de la Búsqueda:** El sistema mostrará el nombre completo del cliente, su ID y su NIT (ej. *ROIDER MILLARES MANO*).
>* **Botón Agregar:** Haga clic en el botón **+ Agregar** para añadir al cliente a una lista de espera temporal. Puede repetir este proceso para agregar múltiples clientes, buscando uno por uno.

![Modal Agregar Cliente3](./imagen/ModalAgregarCliente3.PNG)

>* **Clientes Seleccionados:** A medida que agrega clientes, estos aparecerán listados en este apartado (ej. *Clientes Seleccionados (2)*), donde puede ver su nombre y su ID, y tiene la opción de removerlos (botón 'x') si cometió un error.


>* **Agregar X Cliente(s):** Una vez que la lista de clientes seleccionados esté completa, haga clic en este botón para confirmar y guardar la asociación.
>
>* **Cancelar:** Cierra el modal sin guardar los clientes agregados.

> **Notificaciones de Resultado:**
> * **Éxito:** Si el cliente se inserta correctamente, aparecerá una notificación de **Éxito**.
> * **Error:** Si el cliente ya existe en la campaña, el sistema mostrará una notificación de **Error** indicando que el cliente no puede ser agregado nuevamente.
