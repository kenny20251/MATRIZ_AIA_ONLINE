<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matriz AIA - Análisis de Impacto Ambiental | Ecuador</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        :root {
            --primary-color: #117a65;
            --secondary-color: #16a085;
            --accent-color: #1abc9c;
            --light-color: #e8f8f5;
            --dark-color: #0e6251;
            --text-color: #333;
            --border-radius: 8px;
            --box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: var(--text-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 25px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 800px;
            margin: 0 auto;
        }
        
        .matrix-section {
            background: white;
            padding: 30px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            margin-bottom: 30px;
        }
        
        .section-title {
            font-size: 1.5rem;
            margin-bottom: 25px;
            color: var(--dark-color);
            border-bottom: 2px solid var(--accent-color);
            padding-bottom: 10px;
        }
        
        .company-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark-color);
        }
        
        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(22, 160, 133, 0.1);
        }
        
        textarea {
            min-height: 80px;
            resize: vertical;
        }
        
        .matrix-container {
            overflow-x: auto;
            margin: 25px 0;
            border: 1px solid #e0e0e0;
            border-radius: var(--border-radius);
        }
        
        .matrix-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 1200px;
        }
        
        .matrix-table th {
            background: var(--light-color);
            padding: 15px 12px;
            text-align: center;
            font-weight: 600;
            border: 1px solid #ddd;
            position: sticky;
            top: 0;
        }
        
        .matrix-table td {
            padding: 12px;
            border: 1px solid #ddd;
            text-align: center;
        }
        
        .matrix-table tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        .matrix-table tr:hover {
            background-color: #f0f0f0;
        }
        
        .impact-cell {
            font-weight: 600;
            border-radius: 4px;
        }
        
        .impact-low {
            background-color: #e8f5e9;
            color: #2e7d32;
        }
        
        .impact-medium {
            background-color: #fff3e0;
            color: #ef6c00;
        }
        
        .impact-high {
            background-color: #ffebee;
            color: #c62828;
        }
        
        .impact-very-high {
            background-color: #fce4ec;
            color: #ad1457;
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .summary-card {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            border-left: 5px solid var(--secondary-color);
        }
        
        .summary-card h3 {
            color: var(--dark-color);
            margin-bottom: 15px;
            font-size: 1.2rem;
        }
        
        .summary-value {
            font-size: 2rem;
            font-weight: bold;
            color: var(--primary-color);
            margin-bottom: 10px;
        }
        
        .action-plan {
            margin: 25px 0;
        }
        
        .action-item {
            background: white;
            padding: 20px;
            border-radius: var(--border-radius);
            margin-bottom: 15px;
            border-left: 4px solid var(--secondary-color);
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .action-priority {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-right: 15px;
        }
        
        .priority-high {
            background-color: #ff5252;
            color: white;
        }
        
        .priority-medium {
            background-color: #ff9800;
            color: white;
        }
        
        .priority-low {
            background-color: #4caf50;
            color: white;
        }
        
        .btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 14px 28px;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 10px;
        }
        
        .btn:hover {
            background-color: var(--dark-color);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        .btn-download {
            background-color: #1976d2;
        }
        
        .btn-download:hover {
            background-color: #1565c0;
        }
        
        .btn-evaluate {
            background-color: #ff9800;
        }
        
        .btn-evaluate:hover {
            background-color: #f57c00;
        }
        
        .btn-clear {
            background-color: #f44336;
        }
        
        .btn-clear:hover {
            background-color: #d32f2f;
        }
        
        .btn-suggest {
            background-color: #9c27b0;
        }
        
        .btn-suggest:hover {
            background-color: #7b1fa2;
        }
        
        .tooltip {
            position: relative;
            display: inline-block;
            cursor: help;
            margin-left: 5px;
        }
        
        .tooltip .tooltiptext {
            visibility: hidden;
            width: 220px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 8px;
            position: absolute;
            z-index: 1000;
            bottom: 125%;
            left: 50%;
            margin-left: -110px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 0.8rem;
            line-height: 1.4;
        }
        
        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        
        .controls {
            display: flex;
            gap: 15px;
            margin: 25px 0;
            flex-wrap: wrap;
        }
        
        .legend {
            display: flex;
            gap: 15px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9rem;
        }
        
        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 4px;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #666;
            font-size: 0.9rem;
            border-top: 1px solid #e0e0e0;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: var(--primary-color);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 10px;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .matrix-section {
                padding: 20px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .controls {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Matriz AIA - Análisis de Impacto Ambiental</h1>
            <p class="subtitle">Sistema profesional de evaluación de impactos ambientales para empresas ecuatorianas</p>
        </header>
        
        <div class="matrix-section">
            <h2 class="section-title">Información de la Empresa</h2>
            
            <div class="company-info">
                <div class="form-group">
                    <label for="company-name">Nombre de la Empresa</label>
                    <input type="text" id="company-name" placeholder="Ingrese el nombre de la empresa">
                </div>
                
                <div class="form-group">
                    <label for="sector">Sector Industrial</label>
                    <select id="sector">
                        <option value="">Seleccione el sector</option>
                        <option value="manufactura">Manufactura</option>
                        <option value="agricultura">Agricultura</option>
                        <option value="ganaderia">Ganadería</option>
                        <option value="mineria">Minería</option>
                        <option value="construccion">Construcción</option>
                        <option value="comercio">Comercio</option>
                        <option value="servicios">Servicios</option>
                        <option value="turismo">Turismo</option>
                        <option value="alimentos">Procesamiento de Alimentos</option>
                        <option value="textil">Textil</option>
                        <option value="quimica">Industria Química</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="employees">Número de Empleados</label>
                    <input type="number" id="employees" min="1" value="10">
                </div>
                
                <div class="form-group">
                    <label for="province">Provincia</label>
                    <select id="province">
                        <option value="">Seleccione la provincia</option>
                        <option value="pichincha">Pichincha</option>
                        <option value="guayas">Guayas</option>
                        <option value="azuay">Azuay</option>
                        <option value="manabi">Manabí</option>
                        <option value="tungurahua">Tungurahua</option>
                        <option value="eloro">El Oro</option>
                        <option value="imbabura">Imbabura</option>
                        <option value="loja">Loja</option>
                        <option value="chimborazo">Chimborazo</option>
                        <option value="otra">Otra</option>
                    </select>
                </div>
            </div>
            
            <div class="form-group">
                <label for="project-description">Descripción del Proyecto o Actividad</label>
                <textarea id="project-description" placeholder="Describa brevemente el proyecto o actividad a evaluar"></textarea>
            </div>
        </div>
        
        <div class="matrix-section">
            <h2 class="section-title">Matriz de Identificación de Impactos Ambientales</h2>
            <p>Complete la evaluación de impactos ambientales para cada aspecto identificado:</p>
            
            <div class="legend">
                <div class="legend-item">
                    <div class="legend-color impact-low"></div>
                    <span>Impacto Bajo (1-8 puntos)</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color impact-medium"></div>
                    <span>Impacto Medio (9-24 puntos)</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color impact-high"></div>
                    <span>Impacto Alto (25-48 puntos)</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color impact-very-high"></div>
                    <span>Impacto Muy Alto (49-64 puntos)</span>
                </div>
            </div>
            
            <div class="matrix-container">
                <table class="matrix-table">
                    <thead>
                        <tr>
                            <th>Aspecto Ambiental</th>
                            <th>Actividad Relacionada</th>
                            <th>Impacto Ambiental</th>
                            <th>Significancia
                                <span class="tooltip">?
                                    <span class="tooltiptext">1=Bajo, 2=Medio, 3=Alto, 4=Muy Alto<br>Grado de importancia del impacto</span>
                                </span>
                            </th>
                            <th>Probabilidad
                                <span class="tooltip">?
                                    <span class="tooltiptext">1=Rara, 2=Ocasional, 3=Frecuente, 4=Constante<br>Frecuencia de ocurrencia del impacto</span>
                                </span>
                            </th>
                            <th>Severidad
                                <span class="tooltip">?
                                    <span class="tooltiptext">1=Insignificante, 2=Menor, 3=Moderada, 4=Severa<br>Grado de afectación al ambiente</span>
                                </span>
                            </th>
                            <th>Puntaje Total</th>
                            <th>Nivel de Impacto</th>
                            <th>Medidas de Mitigación</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody id="matrix-body">
                        <!-- Se llenará dinámicamente -->
                    </tbody>
                </table>
            </div>
            
            <div class="controls">
                <button class="btn btn-evaluate" id="evaluate-impacts">
                    <span>📊</span>
                    Evaluar Impactos
                </button>
                <button class="btn" id="add-aspect">
                    <span>➕</span>
                    Agregar Aspecto
                </button>
                <button class="btn btn-suggest" id="suggest-mitigations">
                    <span>💡</span>
                    Sugerir Mitigaciones
                </button>
                <button class="btn btn-clear" id="clear-all">
                    <span>🗑️</span>
                    Borrar Todo
                </button>
                <button class="btn btn-download" id="download-report">
                    <span>📥</span>
                    Descargar Reporte AIA
                </button>
            </div>
        </div>
        
        <div class="matrix-section" id="results-section" style="display: none;">
            <h2 class="section-title">Resultados del Análisis AIA</h2>
            
            <div class="summary-cards">
                <div class="summary-card">
                    <h3>Impacto Ambiental Total</h3>
                    <div class="summary-value" id="total-impact-score">0</div>
                    <p>Puntaje acumulado</p>
                </div>
                <div class="summary-card">
                    <h3>Nivel General</h3>
                    <div class="summary-value" id="overall-impact-level">-</div>
                    <p>Clasificación general</p>
                </div>
                <div class="summary-card">
                    <h3>Aspectos Críticos</h3>
                    <div class="summary-value" id="critical-aspects">0</div>
                    <p>Impactos Altos/Muy Altos</p>
                </div>
                <div class="summary-card">
                    <h3>Eficacia de Mitigación</h3>
                    <div class="summary-value" id="mitigation-effectiveness">0%</div>
                    <p>Medidas implementadas</p>
                </div>
            </div>
            
            <h3 class="section-title">Plan de Acción Recomendado</h3>
            <div class="action-plan" id="action-plan-content">
                <!-- Se llenará dinámicamente -->
            </div>
        </div>
        
        <footer>
            <p>Matriz AIA - Sistema de Análisis de Impacto Ambiental © 2023 | 
               Basado en normativa del Ministerio del Ambiente, Agua y Transición Ecológica del Ecuador</p>
        </footer>
    </div>

    <script>
        // Datos de la matriz AIA
        let matrixData = [];
        
        // Base de conocimientos para recomendaciones de mitigación
        const mitigationRecommendations = {
            "emisiones": [
                "Instalar sistemas de filtración y tratamiento de gases",
                "Implementar programas de mantenimiento preventivo de equipos",
                "Utilizar combustibles más limpios y renovables",
                "Optimizar procesos de combustión para mayor eficiencia",
                "Monitoreo continuo de emisiones con equipos certificados"
            ],
            "agua": [
                "Implementar sistemas de recirculación y reutilización de agua",
                "Instalar medidores de flujo para control de consumo",
                "Utilizar tecnologías de riego por goteo en áreas verdes",
                "Captación y aprovechamiento de agua lluvia",
                "Tratamiento de aguas residuales para reúso"
            ],
            "residuos": [
                "Implementar programa de segregación en la fuente",
                "Compostaje de residuos orgánicos",
                "Alianzas con gestores autorizados de residuos",
                "Reducir uso de materiales desechables",
                "Programas de reutilización y reciclaje interno"
            ],
            "peligrosos": [
                "Almacenamiento en áreas designadas con contención secundaria",
                "Capacitación en manejo seguro de sustancias peligrosas",
                "Hojas de seguridad accesibles para todos los trabajadores",
                "Plan de contingencia para derrames y emergencias",
                "Disposición final mediante gestores autorizados"
            ],
            "energia": [
                "Auditorías energéticas periódicas",
                "Instalación de paneles solares fotovoltaicos",
                "Sistemas de iluminación LED con sensores de movimiento",
                "Optimización de horarios de operación de equipos",
                "Mantenimiento preventivo de sistemas eléctricos"
            ],
            "ruido": [
                "Instalación de barreras acústicas",
                "Programación de actividades ruidosas en horarios específicos",
                "Mantenimiento preventivo de equipos para reducir vibraciones",
                "Uso de equipos de protección personal auditiva",
                "Monitoreo periódico de niveles de ruido"
            ],
            "vertidos": [
                "Sistemas de tratamiento de aguas residuales",
                "Separadores de grasas y aceites",
                "Control de pH y parámetros críticos antes del vertido",
                "Programas de prevención de derrames",
                "Cumplimiento de normativas de vertimiento"
            ],
            "recursos": [
                "Programas de reforestación y compensación",
                "Uso de materiales reciclados y renovables",
                "Optimización en el uso de materias primas",
                "Evaluación de ciclo de vida de productos",
                "Certificaciones de sostenibilidad"
            ],
            "paisaje": [
                "Integración arquitectónica con el entorno",
                "Uso de colores y materiales que armonicen con el paisaje",
                "Mantenimiento de barreras vegetales naturales",
                "Plan de restauración paisajística post-operación",
                "Estudios de impacto visual previos a la construcción"
            ],
            "olores": [
                "Sistemas de tratamiento de olores (biofiltros, carbón activado)",
                "Encapsulación de procesos generadores de olores",
                "Control de temperatura y pH en procesos biológicos",
                "Ventilación forzada con tratamiento de aire",
                "Monitoreo comunitario de olores"
            ]
        };

        // Mapeo de aspectos a categorías de mitigación
        const aspectToCategory = {
            "Emisiones atmosféricas": "emisiones",
            "Consumo de agua": "agua",
            "Generación de residuos sólidos": "residuos",
            "Generación de residuos peligrosos": "peligrosos",
            "Consumo energético": "energia",
            "Ruido y vibraciones": "ruido",
            "Vertidos líquidos": "vertidos",
            "Uso de recursos naturales": "recursos",
            "Alteración del paisaje": "paisaje",
            "Generación de olores": "olores"
        };
        
        document.addEventListener('DOMContentLoaded', function() {
            // Inicializar matriz con aspectos predefinidos
            initializeMatrix();
            
            // Configurar event listeners
            document.getElementById('evaluate-impacts').addEventListener('click', evaluateImpacts);
            document.getElementById('add-aspect').addEventListener('click', addCustomAspect);
            document.getElementById('suggest-mitigations').addEventListener('click', suggestMitigations);
            document.getElementById('clear-all').addEventListener('click', clearAllAspects);
            document.getElementById('download-report').addEventListener('click', downloadReport);
        });
        
        function initializeMatrix() {
            const matrixBody = document.getElementById('matrix-body');
            
            // Aspectos ambientales predefinidos
            const predefinedAspects = [
                {
                    aspect: "Emisiones atmosféricas",
                    activity: "Combustión en procesos industriales",
                    impact: "Contaminación del aire, contribución al cambio climático"
                },
                {
                    aspect: "Consumo de agua",
                    activity: "Procesos productivos y sanitarios",
                    impact: "Agotamiento de recursos hídricos, afectación a ecosistemas"
                },
                {
                    aspect: "Generación de residuos sólidos",
                    activity: "Operaciones generales de la empresa",
                    impact: "Contaminación del suelo, ocupación de espacio en rellenos"
                },
                {
                    aspect: "Generación de residuos peligrosos",
                    activity: "Manejo de productos químicos y sustancias",
                    impact: "Contaminación peligrosa, riesgos para la salud"
                },
                {
                    aspect: "Consumo energético",
                    activity: "Operación de equipos y maquinaria",
                    impact: "Agotamiento de recursos no renovables, emisiones indirectas"
                }
            ];
            
            matrixBody.innerHTML = '';
            matrixData = [];
            
            predefinedAspects.forEach((item, index) => {
                addMatrixRow(item.aspect, item.activity, item.impact, index);
            });
        }
        
        function addMatrixRow(aspect, activity, impact, index) {
            const matrixBody = document.getElementById('matrix-body');
            const row = document.createElement('tr');
            
            row.innerHTML = `
                <td>${aspect}</td>
                <td>${activity}</td>
                <td>${impact}</td>
                <td>
                    <select class="significance" data-index="${index}">
                        <option value="1">1 - Bajo</option>
                        <option value="2" selected>2 - Medio</option>
                        <option value="3">3 - Alto</option>
                        <option value="4">4 - Muy Alto</option>
                    </select>
                </td>
                <td>
                    <select class="probability" data-index="${index}">
                        <option value="1">1 - Rara</option>
                        <option value="2" selected>2 - Ocasional</option>
                        <option value="3">3 - Frecuente</option>
                        <option value="4">4 - Constante</option>
                    </select>
                </td>
                <td>
                    <select class="severity" data-index="${index}">
                        <option value="1">1 - Insignificante</option>
                        <option value="2" selected>2 - Menor</option>
                        <option value="3">3 - Moderada</option>
                        <option value="4">4 - Severa</option>
                    </select>
                </td>
                <td class="total-score" id="score-${index}">8</td>
                <td class="impact-level" id="level-${index}">-</td>
                <td>
                    <textarea class="mitigation" data-index="${index}" placeholder="Describa las medidas de mitigación..." style="width: 100%; height: 60px; font-size: 0.8rem;"></textarea>
                </td>
                <td>
                    <button class="btn-suggest-mitigation" data-index="${index}" style="padding: 5px 10px; font-size: 0.8rem; background: #9c27b0;">
                        💡 Sugerir
                    </button>
                </td>
            `;
            
            matrixBody.appendChild(row);
            
            // Almacenar datos iniciales
            matrixData.push({
                aspect: aspect,
                activity: activity,
                impact: impact,
                significance: 2,
                probability: 2,
                severity: 2,
                totalScore: 8,
                impactLevel: 'MEDIO',
                mitigation: ''
            });
            
            // Agregar event listeners
            const significanceSelect = row.querySelector('.significance');
            const probabilitySelect = row.querySelector('.probability');
            const severitySelect = row.querySelector('.severity');
            const mitigationTextarea = row.querySelector('.mitigation');
            const suggestButton = row.querySelector('.btn-suggest-mitigation');
            
            significanceSelect.addEventListener('change', () => updateMatrixScore(index));
            probabilitySelect.addEventListener('change', () => updateMatrixScore(index));
            severitySelect.addEventListener('change', () => updateMatrixScore(index));
            mitigationTextarea.addEventListener('input', () => updateMitigation(index));
            suggestButton.addEventListener('click', () => suggestMitigationForAspect(index));
            
            // Calcular puntaje inicial
            updateMatrixScore(index);
        }
        
        function updateMatrixScore(index) {
            const significance = parseInt(document.querySelector(`.significance[data-index="${index}"]`).value);
            const probability = parseInt(document.querySelector(`.probability[data-index="${index}"]`).value);
            const severity = parseInt(document.querySelector(`.severity[data-index="${index}"]`).value);
            
            const totalScore = significance * probability * severity;
            
            // Actualizar puntaje total
            document.getElementById(`score-${index}`).textContent = totalScore;
            
            // Determinar nivel de impacto y clase CSS
            let impactLevel, impactClass;
            if (totalScore <= 8) {
                impactLevel = 'BAJO';
                impactClass = 'impact-low';
            } else if (totalScore <= 24) {
                impactLevel = 'MEDIO';
                impactClass = 'impact-medium';
            } else if (totalScore <= 48) {
                impactLevel = 'ALTO';
                impactClass = 'impact-high';
            } else {
                impactLevel = 'MUY ALTO';
                impactClass = 'impact-very-high';
            }
            
            // Actualizar nivel de impacto
            const levelCell = document.getElementById(`level-${index}`);
            levelCell.textContent = impactLevel;
            levelCell.className = `impact-cell ${impactClass}`;
            
            // Actualizar datos en memoria
            matrixData[index].significance = significance;
            matrixData[index].probability = probability;
            matrixData[index].severity = severity;
            matrixData[index].totalScore = totalScore;
            matrixData[index].impactLevel = impactLevel;
        }
        
        function updateMitigation(index) {
            const mitigationText = document.querySelector(`.mitigation[data-index="${index}"]`).value;
            matrixData[index].mitigation = mitigationText;
        }
        
        function addCustomAspect() {
            const aspect = prompt("Ingrese el aspecto ambiental:");
            if (!aspect) return;
            
            const activity = prompt("Ingrese la actividad relacionada:");
            if (!activity) return;
            
            const impact = prompt("Ingrese el impacto ambiental:");
            if (!impact) return;
            
            const newIndex = matrixData.length;
            addMatrixRow(aspect, activity, impact, newIndex);
        }
        
        function clearAllAspects() {
            if (confirm('¿Está seguro de que desea borrar todas las actividades? Esta acción no se puede deshacer.')) {
                const matrixBody = document.getElementById('matrix-body');
                matrixBody.innerHTML = '';
                matrixData = [];
                
                // Ocultar resultados si estaban visibles
                document.getElementById('results-section').style.display = 'none';
                
                alert('Todas las actividades han sido eliminadas. Puede comenzar con una matriz nueva.');
            }
        }
        
        function suggestMitigationForAspect(index) {
            const aspect = matrixData[index].aspect;
            const category = aspectToCategory[aspect] || "residuos"; // Default category
            
            if (mitigationRecommendations[category]) {
                const recommendations = mitigationRecommendations[category];
                const randomRecommendations = getRandomRecommendations(recommendations, 3);
                
                const mitigationText = randomRecommendations.join('\n• ');
                document.querySelector(`.mitigation[data-index="${index}"]`).value = '• ' + mitigationText;
                updateMitigation(index);
                
                alert(`Se han sugerido medidas de mitigación para: ${aspect}`);
            }
        }
        
        function suggestMitigations() {
            if (matrixData.length === 0) {
                alert('No hay aspectos ambientales para sugerir mitigaciones.');
                return;
            }
            
            let suggestedCount = 0;
            
            matrixData.forEach((item, index) => {
                if (!item.mitigation.trim()) { // Solo sugerir si no hay mitigación existente
                    const category = aspectToCategory[item.aspect] || "residuos";
                    
                    if (mitigationRecommendations[category]) {
                        const recommendations = mitigationRecommendations[category];
                        const randomRecommendations = getRandomRecommendations(recommendations, 2);
                        
                        const mitigationText = randomRecommendations.join('\n• ');
                        document.querySelector(`.mitigation[data-index="${index}"]`).value = '• ' + mitigationText;
                        updateMitigation(index);
                        suggestedCount++;
                    }
                }
            });
            
            if (suggestedCount > 0) {
                alert(`Se han sugerido medidas de mitigación para ${suggestedCount} aspectos ambientales.`);
            } else {
                alert('Todos los aspectos ambientales ya tienen medidas de mitigación definidas.');
            }
        }
        
        function getRandomRecommendations(array, count) {
            const shuffled = [...array].sort(() => 0.5 - Math.random());
            return shuffled.slice(0, count);
        }
        
        function evaluateImpacts() {
            // Validar información de la empresa
            const companyName = document.getElementById('company-name').value;
            if (!companyName) {
                alert('Por favor ingrese el nombre de la empresa.');
                return;
            }
            
            if (matrixData.length === 0) {
                alert('No hay aspectos ambientales para evaluar. Por favor agregue al menos un aspecto.');
                return;
            }
            
            // Calcular métricas generales
            const totalImpactScore = matrixData.reduce((sum, item) => sum + item.totalScore, 0);
            const averageImpact = totalImpactScore / matrixData.length;
            const criticalAspects = matrixData.filter(item => 
                item.impactLevel === 'ALTO' || item.impactLevel === 'MUY ALTO'
            ).length;
            
            // Determinar nivel general
            let overallLevel, overallClass;
            if (averageImpact <= 8) {
                overallLevel = 'BAJO';
                overallClass = 'impact-low';
            } else if (averageImpact <= 24) {
                overallLevel = 'MEDIO';
                overallClass = 'impact-medium';
            } else if (averageImpact <= 48) {
                overallLevel = 'ALTO';
                overallClass = 'impact-high';
            } else {
                overallLevel = 'MUY ALTO';
                overallClass = 'impact-very-high';
            }
            
            // Calcular efectividad de mitigación
            const aspectsWithMitigation = matrixData.filter(item => item.mitigation.trim() !== '').length;
            const mitigationEffectiveness = Math.round((aspectsWithMitigation / matrixData.length) * 100);
            
            // Actualizar resultados
            document.getElementById('total-impact-score').textContent = totalImpactScore;
            document.getElementById('overall-impact-level').textContent = overallLevel;
            document.getElementById('overall-impact-level').className = `impact-cell ${overallClass}`;
            document.getElementById('critical-aspects').textContent = criticalAspects;
            document.getElementById('mitigation-effectiveness').textContent = `${mitigationEffectiveness}%`;
            
            // Generar plan de acción
            generateActionPlan();
            
            // Mostrar sección de resultados
            document.getElementById('results-section').style.display = 'block';
            
            // Scroll a resultados
            document.getElementById('results-section').scrollIntoView({ behavior: 'smooth' });
        }
        
        function generateActionPlan() {
            const actionPlanContent = document.getElementById('action-plan-content');
            const highImpacts = matrixData.filter(item => 
                item.impactLevel === 'ALTO' || item.impactLevel === 'MUY ALTO'
            );
            
            let actionsHTML = '';
            
            if (highImpacts.length === 0) {
                actionsHTML = `
                    <div class="action-item">
                        <span class="action-priority priority-low">BAJA</span>
                        <strong>Mantenimiento de Buenas Prácticas</strong>
                        <p>No se identificaron impactos ambientales significativos. Se recomienda mantener las buenas prácticas ambientales actuales y continuar con el monitoreo periódico.</p>
                        <p><strong>Plazo:</strong> Continuo</p>
                    </div>
                `;
            } else {
                highImpacts.forEach((impact, index) => {
                    let priorityClass, priorityText, deadline;
                    
                    if (impact.impactLevel === 'MUY ALTO') {
                        priorityClass = 'priority-high';
                        priorityText = 'ALTA';
                        deadline = 'Inmediato - 1 mes';
                    } else {
                        priorityClass = 'priority-medium';
                        priorityText = 'MEDIA';
                        deadline = '3 - 6 meses';
                    }
                    
                    // Obtener recomendaciones específicas si no hay mitigación definida
                    let mitigationText = impact.mitigation;
                    if (!mitigationText.trim()) {
                        const category = aspectToCategory[impact.aspect] || "residuos";
                        const recommendations = mitigationRecommendations[category] || mitigationRecommendations.residuos;
                        mitigationText = '• ' + getRandomRecommendations(recommendations, 2).join('\n• ');
                    }
                    
                    actionsHTML += `
                        <div class="action-item">
                            <span class="action-priority ${priorityClass}">${priorityText}</span>
                            <strong>${impact.aspect}</strong>
                            <p><strong>Impacto:</strong> ${impact.impact}</p>
                            <p><strong>Actividad:</strong> ${impact.activity}</p>
                            <p><strong>Puntaje:</strong> ${impact.totalScore} (${impact.impactLevel})</p>
                            <p><strong>Medidas Recomendadas:</strong></p>
                            <p style="margin-left: 20px; font-style: italic;">${mitigationText.replace(/\n/g, '<br>')}</p>
                            <p><strong>Plazo:</strong> ${deadline}</p>
                        </div>
                    `;
                });
            }
            
            actionPlanContent.innerHTML = actionsHTML;
        }
        
        function downloadReport() {
            const companyName = document.getElementById('company-name').value;
            if (!companyName) {
                alert('Por favor ingrese el nombre de la empresa antes de generar el reporte.');
                return;
            }
            
            if (matrixData.length === 0) {
                alert('No hay datos de la matriz AIA para generar el reporte.');
                return;
            }
            
            // Mostrar mensaje de procesamiento
            alert('Generando reporte AIA en PDF...');
            
            // Generar PDF con jsPDF
            generatePDFReport();
        }
        
        function generatePDFReport() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Datos para el reporte
            const companyName = document.getElementById('company-name').value;
            const sector = document.getElementById('sector').value;
            const employees = document.getElementById('employees').value;
            const province = document.getElementById('province').value;
            const projectDescription = document.getElementById('project-description').value;
            
            // Configuración inicial
            let yPosition = 20;
            const lineHeight = 7;
            const margin = 20;
            const pageWidth = doc.internal.pageSize.width;
            let pageNumber = 1;
            
            // Función para agregar nueva página
            function addNewPage() {
                doc.addPage();
                yPosition = 20;
                pageNumber++;
                // Agregar número de página
                doc.setFontSize(10);
                doc.setTextColor(100);
                doc.text(`Página ${pageNumber}`, pageWidth - 20, doc.internal.pageSize.height - 10);
                doc.setTextColor(0);
            }
            
            // Cabecera del reporte
            doc.setFontSize(20);
            doc.setTextColor(17, 122, 101);
            doc.text('REPORTE DE MATRIZ AIA', margin, yPosition);
            yPosition += lineHeight * 2;
            
            // Información de la empresa
            doc.setFontSize(12);
            doc.setTextColor(0, 0, 0);
            doc.text(`Empresa: ${companyName}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`Sector: ${sector || 'No especificado'}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`Empleados: ${employees || 'No especificado'}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`Provincia: ${province || 'No especificada'}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`Fecha: ${new Date().toLocaleDateString('es-EC')}`, margin, yPosition);
            yPosition += lineHeight * 2;
            
            // Descripción del proyecto
            if (projectDescription) {
                doc.text('Descripción del Proyecto:', margin, yPosition);
                yPosition += lineHeight;
                const splitDescription = doc.splitTextToSize(projectDescription, pageWidth - 2 * margin);
                doc.text(splitDescription, margin, yPosition);
                yPosition += lineHeight * splitDescription.length;
                yPosition += lineHeight;
            }
            
            // Verificar espacio para la tabla
            if (yPosition > 120) {
                addNewPage();
            }
            
            // Resumen ejecutivo
            doc.setFontSize(14);
            doc.setTextColor(17, 122, 101);
            doc.text('RESUMEN EJECUTIVO', margin, yPosition);
            yPosition += lineHeight * 1.5;
            
            doc.setFontSize(10);
            doc.setTextColor(0, 0, 0);
            
            // Calcular métricas para el resumen
            const totalImpactScore = matrixData.reduce((sum, item) => sum + item.totalScore, 0);
            const criticalAspects = matrixData.filter(item => 
                item.impactLevel === 'ALTO' || item.impactLevel === 'MUY ALTO'
            ).length;
            const aspectsWithMitigation = matrixData.filter(item => item.mitigation.trim() !== '').length;
            const mitigationEffectiveness = Math.round((aspectsWithMitigation / matrixData.length) * 100);
            
            doc.text(`• Total de aspectos evaluados: ${matrixData.length}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`• Puntaje total de impacto: ${totalImpactScore}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`• Aspectos críticos identificados: ${criticalAspects}`, margin, yPosition);
            yPosition += lineHeight;
            doc.text(`• Efectividad de mitigación: ${mitigationEffectiveness}%`, margin, yPosition);
            yPosition += lineHeight * 2;
            
            // Verificar espacio para la tabla
            if (yPosition > 150) {
                addNewPage();
            }
            
            // Matriz AIA detallada
            doc.setFontSize(14);
            doc.setTextColor(17, 122, 101);
            doc.text('MATRIZ AIA DETALLADA', margin, yPosition);
            yPosition += lineHeight * 1.5;
            
            // Configurar tabla
            const tableHeaders = ['Aspecto', 'Actividad', 'Impacto', 'Signif.', 'Prob.', 'Sev.', 'Puntaje', 'Nivel'];
            const tableData = matrixData.map(item => [
                item.aspect,
                item.activity,
                item.impact,
                item.significance.toString(),
                item.probability.toString(),
                item.severity.toString(),
                item.totalScore.toString(),
                item.impactLevel
            ]);
            
            // Función para generar tabla (simplificada)
            doc.setFontSize(8);
            let startY = yPosition;
            
            // Encabezados de tabla
            doc.setFillColor(232, 248, 245);
            doc.rect(margin, startY, pageWidth - 2 * margin, 10, 'F');
            doc.setTextColor(0, 0, 0);
            doc.setFont(undefined, 'bold');
            
            const colWidths = [30, 30, 35, 12, 12, 12, 15, 15];
            let xPosition = margin;
            
            tableHeaders.forEach((header, i) => {
                doc.text(header, xPosition + 2, startY + 6);
                xPosition += colWidths[i];
            });
            
            startY += 10;
            
            // Datos de la tabla
            doc.setFont(undefined, 'normal');
            tableData.forEach((row, rowIndex) => {
                // Verificar si necesita nueva página
                if (startY > doc.internal.pageSize.height - 30) {
                    addNewPage();
                    startY = 20;
                    
                    // Volver a dibujar encabezados
                    doc.setFillColor(232, 248, 245);
                    doc.rect(margin, startY, pageWidth - 2 * margin, 10, 'F');
                    doc.setTextColor(0, 0, 0);
                    doc.setFont(undefined, 'bold');
                    
                    xPosition = margin;
                    tableHeaders.forEach((header, i) => {
                        doc.text(header, xPosition + 2, startY + 6);
                        xPosition += colWidths[i];
                    });
                    
                    startY += 10;
                    doc.setFont(undefined, 'normal');
                }
                
                xPosition = margin;
                row.forEach((cell, cellIndex) => {
                    // Ajustar texto largo
                    let displayText = cell;
                    if (cellIndex < 3 && cell.length > 25) {
                        displayText = cell.substring(0, 22) + '...';
                    }
                    
                    doc.text(displayText, xPosition + 2, startY + 6);
                    xPosition += colWidths[cellIndex];
                });
                
                startY += 8;
            });
            
            yPosition = startY + 10;
            
            // Verificar espacio para medidas de mitigación
            if (yPosition > doc.internal.pageSize.height - 50) {
                addNewPage();
            }
            
            // Medidas de mitigación
            doc.setFontSize(14);
            doc.setTextColor(17, 122, 101);
            doc.text('MEDIDAS DE MITIGACIÓN', margin, yPosition);
            yPosition += lineHeight * 1.5;
            
            doc.setFontSize(10);
            doc.setTextColor(0, 0, 0);
            
            matrixData.forEach((item, index) => {
                if (yPosition > doc.internal.pageSize.height - 30) {
                    addNewPage();
                }
                
                doc.setFont(undefined, 'bold');
                doc.text(`${index + 1}. ${item.aspect}:`, margin, yPosition);
                yPosition += lineHeight;
                
                doc.setFont(undefined, 'normal');
                
                let mitigationText = item.mitigation;
                if (!mitigationText.trim()) {
                    const category = aspectToCategory[item.aspect] || "residuos";
                    const recommendations = mitigationRecommendations[category] || mitigationRecommendations.residuos;
                    mitigationText = '• ' + getRandomRecommendations(recommendations, 2).join('\n• ');
                }
                
                const splitMitigation = doc.splitTextToSize(mitigationText, pageWidth - 2 * margin - 10);
                doc.text(splitMitigation, margin + 5, yPosition);
                yPosition += lineHeight * splitMitigation.length + 5;
            });
            
            // Número de página en la primera página
            doc.setFontSize(10);
            doc.setTextColor(100);
            doc.text('Página 1', pageWidth - 20, doc.internal.pageSize.height - 10);
            
            // Guardar el PDF
            const fileName = `Reporte_AIA_${companyName.replace(/\s+/g, '_')}_${new Date().toISOString().split('T')[0]}.pdf`;
            doc.save(fileName);
            
            alert(`Reporte AIA generado exitosamente: ${fileName}`);
        }
    </script>
</body>
</html>
