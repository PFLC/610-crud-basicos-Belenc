
# Aplicación CRUD de PHP

En el contexto de PHP, CRUD se refiere a las operaciones básicas de creación, lectura, actualización y eliminación de datos en una base de datos utilizando este lenguaje de programación.

Aquí hay una breve descripción de cómo se relaciona cada operación con PHP:

Create (Crear): En PHP, se pueden utilizar funciones y extensiones específicas para interactuar con la base de datos y agregar nuevos registros. Esto generalmente implica la creación de una consulta SQL INSERT para insertar datos en la base de datos desde un formulario web o cualquier otra fuente de entrada de datos.

Read (Leer): Para recuperar datos de la base de datos en PHP, se pueden usar consultas SQL SELECT. Estas consultas se ejecutan utilizando funciones proporcionadas por extensiones como MySQLi o PDO, y luego se procesan los resultados para mostrarlos en la página web o para su posterior procesamiento.

Update (Actualizar): Cuando se necesita actualizar datos en la base de datos, se utilizan consultas SQL UPDATE en PHP. Estas consultas modifican registros existentes según ciertos criterios, como un identificador único, y pueden ser ejecutadas usando las mismas extensiones mencionadas anteriormente.

Delete (Eliminar): Para eliminar datos de la base de datos en PHP, se utilizan consultas SQL DELETE. Estas consultas eliminan registros según ciertos criterios proporcionados y también se ejecutan utilizando las extensiones mencionadas.

## Tecnologías Utilizadas

- **PHP:** Lenguaje de script del lado del servidor utilizado para el desarrollo web.
- **MySQL:** Sistema de gestión de base de datos utilizado para almacenar datos de usuario.
- **HTML & CSS:** Utilizados para estructurar y dar estilo a las páginas web.
- **Tailwind CSS:** Un framework de CSS utilitario para el desarrollo rápido de interfaces de usuario.

## Páginas y Funcionalidades

### 1. Página de Inicio (`display.php`)

![Página de Inicio](images/display.png)

- **Funcionalidad:** Muestra todos los usuarios de la base de datos en un formato de tabla.
- **Características:** 
  - Ver todos los usuarios.
  - Enlaces de navegación para agregar, editar o eliminar información de usuario.

### 2. Agregar Usuario (`user.php`)

![Agregar Usuario](images/add.png)

- **Funcionalidad:** Permite agregar un nuevo usuario a la base de datos.
- **Características:** 
  - Formulario para ingresar detalles del usuario (nombre, correo electrónico, teléfono móvil, contraseña).
  - Validación de datos y envío a la base de datos.

### 3. Editar Usuario (`edit.php`)

![Editar Usuario](images/edit.png)

- **Funcionalidad:** Permite editar detalles de usuarios existentes.
- **Características:** 
  - Formulario prellenado con la información actual del usuario.
  - Actualización de detalles del usuario en la base de datos.

### 4. Eliminar Usuario (`delete.php`)

- **Funcionalidad:** Facilita la eliminación de un usuario de la base de datos.
- **Características:** 
  - Eliminación de información de usuario basada en el ID de usuario.

## Conexión a la Base de Datos (`connect.php`)

- **Propósito:** Establece una conexión con la base de datos MySQL.
- **Credenciales:** Utiliza nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.

## Cómo Ejecutar

Para ejecutar un CRUD en PHP, generalmente seguirías estos pasos:

1. Conexión a la base de datos: Antes de realizar cualquier operación CRUD, necesitas conectarte a tu base de datos. Puedes hacerlo utilizando extensiones como MySQLi o PDO en PHP. Aquí hay un ejemplo utilizando PDO:
<?php
$dsn = 'mysql:host=localhost;dbname=nombre_basedatos';
$usuario = 'usuario';
$contraseña = 'contraseña';

try {
    $conexion = new PDO($dsn, $usuario, $contraseña);
    $conexion->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Conexión exitosa";
} catch (PDOException $e) {
    echo "Error de conexión: " . $e->getMessage();
}
?>
2. Operaciones CRUD: Una vez que tienes una conexión establecida, puedes realizar las operaciones CRUD. Aquí tienes un ejemplo básico de cada una:

Create (Crear):

<?php
$nombre = "Ejemplo";
$email = "ejemplo@example.com";
$edad = 25;

$sql = "INSERT INTO usuarios (nombre, email, edad) VALUES (:nombre, :email, :edad)";
$stmt = $conexion->prepare($sql);
$stmt->bindParam(':nombre', $nombre);
$stmt->bindParam(':email', $email);
$stmt->bindParam(':edad', $edad);

if ($stmt->execute()) {
    echo "Usuario creado exitosamente";
} else {
    echo "Error al crear usuario";
}
?>
Read (Leer):
php
Copy code
<?php
$sql = "SELECT * FROM usuarios";
$stmt = $conexion->prepare($sql);
$stmt->execute();
$usuarios = $stmt->fetchAll(PDO::FETCH_ASSOC);
foreach ($usuarios as $usuario) {
    echo "Nombre: " . $usuario['nombre'] . ", Email: " . $usuario['email'] . ", Edad: " . $usuario['edad'] . "<br>";
}
?>
Update (Actualizar):
php
Copy code
<?php
$nuevo_nombre = "Nuevo nombre";
$id_usuario = 1;

$sql = "UPDATE usuarios SET nombre = :nombre WHERE id = :id";
$stmt = $conexion->prepare($sql);
$stmt->bindParam(':nombre', $nuevo_nombre);
$stmt->bindParam(':id', $id_usuario);

if ($stmt->execute()) {
    echo "Usuario actualizado exitosamente";
} else {
    echo "Error al actualizar usuario";
}
?>
Delete (Eliminar):
php
Copy code
<?php
$id_usuario = 1;

$sql = "DELETE FROM usuarios WHERE id = :id";
$stmt = $conexion->prepare($sql);
$stmt->bindParam(':id', $id_usuario);

if ($stmt->execute()) {
    echo "Usuario eliminado exitosamente";
} else {
    echo "Error al eliminar usuario";
}
?>
3. Cerrar conexión: Una vez que hayas terminado de trabajar con la base de datos, es una buena práctica cerrar la conexión:
<?php
$conexion = null;
?>
Recuerda que este es solo un ejemplo básico y que en un entorno de producción deberías considerar aspectos de seguridad, manejo de errores y otros casos especiales. Además, el código puede variar dependiendo del tipo de base de datos que estés utilizando y de tus necesidades específicas.
## Nota de Seguridad

Esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Es recomendable utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos para prevenir ataques de inyección SQL.

---

Siéntete libre de contribuir a este proyecto o sugerir mejoras. Para cualquier consulta o problema, por favor abre un issue en este repositorio.

