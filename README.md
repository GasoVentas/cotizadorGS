<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cotización - GasoProLatam</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f4f4f4;
    }
    .container {
        max-width: 800px;
        margin: 20px auto;
        padding: 20px;
        background-color: #fff;
        border-radius: 10px;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
    }
    h1 {
        text-align: center;
        font-size: 28px;
        font-weight: bold;
        color: #333;
    }
    table {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 20px;
    }
    th, td {
        padding: 8px;
        border-bottom: 1px solid #ddd;
        text-align: left;
    }
    th {
        background-color: #f2f2f2;
    }
    input[type="text"], input[type="date"] {
        width: calc(100% - 16px);
        padding: 8px;
        box-sizing: border-box;
    }
    .btn-container {
        text-align: center;
        margin-bottom: 20px;
    }
    .btn-generate, .btn-add {
        padding: 10px 20px;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease;
    }
    .btn-generate:hover, .btn-add:hover {
        background-color: #0056b3;
    }
    .result-box {
        border: 1px solid #ccc;
        padding: 20px;
        border-radius: 10px;
        background-color: #f9f9f9;
    }
    .result-text {
        font-size: 16px;
        line-height: 1.6;
        color: #333;
    }
    p {
        margin: 10px 0;
        font-size: 16px;
        color: #333;
    }
</style>
</head>
<body>
<div class="container">
    <h1>GasoProLatam</h1>
    <table>
        <tr>
            <th>Número de Cotización:</th>
            <td><span id="numeroCotizacion"></span></td>
        </tr>
        <tr>
            <th>Fecha:</th>
            <td><input type="date" id="fecha"></td>
        </tr>
        <tr>
            <th>NIT:</th>
            <td><input type="text" id="nit" placeholder="000000000-0"></td>
        </tr>
        <tr>
            <th>Teléfono:</th>
            <td><input type="text" id="telefono" placeholder="318-335-1283"></td>
        </tr>
        <tr>
            <th>Dirección:</th>
            <td><input type="text" id="direccion" placeholder="Calle 123, Ciudad, País"></td>
        </tr>
        <tr>
            <th>Departamento:</th>
            <td><input type="text" id="departamento" placeholder="Nombre del departamento"></td>
        </tr>
    </table>
    <h2>Descripción del Elemento</h2>
    <table id="elementos">
        <tr>
            <th>Tipo de Elemento</th>
            <th>Cantidad</th>
            <th>Valor Unitario</th>
            <th>Total</th>
        </tr>
        <tr>
            <td><input type="text" class="tipo_elemento" placeholder="Tipo"></td>
            <td><input type="text" class="cantidad" placeholder="1"></td>
            <td><input type="text" class="valor_unitario" placeholder="$100"></td>
            <td><input type="text" class="total" disabled></td>
        </tr>
    </table>
    <div class="btn-container">
        <button class="btn-add" onclick="agregarFila()">Agregar Elemento</button>
        <button class="btn-generate" onclick="generarCotizacion()">Generar Cotización</button>
    </div>
    <div id="result" class="result-box"></div>
    <p>Email de contacto: <a href="mailto:gasoprolatam@outlook.com">gasoprolatam@outlook.com</a></p>
    <p>Celular: 318-335-1283</p>
</div>

<script>
    var numeroCotizacion = 1; // Inicializar el número de cotización

    function agregarFila() {
        var tabla = document.getElementById('elementos');
        var fila = tabla.insertRow(-1);
        var tipoElemento = fila.insertCell(0);
        var cantidad = fila.insertCell(1);
        var valorUnitario = fila.insertCell(2);
        var total = fila.insertCell(3);

        tipoElemento.innerHTML = '<input type="text" class="tipo_elemento" placeholder="Tipo">';
        cantidad.innerHTML = '<input type="text" class="cantidad" placeholder="1">';
        valorUnitario.innerHTML = '<input type="text" class="valor_unitario" placeholder="$100">';
        total.innerHTML = '<input type="text" class="total" disabled>';
    }

    function generarCotizacion() {
        var elementos = document.querySelectorAll('#elementos tr:not(:first-child)');
        var totalVenta = 0;

        elementos.forEach(function(elemento) {
            var tipoElemento = elemento.querySelector('.tipo_elemento').value;
            var cantidad = parseFloat(elemento.querySelector('.cantidad').value);
            var valorUnitario = parseFloat(elemento.querySelector('.valor_unitario').value.replace('$', '').replace(',', ''));
            var total = (cantidad * valorUnitario);
            totalVenta += parseFloat(total);
            elemento.querySelector('.total').value = formatMoney(total);
        });

        var valorIVA = (totalVenta * 0.19);
        var totalConIVA = (totalVenta + parseFloat(valorIVA));

        var fecha = document.getElementById('fecha').value;
        var nit = document.getElementById('nit').value;
        var telefono = document.getElementById('telefono').value;
        var direccion = document.getElementById('direccion').value;
        var departamento = document.getElementById('departamento').value;

        var resultText = '<div class="result-text">' +
                            '<p style="font-weight: bold;">Cotización - GasoProLatam</p>' +
                            '<hr>' +
                            '<p><strong>Número de Cotización:</strong> ' + numeroCotizacion++ + '</p>' +
                            '<p><strong>Fecha:</strong> ' + fecha + '</p>' +
                            '<p><strong>NIT:</strong> ' + nit + '</p>' +
                            '<p><strong>Teléfono:</strong> ' + telefono + '</p>' +
                            '<p><strong>Dirección:</strong> ' + direccion + '</p>' +
                            '<p><strong>Departamento:</strong> ' + departamento + '</p>' +
                            '<hr>' +
                            '<h2>Descripción del Elemento</h2>' +
                            '<table style="border-collapse: collapse; width: 100%;">' +
                                '<tr>' +
                                    '<th style="border: 1px solid #dddddd; padding: 8px;">Tipo de Elemento</th>' +
                                    '<th style="border: 1px solid #dddddd; padding: 8px;">Cantidad</th>' +
                                    '<th style="border: 1px solid #dddddd; padding: 8px;">Valor Unitario</th>' +
                                    '<th style="border: 1px solid #dddddd; padding: 8px;">Total</th>' +
                                '</tr>';

        elementos.forEach(function(elemento) {
            var tipoElemento = elemento.querySelector('.tipo_elemento').value;
            var cantidad = parseFloat(elemento.querySelector('.cantidad').value);
            var valorUnitario = parseFloat(elemento.querySelector('.valor_unitario').value.replace('$', '').replace(',', ''));
            var total = (cantidad * valorUnitario);

            resultText += '<tr>' +
                            '<td style="border: 1px solid #dddddd; padding: 8px;">' + tipoElemento + '</td>' +
                            '<td style="border: 1px solid #dddddd; padding: 8px;">' + cantidad + '</td>' +
                            '<td style="border: 1px solid #dddddd; padding: 8px;">' + formatMoney(valorUnitario) + '</td>' +
                            '<td style="border: 1px solid #dddddd; padding: 8px;">' + formatMoney(total) + '</td>' +
                          '</tr>';
        });

        resultText += '</table>' +
                      '<p><strong>Total Venta:</strong> ' + formatMoney(totalVenta) + '</p>' +
                      '<p><strong>Valor del IVA (19%):</strong> ' + formatMoney(valorIVA) + '</p>' +
                      '<p><strong>Total con IVA:</strong> ' + formatMoney(totalConIVA) + '</p>' +
                    '</div>';

        document.getElementById('result').innerHTML = resultText;
    }

    function formatMoney(amount) {
        return '$' + amount.toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    }
</script>
</body>
</html>
