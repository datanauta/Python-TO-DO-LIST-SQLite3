# Python-TO-DO-LIST-SQLite3
Creación de un TO DO LIST con SQLite3 donde podemos, insertar, mostrar, eliminar y salir

import sqlite3

conn = sqlite3.connect("tareas.db")
cursor = conn.cursor()

cursor.execute("""
    CREATE TABLE IF NOT EXISTS tareas(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    descripcion TEXT    
    )

""")
conn.commit()

number = 0

while number != 4:

    print('----------------Menú---------------------')
    print('1.Añadir una tarea')
    print('2.Eliminar una tarea')
    print('3.Mostrar tareas')
    print('4.Salir')
    print('-------------------------------------')

    number = int(input('Introduce la acción a realizar (1-5):'))

    if number == 1:
        task = input('Nueva tarea:')
        cursor.execute("INSERT INTO tareas (descripcion) VALUES (?)",(task,))
        conn.commit()
        print('✅ Tarea añadida')

    elif number == 2:
        task_id = int(input('Introduce el ID de la tarea a eliminar:'))
        cursor.execute("DELETE FROM tareas where id= ?",(task_id,))
        conn.commit()
        print('❌Tarea eliminada')


    elif number == 3:
        cursor.execute("SELECT id, descripcion FROM tareas")
        tasks = cursor.fetchall()
        if tasks:
            for t in tasks:
                print(f'{t[0]}. {t[1]}')
        else:
            print('📭 No hay tareas')

    elif number == 4:
        print('👋')
        break

    else:

        print(f'La opción : {number} no es correcta')
