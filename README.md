<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego Matemático V2 - Graficación Avanzada</title>
    <style>
        /* RESET Y VARIABLES CSS */
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --success-color: #27ae60;
            --danger-color: #e74c3c;
            --warning-color: #f39c12;
            --info-color: #17a2b8;
            --light-color: #ecf0f1;
            --dark-color: #2c3e50;
            --border-radius: 12px;
            --box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            min-height: 100vh;
            line-height: 1.6;
            color: var(--dark-color);
        }

        /* CONTENEDORES PRINCIPALES */
        .main-container {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            padding: 2rem;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--secondary-color), var(--success-color));
        }

        /* TIPOGRAFÍA */
        .logo {
            font-size: 3rem;
            font-weight: 900;
            background: linear-gradient(45deg, var(--secondary-color), var(--success-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-align: center;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .subtitle {
            text-align: center;
            color: var(--dark-color);
            opacity: 0.8;
            margin-bottom: 2rem;
            font-size: 1.1rem;
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-color);
            margin: 2rem 0 1rem 0;
            position: relative;
            padding-left: 20px;
        }

        .section-title::before {
            content: '';
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 4px;
            height: 24px;
            background: var(--secondary-color);
            border-radius: 2px;
        }

        /* FORMULARIOS Y INPUTS */
        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--dark-color);
            font-size: 0.95rem;
        }

        .form-input {
            width: 100%;
            padding: 1rem;
            border: 2px solid #e1e8ed;
            border-radius: 8px;
            font-size: 1rem;
            transition: var(--transition);
            background: rgba(255, 255, 255, 0.9);
        }

        .form-input:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
            transform: translateY(-1px);
        }

        .form-input:invalid {
            border-color: var(--danger-color);
        }

        /* SELECTOR DE MODO */
        .mode-selector {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
            margin: 2rem 0;
        }

        .mode-option {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.75rem;
            padding: 1.2rem;
            border: 2px solid #e1e8ed;
            border-radius: var(--border-radius);
            cursor: pointer;
            transition: var(--transition);
            font-weight: 600;
            background: rgba(255, 255, 255, 0.5);
        }

        .mode-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
        }

        .mode-option.selected {
            background: var(--secondary-color);
            color: white;
            border-color: var(--secondary-color);
            transform: translateY(-2px);
        }

        .mode-icon {
            font-size: 1.5rem;
        }

        .mode-time {
            font-size: 0.85rem;
            opacity: 0.8;
        }

        /* BOTONES */
        .btn {
            padding: 1rem 2rem;
            border: none;
            border-radius: var(--border-radius);
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            text-decoration: none;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--secondary-color), #2980b9);
            color: white;
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success-color), #229954);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(135deg, #6c757d, #545b62);
            color: white;
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger-color), #c0392b);
            color: white;
        }

        .btn-large {
            padding: 1.25rem 3rem;
            font-size: 1.1rem;
        }

        /* LAYOUT DEL JUEGO */
        .game-container {
            max-width: 1400px;
            width: 100%;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding: 1.5rem;
            background: rgba(255, 255, 255, 0.1);
            border-radius: var(--border-radius);
            backdrop-filter: blur(10px);
        }

        .game-title {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .timer-container {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .timer {
            font-size: 2rem;
            font-weight: 900;
            color: var(--danger-color);
            background: rgba(255, 255, 255, 0.9);
            padding: 0.75rem 1.5rem;
            border-radius: var(--border-radius);
            border: 3px solid var(--danger-color);
            box-shadow: 0 4px 16px rgba(231, 76, 60, 0.3);
            min-width: 120px;
            text-align: center;
        }

        .timer.warning {
            animation: pulse 1s infinite;
            color: var(--warning-color);
            border-color: var(--warning-color);
        }

        .timer.critical {
            animation: shake 0.5s infinite;
            color: var(--danger-color);
            border-color: var(--danger-color);
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        /* EQUIPOS */
        .teams-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .team-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: var(--border-radius);
            padding: 1.5rem;
            border: 2px solid #e1e8ed;
            transition: var(--transition);
            position: relative;
        }

        .team-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            border-radius: var(--border-radius) var(--border-radius) 0 0;
        }

        .team-card.team-a::before {
            background: linear-gradient(90deg, #3498db, #2980b9);
        }

        .team-card.team-b::before {
            background: linear-gradient(90deg, #e74c3c, #c0392b);
        }

        .team-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .team-name {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .team-score {
            background: var(--success-color);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-weight: 600;
            min-width: 60px;
            text-align: center;
        }

        .function-display {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border: 2px solid #dee2e6;
            border-radius: var(--border-radius);
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            font-family: 'Courier New', monospace;
            font-size: 1.3rem;
            font-weight: bold;
            text-align: center;
            color: var(--primary-color);
            position: relative;
        }

        .function-display::before {
            content: 'f(x) = ';
            font-weight: normal;
            color: var(--secondary-color);
        }

        /* TABLA DE VALORES */
        .values-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 1.5rem;
            border-radius: var(--border-radius);
            overflow: hidden;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
        }

        .values-table th {
            background: linear-gradient(135deg, var(--primary-color), #34495e);
            color: white;
            padding: 1rem;
            font-weight: 600;
            text-align: center;
            font-size: 1.1rem;
        }

        .values-table td {
            padding: 0.75rem;
            text-align: center;
            border-bottom: 1px solid #e1e8ed;
            background: rgba(255, 255, 255, 0.8);
        }

        .values-table tr:hover td {
            background: rgba(52, 152, 219, 0.05);
        }

        .values-input {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid transparent;
            border-radius: 6px;
            text-align: center;
            font-size: 1rem;
            font-weight: 600;
            background: rgba(255, 255, 255, 0.9);
            transition: var(--transition);
        }

        .values-input:focus {
            border-color: var(--secondary-color);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        .values-input.correct {
            background: #d4edda;
            border-color: var(--success-color);
            color: var(--success-color);
        }

        .values-input.incorrect {
            background: #f8d7da;
            border-color: var(--danger-color);
            color: var(--danger-color);
        }

        .x-value {
            font-weight: 700;
            font-size: 1.1rem;
            color: var(--primary-color);
        }

        /* GRÁFICO */
        .graph-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: var(--border-radius);
            padding: 2rem;
            margin: 2rem 0;
            border: 2px solid #e1e8ed;
        }

        .graph-title {
            text-align: center;
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
        }

        .canvas-wrapper {
            position: relative;
            width: 100%;
            height: 500px;
            border: 2px solid #dee2e6;
            border-radius: var(--border-radius);
            background: linear-gradient(45deg, #f8f9fa 25%, transparent 25%), 
                        linear-gradient(-45deg, #f8f9fa 25%, transparent 25%), 
                        linear-gradient(45deg, transparent 75%, #f8f9fa 75%), 
                        linear-gradient(-45deg, transparent 75%, #f8f9fa 75%);
            background-size: 20px 20px;
            background-position: 0 0, 0 10px, 10px -10px, -10px 0px;
            overflow: hidden;
        }

        .axis {
            position: absolute;
            background: var(--dark-color);
            z-index: 2;
        }

        .axis-x {
            width: 100%;
            height: 3px;
            top: 50%;
            left: 0;
            transform: translateY(-50%);
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .axis-y {
            width: 3px;
            height: 100%;
            left: 50%;
            top: 0;
            transform: translateX(-50%);
            box-shadow: 2px 0 4px rgba(0,0,0,0.1);
        }

        .grid-line {
            position: absolute;
            background: rgba(52, 152, 219, 0.2);
            z-index: 1;
        }

        .grid-line.vertical {
            width: 1px;
            height: 100%;
            top: 0;
        }

        .grid-line.horizontal {
            width: 100%;
            height: 1px;
            left: 0;
        }

        .axis-label {
            position: absolute;
            font-weight: 600;
            color: var(--primary-color);
            background: rgba(255, 255, 255, 0.9);
            padding: 0.25rem 0.5rem;
            border-radius: 4px;
            font-size: 0.9rem;
            z-index: 3;
        }

        .point {
            position: absolute;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            transform: translate(-50%, -50%);
            z-index: 4;
            cursor: pointer;
            transition: var(--transition);
            border: 3px solid white;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }

        .point:hover {
            transform: translate(-50%, -50%) scale(1.5);
            z-index: 5;
        }

        .point.team-a {
            background: var(--secondary-color);
        }

        .point.team-b {
            background: var(--danger-color);
        }

        .point.correct {
            background: var(--success-color);
            animation: correctPulse 2s infinite;
        }

        .point.incorrect {
            background: var(--danger-color);
            animation: incorrectShake 1s infinite;
        }

        .point.reference {
            background: rgba(44, 62, 80, 0.3);
            border-color: var(--dark-color);
        }

        @keyframes correctPulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
        }

        @keyframes incorrectShake {
            0%, 100% { transform: translate(-50%, -50%); }
            25% { transform: translate(-60%, -50%); }
            75% { transform: translate(-40%, -50%); }
        }

        .point-tooltip {
            position: absolute;
            background: var(--dark-color);
            color: white;
            padding: 0.5rem;
            border-radius: 6px;
            font-size: 0.85rem;
            white-space: nowrap;
            z-index: 6;
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
        }

        .point:hover .point-tooltip {
            opacity: 1;
        }

        /* CONTROLES DEL JUEGO */
        .game-controls {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin: 2rem 0;
            flex-wrap: wrap;
        }

        /* RESULTADOS */
        .results-container {
            max-width: 1200px;
            width: 100%;
        }

        .winner-announcement {
            text-align: center;
            padding: 3rem 2rem;
            background: linear-gradient(135deg, #27ae60, #229954);
            color: white;
            border-radius: var(--border-radius);
            margin-bottom: 2rem;
            position: relative;
            overflow: hidden;
        }

        .winner-announcement::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: repeating-linear-gradient(
                45deg,
                transparent,
                transparent 10px,
                rgba(255,255,255,0.1) 10px,
                rgba(255,255,255,0.1) 20px
            );
            animation: confetti 3s linear infinite;
        }

        @keyframes confetti {
            0% { transform: translateX(-100%) translateY(-100%); }
            100% { transform: translateX(0) translateY(0); }
        }

        .winner-text {
            font-size: 2.5rem;
            font-weight: 900;
            margin-bottom: 1rem;
            position: relative;
            z-index: 2;
        }

        .winner-score {
            font-size: 1.3rem;
            opacity: 0.9;
            position: relative;
            z-index: 2;
        }

        .results-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .result-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: var(--border-radius);
            padding: 2rem;
            border: 2px solid #e1e8ed;
            transition: var(--transition);
        }

        .result-card.winner {
            border-color: var(--success-color);
            background: linear-gradient(135deg, rgba(39, 174, 96, 0.1), rgba(255, 255, 255, 0.95));
            transform: scale(1.02);
        }

        .comparison-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1rem;
            border-radius: var(--border-radius);
            overflow: hidden;
        }

        .comparison-table th {
            background: var(--primary-color);
            color: white;
            padding: 1rem;
            text-align: center;
            font-weight: 600;
        }

        .comparison-table td {
            padding: 0.75rem;
            text-align: center;
            border-bottom: 1px solid #e1e8ed;
            background: rgba(255, 255, 255, 0.8);
        }

        .comparison-table tr:nth-child(even) td {
            background: rgba(248, 249, 250, 0.8);
        }

        .status-icon {
            font-size: 1.2rem;
            font-weight: bold;
        }

        .status-correct {
            color: var(--success-color);
        }

        .status-incorrect {
            color: var(--danger-color);
        }

        /* SEGURIDAD */
        .security-alert {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--danger-color);
            color: white;
            padding: 1rem 1.5rem;
            border-radius: var(--border-radius);
            box-shadow: 0 8px 32px rgba(231, 76, 60, 0.3);
            z-index: 10000;
            font-weight: 600;
            animation: slideIn 0.3s ease;
            max-width: 300px;
        }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .security-counter {
            position: fixed;
            top: 80px;
            right: 20px;
            background: var(--warning-color);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: var(--border-radius);
            font-weight: 600;
            z-index: 10000;
        }

        /* PANTALLAS OCULTAS */
        .screen {
            display: none;
        }

        .screen.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .screen-transition {
            animation: fadeOut 0.3s ease forwards;
        }

        @keyframes fadeOut {
            from { opacity: 1; transform: translateY(0); }
            to { opacity: 0; transform: translateY(-20px); }
        }

        /* RESPONSIVE */
        @media (max-width: 1200px) {
            .teams-grid {
                grid-template-columns: 1fr;
            }
            
            .results-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 768px) {
            .mode-selector {
                grid-template-columns: 1fr;
            }
            
            .game-header {
                flex-direction: column;
                gap: 1rem;
                text-align: center;
            }
            
            .timer {
                font-size: 1.5rem;
            }
            
            .logo {
                font-size: 2rem;
            }
            
            .game-controls {
                flex-direction: column;
                align-items: center;
            }
            
            .canvas-wrapper {
                height: 300px;
            }
        }

        @media (max-width: 480px) {
            .card {
                padding: 1rem;
                margin: 10px;
            }
            
            .btn {
                padding: 0.75rem 1.5rem;
                font-size: 0.9rem;
            }
            
            .values-table th,
            .values-table td {
                padding: 0.5rem 0.25rem;
                font-size: 0.9rem;
            }
        }

        /* ANIMACIONES ADICIONALES */
        .bounce-in {
            animation: bounceIn 0.6s ease;
        }

        @keyframes bounceIn {
            0% { transform: scale(0.3); opacity: 0; }
            50% { transform: scale(1.05); }
            70% { transform: scale(0.9); }
            100% { transform: scale(1); opacity: 1; }
        }

        .slide-up {
            animation: slideUp 0.4s ease;
        }

        @keyframes slideUp {
            from { transform: translateY(30px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 3px;
            overflow: hidden;
            margin-top: 1rem;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--success-color), var(--secondary-color));
            transition: width 1s ease;
            border-radius: 3px;
        }

        /* EFECTOS ESPECIALES */
        .particle {
            position: fixed;
            pointer-events: none;
            z-index: 10000;
        }

        .celebration-text {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 4rem;
            font-weight: 900;
            color: var(--success-color);
            z-index: 10000;
            animation: celebrationPulse 2s ease-in-out;
            pointer-events: none;
        }

        @keyframes celebrationPulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
            50% { transform: translate(-50%, -50%) scale(1.2); opacity: 1; }
        }
    </style>
</head>
<body>
    <!-- PANTALLA DE INICIO -->
    <div class="main-container">
        <div class="card screen active" id="startScreen" style="max-width: 600px; width: 100%;">
            <div class="logo">🎯 Juego Matemático V2</div>
            <p class="subtitle">Sistema Avanzado de Graficación de Funciones<br>Preparatoria - 4º Semestre</p>
            
            <div class="form-group">
                <label class="form-label" for="teamAName">
                    <span>👥</span> Nombre del Equipo A:
                </label>
                <input type="text" 
                       id="teamAName" 
                       class="form-input" 
                       placeholder="Ingresa el nombre del Equipo A"
                       required
                       maxlength="30">
            </div>
            
            <div class="form-group">
                <label class="form-label" for="teamBName">
                    <span>👥</span> Nombre del Equipo B:
                </label>
                <input type="text" 
                       id="teamBName" 
                       class="form-input" 
                       placeholder="Ingresa el nombre del Equipo B"
                       required
                       maxlength="30">
            </div>
            
            <div class="mode-selector">
                <div class="mode-option" data-mode="mental">
                    <div>
                        <div class="mode-icon">🧠</div>
                        <strong>Modo Mental</strong>
                        <div class="mode-time">5 minutos</div>
                    </div>
                </div>
                <div class="mode-option selected" data-mode="notebook">
                    <div>
                        <div class="mode-icon">📝</div>
                        <strong>Modo Libreta</strong>
                        <div class="mode-time">10 minutos</div>
                    </div>
                </div>
            </div>
            
            <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                <button class="btn btn-secondary" onclick="showInstructions()">
                    📖 Ver Instrucciones
                </button>
                <button class="btn btn-primary btn-large" onclick="validateAndStartGame()">
                    🚀 Iniciar Juego
                </button>
            </div>
        </div>
    </div>

    <!-- PANTALLA DE INSTRUCCIONES -->
    <div class="main-container">
        <div class="card screen" id="instructionsScreen" style="max-width: 800px; width: 100%;">
            <div class="logo">📘 Instrucciones del Juego</div>
            
            <div class="section-title">🎮 ¿Cómo jugar?</div>
            <p>Cada equipo recibirá una función matemática diferente que deberán resolver completando una tabla de valores y visualizando los resultados en un plano cartesiano animado.</p>
            
            <div class="section-title">📝 Pasos del juego:</div>
            <ul style="margin-left: 2rem; margin-bottom: 1.5rem;">
                <li style="margin-bottom: 0.5rem;">Se asignará una función matemática única a cada equipo</li>
                <li style="margin-bottom: 0.5rem;">Completen la tabla calculando f(x) para cada valor de x dado (-3 a 3)</li>
                <li style="margin-bottom: 0.5rem;">Presionen "Graficar" para visualizar sus puntos en el plano cartesiano</li>
                <li style="margin-bottom: 0.5rem;">Envíen sus respuestas antes de que termine el tiempo</li>
                <li style="margin-bottom: 0.5rem;">El sistema validará automáticamente sus respuestas</li>
            </ul>
            
            <div class="section-title">⚡ Reglas importantes:</div>
            <ul style="margin-left: 2rem; margin-bottom: 1.5rem;">
                <li style="margin-bottom: 0.5rem;">⏱️ <strong>Tiempo límite:</strong> 5 minutos (Mental) / 10 minutos (Libreta)</li>
                <li style="margin-bottom: 0.5rem;">📊 <strong>Tolerancia:</strong> ±0.1 para respuestas numéricas</li>
                <li style="margin-bottom: 0.5rem;">🏆 <strong>Victoria:</strong> El equipo con más respuestas correctas gana</li>
                <li style="margin-bottom: 0.5rem;">🔄 <strong>Graficación:</strong> Visualización en tiempo real</li>
            </ul>
            
            <div class="section-title">🔒 Sistema anti-trampa:</div>
            <ul style="margin-left: 2rem; margin-bottom: 1.5rem;">
                <li style="margin-bottom: 0.5rem;">🚫 Se detectarán cambios de pestaña/ventana (máximo 3 avisos)</li>
                <li style="margin-bottom: 0.5rem;">🚫 Clic derecho bloqueado durante el juego</li>
                <li style="margin-bottom: 0.5rem;">🚫 Atajos de teclado deshabilitados (Ctrl+C/V/A, F12, etc.)</li>
                <li style="margin-bottom: 0.5rem;">🚫 Solo se permiten valores numéricos en las respuestas</li>
                <li style="margin-bottom: 0.5rem;">⚠️ Demasiados intentos de trampa finalizarán el juego automáticamente</li>
            </ul>
            
            <div class="section-title">🧮 Funciones incluidas:</div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; margin-bottom: 2rem;">
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">x² + 6x + 8</div>
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">2x + 2</div>
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">x³ - 3</div>
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">1/x</div>
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">√(2x)</div>
                <div style="background: #f8f9fa; padding: 1rem; border-radius: 8px; text-align: center; font-family: monospace;">2x² + 2</div>
            </div>
            
            <div style="text-align: center;">
                <button class="btn btn-primary btn-large" onclick="hideInstructions()">
                    ✅ ¡Entendido, estoy listo!
                </button>
            </div>
        </div>
    </div>

    <!-- PANTALLA DEL JUEGO -->
    <div class="main-container">
        <div class="card screen game-container" id="gameScreen">
            <div class="game-header">
                <div class="game-title">🎮 Juego en Progreso</div>
                <div class="timer-container">
                    <div class="timer" id="gameTimer">10:00</div>
                    <div style="display: flex; flex-direction: column; align-items: center; gap: 0.5rem;">
                        <div style="font-size: 0.9rem; font-weight: 600; color: var(--primary-color);">Progreso</div>
                        <div class="progress-bar" style="width: 100px;">
                            <div class="progress-fill" id="timeProgress" style="width: 100%;"></div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="teams-grid">
                <!-- Equipo A -->
                <div class="team-card team-a">
                    <div class="team-header">
                        <div class="team-name" id="teamADisplayName">Equipo A</div>
                        <div class="team-score" id="teamAScore">0/7</div>
                    </div>
                    
                    <div class="function-display" id="teamAFunction">x² + 2x + 1</div>
                    
                    <table class="values-table">
                        <thead>
                            <tr>
                                <th>x</th>
                                <th>f(x)</th>
                            </tr>
                        </thead>
                        <tbody id="teamATable">
                            <!-- Se llena dinámicamente -->
                        </tbody>
                    </table>
                    
                    <div style="text-align: center;">
                        <button class="btn btn-primary" onclick="plotTeamGraph('A')">
                            📊 Graficar Equipo A
                        </button>
                    </div>
                </div>
                
                <!-- Equipo B -->
                <div class="team-card team-b">
                    <div class="team-header">
                        <div class="team-name" id="teamBDisplayName">Equipo B</div>
                        <div class="team-score" id="teamBScore">0/7</div>
                    </div>
                    
                    <div class="function-display" id="teamBFunction">2x + 3</div>
                    
                    <table class="values-table">
                        <thead>
                            <tr>
                                <th>x</th>
                                <th>f(x)</th>
                            </tr>
                        </thead>
                        <tbody id="teamBTable">
                            <!-- Se llena dinámicamente -->
                        </tbody>
                    </table>
                    
                    <div style="text-align: center;">
                        <button class="btn btn-danger" onclick="plotTeamGraph('B')">
                            📊 Graficar Equipo B
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="graph-container">
                <div class="graph-title">📈 Plano Cartesiano Interactivo</div>
                <div class="canvas-wrapper" id="graphCanvas">
                    <div class="axis axis-x"></div>
                    <div class="axis axis-y"></div>
                    <!-- Se agregan líneas de cuadrícula y puntos dinámicamente -->
                </div>
                <div style="display: flex; justify-content: center; gap: 2rem; margin-top: 1rem; flex-wrap: wrap;">
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: var(--secondary-color); border-radius: 50%; border: 2px solid white;"></div>
                        <span id="teamALegend">Equipo A</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: var(--danger-color); border-radius: 50%; border: 2px solid white;"></div>
                        <span id="teamBLegend">Equipo B</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: rgba(44, 62, 80, 0.3); border: 2px solid var(--dark-color); border-radius: 50%;"></div>
                        <span>Valores correctos</span>
                    </div>
                </div>
            </div>
            
            <div class="game-controls">
                <button class="btn btn-secondary" onclick="clearGraph()">
                    🧹 Limpiar Gráfico
                </button>
                <button class="btn btn-success btn-large" onclick="submitAnswers()">
                    🚀 Enviar Respuestas Finales
                </button>
            </div>
        </div>
    </div>

    <!-- PANTALLA DE RESULTADOS -->
    <div class="main-container">
        <div class="card screen results-container" id="resultsScreen">
            <div class="winner-announcement" id="winnerAnnouncement">
                <div class="winner-text" id="winnerText">🏆 ¡Tenemos un ganador!</div>
                <div class="winner-score" id="winnerScore">Resultados calculando...</div>
            </div>
            
            <div class="results-grid">
                <div class="result-card" id="resultCardA">
                    <div class="team-header">
                        <div class="team-name" id="resultTeamAName">Equipo A</div>
                        <div class="team-score" id="resultScoreA">0/7</div>
                    </div>
                    
                    <div style="margin: 1rem 0;">
                        <strong>Función asignada:</strong>
                        <div class="function-display" id="resultFunctionA" style="margin-top: 0.5rem; font-size: 1.1rem;">f(x) = ?</div>
                    </div>
                    
                    <table class="comparison-table">
                        <thead>
                            <tr>
                                <th>x</th>
                                <th>Su respuesta</th>
                                <th>Correcta</th>
                                <th>Estado</th>
                            </tr>
                        </thead>
                        <tbody id="comparisonTableA">
                            <!-- Se llena dinámicamente -->
                        </tbody>
                    </table>
                </div>
                
                <div class="result-card" id="resultCardB">
                    <div class="team-header">
                        <div class="team-name" id="resultTeamBName">Equipo B</div>
                        <div class="team-score" id="resultScoreB">0/7</div>
                    </div>
                    
                    <div style="margin: 1rem 0;">
                        <strong>Función asignada:</strong>
                        <div class="function-display" id="resultFunctionB" style="margin-top: 0.5rem; font-size: 1.1rem;">f(x) = ?</div>
                    </div>
                    
                    <table class="comparison-table">
                        <thead>
                            <tr>
                                <th>x</th>
                                <th>Su respuesta</th>
                                <th>Correcta</th>
                                <th>Estado</th>
                            </tr>
                        </thead>
                        <tbody id="comparisonTableB">
                            <!-- Se llena dinámicamente -->
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div class="graph-container">
                <div class="graph-title">📊 Comparación Final - Respuestas vs Valores Correctos</div>
                <div class="canvas-wrapper" id="finalGraphCanvas">
                    <div class="axis axis-x"></div>
                    <div class="axis axis-y"></div>
                </div>
                <div style="display: flex; justify-content: center; gap: 2rem; margin-top: 1rem; flex-wrap: wrap;">
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: var(--success-color); border-radius: 50%; border: 2px solid white;"></div>
                        <span>Respuestas correctas</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: var(--danger-color); border-radius: 50%; border: 2px solid white;"></div>
                        <span>Respuestas incorrectas</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <div style="width: 16px; height: 16px; background: rgba(44, 62, 80, 0.5); border: 2px solid var(--dark-color); border-radius: 50%;"></div>
                        <span>Valores de referencia</span>
                    </div>
                </div>
            </div>
            
            <div style="text-align: center; margin-top: 2rem;">
                <button class="btn btn-primary btn-large" onclick="restartGame()">
                    🔄 Reiniciar Juego
                </button>
            </div>
        </div>
    </div>

    <script>
        // ================================
        // CONFIGURACIÓN GLOBAL Y DATOS
        // ================================
        
        const MATH_FUNCTIONS = [
            { 
                expr: "x^2 + 6*x + 8", 
                display: "x² + 6x + 8",
                type: "polynomial"
            },
            { 
                expr: "2*x + 2", 
                display: "2x + 2",
                type: "linear"
            },
            { 
                expr: "2*x", 
                display: "2x",
                type: "linear"
            },
            { 
                expr: "2*x - 1", 
                display: "2x - 1",
                type: "linear"
            },
            { 
                expr: "x + 2", 
                display: "x + 2",
                type: "linear"
            },
            { 
                expr: "x + 3", 
                display: "x + 3",
                type: "linear"
            },
            { 
                expr: "1/x", 
                display: "1/x",
                type: "rational",
                domain: "x ≠ 0"
            },
            { 
                expr: "x^2 + 3*x + 2", 
                display: "x² + 3x + 2",
                type: "polynomial"
            },
            { 
                expr: "x^3 - 3", 
                display: "x³ - 3",
                type: "polynomial"
            },
            { 
                expr: "3*x - 2", 
                display: "3x - 2",
                type: "linear"
            },
            { 
                expr: "2*x^2 + 2", 
                display: "2x² + 2",
                type: "polynomial"
            },
            { 
                expr: "Math.sqrt(2*Math.abs(x))", 
                display: "√(2|x|)",
                type: "radical"
            },
            {
                expr: "x^2 - 4",
                display: "x² - 4",
                type: "polynomial"
            },
            {
                expr: "-x^2 + 4",
                display: "-x² + 4",
                type: "polynomial"
            },
            {
                expr: "0.5*x^3 + 1",
                display: "½x³ + 1",
                type: "polynomial"
            }
        ];

        const X_VALUES = [-3, -2, -1, 0, 1, 2, 3];
        const TOLERANCE = 0.1;
        
        // Estado global del juego
        let gameState = {
            // Configuración inicial
            teamA: { name: '', function: null, answers: [], score: 0 },
            teamB: { name: '', function: null, answers: [], score: 0 },
            gameMode: 'notebook', // 'mental' o 'notebook'
            
            // Estado del juego
            isActive: false,
            timeRemaining: 600, // segundos
            totalTime: 600,
            timerInterval: null,
            
            // Seguridad
            securityViolations: 0,
            maxViolations: 3,
            securityActive: false,
            
            // UI
            currentScreen: 'start',
            graphPoints: { A: [], B: [], reference: [] }
        };

        // ================================
        // FUNCIONES DE NAVEGACIÓN
        // ================================
        
        function showScreen(screenId) {
            // Ocultar todas las pantallas
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            
            // Mostrar la pantalla solicitada
            const targetScreen = document.getElementById(screenId + 'Screen');
            if (targetScreen) {
                targetScreen.classList.add('active');
                gameState.currentScreen = screenId;
            }
        }

        function showInstructions() {
            showScreen('instructions');
        }

        function hideInstructions() {
            showScreen('start');
        }

        function validateAndStartGame() {
            const teamAName = document.getElementById('teamAName').value.trim();
            const teamBName = document.getElementById('teamBName').value.trim();
            
            // Validaciones
            if (!teamAName || !teamBName) {
                showAlert('Por favor, ingresa los nombres de ambos equipos.', 'warning');
                return;
            }
            
            if (teamAName === teamBName) {
                showAlert('Los nombres de los equipos deben ser diferentes.', 'warning');
                return;
            }
            
            if (teamAName.length < 2 || teamBName.length < 2) {
                showAlert('Los nombres deben tener al menos 2 caracteres.', 'warning');
                return;
            }
            
            // Configurar equipos
            gameState.teamA.name = teamAName;
            gameState.teamB.name = teamBName;
            gameState.gameMode = document.querySelector('.mode-option.selected').dataset.mode;
            
            // Iniciar juego
            initializeGame();
        }

        function initializeGame() {
            try {
                // Asignar funciones aleatorias diferentes
                const availableFunctions = [...MATH_FUNCTIONS];
                gameState.teamA.function = availableFunctions.splice(
                    Math.floor(Math.random() * availableFunctions.length), 1
                )[0];
                gameState.teamB.function = availableFunctions[
                    Math.floor(Math.random() * availableFunctions.length)
                ];
                
                // Configurar tiempo según el modo
                gameState.totalTime = gameState.gameMode === 'mental' ? 300 : 600; // 5 o 10 minutos
                gameState.timeRemaining = gameState.totalTime;
                
                // Configurar UI
                setupGameUI();
                
                // Crear tablas de valores
                createValuesTables();
                
                // Configurar gráfico
                setupGraph();
                
                // Iniciar timer
                startGameTimer();
                
                // Activar seguridad
                enableSecuritySystem();
                
                // Cambiar a pantalla de juego
                showScreen('game');
                
                gameState.isActive = true;
                
                console.log('🎮 Juego iniciado:', {
                    teamA: gameState.teamA.name,
                    teamB: gameState.teamB.name,
                    mode: gameState.gameMode,
                    timeLimit: gameState.totalTime
                });
                
            } catch (error) {
                console.error('Error iniciando juego:', error);
                showAlert('Error al iniciar el juego. Por favor, intenta de nuevo.', 'danger');
            }
        }

        function setupGameUI() {
            // Nombres de equipos
            document.getElementById('teamADisplayName').textContent = gameState.teamA.name;
            document.getElementById('teamBDisplayName').textContent = gameState.teamB.name;
            document.getElementById('teamALegend').textContent = gameState.teamA.name;
            document.getElementById('teamBLegend').textContent = gameState.teamB.name;
            
            // Funciones
            document.getElementById('teamAFunction').textContent = gameState.teamA.function.display;
            document.getElementById('teamBFunction').textContent = gameState.teamB.function.display;
            
            // Resetear puntajes
            updateTeamScore('A', 0);
            updateTeamScore('B', 0);
        }

        function createValuesTables() {
            createTeamTable('A');
            createTeamTable('B');
        }

        function createTeamTable(team) {
            const tableBody = document.getElementById(`team${team}Table`);
            tableBody.innerHTML = '';
            
            X_VALUES.forEach((x, index) => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="x-value">${x}</td>
                    <td>
                        <input type="number" 
                               step="0.01" 
                               class="values-input secure-input" 
                               id="input_${team}_${index}"
                               data-team="${team}" 
                               data-index="${index}"
                               data-x="${x}"
                               placeholder="f(${x})">
                    </td>
                `;
                tableBody.appendChild(row);
            });
        }

        // ================================
        // SISTEMA DE TIMER Y PROGRESO
        // ================================
        
        function startGameTimer() {
            updateTimerDisplay();
            updateProgressBar();
            
            gameState.timerInterval = setInterval(() => {
                gameState.timeRemaining--;
                updateTimerDisplay();
                updateProgressBar();
                
                // Alertas de tiempo
                if (gameState.timeRemaining === 60) {
                    showAlert('⚠️ ¡Solo queda 1 minuto!', 'warning');
                    document.getElementById('gameTimer').classList.add('warning');
                }
                
                if (gameState.timeRemaining === 30) {
                    showAlert('🚨 ¡Solo quedan 30 segundos!', 'danger');
                    document.getElementById('gameTimer').classList.add('critical');
                }
                
                if (gameState.timeRemaining <= 0) {
                    endGame('timeout');
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(gameState.timeRemaining / 60);
            const seconds = gameState.timeRemaining % 60;
            const display = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
            const timerElement = document.getElementById('gameTimer');
            if (timerElement) {
                timerElement.textContent = display;
            }
        }

        function updateProgressBar() {
            const progress = (gameState.timeRemaining / gameState.totalTime) * 100;
            const progressBar = document.getElementById('timeProgress');
            if (progressBar) {
                progressBar.style.width = `${Math.max(0, progress)}%`;
            }
        }

        function stopGameTimer() {
            if (gameState.timerInterval) {
                clearInterval(gameState.timerInterval);
                gameState.timerInterval = null;
            }
        }

        // ================================
        // SISTEMA DE GRAFICACIÓN
        // ================================
        
        function setupGraph() {
            const canvas = document.getElementById('graphCanvas');
            canvas.innerHTML = `
                <div class="axis axis-x"></div>
                <div class="axis axis-y"></div>
            `;
            
            // Crear líneas de cuadrícula
            createGridLines(canvas);
            
            // Agregar etiquetas de ejes
            addAxisLabels(canvas);
        }

        function createGridLines(canvas) {
            const gridSpacing = canvas.offsetWidth / 10; // 10x10 grid
            
            // Líneas verticales
            for (let i = 1; i < 10; i++) {
                const line = document.createElement('div');
                line.className = 'grid-line vertical';
                line.style.left = `${i * gridSpacing}px`;
                canvas.appendChild(line);
            }
            
            // Líneas horizontales
            for (let i = 1; i < 10; i++) {
                const line = document.createElement('div');
                line.className = 'grid-line horizontal';
                line.style.top = `${i * gridSpacing}px`;
                canvas.appendChild(line);
            }
        }

        function addAxisLabels(canvas) {
            const width = canvas.offsetWidth;
            const height = canvas.offsetHeight;
            
            // Etiquetas del eje X
            for (let i = -5; i <= 5; i++) {
                if (i === 0) continue;
                
                const label = document.createElement('div');
                label.className = 'axis-label';
                label.textContent = i;
                label.style.left = `${((i + 5) / 10) * width - 10}px`;
                label.style.top = `${height / 2 + 10}px`;
                canvas.appendChild(label);
            }
            
            // Etiquetas del eje Y
            for (let i = -5; i <= 5; i++) {
                if (i === 0) continue;
                
                const label = document.createElement('div');
                label.className = 'axis-label';
                label.textContent = -i; // Invertido porque Y aumenta hacia abajo
                label.style.left = `${width / 2 + 10}px`;
                label.style.top = `${((i + 5) / 10) * height - 10}px`;
                canvas.appendChild(label);
            }
        }

        function plotTeamGraph(team) {
            const answers = collectTeamAnswers(team);
            const functionObj = gameState[`team${team}`].function;
            
            // Limpiar puntos anteriores del equipo
            clearTeamPoints(team);
            
            // Graficar puntos del equipo
            const canvas = document.getElementById('graphCanvas');
            const width = canvas.offsetWidth;
            const height = canvas.offsetHeight;
            
            answers.forEach((answer, index) => {
                if (answer.value !== null && !isNaN(answer.value)) {
                    const point = createGraphPoint(answer.x, answer.value, team, index);
                    canvas.appendChild(point);
                    
                    // Animación de aparición
                    setTimeout(() => {
                        point.style.transform = 'translate(-50%, -50%) scale(1)';
                        point.style.opacity = '1';
                    }, index * 100);
                }
            });
            
            // Actualizar contador de puntos graficados
            const pointCount = answers.filter(a => a.value !== null && !isNaN(a.value)).length;
            showAlert(`📊 ${pointCount} puntos graficados para ${gameState[`team${team}`].name}`, 'info');
        }

        function createGraphPoint(x, y, team, index) {
            const canvas = document.getElementById('graphCanvas');
            const width = canvas.offsetWidth;
            const height = canvas.offsetHeight;
            
            const point = document.createElement('div');
            point.className = `point team-${team.toLowerCase()}`;
            point.id = `point_${team}_${index}`;
            
            // Convertir coordenadas matemáticas a píxeles
            const pixelX = ((x + 5) / 10) * width;
            const pixelY = height - ((y + 5) / 10) * height;
            
            point.style.left = `${pixelX}px`;
            point.style.top = `${pixelY}px`;
            point.style.transform = 'translate(-50%, -50%) scale(0)';
            point.style.opacity = '0';
            point.style.transition = 'all 0.3s ease';
            
            // Tooltip
            const tooltip = document.createElement('div');
            tooltip.className = 'point-tooltip';
            tooltip.textContent = `${gameState[`team${team}`].name}: (${x}, ${y.toFixed(2)})`;
            tooltip.style.bottom = '120%';
            tooltip.style.left = '50%';
            tooltip.style.transform = 'translateX(-50%)';
            point.appendChild(tooltip);
            
            return point;
        }

        function clearTeamPoints(team) {
            const canvas = document.getElementByI
