//Script de limpieza de datos con Power Query
Limpio y trnasformo la tabla de ventas utilizando leguaje M en Power Query

let
    // PASO 1: Cargar el archivo CSV.
    Origen = Csv.Document(
        File.Contents("C:\Users\Pamela Guzman\Desktop\CODERHOUSE\POWER BI\ventas_raw.csv"),
        [Delimiter = ",", Columns = 5, Encoding = 65001, QuoteStyle = QuoteStyle.None]
    ),

    // PASO 2: Promover los encabezados de las columnas.
    #"Encabezados promovidos" = Table.PromoteHeaders(
        Origen,
        [PromoteAllScalars = true]
    ),

    // PASO 3: Asignar los tipos de datos correspondientes.
    #"Tipo de columna cambiado" = Table.TransformColumnTypes(
        #"Encabezados promovidos",
        {
            {"id_venta", Int64.Type},
            {"nombre_producto", type text},
            {"categoria", type text},
            {"precio", Currency.Type},
            {"fecha_venta", type date}
        },
        "es"
    ),

    // PASO 4: Eliminar espacios al inicio y al final de los nombres.
    #"Nombres limpios" = Table.TransformColumns(
        #"Tipo de columna cambiado",
        {{"nombre_producto", Text.Trim, type text}}
    ),

    // PASO 5: Eliminar espacios y estandarizar las categorías.
    #"Categorias limpias" = Table.TransformColumns(
        #"Nombres limpios",
        {{"categoria", each Text.Proper(Text.Trim(_)), type text}}
    ),

    // PASO 6: Eliminar las filas que tienen categoría Prueba.
    #"Filas filtradas" = Table.SelectRows(
        #"Categorias limpias",
        each [categoria] <> "Prueba"
    )

in
    // RESULTADO FINAL: devolver la tabla limpia.
    #"Filas filtradas"
