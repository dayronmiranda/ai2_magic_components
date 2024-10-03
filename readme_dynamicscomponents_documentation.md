# Documentación Completa de la Extensión DynamicComponents para MIT App Inventor

## Índice

- [Introducción](#introducción)
- [Instalación](#instalación)
- [Descripción General](#descripción-general)
- [Clases Principales](#clases-principales)
  - [DynamicComponents](#dynamiccomponents)
  - [Metadata](#metadata)
  - [Utils](#utils)
- [Métodos y Funciones de DynamicComponents](#métodos-y-funciones-de-dynamiccomponents)
  - [Create](#create)
  - [GetComponent](#getcomponent)
  - [SetProperty](#setproperty)
  - [GetProperty](#getproperty)
  - [SetProperties](#setproperties)
  - [GetProperties](#getproperties)
  - [CallFunction](#callfunction)
  - [GetId](#getid)
  - [GetType](#gettype)
  - [Exists](#exists)
  - [Remove](#remove)
  - [RemoveAll](#removeall)
  - [GetAllIds](#getallids)
  - [AnyComponent](#anycomponent)
  - [VersionName](#versionname)
  - [VersionCode](#versioncode)
- [Clases Auxiliares](#clases-auxiliares)
  - [Metadata](#metadata-detallado)
    - [Descripción](#descripción-de-metadata)
    - [Métodos Principales](#métodos-principales-de-metadata)
  - [Utils](#utils-detallado)
    - [Descripción](#descripción-de-utils)
    - [Métodos Principales](#métodos-principales-de-utils)
- [Ejemplos de Uso](#ejemplos-de-uso)
- [Consideraciones Adicionales](#consideraciones-adicionales)
- [Créditos](#créditos)

## Introducción

La extensión **DynamicComponents** para MIT App Inventor permite a los desarrolladores crear y manipular componentes de interfaz de usuario dinámicamente en tiempo de ejecución. Esto proporciona una gran flexibilidad para construir aplicaciones más interactivas y adaptativas.

## Instalación

1. Descargue el archivo `.aix` desde el [repositorio oficial](https://github.com/ysfchn/DynamicComponents-AI2).
2. En MIT App Inventor, vaya a **Extensiones** > **Importar extensión**.
3. Seleccione el archivo `.aix` descargado e impórtelo.
4. La extensión aparecerá en la paleta de componentes bajo **Extensiones**.

## Descripción General

La extensión está compuesta por las siguientes clases:

- **DynamicComponents**: Clase principal que expone métodos para crear y manipular componentes dinámicos.
- **Metadata**: Gestiona los metadatos de los componentes, como propiedades y métodos. Esta clase es fundamental para el funcionamiento interno de la extensión, ya que permite acceder y manipular propiedades y métodos de los componentes mediante reflexión.
- **Utils**: Proporciona utilidades auxiliares para operaciones comunes y conversión de tipos. Esta clase es esencial para manejar conversiones de datos, ejecución en el hilo de la interfaz de usuario y otras operaciones de soporte.

## Clases Principales

### DynamicComponents

La clase `DynamicComponents` es la principal de la extensión y extiende `AndroidNonvisibleComponent` e implementa `Component`. Proporciona todos los métodos necesarios para crear y manipular componentes dinámicamente.

#### Constructor


public DynamicComponents(ComponentContainer container)


- **Descripción**: Inicializa una nueva instancia de `DynamicComponents`.
- **Parámetros**:
  - `container`: El contenedor de componentes de MIT App Inventor.

#### Atributos Internos

- `components`: Un `HashMap` que almacena los componentes creados dinámicamente, utilizando sus identificadores como claves.
- `metadata`: Una instancia de la clase `Metadata` para acceder a los metadatos de los componentes.
- `container`: El contenedor principal donde se inicializa la extensión.

### Metadata

La clase `Metadata` maneja la obtención y almacenamiento de metadatos de los componentes, facilitando el acceso a sus propiedades y métodos mediante reflexión.

#### Importancia de Metadata

La clase `Metadata` es crucial para la extensión, ya que permite:

- Obtener información detallada de las propiedades y métodos disponibles en los componentes.
- Acceder y modificar propiedades y métodos en tiempo de ejecución.
- Almacenar en caché la información de metadatos para mejorar el rendimiento.

### Utils

La clase `Utils` proporciona métodos auxiliares para operaciones comunes, como conversión de tipos, manejo de excepciones y acceso a campos y métodos privados mediante reflexión.

#### Importancia de Utils

La clase `Utils` es esencial para:

- Convertir valores entre diferentes tipos de datos.
- Ejecutar acciones en el hilo de la interfaz de usuario.
- Acceder a métodos y campos privados de los componentes.
- Manejar excepciones y errores de manera consistente.

## Métodos y Funciones de DynamicComponents

A continuación, se detallan todos los métodos y funciones disponibles en la clase `DynamicComponents`.

### Create


@SimpleFunction(description = "Crea un nuevo componente dinámicamente y lo agrega al contenedor especificado.")
public void Create(String componentName, Object id, Object parent)


- **Descripción**: Crea un componente del tipo `componentName`, le asigna un identificador `id` y lo agrega al `parent`.
- **Parámetros**:
  - `componentName`: Nombre del componente a crear (por ejemplo, `"Button"`, `"Label"`).
  - `id`: Identificador único para el componente.
  - `parent`: Contenedor o componente padre donde se agregará el nuevo componente.
- **Implementación Interna**:
  - Utiliza la clase `Metadata` para obtener la clase correspondiente al `componentName`.
  - Usa `Utils.getObject` para crear una instancia del componente.
  - Agrega el componente al contenedor especificado.
  - Almacena el componente en el `HashMap` `components` con su `id`.

### GetComponent


@SimpleFunction(description = "Obtiene la instancia del componente dinámico con el identificador especificado.")
public AndroidViewComponent GetComponent(Object id)


- **Descripción**: Devuelve la instancia del componente asociado al `id`.
- **Parámetros**:
  - `id`: Identificador del componente.
- **Retorno**: Instancia de `AndroidViewComponent`.
- **Implementación Interna**:
  - Recupera el componente del `HashMap` `components` utilizando el `id`.

### SetProperty


@SimpleFunction(description = "Establece el valor de una propiedad del componente especificado.")
public void SetProperty(Object id, String propertyName, Object value)


- **Descripción**: Establece el valor de la propiedad `propertyName` del componente con `id`.
- **Parámetros**:
  - `id`: Identificador del componente.
  - `propertyName`: Nombre de la propiedad.
  - `value`: Nuevo valor para la propiedad.
- **Implementación Interna**:
  - Utiliza `Metadata` para obtener el método `setter` correspondiente a la propiedad.
  - Usa `Utils.castValue` para convertir el `value` al tipo adecuado.
  - Invoca el método `setter` en el componente.

### GetProperty


@SimpleFunction(description = "Obtiene el valor de una propiedad del componente especificado.")
public Object GetProperty(Object id, String propertyName)


- **Descripción**: Obtiene el valor de la propiedad `propertyName` del componente con `id`.
- **Parámetros**:
  - `id`: Identificador del componente.
  - `propertyName`: Nombre de la propiedad.
- **Retorno**: Valor de la propiedad.
- **Implementación Interna**:
  - Utiliza `Metadata` para obtener el método `getter` correspondiente a la propiedad.
  - Invoca el método `getter` en el componente y devuelve el valor.

### SetProperties


@SimpleFunction(description = "Establece múltiples propiedades del componente especificado.")
public void SetProperties(Object id, YailDictionary properties)


- **Descripción**: Establece múltiples propiedades del componente usando un diccionario.
- **Parámetros**:
  - `id`: Identificador del componente.
  - `properties`: Diccionario con pares `propiedad: valor`.
- **Implementación Interna**:
  - Itera sobre el diccionario y llama a `SetProperty` para cada par.

### GetProperties


@SimpleFunction(description = "Obtiene un diccionario con todas las propiedades del componente especificado.")
public YailDictionary GetProperties(Object id)


- **Descripción**: Devuelve un diccionario con todas las propiedades y sus valores actuales.
- **Parámetros**:
  - `id`: Identificador del componente.
- **Retorno**: `YailDictionary` con propiedades y valores.
- **Implementación Interna**:
  - Utiliza `Metadata` para obtener la lista de propiedades.
  - Itera sobre las propiedades y usa `GetProperty` para obtener los valores.

### CallFunction


@SimpleFunction(description = "Llama a un método del componente especificado con los argumentos proporcionados.")
public Object CallFunction(Object id, String functionName, Object... args)


- **Descripción**: Invoca un método `functionName` del componente con `id` y pasa los argumentos `args`.
- **Parámetros**:
  - `id`: Identificador del componente.
  - `functionName`: Nombre del método a invocar.
  - `args`: Argumentos para el método.
- **Retorno**: Resultado de la invocación del método.
- **Implementación Interna**:
  - Utiliza `Metadata` para obtener el método correspondiente.
  - Convierte los argumentos al tipo correcto usando `Utils.castValue`.
  - Invoca el método en el componente.

### GetId


@SimpleFunction(description = "Obtiene el identificador del componente proporcionado.")
public Object GetId(AndroidViewComponent component)


- **Descripción**: Devuelve el identificador asociado al componente dinámico.
- **Parámetros**:
  - `component`: Instancia del componente.
- **Retorno**: Identificador del componente.
- **Implementación Interna**:
  - Recorre el `HashMap` `components` para encontrar la clave que corresponde al componente dado.

### GetType


@SimpleFunction(description = "Obtiene el tipo de componente del componente especificado.")
public String GetType(Object id)


- **Descripción**: Devuelve el tipo (clase) del componente asociado al `id`.
- **Parámetros**:
  - `id`: Identificador del componente.
- **Retorno**: Nombre del tipo de componente.
- **Implementación Interna**:
  - Obtiene el componente y devuelve su clase utilizando `getClass().getSimpleName()`.

### Exists


@SimpleFunction(description = "Verifica si existe un componente con el identificador especificado.")
public boolean Exists(Object id)


- **Descripción**: Comprueba si un componente con `id` existe.
- **Parámetros**:
  - `id`: Identificador del componente.
- **Retorno**: `true` si existe, `false` en caso contrario.
- **Implementación Interna**:
  - Verifica si el `id` está presente en el `HashMap` `components`.

### Remove


@SimpleFunction(description = "Elimina el componente con el identificador especificado.")
public void Remove(Object id)


- **Descripción**: Elimina el componente asociado al `id` y lo remueve de su contenedor.
- **Parámetros**:
  - `id`: Identificador del componente a eliminar.
- **Implementación Interna**:
  - Obtiene el componente.
  - Remueve el componente de su contenedor padre.
  - Elimina el componente del `HashMap` `components`.

### RemoveAll


@SimpleFunction(description = "Elimina todos los componentes dinámicos creados.")
public void RemoveAll()


- **Descripción**: Elimina todos los componentes dinámicos creados previamente.
- **Implementación Interna**:
  - Itera sobre todos los componentes en `components` y llama a `Remove` para cada uno.

### GetAllIds


@SimpleFunction(description = "Obtiene una lista de todos los identificadores de componentes dinámicos.")
public YailList GetAllIds()


- **Descripción**: Devuelve una lista con todos los identificadores de componentes actuales.
- **Retorno**: `YailList` de identificadores.
- **Implementación Interna**:
  - Devuelve las claves del `HashMap` `components` como una lista.

### AnyComponent


@SimpleFunction(description = "Obtiene una instancia de cualquier componente especificado.")
public AndroidViewComponent AnyComponent(String componentName)


- **Descripción**: Crea una instancia de un componente sin agregarlo a ningún contenedor.
- **Parámetros**:
  - `componentName`: Nombre del componente a crear.
- **Retorno**: Instancia de `AndroidViewComponent`.
- **Implementación Interna**:
  - Utiliza `Utils.getObject` para crear una instancia del componente.

### VersionName


@SimpleProperty(description = "Obtiene el nombre de la versión de la extensión.")
public String VersionName()


- **Descripción**: Devuelve el nombre de la versión actual de la extensión.
- **Retorno**: Cadena con el nombre de la versión.

### VersionCode


@SimpleProperty(description = "Obtiene el código de la versión de la extensión.")
public int VersionCode()


- **Descripción**: Devuelve el código numérico de la versión actual.
- **Retorno**: Número entero representando el código de versión.

## Clases Auxiliares

### Metadata (Detallado)

#### Descripción de Metadata

La clase `Metadata` es responsable de manejar todos los metadatos relacionados con los componentes de MIT App Inventor. Esto incluye:

- Información sobre las propiedades (nombres, tipos, métodos `getter` y `setter`).
- Información sobre los métodos disponibles en los componentes.
- Almacenamiento en caché de metadatos para mejorar el rendimiento.

#### Atributos Internos

- `componentInfoCache`: Un `HashMap` que almacena la información de componentes para evitar múltiples accesos por reflexión.
- `propertyInfoCache`: Un `HashMap` que almacena información de propiedades por componente.
- `methodInfoCache`: Un `HashMap` que almacena información de métodos por componente.

#### Métodos Principales de Metadata

- **getComponentInfo(String componentName)**: Obtiene la clase del componente basado en su nombre.
  - **Implementación**: Utiliza el paquete de componentes de MIT App Inventor y busca la clase correspondiente.
- **getPropertyInfo(Object component, String propertyName)**: Obtiene los métodos `getter` y `setter` para una propiedad específica.
  - **Implementación**: Usa reflexión para encontrar los métodos correspondientes y los almacena en caché.
- **getMethodInfo(Object component, String methodName, Class<?>... parameterTypes)**: Obtiene un método específico del componente.
  - **Implementación**: Usa reflexión para obtener el método y lo almacena en caché.
- **getAllProperties(Object component)**: Devuelve una lista de todas las propiedades disponibles en el componente.
  - **Implementación**: Usa reflexión para listar todos los métodos `getter` y `setter` y extraer los nombres de las propiedades.

### Utils (Detallado)

#### Descripción de Utils

La clase `Utils` proporciona métodos utilitarios esenciales para el funcionamiento de la extensión. Facilita operaciones que son recurrentes y necesarias para manejar los componentes dinámicos.

#### Métodos Principales de Utils

- **getObject(String className)**: Crea una instancia de la clase especificada.
  - **Parámetros**:
    - `className`: Nombre completo de la clase (incluyendo el paquete).
  - **Implementación**: Usa `Class.forName` y `newInstance` para crear la instancia.
- **castValue(Object value, Class<?> targetType)**: Convierte un valor al tipo de destino.
  - **Parámetros**:
    - `value`: Valor a convertir.
    - `targetType`: Clase del tipo de destino.
  - **Implementación**: Maneja conversiones para tipos primitivos, objetos y tipos específicos de App Inventor.
- **runOnUiThread(Runnable action)**: Ejecuta una acción en el hilo de interfaz de usuario.
  - **Parámetros**:
    - `action`: Objeto `Runnable` que contiene la acción a ejecutar.
  - **Implementación**: Usa `Looper.getMainLooper()` y un `Handler` para ejecutar en el hilo principal.
- **getContext(ComponentContainer container)**: Obtiene el contexto de la aplicación.
  - **Parámetros**:
    - `container`: Contenedor del componente.
  - **Retorno**: Contexto de la aplicación (`Context`).
- **getField(Object object, String fieldName)**: Obtiene el valor de un campo (incluyendo privados) de un objeto.
  - **Parámetros**:
    - `object`: Objeto del cual obtener el campo.
    - `fieldName`: Nombre del campo.
  - **Implementación**: Usa reflexión para acceder al campo, incluso si es privado.
- **setField(Object object, String fieldName, Object value)**: Establece el valor de un campo (incluyendo privados) de un objeto.
  - **Parámetros**:
    - `object`: Objeto al cual establecer el campo.
    - `fieldName`: Nombre del campo.
    - `value`: Valor a establecer.
  - **Implementación**: Usa reflexión para modificar el campo, incluso si es privado.
- **getMethod(Object object, String methodName, Class<?>... parameterTypes)**: Obtiene un método de un objeto.
  - **Parámetros**:
    - `object`: Objeto del cual obtener el método.
    - `methodName`: Nombre del método.
    - `parameterTypes`: Tipos de los parámetros del método.
  - **Implementación**: Usa reflexión para obtener el método, incluso si es privado.

## Ejemplos de Uso

### Crear un Componente Dinámico


// Crear una instancia de DynamicComponents
DynamicComponents dynamicComponents = new DynamicComponents(container);

// Crear un botón dinámico y agregarlo a un VerticalArrangement
dynamicComponents.Create("Button", "btnDynamic", verticalArrangement1);

// Establecer propiedades del botón
dynamicComponents.SetProperty("btnDynamic", "Text", "Presione Aquí");
dynamicComponents.SetProperty("btnDynamic", "BackgroundColor", Color.RED);

// Obtener el valor de una propiedad
String buttonText = (String) dynamicComponents.GetProperty("btnDynamic", "Text");

// Verificar si el componente existe
boolean exists = dynamicComponents.Exists("btnDynamic");

// Eliminar el componente
dynamicComponents.Remove("btnDynamic");


### Establecer Múltiples Propiedades


// Crear un diccionario de propiedades
YailDictionary properties = new YailDictionary();
properties.put("Text", "Nuevo Texto");
properties.put("TextColor", Color.BLUE);
properties.put("Enabled", true);

// Establecer múltiples propiedades a la vez
dynamicComponents.SetProperties("btnDynamic", properties);


### Llamar a un Método de un Componente


// Llamar al método 'RequestFocus' del componente
dynamicComponents.CallFunction("btnDynamic", "RequestFocus");

// Llamar al método 'SetText' con un argumento
dynamicComponents.CallFunction("btnDynamic", "SetText", "Texto Actualizado");


### Obtener Todos los Identificadores


// Obtener lista de todos los IDs
YailList allIds = dynamicComponents.GetAllIds();

// Iterar sobre los IDs
for (Object id : allIds.toArray()) {
    // Obtener tipo de cada componente
    String type = dynamicComponents.GetType(id);
    // Realizar operaciones según el tipo
}


## Consideraciones Adicionales

- **Identificadores Únicos**: Es fundamental asignar identificadores únicos a cada componente dinámico para evitar conflictos.
- **Tipos de Datos**: Al establecer propiedades o llamar a funciones, asegúrese de proporcionar valores del tipo correcto. La clase `Utils` ayuda en la conversión de tipos.
- **Reflexión**: La extensión utiliza reflexión para acceder a propiedades y métodos. Tenga en cuenta que esto puede afectar el rendimiento en algunos casos.
- **Seguridad**: Manipular componentes mediante reflexión puede tener implicaciones de seguridad. Use estas funcionalidades con precaución.
- **Compatibilidad**: No todos los componentes o propiedades pueden ser compatibles debido a limitaciones del entorno de App Inventor o del sistema Android.
- **Hilos de Ejecución**: Al manipular componentes que afectan la interfaz de usuario, asegúrese de ejecutar las operaciones en el hilo principal. La clase `Utils` proporciona métodos para facilitar esto.

## Créditos

- **Autor**: Yusuf Cihan
- **Repositorio**: [DynamicComponents-AI2](https://github.com/ysfchn/DynamicComponents-AI2)
- **Licencia**: [MIT License](https://github.com/ysfchn/DynamicComponents-AI2/blob/main/LICENSE)
