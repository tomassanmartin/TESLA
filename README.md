import mysql.connector as db
# Connect with the MySQL Server
mydb = db.connect(
    host='localhost',
    user='root',
    passwd='xx',
    database='InfoAeropuertos'
)

miCursor = mydb.cursor()

#ingreso de los 3 nuevos aeropuertos
sqlsentence = 'INSERT INTO aeropuertos (id, ident, type , name , elevation_ft , municipality , iata_code, score) VALUES (%s, %s, %s, %s, %s, %s, %s, %s)'
val = [
    ('39340', 'SHCC', 'heliport', 'Clínica Las Condes Heliport','2461', 'Santiago', '', '25'),
    ('39379', 'SHMA', 'heliport', 'Clínica Santa María Heliport','2028', 'Santiago', '', '25'),
    ('39390', 'SHPT', 'heliport', 'Portillo Heliport','9000', 'Los Andes', '', '25')
]

miCursor.executemany(sqlsentence, val)
mydb.commit()
#Busqueda de los aeropuertos mayores a 5000 pies de altura
miCursor = mydb.cursor()
sqlWHERE = 'SELECT * FROM aeropuertos WHERE elevation_ft > 5000'
miCursor.execute(sqlWHERE)
rows = miCursor.fetchall()
for row in rows:
   print(row[3],row[2],row[5],row[4])
