//1)Si en lugar de Text.Proper hubieras usado Text.Upper para estandarizar la categoría, ¿qué tendrías que cambiar en el filtro de los registros de prueba? ¿Por qué?
Tendría que cambiar el filtro de "Prueba" por "PRUEBA".
Esto se debe a que Text.Upper convierte todas las letras a mayúsculas. Por lo tanto, para que el filtro funcione correctamente, el texto debe coincidir con ese formato.

//2)Si mañana llega un registro con la categoría "prueba " (con un espacio al final), ¿tu script lo elimina? Si no, ¿qué paso agregarías y en qué lugar del script?
Sí, mi script lo elimina porque antes de aplicar el filtro utilizo Text.Trim, que elimina los espacios al principio y al final del texto.
De esta manera, "prueba " se transforma en "Prueba" y puede ser identificado por el filtro.
No necesito agregar otro paso porque ya tengo esa transformación en el código.

//3)¿Cuál es la diferencia entre usar Text.Trim y Text.Clean en M?
Text.Trim elimina los espacios al principio y al final de un texto, mientras que Text.Clean elimina caracteres no imprimibles que pueden afectar la calidad de los datos.

//4)¿Por qué filtraste los registros "PRUEBA" después de estandarizar la categoría y no antes?
Porque primero necesitaba unificar el formato de las categorías para que todas tuvieran la misma escritura.
Por ejemplo, podía tener categorías como "PRUEBA", "prueba" o "Prueba".
Al aplicar primero Text.Trim y Text.Proper, todas quedan como "Prueba". Así puedo aplicar el filtro correctamente y eliminar todos los registros de prueba.





