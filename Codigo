<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Análise de Variação de Preços da Cesta Básica</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f9;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #333;
            border-bottom: 2px solid #007bff;
            padding-bottom: 10px;
        }
        label {
            display: block;
            margin-top: 10px;
            font-weight: bold;
        }
        input[type="text"], input[type="number"] {
            width: calc(100% - 22px);
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 20px;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .resultado {
            margin-top: 30px;
            padding: 15px;
            border: 1px dashed #007bff;
            border-radius: 4px;
            background-color: #e9f5ff;
        }
        .abuso {
            color: #cc0000;
            font-weight: bold;
            font-size: 1.1em;
            margin-top: 10px;
            padding: 5px;
            border: 2px solid #cc0000;
            background-color: #ffcccc;
            border-radius: 4px;
            text-align: center;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Análise de Preços da Cesta Básica</h2>

    <form id="formAnalise">
        <label for="nome">Nome do Produto:</label>
        <input type="text" id="nome" required>

        <label for="precoAnterior">Preço Mês Anterior (R$):</label>
        <input type="number" id="precoAnterior" step="0.01" min="0" required>

        <label for="precoAtual">Preço Mês Atual (R$):</label>
        <input type="number" id="precoAtual" step="0.01" min="0" required>

        <button type="submit">Analisar Variação</button>
    </form>

    <div class="resultado" id="resultado">
        <p>Preencha os dados e clique em "Analisar Variação" para ver o resultado.</p>
    </div>

</div>

<script>
    document.getElementById('formAnalise').addEventListener('submit', function(event) {
        event.preventDefault(); // Impede o recarregamento da página

        // 1. Coleta de Dados
        const nomeProduto = document.getElementById('nome').value;
        const precoAnterior = parseFloat(document.getElementById('precoAnterior').value);
        const precoAtual = parseFloat(document.getElementById('precoAtual').value);
        const resultadoDiv = document.getElementById('resultado');

        // Variáveis de Saída
        let variacaoPercentual;
        let situacao;
        let alertaAbuso = "";

        // 2. Cálculos
        if (precoAnterior > 0) {
            variacaoPercentual = ((precoAtual - precoAnterior) / precoAnterior) * 100;
        } else if (precoAtual > 0) {
            // Se o anterior era 0 e o atual > 0, é um aumento extremo
            variacaoPercentual = 99999;
        } else {
            // Se ambos são 0
            variacaoPercentual = 0;
        }

        // 3. Classificação da Situação
        if (variacaoPercentual > 0) {
            situacao = "AUMENTO";
        } else if (variacaoPercentual < 0) {
            situacao = "QUEDA";
        } else {
            situacao = "ESTÁVEL";
        }

        // 4. Sinalização de Abuso (> 10%)
        if (variacaoPercentual > 10.0) {
            alertaAbuso = `<p class="abuso">*** SINAL DE ALERTA: AUMENTO SUPERIOR a 10% (ABUSO) ***</p>`;
        }

        // 5. Exibição do Relatório
        const relatorioHTML = `
            <h3>RELATÓRIO DE VARIAÇÃO</h3>
            <p><strong>Produto:</strong> ${nomeProduto}</p>
            <p><strong>Preço Ant. (R$):</strong> ${precoAnterior.toFixed(2)}</p>
            <p><strong>Preço Atual (R$):</strong> ${precoAtual.toFixed(2)}</p>
            <p><strong>Variação Percentual:</strong> ${variacaoPercentual.toFixed(2)}%</p>
            <p><strong>Situação:</strong> <span style="font-weight: bold; color: ${variacaoPercentual > 0 ? 'red' : variacaoPercentual < 0 ? 'green' : 'blue'};">${situacao}</span></p>
            ${alertaAbuso}
        `;

        resultadoDiv.innerHTML = relatorioHTML;
    });
</script>

</body>
</html>}
