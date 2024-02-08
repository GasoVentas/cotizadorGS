
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cotizador GSPL</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f7f7f7;
        }
        .container {
            background-color: #fff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
        }
        h1 {
            margin-bottom: 20px;
            color: #333;
        }
        label {
            display: block;
            text-align: left;
            margin-bottom: 5px;
            color: #555;
        }
        input, select {
            width: calc(100% - 10px);
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .producto {
            border-top: 1px solid #ccc;
            padding-top: 15px;
            margin-top: 15px;
        }
        #cotizacion {
            display: inline-block;
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            border-radius: 4px;
            font-weight: bold;
            margin-bottom: 15px;
        }
        button {
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            padding: 10px 20px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #0056b3;
        }
        #resultado {
            margin-top: 20px;
            text-align: left;
            border-top: 1px solid #ccc;
            padding-top: 20px;
            background-color: #f3f3f3;
            border-radius: 4px;
        }
        #resultado div {
            padding: 10px;
            border-bottom: 1px solid #ccc;
        }
        #resultado div:last-child {
            border-bottom: none;
        }
        #resultado strong {
            width: 150px;
            display: inline-block;
            font-weight: normal;
            color: #555;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Cotizador GSPL</h1>
        
        <label for="nombreEmpresa">Nombre de la empresa:</label>
        <input type="text" id="nombreEmpresa" placeholder="Ingrese el nombre de la empresa">
        
        <label for="nit">NIT:</label>
        <input type="text" id="nit" placeholder="Ingrese el NIT de la empresa">
        
        <div id="productos">
            <label for="nombreProducto">Nombre del producto:</label>
            <input type="text" id="nombreProducto" placeholder="Ingrese el nombre del producto">
            
            <label for="valor">Valor unitario del producto:</label>
            <input type="number" id="valor" placeholder="Ingrese el valor unitario del producto">

            <label for="cantidad">Cantidad:</label>
            <input type="number" id="cantidad" placeholder="Ingrese la cantidad del producto" value="1">
        </div>
        
        <label for="cotizacion">Número de cotización:</label>
        <span id="cotizacion">01</span>
        
        <button onclick="generarCotizacion()">Generar Cotización</button>
        
        <div id="resultado"></div>
        <div id="mensaje"></div>
    </div>

    <script>
        var contadorCotizacion = 1;

        function generarCotizacion() {
            var nombreEmpresa = document.getElementById('nombreEmpresa').value;
            var nit = document.getElementById('nit').value;
            var nombreProducto = document.getElementById('nombreProducto').value;
            var valor = parseFloat(document.getElementById('valor').value);
            var cantidad = parseInt(document.getElementById('cantidad').value);
            var iva = valor * 0.19; // 19% de IVA
            var total = (valor * cantidad) + iva;

            var resultado = "<div><strong>Nombre de la empresa:</strong> " + nombreEmpresa + "</div>";
            resultado += "<div><strong>NIT:</strong> " + nit + "</div>";
            resultado += "<div><strong>Nombre del producto:</strong> " + nombreProducto + "</div>";
            resultado += "<div><strong>Valor unitario del producto:</strong> $" + numberWithCommas(valor.toFixed(0)) + "</div>";
            resultado += "<div><strong>Cantidad:</strong> " + cantidad + "</div>";
            resultado += "<div><strong>IVA (19%):</strong> $" + numberWithCommas(iva.toFixed(0)) + "</div>";
            resultado += "<div><strong>Total a pagar:</strong> $" + numberWithCommas(total.toFixed(0)) + "</div>";

            document.getElementById('resultado').innerHTML = resultado;
            document.getElementById('cotizacion').innerText = formatNumeroCotizacion(contadorCotizacion);
            contadorCotizacion++;
            document.getElementById('mensaje').innerHTML = "La cotización ha sido generada correctamente.";
        }

        function formatNumeroCotizacion(numero) {
            var str = numero.toString();
            return str.padStart(2, '0');
        }

        // Función para agregar separadores de miles con puntos
        function numberWithCommas(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
        }
    </script>
</body>
</html>
