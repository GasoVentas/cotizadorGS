<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cotizador de IVA</title>
</head>
<body>
    <h1>Cotizador de IVA</h1>
    
    <label for="valor">Valor del producto:</label>
    <input type="number" id="valor" placeholder="Ingrese el valor del producto"><br>
    
    <button onclick="calcularIVA()">Calcular IVA</button>
    
    <div id="resultado"></div>
    <div id="mensaje"></div>

    <script>
        function calcularIVA() {
            var valor = parseFloat(document.getElementById('valor').value);
            var iva = valor * 0.19; // 19% de IVA
            var total = valor + iva;
            
            var resultado = "Valor del producto: $" + valor.toFixed(2) + "<br>";
            resultado += "IVA (19%): $" + iva.toFixed(2) + "<br>";
            resultado += "Total a pagar: $" + total.toFixed(2);
            
            document.getElementById('resultado').innerHTML = resultado;
            
            // Agregar mensaje de confirmación
            document.getElementById('mensaje').innerHTML = "El IVA ha sido calculado correctamente.";
        }
    </script>
</body>
</html>
