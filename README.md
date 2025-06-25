import sqlite3
import time

def base_de_datos():
    try:
        conexion = sqlite3.connect("comercio.sqlite")
        cursor_sql = conexion.cursor()

        cursor_sql.execute("""
            CREATE TABLE IF NOT EXISTS venta (
                numero_cliente INTEGER,
                cliente TEXT,
                fecha TEXT,
                combosS NUMERIC,
                combosD NUMERIC,
                combosT NUMERIC,
                flurby NUMERIC,
                total REAL
            )
        """)

        cursor_sql.execute("""
            CREATE TABLE IF NOT EXISTS registro (
                encargado TEXT,
                fecha TEXT,
                evento TEXT,
                total REAL
            )
        """)

        conexion.commit()
        conexion.close()
        print("Base y tablas creadas correctamente.")
        
    except:
        print("Hubo un error al crear la base o las tablas.")


def insertar_venta(cliente, fecha, cs, cd, ct, fl, total):
    try:
        conexion = sqlite3.connect("comercio.sqlite")
        cursor = conexion.cursor()
        cursor.execute("INSERT INTO venta (cliente, fecha, combosS, combosD, combosT, flurby, total) VALUES (?, ?, ?, ?, ?, ?, ?)",
                       (cliente, fecha, cs, cd, ct, fl, total))
        conexion.commit()
        conexion.close()
        print("Venta ingresada con éxito.")
    except:
        print("Error al guardar la venta.")


def insert_registro(encargado, fecha, evento, total):
    try:
        conexion = sqlite3.connect("comercio.sqlite")
        cursor = conexion.cursor()
        cursor.execute("INSERT INTO registro (encargado, fecha, evento, total) VALUES (?, ?, ?, ?)",
                       (encargado, fecha, evento, total))
        conexion.commit()
        conexion.close()
        print("Registro guardado.")
    except:
        print("Error al guardar el registro.")


