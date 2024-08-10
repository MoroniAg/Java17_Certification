### Crear conexiones, ejecutar sentencias básicas, preparadas y llamables, procesar resultados de consultas y controlar transacciones usando JDBC API

La API de JDBC (Java Database Connectivity) es el estándar de la industria para la conectividad de bases de datos en Java. Permite a las aplicaciones Java interactuar con bases de datos relacionales mediante la ejecución de sentencias SQL, el procesamiento de resultados de consultas y el control de transacciones.

### 1. Crear conexiones con JDBC

Para interactuar con una base de datos, primero necesitas establecer una conexión usando `DriverManager`. Esto implica proporcionar la URL de la base de datos, un nombre de usuario y una contraseña.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConexionJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            if (conn != null) {
                System.out.println("Conexión exitosa a la base de datos.");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 2. Ejecutar sentencias básicas

Una vez establecida la conexión, puedes ejecutar sentencias SQL utilizando objetos `Statement`.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class SentenciasBasicasJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {
             
            String sql = "CREATE TABLE ejemplo (id INT PRIMARY KEY, nombre VARCHAR(50))";
            stmt.executeUpdate(sql);
            System.out.println("Tabla creada exitosamente.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 3. Ejecutar sentencias preparadas (Prepared Statements)

Las sentencias preparadas permiten parametrizar las consultas SQL, lo que mejora la seguridad y el rendimiento, especialmente en el contexto de consultas repetitivas.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class SentenciasPreparadasJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            String sql = "INSERT INTO ejemplo (id, nombre) VALUES (?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(sql);
            pstmt.setInt(1, 1);
            pstmt.setString(2, "Carlos");
            pstmt.executeUpdate();

            System.out.println("Registro insertado exitosamente.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 4. Ejecutar sentencias llamables (Callable Statements)

Las sentencias llamables se utilizan para ejecutar procedimientos almacenados en la base de datos.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.CallableStatement;
import java.sql.SQLException;

public class SentenciasLlamablesJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            String sql = "{call mi_procedimiento(?, ?)}";
            CallableStatement cstmt = conn.prepareCall(sql);
            cstmt.setInt(1, 1);
            cstmt.setString(2, "Carlos");
            cstmt.execute();

            System.out.println("Procedimiento almacenado ejecutado exitosamente.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 5. Procesar resultados de consultas

Después de ejecutar una consulta, puedes procesar los resultados utilizando un objeto `ResultSet`.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ProcesarResultadosJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {
             
            String sql = "SELECT id, nombre FROM ejemplo";
            ResultSet rs = stmt.executeQuery(sql);

            while (rs.next()) {
                int id = rs.getInt("id");
                String nombre = rs.getString("nombre");
                System.out.println("ID: " + id + ", Nombre: " + nombre);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 6. Controlar transacciones

Por defecto, las transacciones en JDBC se manejan de forma automática. Sin embargo, puedes desactivar el modo de auto-commit y controlar las transacciones manualmente.

**Ejemplo:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ControlTransaccionesJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base_de_datos";
        String user = "usuario";
        String password = "contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Desactiva el auto-commit

            try (Statement stmt = conn.createStatement()) {
                String sql1 = "INSERT INTO ejemplo (id, nombre) VALUES (2, 'Ana')";
                stmt.executeUpdate(sql1);

                String sql2 = "INSERT INTO ejemplo (id, nombre) VALUES (3, 'Luis')";
                stmt.executeUpdate(sql2);

                conn.commit(); // Cometer transacción si todo fue exitoso
                System.out.println("Transacción cometida exitosamente.");
            } catch (SQLException e) {
                conn.rollback(); // Deshacer transacción en caso de error
                System.out.println("Transacción deshecha debido a un error.");
                e.printStackTrace();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### Conclusión y Consideraciones Adicionales

El uso de la API JDBC en Java es fundamental para cualquier aplicación que interactúe con bases de datos relacionales. Es importante dominar no solo la creación de conexiones y la ejecución de consultas, sino también el manejo de transacciones y la gestión adecuada de los recursos. Familiarizarse con las sentencias preparadas y llamables es crucial para escribir código seguro y eficiente. Además, comprender cómo procesar los resultados de las consultas y manejar las transacciones te permitirá construir aplicaciones robustas y confiables.