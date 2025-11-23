[Formulariindex.html.html](https://github.com/user-attachments/files/23699234/Formulariindex.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evaluación: Terremotos, Volcanes y Tsunamis</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .question-card {
            transition: all 0.3s ease;
        }
        .option-btn {
            transition: all 0.2s ease;
        }
        .option-btn:hover {
            transform: translateX(5px);
        }
        .correct {
            background-color: #10b981 !important;
            color: white !important;
        }
        .incorrect {
            background-color: #ef4444 !important;
            color: white !important;
        }
        .disabled {
            pointer-events: none;
            opacity: 0.6;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen py-8">
    <div class="container mx-auto px-4 max-w-4xl">
        <!-- Login Form -->
        <div id="loginForm" class="bg-white rounded-lg shadow-lg p-8 max-w-md mx-auto">
            <h2 class="text-3xl font-bold text-indigo-700 mb-6 text-center">🌋 Evaluación: La Tierra se Estremece</h2>
            <p class="text-gray-600 mb-6 text-center">Terremotos, Volcanes y Tsunamis - 2do Grado</p>
            <form onsubmit="startQuiz(event)" class="space-y-4">
                <div>
                    <label class="block text-gray-700 font-semibold mb-2">Nombre Completo del Estudiante:</label>
                    <input 
                        type="text" 
                        id="studentName" 
                        required 
                        placeholder="Ej: Juan Pérez García"
                        class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:border-indigo-500 focus:outline-none"
                    >
                </div>
                <div>
                    <label class="block text-gray-700 font-semibold mb-2">Curso/Sección:</label>
                    <input 
                        type="text" 
                        id="studentSection" 
                        required 
                        placeholder="Ej: 2do A"
                        class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:border-indigo-500 focus:outline-none"
                    >
                </div>
                <button type="submit" class="w-full bg-indigo-600 text-white py-3 rounded-lg hover:bg-indigo-700 transition-colors font-semibold">
                    Comenzar Evaluación →
                </button>
            </form>
        </div>

        <!-- Header -->
        <header id="quizHeader" class="hidden bg-white rounded-lg shadow-lg p-6 mb-8">
            <div class="flex justify-between items-start mb-4">
                <div>
                    <h1 class="text-3xl font-bold text-indigo-700 mb-2">🌋 Evaluación: La Tierra se Estremece</h1>
                    <p class="text-gray-600">Estudiante: <span id="displayName" class="font-semibold"></span></p>
                    <p class="text-gray-600">Sección: <span id="displaySection" class="font-semibold"></span></p>
                </div>
                <div class="text-right">
                    <span class="text-sm font-semibold text-indigo-600 block">Pregunta <span id="currentQuestion">1</span> de 15</span>
                    <span class="text-sm font-semibold text-green-600 block">Puntuación: <span id="score">0</span>/15</span>
                </div>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-2">
                <div id="progressBar" class="bg-indigo-600 h-2 rounded-full transition-all duration-300" style="width: 6.67%"></div>
            </div>
        </header>

        <!-- Quiz Container -->
        <div id="quizContainer" class="hidden space-y-6">
            <!-- Las preguntas se cargarán aquí dinámicamente -->
        </div>

        <!-- Navigation Buttons -->
        <div id="navButtons" class="hidden flex justify-between mt-8">
            <button id="prevBtn" class="bg-gray-500 text-white px-6 py-3 rounded-lg hover:bg-gray-600 transition-colors disabled:opacity-50 disabled:cursor-not-allowed" disabled>
                ← Anterior
            </button>
            <button id="nextBtn" class="bg-indigo-600 text-white px-6 py-3 rounded-lg hover:bg-indigo-700 transition-colors">
                Siguiente →
            </button>
        </div>

        <!-- Results -->
        <div id="results" class="hidden bg-white rounded-lg shadow-lg p-8 mt-8">
            <h2 class="text-3xl font-bold text-center mb-4">¡Evaluación Completada! 🎉</h2>
            <div class="bg-indigo-50 rounded-lg p-6 mb-6">
                <p class="text-gray-700 mb-2"><strong>Estudiante:</strong> <span id="resultName"></span></p>
                <p class="text-gray-700 mb-2"><strong>Sección:</strong> <span id="resultSection"></span></p>
                <p class="text-gray-700"><strong>Fecha:</strong> <span id="resultDate"></span></p>
            </div>
            <div class="text-center">
                <p class="text-6xl font-bold text-indigo-600 mb-4"><span id="finalScore">0</span>/15</p>
                <p class="text-2xl mb-2"><span id="percentage">0</span>%</p>
                <p id="resultMessage" class="text-xl text-gray-700 mb-6"></p>
                <div class="space-x-4">
                    <button onclick="downloadResult()" class="bg-green-600 text-white px-8 py-3 rounded-lg hover:bg-green-700 transition-colors">
                        📥 Descargar Resultado
                    </button>
                    <button onclick="location.reload()" class="bg-indigo-600 text-white px-8 py-3 rounded-lg hover:bg-indigo-700 transition-colors">
                        Nueva Evaluación
                    </button>
                </div>
            </div>
        </div>

        <!-- Teacher Panel -->
        <div id="teacherPanel" class="hidden mt-8 bg-white rounded-lg shadow-lg p-6">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-2xl font-bold text-indigo-700">📊 Panel del Profesor</h3>
                <button onclick="exportAllResults()" class="bg-green-600 text-white px-4 py-2 rounded-lg hover:bg-green-700 transition-colors text-sm">
                    📊 Exportar Todo a Excel
                </button>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full">
                    <thead>
                        <tr class="bg-indigo-100">
                            <th class="px-4 py-2 text-left">Estudiante</th>
                            <th class="px-4 py-2 text-left">Sección</th>
                            <th class="px-4 py-2 text-center">Puntuación</th>
                            <th class="px-4 py-2 text-center">Porcentaje</th>
                            <th class="px-4 py-2 text-left">Fecha/Hora</th>
                        </tr>
                    </thead>
                    <tbody id="resultsTable">
                        <!-- Los resultados se cargarán aquí -->
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        const quizData = [
            {
                question: "1. ¿Qué es la geomorfología?",
                options: [
                    "La ciencia que estudia los animales y plantas",
                    "La rama de la geografía física que estudia las formas del relieve terrestre",
                    "La ciencia que estudia el clima y la atmósfera"
                ],
                correct: 1
            },
            {
                question: "2. ¿Cuál fue la magnitud del terremoto que devastó Haití en enero de 2010?",
                options: [
                    "7.0 grados",
                    "8.8 grados",
                    "6.5 grados"
                ],
                correct: 0
            },
            {
                question: "3. ¿Qué son las placas tectónicas?",
                options: [
                    "Capas de hielo en los polos",
                    "Grandes bloques de la corteza terrestre que se mueven",
                    "Rocas volcánicas solidificadas"
                ],
                correct: 1
            },
            {
                question: "4. ¿Qué país tuvo un terremoto de 8.8 grados en febrero de 2010 pero con menos víctimas que Haití?",
                options: [
                    "México",
                    "Japón",
                    "Chile"
                ],
                correct: 2
            },
            {
                question: "5. ¿Qué es el Cinturón de Fuego del Pacífico?",
                options: [
                    "Una zona con alta actividad volcánica y sísmica alrededor del Océano Pacífico",
                    "Una región desértica muy caliente",
                    "Un volcán gigante en el Pacífico"
                ],
                correct: 0
            },
            {
                question: "6. ¿Qué significa 'vulnerabilidad' en el contexto de desastres naturales?",
                options: [
                    "La intensidad del fenómeno natural",
                    "El grado de fragilidad o debilidad de una comunidad ante un evento peligroso",
                    "La ubicación geográfica de una ciudad"
                ],
                correct: 1
            },
            {
                question: "7. ¿Cuáles son las tres capas principales de la estructura interna de la Tierra?",
                options: [
                    "Corteza, manto y núcleo",
                    "Arena, piedras y lava",
                    "Tierra, agua y aire"
                ],
                correct: 0
            },
            {
                question: "8. ¿Qué es un tsunami o maremoto?",
                options: [
                    "Una ola gigante causada generalmente por un terremoto submarino",
                    "Una tormenta tropical muy fuerte",
                    "El agua que sale de un volcán"
                ],
                correct: 0
            },
            {
                question: "9. ¿Qué país implementó normas estrictas de construcción antisísmica tras grandes terremotos?",
                options: [
                    "República Dominicana",
                    "Chile",
                    "Cuba"
                ],
                correct: 1
            },
            {
                question: "10. ¿Cuál es el principal sistema montañoso de República Dominicana formado por fenómenos geológicos?",
                options: [
                    "Los Alpes Dominicanos",
                    "La Cordillera Central",
                    "La Sierra del Pacífico"
                ],
                correct: 1
            },
            {
                question: "11. ¿Qué tipo de límite de placas ocurre cuando dos placas se separan?",
                options: [
                    "Convergencia o colisión",
                    "Divergencia o separación",
                    "Transformación o deslizamiento"
                ],
                correct: 1
            },
            {
                question: "12. ¿Qué porcentaje aproximado de la población murió en el terremoto de Haití en 2010?",
                options: [
                    "1% de la población",
                    "3% de la población",
                    "5% de la población"
                ],
                correct: 1
            },
            {
                question: "13. ¿Cuál de estos NO es un concepto relacionado con la gestión de riesgos de desastres?",
                options: [
                    "Amenaza o peligro",
                    "Vulnerabilidad",
                    "Temperatura global"
                ],
                correct: 2
            },
            {
                question: "14. ¿Qué país tiene infraestructura avanzada con edificios flexibles y simulacros nacionales regulares?",
                options: [
                    "Japón",
                    "Cuba",
                    "Colombia"
                ],
                correct: 0
            },
            {
                question: "15. ¿Qué competencia fundamental se desarrolla al proponer proyectos comunitarios de prevención?",
                options: [
                    "Competencia artística",
                    "Competencia ética y ciudadana",
                    "Competencia deportiva"
                ],
                correct: 1
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;
        let answeredQuestions = new Array(quizData.length).fill(false);
        let studentName = '';
        let studentSection = '';
        let startTime = null;
        let detailedAnswers = [];

        function startQuiz(event) {
            event.preventDefault();
            studentName = document.getElementById('studentName').value.trim();
            studentSection = document.getElementById('studentSection').value.trim();
            startTime = new Date();

            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('quizHeader').classList.remove('hidden');
            document.getElementById('quizContainer').classList.remove('hidden');
            document.getElementById('navButtons').classList.remove('hidden');

            document.getElementById('displayName').textContent = studentName;
            document.getElementById('displaySection').textContent = studentSection;

            renderQuestion();
        }

        function renderQuestion() {
            const container = document.getElementById('quizContainer');
            const question = quizData[currentQuestionIndex];
            
            container.innerHTML = `
                <div class="question-card bg-white rounded-lg shadow-lg p-6">
                    <h3 class="text-xl font-bold text-gray-800 mb-6">${question.question}</h3>
                    <div class="space-y-3">
                        ${question.options.map((option, index) => `
                            <button 
                                class="option-btn w-full text-left p-4 rounded-lg border-2 border-gray-300 hover:border-indigo-500 hover:bg-indigo-50 ${answeredQuestions[currentQuestionIndex] ? 'disabled' : ''}"
                                onclick="checkAnswer(${index})"
                                id="option-${index}"
                            >
                                <span class="font-semibold">${String.fromCharCode(65 + index)}.</span> ${option}
                            </button>
                        `).join('')}
                    </div>
                    <div id="feedback" class="mt-4 p-4 rounded-lg hidden"></div>
                </div>
            `;

            updateProgress();
            updateButtons();
        }

        function checkAnswer(selectedIndex) {
            if (answeredQuestions[currentQuestionIndex]) return;

            const question = quizData[currentQuestionIndex];
            const isCorrect = selectedIndex === question.correct;
            const feedback = document.getElementById('feedback');
            
            // Guardar respuesta detallada
            detailedAnswers.push({
                question: question.question,
                selectedAnswer: question.options[selectedIndex],
                correctAnswer: question.options[question.correct],
                isCorrect: isCorrect
            });

            document.querySelectorAll('.option-btn').forEach(btn => {
                btn.classList.add('disabled');
            });

            const selectedBtn = document.getElementById(`option-${selectedIndex}`);
            selectedBtn.classList.add(isCorrect ? 'correct' : 'incorrect');

            if (!isCorrect) {
                document.getElementById(`option-${question.correct}`).classList.add('correct');
            }

            feedback.classList.remove('hidden');
            if (isCorrect) {
                score++;
                feedback.className = 'mt-4 p-4 rounded-lg bg-green-100 border border-green-400 text-green-800';
                feedback.innerHTML = '✅ ¡Correcto! Excelente trabajo.';
            } else {
                feedback.className = 'mt-4 p-4 rounded-lg bg-red-100 border border-red-400 text-red-800';
                feedback.innerHTML = `❌ Incorrecto. La respuesta correcta es: ${question.options[question.correct]}`;
            }

            answeredQuestions[currentQuestionIndex] = true;
            document.getElementById('score').textContent = score;
        }

        function updateProgress() {
            document.getElementById('currentQuestion').textContent = currentQuestionIndex + 1;
            const progress = ((currentQuestionIndex + 1) / quizData.length) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function updateButtons() {
            const prevBtn = document.getElementById('prevBtn');
            const nextBtn = document.getElementById('nextBtn');

            prevBtn.disabled = currentQuestionIndex === 0;

            if (currentQuestionIndex === quizData.length - 1) {
                nextBtn.textContent = 'Ver Resultados';
                nextBtn.onclick = showResults;
            } else {
                nextBtn.textContent = 'Siguiente →';
                nextBtn.onclick = nextQuestion;
            }
        }

        function nextQuestion() {
            if (currentQuestionIndex < quizData.length - 1) {
                currentQuestionIndex++;
                renderQuestion();
            }
        }

        function prevQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                renderQuestion();
            }
        }

        function showResults() {
            const endTime = new Date();
            const percentage = (score / quizData.length) * 100;
            
            // Guardar resultado en localStorage
            saveResult({
                name: studentName,
                section: studentSection,
                score: score,
                total: quizData.length,
                percentage: percentage,
                date: endTime.toLocaleString('es-DO'),
                timestamp: endTime.getTime(),
                detailedAnswers: detailedAnswers
            });

            document.getElementById('quizHeader').classList.add('hidden');
            document.getElementById('quizContainer').classList.add('hidden');
            document.getElementById('navButtons').classList.add('hidden');
            document.getElementById('results').classList.remove('hidden');
            
            document.getElementById('resultName').textContent = studentName;
            document.getElementById('resultSection').textContent = studentSection;
            document.getElementById('resultDate').textContent = endTime.toLocaleString('es-DO');
            document.getElementById('finalScore').textContent = score;
            document.getElementById('percentage').textContent = percentage.toFixed(0);

            let message = '';
            if (percentage >= 90) {
                message = '🌟 ¡Excelente! Dominas el tema completamente.';
            } else if (percentage >= 70) {
                message = '👍 ¡Muy bien! Tienes un buen conocimiento del tema.';
            } else if (percentage >= 50) {
                message = '📚 Bien, pero necesitas repasar algunos conceptos.';
            } else {
                message = '💪 Sigue estudiando, puedes mejorar mucho más.';
            }
            document.getElementById('resultMessage').textContent = message;

            // Mostrar panel del profesor
            loadTeacherPanel();
        }

        function saveResult(result) {
            let results = JSON.parse(localStorage.getItem('quizResults') || '[]');
            results.push(result);
            localStorage.setItem('quizResults', JSON.stringify(results));
        }

        function loadTeacherPanel() {
            const results = JSON.parse(localStorage.getItem('quizResults') || '[]');
            const tableBody = document.getElementById('resultsTable');
            
            if (results.length > 0) {
                document.getElementById('teacherPanel').classList.remove('hidden');
                
                // Ordenar por timestamp (más reciente primero)
                results.sort((a, b) => b.timestamp - a.timestamp);
                
                tableBody.innerHTML = results.map((result, index) => `
                    <tr class="${index % 2 === 0 ? 'bg-gray-50' : 'bg-white'}">
                        <td class="px-4 py-3">${result.name}</td>
                        <td class="px-4 py-3">${result.section}</td>
                        <td class="px-4 py-3 text-center font-bold">${result.score}/${result.total}</td>
                        <td class="px-4 py-3 text-center">
                            <span class="px-3 py-1 rounded-full text-sm font-semibold ${
                                result.percentage >= 90 ? 'bg-green-200 text-green-800' :
                                result.percentage >= 70 ? 'bg-blue-200 text-blue-800' :
                                result.percentage >= 50 ? 'bg-yellow-200 text-yellow-800' :
                                'bg-red-200 text-red-800'
                            }">
                                ${result.percentage.toFixed(0)}%
                            </span>
                        </td>
                        <td class="px-4 py-3 text-sm">${result.date}</td>
                    </tr>
                `).join('');
            }
        }

        function downloadResult() {
            const results = JSON.parse(localStorage.getItem('quizResults') || '[]');
            const currentResult = results[results.length - 1];
            
            let content = `EVALUACIÓN: LA TIERRA SE ESTREMECE
Terremotos, Volcanes y Tsunamis - 2do Grado
==========================================

DATOS DEL ESTUDIANTE:
Nombre: ${currentResult.name}
Sección: ${currentResult.section}
Fecha: ${currentResult.date}

RESULTADO:
Puntuación: ${currentResult.score}/${currentResult.total}
Porcentaje: ${currentResult.percentage.toFixed(2)}%

DETALLE DE RESPUESTAS:
==========================================
`;

            currentResult.detailedAnswers.forEach((answer, index) => {
                content += `\n${index + 1}. ${answer.question}
Tu respuesta: ${answer.selectedAnswer} ${answer.isCorrect ? '✓' : '✗'}
${!answer.isCorrect ? `Respuesta correcta: ${answer.correctAnswer}` : ''}
------------------------------------------
`;
            });

            const blob = new Blob([content], { type: 'text/plain' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `Evaluacion_${currentResult.name.replace(/\s+/g, '_')}_${Date.now()}.txt`;
            a.click();
        }

        function exportAllResults() {
            const results = JSON.parse(localStorage.getItem('quizResults') || '[]');
            
            let csv = 'Nombre,Sección,Puntuación,Total,Porcentaje,Fecha\n';
            results.forEach(result => {
                csv += `"${result.name}","${result.section}",${result.score},${result.total},${result.percentage.toFixed(2)},"${result.date}"\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `Resultados_Evaluacion_${Date.now()}.csv`;
            a.click();
        }

        // Event Listeners
        document.getElementById('prevBtn').addEventListener('click', prevQuestion);

        // Cargar panel del profesor al inicio si hay resultados
        window.addEventListener('load', () => {
            const results = JSON.parse(localStorage.getItem('quizResults') || '[]');
            if (results.length > 0 && document.getElementById('loginForm').classList.contains('hidden') === false) {
                // Mostrar botón para ver resultados anteriores
                const loginForm = document.getElementById('loginForm');
                const viewResultsBtn = document.createElement('button');
                viewResultsBtn.type = 'button';
                viewResultsBtn.className = 'w-full mt-4 bg-gray-600 text-white py-2 rounded-lg hover:bg-gray-700 transition-colors text-sm';
                viewResultsBtn.textContent = '👨‍🏫 Ver Resultados Anteriores (Profesor)';
                viewResultsBtn.onclick = () => {
                    document.getElementById('loginForm').classList.add('hidden');
                    document.getElementById('teacherPanel').classList.remove('hidden');
                    loadTeacherPanel();
                };
                loginForm.querySelector('form').appendChild(viewResultsBtn);
            }
        });
    </script>
</body>
</html>
