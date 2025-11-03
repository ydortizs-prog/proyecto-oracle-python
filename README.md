# proyecto-oracle-python


![Uploading image.png…]()
![Uploading image.png…]()
![82106907-6514-4d51-a1da-12740335f5b0](https://github.com/user-attachments/assets/a5c743e8-b395-4ce2-a7ba-cb39024a8453)

[app.py](https://github.com/user-attachments/files/23294038/app.py)
import oracledb
import os

# ¡ESTA ES LA LÍNEA NUEVA IMPORTANTE!
# Le dice a Python dónde encontrar el "traductor" (Instant Client)
try:
    oracledb.init_oracle_client(lib_dir=r"C:\oracle_client")
except Exception as e:
    print("Error al iniciar el cliente de Oracle:", e)
    os._exit(1) # Detiene el script si no encuentra el cliente

# 1. Datos de conexión
user = "tienda"
password = "14064"
dsn = "localhost/xe" 

# 2. Consulta simple
sql = "SELECT * FROM PRODUCTOS"

print("Iniciando conexion a la base de datos Oracle...")

try:
    with oracledb.connect(user=user, password=password, dsn=dsn) as connection:
        print("¡Conexion exitosa!")

        with connection.cursor() as cursor:
            cursor.execute(sql)
            print("--- Resultados de la consulta ---")
            for row in cursor:
                print(row)
            print("---------------------------------")

except oracledb.DatabaseError as e:
    error, = e.args
    print("Error durante la conexion o consulta:", error.message)

print("Script finalizado.")
