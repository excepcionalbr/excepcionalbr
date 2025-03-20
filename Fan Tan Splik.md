<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App de Estatísticas de Resultados</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
        }
    </style>
</head>
<body class="bg-black min-h-screen flex flex-col items-center justify-center">

    <div class="bg-gray-900 text-white p-6 rounded-lg shadow-lg w-full max-w-md border border-red-500">
        <h1 class="text-3xl font-bold mb-4 text-center text-red-500">Estatísticas de Resultados</h1>
        
        <form id="resultForm" class="mb-4">
            <label for="result" class="block text-gray-300 mb-1">Insira o resultado (1, 2, 3 ou 4):</label>
            <input type="number" id="result" name="result" min="1" max="4" class="mt-1 p-2 border border-gray-600 rounded w-full bg-gray-800 text-white focus:ring-2 focus:ring-red-500 focus:outline-none" required>
            
            <button type="submit" class="mt-4 bg-red-500 text-white py-2 px-4 rounded w-full font-bold hover:bg-red-600 transition duration-300">
                <i class="fas fa-plus-circle"></i> Adicionar Resultado
            </button>
        </form>

        <div id="statistics" class="mb-4">
            <h2 class="text-xl font-bold mb-2 text-red-500">Últimos 10 Resultados</h2>
            <ul id="resultList" class="list-none mb-4 flex flex-wrap gap-2">
                <!-- Resultados serão adicionados aqui -->
            </ul>

            <div id="percentages" class="text-gray-300">
                <!-- Porcentagens serão exibidas aqui -->
            </div>
        </div>
    </div>

    <script>
        const resultForm = document.getElementById('resultForm');
        const resultList = document.getElementById('resultList');
        const percentagesDiv = document.getElementById('percentages');
        let results = [];

        resultForm.addEventListener('submit', function(event) {
            event.preventDefault();
            const result = parseInt(document.getElementById('result').value);
            if (result >= 1 && result <= 4) {
                if (results.length === 10) {
                    results.shift();
                }
                results.push(result);
                updateResults();
                updatePercentages();
            }
            resultForm.reset();
        });

        function updateResults() {
            resultList.innerHTML = '';
            results.forEach(result => {
                const li = document.createElement('li');
                li.className = "px-3 py-1 bg-gray-800 text-red-400 font-bold rounded";
                li.textContent = result;
                resultList.appendChild(li);
            });
        }

        function updatePercentages() {
            const counts = [0, 0, 0, 0];
            results.forEach(result => {
                counts[result - 1]++;
            });

            percentagesDiv.innerHTML = `
                <p>1: <span class="text-red-500">${(counts[0] / results.length * 100).toFixed(2)}%</span></p>
                <p>2: <span class="text-red-500">${(counts[1] / results.length * 100).toFixed(2)}%</span></p>
                <p>3: <span class="text-red-500">${(counts[2] / results.length * 100).toFixed(2)}%</span></p>
                <p>4: <span class="text-red-500">${(counts[3] / results.length * 100).toFixed(2)}%</span></p>
            `;
        }
    </script>

</body>
</html>
