# Multiplicar
Joc de multiplicacions 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego de Tablas de Multiplicar</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            text-align: center;
        }
        .container {
            margin: 20px auto;
            width: 80%;
        }
        .operation, .result, .trophy {
            margin: 20px;
            font-size: 24px;
        }
        .btn {
            padding: 10px 20px;
            margin: 10px;
            font-size: 18px;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Juego de Tablas de Multiplicar</h1>

        <!-- Operaciones -->
        <div id="game-area" class="operation">
            <p>¿Cuánto es <span id="multiplication">6 x 4</span>?</p>
            <input type="number" id="answer" placeholder="Tu respuesta">
            <button class="btn" id="submit">Enviar</button>
        </div>

        <!-- Resultados -->
        <div id="result-area" class="result hidden">
            <p id="result-message">Correcto/Incorrecto</p>
            <button class="btn" id="next">Siguiente</button>
        </div>

        <!-- Trofeos -->
        <div id="trophy-area" class="trophy hidden">
            <h2>¡Felicidades!</h2>
            <p id="trophy-message"></p>
        </div>
    </div>

    <script>
        const operations = [];
        let currentOperationIndex = 0;
        let correctAnswers = 0;
        const numOperations = 10; // Puedes cambiar esto a 50 si prefieres más operaciones

        function generateMultiplication() {
            const num1 = Math.floor(Math.random() * 10) + 1;
            const num2 = Math.floor(Math.random() * 10) + 1;
            return { num1, num2, result: num1 * num2 };
        }

        function loadNextOperation() {
            if (currentOperationIndex < numOperations) {
                const operation = generateMultiplication();
                operations.push(operation);
                document.getElementById('multiplication').textContent = `${operation.num1} x ${operation.num2}`;
            } else {
                // Mostrar el resultado final y los trofeos
                document.getElementById('game-area').classList.add('hidden');
                document.getElementById('result-area').classList.add('hidden');
                document.getElementById('trophy-area').classList.remove('hidden');

                document.getElementById('trophy-message').textContent = `Has acertado ${correctAnswers} de ${numOperations}.`;
                if (correctAnswers / numOperations >= 0.9) {
                    document.getElementById('trophy-message').textContent += " ¡Has ganado una medalla de oro!";
                } else if (correctAnswers / numOperations >= 0.8) {
                    document.getElementById('trophy-message').textContent += " ¡Has ganado una medalla de plata!";
                } else {
                    document.getElementById('trophy-message').textContent += " ¡Sigue mejorando!";
                }
            }
        }

        document.getElementById('submit').addEventListener('click', function () {
            const userAnswer = parseInt(document.getElementById('answer').value);
            const currentOperation = operations[currentOperationIndex];

            if (userAnswer === currentOperation.result) {
                correctAnswers++;
                document.getElementById('result-message').textContent = '¡Correcto!';
            } else {
                document.getElementById('result-message').textContent = `Incorrecto. La respuesta era ${currentOperation.result}.`;
            }

            document.getElementById('result-area').classList.remove('hidden');
            document.getElementById('game-area').classList.add('hidden');
        });

        document.getElementById('next').addEventListener('click', function () {
            currentOperationIndex++;
            document.getElementById('result-area').classList.add('hidden');
            document.getElementById('game-area').classList.remove('hidden');
            loadNextOperation();
        });

        // Inicia el juego con la primera operación
        loadNextOperation();
    </script>
</body>
</html>
