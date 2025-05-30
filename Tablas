<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Topos FC - Dashboard Mejorado v4</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <style>
        /* ESTILOS CSS (Mismos que la v3) */
        :root {
            --primary-color: #4A55A2; --primary-light: #6A75C2; --primary-dark: #3A4582;
            --secondary-color: #A0E9FF; --text-color: #333333; --text-light: #555555;
            --bg-color: #F4F7FC; --card-bg: #FFFFFF; --border-color: #E0E0E0;
            --sidebar-text: #E0E7FF; --sidebar-text-hover: #FFFFFF;
            --shadow-light: rgba(0, 0, 0, 0.05); --shadow-medium: rgba(0, 0, 0, 0.1);
            --danger-color: #dc3545;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        html { scroll-behavior: smooth; }
        body {
            font-family: 'Poppins', sans-serif; background-color: var(--bg-color); color: var(--text-color);
            line-height: 1.6; display: flex; min-height: 100vh;
        }
        .dashboard-container { display: flex; width: 100%; }
        .sidebar {
            width: 260px; background: linear-gradient(180deg, var(--primary-color) 0%, var(--primary-dark) 100%);
            color: var(--sidebar-text); padding: 25px 0; display: flex; flex-direction: column;
            flex-shrink: 0; box-shadow: 2px 0 10px var(--shadow-medium);
        }
        .sidebar-header { padding: 0 25px 25px 25px; text-align: center; border-bottom: 1px solid var(--primary-light); }
        .sidebar-header h1 { margin: 0; font-size: 2em; font-weight: 700; color: #FFFFFF; letter-spacing: 1px; }
        .sidebar-nav ul { list-style: none; margin-top: 20px; }
        .sidebar-nav li a {
            display: flex; align-items: center; padding: 15px 25px; text-decoration: none;
            color: var(--sidebar-text); font-size: 1.05em; font-weight: 500;
            transition: background-color 0.3s ease, color 0.3s ease, transform 0.2s ease;
            margin: 8px 15px; border-radius: 8px;
        }
        .sidebar-nav li a i { margin-right: 15px; width: 22px; text-align: center; font-size: 1.2em; }
        .sidebar-nav li a:hover, .sidebar-nav li a:focus {
            background-color: var(--primary-light); color: var(--sidebar-text-hover); transform: translateX(5px);
        }
        .main-content { flex-grow: 1; padding: 30px; overflow-y: auto; }
        .main-header { margin-bottom: 30px; }
        .welcome-banner {
            background-color: var(--secondary-color); color: var(--primary-dark); padding: 20px 25px;
            border-radius: 12px; font-size: 1em; font-weight: 500; box-shadow: 0 4px 15px var(--shadow-light);
        }
        .welcome-banner i { margin-right: 10px; }
        .content-section { padding-top: 70px; margin-top: -70px; margin-bottom: 40px; }
        .content-section h2 {
            color: var(--primary-dark); font-size: 2.2em; font-weight: 600; margin-bottom: 25px;
            border-bottom: 3px solid var(--primary-light); padding-bottom: 10px; display: inline-block;
        }
        .card {
            background-color: var(--card-bg); padding: 25px; border-radius: 12px;
            box-shadow: 0 5px 20px var(--shadow-light); margin-bottom: 30px;
        }
        .card h3 { color: var(--primary-color); font-size: 1.5em; margin-top: 0; margin-bottom: 20px; font-weight: 600; }
        .card h4 { color: var(--primary-dark); font-size: 1.2em; margin-top: 20px; margin-bottom: 10px; font-weight: 500; border-bottom: 1px solid var(--border-color); padding-bottom:5px;}
        .card p.form-description, .card p.info-text { font-size: 0.9em; color: var(--text-light); margin-bottom: 15px; font-style: italic;}

        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { text-align: left; padding: 12px 15px; border-bottom: 1px solid var(--border-color); vertical-align: middle; font-size:0.9em;} /* Reducido para más info */
        thead tr { background-color: var(--primary-light); color: #FFFFFF; font-weight: 600; font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px; }
        thead th:first-child { border-top-left-radius: 8px; }
        thead th:last-child { border-top-right-radius: 8px; }
        tbody tr:nth-child(even) { background-color: #F9FAFF; }
        tbody tr:hover { background-color: #E9EDFF; }
        .actions-cell button {
            background: none; border: none; color: var(--primary-color); cursor: pointer; margin: 0 5px; font-size: 1em; padding: 5px; /* Reducido */
        }
        .actions-cell button.delete-btn { color: var(--danger-color); }
        .actions-cell button:hover { opacity: 0.7; }

        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; margin-bottom: 5px; font-weight: 500; color: var(--text-light); font-size: 0.9em;}
        .form-group input[type="text"], .form-group input[type="date"], .form-group input[type="number"], .form-group select, .form-group textarea {
            width: 100%; padding: 10px 12px; border: 1px solid var(--border-color);
            border-radius: 8px; font-size: 0.95em; font-family: 'Poppins', sans-serif;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            border-color: var(--primary-color); box-shadow: 0 0 0 3px rgba(74, 85, 162, 0.2); outline: none;
        }
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; }
        .dynamic-input-row { display: flex; gap: 10px; align-items: center; margin-bottom: 10px; }
        .dynamic-input-row select { flex-grow: 1; }
        .dynamic-input-row input[type="number"] { width: 70px; flex-grow: 0; }
        .dynamic-input-row .remove-row-btn { background: var(--danger-color); color:white; border:none; padding: 5px 8px; border-radius:50%; cursor:pointer; font-size:0.8em; line-height:1;}


        .btn {
            background-color: var(--primary-color); color: white; padding: 10px 20px; border: none;
            border-radius: 8px; cursor: pointer; font-size: 0.95em; font-weight: 500;
            transition: background-color 0.3s ease, transform 0.2s ease;
            display: inline-flex; align-items: center; justify-content: center; margin-top: 10px;
        }
        .btn i { margin-right: 8px; }
        .btn:hover { background-color: var(--primary-dark); transform: translateY(-2px); }
        .btn-danger { background-color: var(--danger-color); }
        .btn-danger:hover { background-color: #c82333; }
        .btn-secondary { background-color: #6c757d; }
        .btn-secondary:hover { background-color: #5a6268; }
        .form-actions { margin-top: 20px; }

        p.no-data-message { text-align:center; color: var(--text-light); margin-top: 20px; padding: 10px; background-color: #f8f9fa; border-radius: 8px;}

        @media (max-width: 768px) {
            /* ... (mismos estilos responsivos que antes) ... */
             .sidebar { width: 100%; height: auto; padding: 15px 0; }
            .sidebar-nav ul { display: flex; flex-wrap: wrap; justify-content: center; margin-top: 10px; }
            .main-content { padding: 20px; }
            .content-section h2 { font-size: 1.8em; }
            .card { padding: 20px; }
            th, td { padding: 10px; font-size: 0.80em; } /* Reducido aún más para móviles */
            .table-responsive { display: block; width: 100%; overflow-x: auto; }
            .table-responsive table { min-width: 500px; }
            .form-grid { grid-template-columns: 1fr; }
            .dynamic-input-row { flex-direction: column; align-items: stretch;}
            .dynamic-input-row input[type="number"] { width: 100%; }
        }
    </style>
</head>
<body>
    <div class="dashboard-container">
        <aside class="sidebar">
            <div class="sidebar-header"><h1>Topos FC</h1></div>
            <nav class="sidebar-nav">
                 <ul>
                    <li><a href="#dashboard"><i class="fas fa-tachometer-alt"></i> Dashboard</a></li>
                    <li><a href="#jugadores"><i class="fas fa-users"></i> Jugadores</a></li>
                    <li><a href="#partidos"><i class="fas fa-calendar-alt"></i> Partidos</a></li>
                    <li><a href="#goleadores"><i class="fas fa-futbol"></i> Goleadores</a></li>
                    <li><a href="#asistentes"><i class="fas fa-hands-helping"></i> Asistentes</a></li>
                    <li><a href="#tarjetas"><i class="fas fa-id-card"></i> Tarjetas</a></li>
                    <li><a href="#sanciones"><i class="fas fa-gavel"></i> Sanciones</a></li>
                </ul>
            </nav>
        </aside>

        <main class="main-content">
            <header class="main-header">
                <div class="welcome-banner">
                    <i class="fas fa-cogs"></i> ¡Bienvenido! Formularios mejorados con selectores de jugadores.
                </div>
            </header>

            <!-- SECCIÓN DASHBOARD PRINCIPAL (Calculada) -->
            <section id="dashboard" class="content-section">
                <h2><i class="fas fa-chart-line"></i> Dashboard Principal</h2>
                <div class="card">
                    <h3>Estadísticas Globales de Jugadores (Calculadas)</h3>
                    <p class="info-text">Estas estadísticas se calculan automáticamente a partir de los datos de Jugadores y Partidos.</p>
                    <div class="table-responsive">
                        <table id="tabla-stats-globales">
                            <thead><tr><th>Nombre</th><th>PJ</th><th>Goles</th><th>Asist.</th><th>TA</th><th>TR</th><th>Autog.</th></tr></thead>
                            <tbody id="tbody-stats-globales"></tbody>
                        </table>
                    </div>
                    <p id="no-stats-globales-mensaje" class="no-data-message">No hay datos para mostrar. Agrega jugadores y partidos.</p>
                </div>
            </section>

            <!-- SECCIÓN JUGADORES (Editable Manualmente) -->
            <section id="jugadores" class="content-section">
                <h2><i class="fas fa-user-plus"></i> Gestión de Jugadores</h2>
                <div class="card">
                    <h3>Agregar / Editar Jugador</h3>
                    <form id="form-jugador">
                        <input type="hidden" id="jugador-id">
                        <div class="form-grid">
                            <div class="form-group"><label for="nombre-jugador">Nombre del Jugador:</label><input type="text" id="nombre-jugador" required></div>
                            <div class="form-group"><label for="posicion-jugador">Posición:</label><input type="text" id="posicion-jugador"></div>
                            <div class="form-group">
                                <label for="estado-jugador">Estado:</label>
                                <select id="estado-jugador">
                                    <option value="Activo">Activo</option><option value="Lesionado">Lesionado</option>
                                    <option value="Sancionado">Sancionado</option><option value="Inactivo">Inactivo</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-actions">
                            <button type="submit" class="btn" id="btn-guardar-jugador"><i class="fas fa-save"></i> Guardar Jugador</button>
                            <button type="button" class="btn btn-danger" id="btn-cancelar-edicion-jugador" style="display:none;"><i class="fas fa-times"></i> Cancelar</button>
                        </div>
                    </form>
                </div>
                <div class="card">
                    <h3>Lista de Jugadores</h3>
                    <div class="table-responsive">
                        <table id="tabla-jugadores">
                            <thead><tr><th>Nombre</th><th>Posición</th><th>Estado</th><th>Acciones</th></tr></thead>
                            <tbody id="tbody-jugadores"></tbody>
                        </table>
                    </div>
                     <p id="no-jugadores-mensaje" class="no-data-message">No hay jugadores registrados.</p>
                </div>
            </section>

            <!-- SECCIÓN PARTIDOS (Con Selectores Dinámicos) -->
            <section id="partidos" class="content-section">
                <h2><i class="fas fa-calendar-check"></i> Gestión de Partidos</h2>
                <div class="card">
                    <h3>Agregar / Editar Partido</h3>
                    <form id="form-partido">
                        <input type="hidden" id="partido-id">
                        <div class="form-grid">
                            <div class="form-group"><label for="partido-fecha">Fecha:</label><input type="date" id="partido-fecha" required></div>
                            <div class="form-group"><label for="partido-rival">Rival:</label><input type="text" id="partido-rival" required></div>
                            <div class="form-group"><label for="partido-res-local">Res. Topos:</label><input type="number" id="partido-res-local" min="0" value="0"></div>
                            <div class="form-group"><label for="partido-res-visitante">Res. Rival:</label><input type="number" id="partido-res-visitante" min="0" value="0"></div>
                        </div>
                        
                        <h4>Goles</h4>
                        <div id="partido-goleadores-container">
                            <!-- Filas de goleadores se añadirán aquí -->
                        </div>
                        <button type="button" class="btn btn-secondary btn-sm" id="btn-add-goleador"><i class="fas fa-plus"></i> Añadir Goleador</button>

                        <h4>Asistencias</h4>
                        <div id="partido-asistencias-container">
                            <!-- Filas de asistencias se añadirán aquí -->
                        </div>
                        <button type="button" class="btn btn-secondary btn-sm" id="btn-add-asistencia"><i class="fas fa-plus"></i> Añadir Asistencia</button>

                        <h4>Tarjetas</h4>
                        <div id="partido-tarjetas-container">
                            <!-- Filas de tarjetas se añadirán aquí -->
                        </div>
                        <button type="button" class="btn btn-secondary btn-sm" id="btn-add-tarjeta"><i class="fas fa-plus"></i> Añadir Tarjeta</button>

                        <h4>Autogoles (del rival, o propios)</h4>
                        <div id="partido-autogoles-container">
                             <!-- Filas de autogoles se añadirán aquí -->
                        </div>
                        <button type="button" class="btn btn-secondary btn-sm" id="btn-add-autogol"><i class="fas fa-plus"></i> Añadir Autogol</button>
                        
                        <div class="form-actions">
                            <button type="submit" class="btn" id="btn-guardar-partido"><i class="fas fa-save"></i> Guardar Partido</button>
                            <button type="button" class="btn btn-danger" id="btn-cancelar-partido" style="display:none;"><i class="fas fa-times"></i> Cancelar</button>
                        </div>
                    </form>
                </div>
                <div class="card">
                    <h3>Historial de Partidos</h3>
                    <div class="table-responsive">
                        <table id="tabla-partidos">
                            <thead><tr><th>Fecha</th><th>Rival</th><th>Resultado</th><th>Goleadores</th><th>Asistencias</th><th>Tarjetas</th><th>Autogoles</th><th>Acciones</th></tr></thead>
                            <tbody id="tbody-partidos"></tbody>
                        </table>
                    </div>
                    <p id="no-partidos-mensaje" class="no-data-message">No hay partidos registrados.</p>
                </div>
            </section>

            <!-- SECCIÓN GOLEADORES (Calculada) -->
             <section id="goleadores" class="content-section">
                <h2><i class="fas fa-futbol"></i> Tabla de Goleadores (Calculada)</h2>
                <div class="card">
                     <p class="info-text">Actualizada desde la sección Partidos.</p>
                    <div class="table-responsive">
                        <table id="tabla-goleadores">
                            <thead><tr><th>#</th><th>Nombre Jugador</th><th>Goles</th></tr></thead>
                            <tbody id="tbody-goleadores"></tbody>
                        </table>
                    </div>
                    <p id="no-goleadores-mensaje" class="no-data-message">No hay goleadores para mostrar.</p>
                </div>
            </section>

            <!-- SECCIÓN ASISTENTES (Calculada) -->
            <section id="asistentes" class="content-section">
                <h2><i class="fas fa-hands-helping"></i> Tabla de Asistentes (Calculada)</h2>
                 <div class="card">
                    <p class="info-text">Actualizada desde la sección Partidos.</p>
                    <div class="table-responsive">
                        <table id="tabla-asistentes">
                            <thead><tr><th>#</th><th>Nombre Jugador</th><th>Asistencias</th></tr></thead>
                            <tbody id="tbody-asistentes"></tbody>
                        </table>
                    </div>
                    <p id="no-asistentes-mensaje" class="no-data-message">No hay asistentes para mostrar.</p>
                </div>
            </section>

            <!-- SECCIÓN TARJETAS (Calculada) -->
            <section id="tarjetas" class="content-section">
                <h2><i class="fas fa-id-card"></i> Registro de Tarjetas (Calculado)</h2>
                <div class="card">
                    <p class="info-text">Actualizada desde la sección Partidos.</p>
                    <div class="table-responsive">
                        <table id="tabla-tarjetas">
                            <thead><tr><th>Nombre Jugador</th><th>Amarillas (TA)</th><th>Rojas (TR)</th></tr></thead>
                            <tbody id="tbody-tarjetas"></tbody>
                        </table>
                    </div>
                    <p id="no-tarjetas-mensaje" class="no-data-message">No hay registros de tarjetas para mostrar.</p>
                </div>
            </section>

            <!-- SECCIÓN SANCIONES (Con Selector de Jugador) -->
            <section id="sanciones" class="content-section">
                <h2><i class="fas fa-user-times"></i> Control de Sanciones (Asistencia)</h2>
                <div class="card">
                    <h3>Agregar / Editar Sanción</h3>
                     <form id="form-sancion">
                        <input type="hidden" id="sancion-id">
                        <div class="form-grid">
                            <div class="form-group">
                                <label for="sancion-jugador-id">Nombre Jugador:</label>
                                <select id="sancion-jugador-id" required>
                                    <option value="">-- Selecciona Jugador --</option>
                                    <!-- Opciones de jugador se poblarán aquí -->
                                </select>
                            </div>
                            <div class="form-group"><label for="sancion-confirmados">Part. Confirmados:</label><input type="number" id="sancion-confirmados" min="0" value="0"></div>
                            <div class="form-group"><label for="sancion-asistidos">Part. Asistidos:</label><input type="number" id="sancion-asistidos" min="0" value="0"></div>
                            <div class="form-group"><label for="sancion-faltas">Faltas (Conf. y no asistió):</label><input type="number" id="sancion-faltas" min="0" value="0"></div>
                        </div>
                        <div class="form-actions">
                            <button type="submit" class="btn" id="btn-guardar-sancion"><i class="fas fa-save"></i> Guardar Sanción</button>
                            <button type="button" class="btn btn-danger" id="btn-cancelar-sancion" style="display:none;"><i class="fas fa-times"></i> Cancelar</button>
                        </div>
                    </form>
                </div>
                <div class="card">
                    <h3>Resumen de Sanciones</h3>
                    <div class="table-responsive">
                        <table id="tabla-sanciones">
                            <thead><tr><th>Jugador</th><th>P. Confirmados</th><th>P. Asistidos</th><th>Faltas</th><th>Acciones</th></tr></thead>
                            <tbody id="tbody-sanciones"></tbody>
                        </table>
                    </div>
                    <p id="no-sanciones-mensaje" class="no-data-message">No hay sanciones registradas.</p>
                </div>
            </section>
        </main>
    </div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    // --- NAVEGACIÓN BÁSICA ---
    const navLinks = document.querySelectorAll('.sidebar-nav a');
    navLinks.forEach(link => { link.addEventListener('click', () => {}); });
    if (!window.location.hash) { window.location.hash = "#dashboard"; }

    // --- FUNCIONES GENERALES DE FORMULARIO ---
    function resetForm(formElement, idInputElement, submitButtonElement, cancelButtonElement, defaultButtonText) {
        formElement.reset();
        if (idInputElement) idInputElement.value = '';
        submitButtonElement.innerHTML = `<i class="fas fa-save"></i> ${defaultButtonText}`;
        if (cancelButtonElement) cancelButtonElement.style.display = 'none';
        
        // Limpiar contenedores dinámicos del formulario de partidos si es ese formulario
        if (formElement.id === 'form-partido') {
            document.getElementById('partido-goleadores-container').innerHTML = '';
            document.getElementById('partido-asistencias-container').innerHTML = '';
            document.getElementById('partido-tarjetas-container').innerHTML = '';
            document.getElementById('partido-autogoles-container').innerHTML = '';
        }

        const firstInput = formElement.querySelector('input:not([type="hidden"]), select, textarea');
        if (firstInput) firstInput.focus();
    }
    
    function loadDataToForm(dataObject, formElement, idInputElement, submitButtonElement, cancelButtonElement, updateButtonText) {
        resetForm(formElement, idInputElement, submitButtonElement, cancelButtonElement, defaultButtonText); // Limpiar primero
        if (idInputElement) idInputElement.value = dataObject.id;

        for (const key in dataObject) {
            if (key === 'id') continue;

            if (formElement.elements[key]) {
                 formElement.elements[key].value = dataObject[key];
            } else if (formElement.elements[`partido-${key.replace('_', '-')}`]) { 
                formElement.elements[`partido-${key.replace('_', '-')}`].value = dataObject[key];
            } else if (formElement.elements[`jugador-${key.replace('_', '-')}`]) {
                 formElement.elements[`jugador-${key.replace('_', '-')}`].value = dataObject[key];
            } else if (formElement.elements[`sancion-${key.replace('_', '-')}`]) {
                 if(key === 'jugador_id' && formElement.elements['sancion-jugador-id']) { // Caso especial para el select de sanciones
                    formElement.elements['sancion-jugador-id'].value = dataObject[key];
                 } else {
                    formElement.elements[`sancion-${key.replace('_', '-')}`].value = dataObject[key];
                 }
            }
        }

        // Cargar datos dinámicos para el formulario de partidos
        if (formElement.id === 'form-partido') {
            dataObject.goles_detalle?.forEach(g => addDynamicRow('goleador', g.jugador_id, g.cantidad));
            dataObject.asistencias_detalle?.forEach(a => addDynamicRow('asistencia', a.jugador_id, a.cantidad));
            dataObject.tarjetas_detalle?.forEach(t => addDynamicRow('tarjeta', t.jugador_id, null, t.tipo));
            dataObject.autogoles_detalle?.forEach(ag => addDynamicRow('autogol', ag.jugador_id, ag.cantidad));
        }


        submitButtonElement.innerHTML = `<i class="fas fa-sync-alt"></i> ${updateButtonText}`;
        if (cancelButtonElement) cancelButtonElement.style.display = 'inline-block';
        const firstInput = formElement.querySelector('input:not([type="hidden"]), select, textarea');
        if (firstInput) firstInput.focus();
        window.scrollTo({ top: formElement.closest('.card').offsetTop - 20, behavior: 'smooth' });
    }

    // --- DATOS CRUDOS (LocalStorage) ---
    const STORAGE_KEY_JUGADORES = 'topos_fc_jugadores_v4'; 
    const STORAGE_KEY_PARTIDOS = 'topos_fc_partidos_v4';
    const STORAGE_KEY_SANCIONES = 'topos_fc_sanciones_v4'; 

    let jugadores = JSON.parse(localStorage.getItem(STORAGE_KEY_JUGADORES)) || [];
    let partidos = JSON.parse(localStorage.getItem(STORAGE_KEY_PARTIDOS)) || [];
    let sanciones = JSON.parse(localStorage.getItem(STORAGE_KEY_SANCIONES)) || [];

    function guardarJugadores() { localStorage.setItem(STORAGE_KEY_JUGADORES, JSON.stringify(jugadores)); }
    function guardarPartidos() { localStorage.setItem(STORAGE_KEY_PARTIDOS, JSON.stringify(partidos)); }
    function guardarSanciones() { localStorage.setItem(STORAGE_KEY_SANCIONES, JSON.stringify(sanciones)); }

    // --- FUNCIÓN PARA POBLAR SELECTORES DE JUGADORES ---
    function poblarSelectoresDeJugadores(selectElement) {
        if (!selectElement) return;
        const currentValue = selectElement.value; // Guardar valor actual si existe
        selectElement.innerHTML = '<option value="">-- Selecciona Jugador --</option>';
        jugadores.forEach(j => {
            const option = document.createElement('option');
            option.value = j.id; // Usar ID del jugador como valor
            option.textContent = j.nombre;
            selectElement.appendChild(option);
        });
        if (currentValue) selectElement.value = currentValue; // Restaurar valor si es posible
    }

    // --- SECCIÓN: JUGADORES ---
    const formJugador = document.getElementById('form-jugador');
    const jugadorIdInput = document.getElementById('jugador-id');
    const tbodyJugadores = document.getElementById('tbody-jugadores');
    const btnGuardarJugador = document.getElementById('btn-guardar-jugador');
    const btnCancelarEdicionJugador = document.getElementById('btn-cancelar-edicion-jugador');
    const noJugadoresMensaje = document.getElementById('no-jugadores-mensaje');

    function renderizarJugadores() {
        tbodyJugadores.innerHTML = '';
        noJugadoresMensaje.style.display = jugadores.length === 0 ? 'block' : 'none';
        jugadores.forEach((jugador) => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${jugador.nombre}</td><td>${jugador.posicion || '-'}</td><td>${jugador.estado}</td>
                <td class="actions-cell">
                    <button class="edit-btn" data-type="jugador" data-id="${jugador.id}" title="Editar"><i class="fas fa-edit"></i></button>
                    <button class="delete-btn" data-type="jugador" data-id="${jugador.id}" title="Eliminar"><i class="fas fa-trash-alt"></i></button>
                </td>`;
            tbodyJugadores.appendChild(tr);
        });
        addEventListenersToTableButtons();
        // Poblar todos los selectores de jugadores en la app
        document.querySelectorAll('select.selector-jugador, #sancion-jugador-id').forEach(poblarSelectoresDeJugadores);
        actualizarTodasLasTablasCalculadas(); 
    }
    formJugador.addEventListener('submit', (e) => {
        e.preventDefault();
        const data = {
            id: jugadorIdInput.value || Date.now().toString(),
            nombre: formJugador.elements['nombre-jugador'].value.trim(),
            posicion: formJugador.elements['posicion-jugador'].value.trim(),
            estado: formJugador.elements['estado-jugador'].value
        };
        if (!data.nombre) { alert('El nombre del jugador es obligatorio.'); return; }
        
        // Validar que el nombre del jugador no exista ya (excepto si se está editando el mismo jugador)
        const nombreExistente = jugadores.find(j => j.nombre.toLowerCase() === data.nombre.toLowerCase() && j.id !== data.id);
        if (nombreExistente) {
            alert('Ya existe un jugador con este nombre.');
            return;
        }

        const existingIndex = jugadores.findIndex(j => j.id === data.id);
        if (existingIndex > -1 && jugadorIdInput.value) {
            jugadores[existingIndex] = data;
        } else {
            jugadores.push(data);
        }
        guardarJugadores(); renderizarJugadores();
        resetForm(formJugador, jugadorIdInput, btnGuardarJugador, btnCancelarEdicionJugador, 'Guardar Jugador');
    });
    btnCancelarEdicionJugador.addEventListener('click', () => resetForm(formJugador, jugadorIdInput, btnGuardarJugador, btnCancelarEdicionJugador, 'Guardar Jugador'));

    // --- SECCIÓN: PARTIDOS (Con Selectores Dinámicos) ---
    const formPartido = document.getElementById('form-partido');
    const partidoIdInput = document.getElementById('partido-id');
    const tbodyPartidos = document.getElementById('tbody-partidos');
    const btnGuardarPartido = document.getElementById('btn-guardar-partido');
    const btnCancelarPartido = document.getElementById('btn-cancelar-partido');
    const noPartidosMensaje = document.getElementById('no-partidos-mensaje');

    // Funciones para añadir filas dinámicas al form de partido
    function addDynamicRow(type, jugadorId = '', cantidad = 1, tipoTarjeta = 'TA') {
        const containerId = `partido-${type}es-container`; // goleadores, asistencias, etc.
        const container = document.getElementById(containerId);
        if (!container) return;

        const div = document.createElement('div');
        div.className = 'dynamic-input-row';

        const selectJugador = document.createElement('select');
        selectJugador.className = 'selector-jugador'; // Clase para poblarlo
        selectJugador.name = `${type}_jugador_id[]`;
        poblarSelectoresDeJugadores(selectJugador); // Poblarlo inmediatamente
        selectJugador.value = jugadorId;

        let inputCantidad;
        if (type === 'goleador' || type === 'asistencia' || type === 'autogol') {
            inputCantidad = document.createElement('input');
            inputCantidad.type = 'number';
            inputCantidad.name = `${type}_cantidad[]`;
            inputCantidad.min = '1';
            inputCantidad.value = cantidad;
            inputCantidad.required = true;
        }
        
        let selectTipoTarjeta;
        if (type === 'tarjeta') {
            selectTipoTarjeta = document.createElement('select');
            selectTipoTarjeta.name = 'tarjeta_tipo[]';
            selectTipoTarjeta.innerHTML = `
                <option value="TA" ${tipoTarjeta === 'TA' ? 'selected' : ''}>Amarilla (TA)</option>
                <option value="TR" ${tipoTarjeta === 'TR' ? 'selected' : ''}>Roja (TR)</option>
            `;
        }

        const removeBtn = document.createElement('button');
        removeBtn.type = 'button';
        removeBtn.className = 'remove-row-btn';
        removeBtn.innerHTML = '&times;';
        removeBtn.onclick = () => div.remove();

        div.appendChild(selectJugador);
        if (inputCantidad) div.appendChild(inputCantidad);
        if (selectTipoTarjeta) div.appendChild(selectTipoTarjeta);
        div.appendChild(removeBtn);
        container.appendChild(div);
    }

    document.getElementById('btn-add-goleador').addEventListener('click', () => addDynamicRow('goleador'));
    document.getElementById('btn-add-asistencia').addEventListener('click', () => addDynamicRow('asistencia'));
    document.getElementById('btn-add-tarjeta').addEventListener('click', () => addDynamicRow('tarjeta'));
    document.getElementById('btn-add-autogol').addEventListener('click', () => addDynamicRow('autogol'));


    function renderizarPartidos() {
        tbodyPartidos.innerHTML = '';
        noPartidosMensaje.style.display = partidos.length === 0 ? 'block' : 'none';
        partidos.forEach((partido) => {
            const tr = document.createElement('tr');
            const resultado = `${partido.res_local} - ${partido.res_visitante}`;
            
            // Formatear los detalles para visualización en la tabla
            const formatDetalle = (detalleArray, tipo) => {
                if (!detalleArray || detalleArray.length === 0) return '-';
                return detalleArray.map(item => {
                    const jugador = jugadores.find(j => j.id === item.jugador_id);
                    const nombreJugador = jugador ? jugador.nombre : 'Desconocido';
                    if (tipo === 'tarjeta') return `${nombreJugador}(${item.tipo})`;
                    return `${nombreJugador}${item.cantidad > 1 ? `(${item.cantidad})` : ''}`;
                }).join(', ');
            };

            tr.innerHTML = `
                <td>${partido.fecha}</td><td>${partido.rival}</td><td>${resultado}</td>
                <td>${formatDetalle(partido.goles_detalle, 'gol')}</td>
                <td>${formatDetalle(partido.asistencias_detalle, 'asistencia')}</td>
                <td>${formatDetalle(partido.tarjetas_detalle, 'tarjeta')}</td>
                <td>${formatDetalle(partido.autogoles_detalle, 'autogol')}</td>
                <td class="actions-cell">
                    <button class="edit-btn" data-type="partido" data-id="${partido.id}" title="Editar"><i class="fas fa-edit"></i></button>
                    <button class="delete-btn" data-type="partido" data-id="${partido.id}" title="Eliminar"><i class="fas fa-trash-alt"></i></button>
                </td>`;
            tbodyPartidos.appendChild(tr);
        });
        addEventListenersToTableButtons();
        actualizarTodasLasTablasCalculadas(); 
    }
    formPartido.addEventListener('submit', (e) => {
        e.preventDefault();
        
        const goles_detalle = Array.from(document.querySelectorAll('#partido-goleadores-container .dynamic-input-row')).map(row => ({
            jugador_id: row.querySelector('select[name="goleador_jugador_id[]"]').value,
            cantidad: parseInt(row.querySelector('input[name="goleador_cantidad[]"]').value) || 0
        })).filter(g => g.jugador_id && g.cantidad > 0);

        const asistencias_detalle = Array.from(document.querySelectorAll('#partido-asistencias-container .dynamic-input-row')).map(row => ({
            jugador_id: row.querySelector('select[name="asistencia_jugador_id[]"]').value,
            cantidad: parseInt(row.querySelector('input[name="asistencia_cantidad[]"]').value) || 0
        })).filter(a => a.jugador_id && a.cantidad > 0);
        
        const tarjetas_detalle = Array.from(document.querySelectorAll('#partido-tarjetas-container .dynamic-input-row')).map(row => ({
            jugador_id: row.querySelector('select[name="tarjeta_jugador_id[]"]').value,
            tipo: row.querySelector('select[name="tarjeta_tipo[]"]').value
        })).filter(t => t.jugador_id);

        const autogoles_detalle = Array.from(document.querySelectorAll('#partido-autogoles-container .dynamic-input-row')).map(row => ({
            jugador_id: row.querySelector('select[name="autogol_jugador_id[]"]').value, // Podría ser "Rival" o un jugador propio
            cantidad: parseInt(row.querySelector('input[name="autogol_cantidad[]"]').value) || 0
        })).filter(ag => ag.jugador_id && ag.cantidad > 0);


        const data = {
            id: partidoIdInput.value || Date.now().toString(),
            fecha: formPartido.elements['partido-fecha'].value,
            rival: formPartido.elements['partido-rival'].value.trim(),
            res_local: parseInt(formPartido.elements['partido-res-local'].value) || 0,
            res_visitante: parseInt(formPartido.elements['partido-res-visitante'].value) || 0,
            goles_detalle,
            asistencias_detalle,
            tarjetas_detalle,
            autogoles_detalle
        };

        if (!data.fecha || !data.rival) { alert('Fecha y Rival son obligatorios.'); return; }
        const existingIndex = partidos.findIndex(p => p.id === data.id);
        if (existingIndex > -1 && partidoIdInput.value) partidos[existingIndex] = data;
        else partidos.push(data);
        
        guardarPartidos(); renderizarPartidos();
        resetForm(formPartido, partidoIdInput, btnGuardarPartido, btnCancelarPartido, 'Guardar Partido');
    });
    btnCancelarPartido.addEventListener('click', () => resetForm(formPartido, partidoIdInput, btnGuardarPartido, btnCancelarPartido, 'Guardar Partido'));


    // --- FUNCIONES DE CÁLCULO Y RENDERIZADO PARA TABLAS DEPENDIENTES (Adaptadas a la nueva estructura de partidos) ---
    
    // 1. ESTADÍSTICAS GLOBALES
    const tbodyStatsGlobales = document.getElementById('tbody-stats-globales');
    const noStatsGlobalesMensaje = document.getElementById('no-stats-globales-mensaje');
    function calcularYRenderizarStatsGlobales() {
        tbodyStatsGlobales.innerHTML = '';
        if (jugadores.length === 0) {
            noStatsGlobalesMensaje.style.display = 'block'; return;
        }
        noStatsGlobalesMensaje.style.display = 'none';

        const statsAgregadas = {};
        jugadores.forEach(j => {
            statsAgregadas[j.id] = { nombre: j.nombre, pj: 0, goles: 0, asist: 0, ta: 0, tr: 0, autog: 0 };
        });

        partidos.forEach(partido => {
            const participantesDelPartido = new Set();

            partido.goles_detalle?.forEach(g => {
                if (statsAgregadas[g.jugador_id]) {
                    statsAgregadas[g.jugador_id].goles += g.cantidad;
                    participantesDelPartido.add(g.jugador_id);
                }
            });
            partido.asistencias_detalle?.forEach(a => {
                if (statsAgregadas[a.jugador_id]) {
                    statsAgregadas[a.jugador_id].asist += a.cantidad;
                    participantesDelPartido.add(a.jugador_id);
                }
            });
            partido.tarjetas_detalle?.forEach(t => {
                if (statsAgregadas[t.jugador_id]) {
                    if (t.tipo === 'TA') statsAgregadas[t.jugador_id].ta++;
                    else if (t.tipo === 'TR') statsAgregadas[t.jugador_id].tr++;
                    participantesDelPartido.add(t.jugador_id);
                }
            });
             partido.autogoles_detalle?.forEach(ag => {
                // Solo contar autogoles si el jugador_id corresponde a un jugador del equipo
                if (statsAgregadas[ag.jugador_id]) {
                    statsAgregadas[ag.jugador_id].autog += ag.cantidad;
                    participantesDelPartido.add(ag.jugador_id);
                }
            });

            participantesDelPartido.forEach(jugadorId => {
                if (statsAgregadas[jugadorId]) statsAgregadas[jugadorId].pj++;
            });
        });

        const statsArray = Object.values(statsAgregadas).sort((a,b) => a.nombre.localeCompare(b.nombre));
        statsArray.forEach(stat => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${stat.nombre}</td><td>${stat.pj}</td><td>${stat.goles}</td><td>${stat.asist}</td>
                <td>${stat.ta}</td><td>${stat.tr}</td><td>${stat.autog}</td>`;
            tbodyStatsGlobales.appendChild(tr);
        });
        if(statsArray.length === 0 && jugadores.length > 0){ 
            jugadores.forEach(j => {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td>${j.nombre}</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>`;
                tbodyStatsGlobales.appendChild(tr);
            });
            noStatsGlobalesMensaje.style.display = 'none';
        } else if (statsArray.length === 0 && jugadores.length === 0) {
             noStatsGlobalesMensaje.style.display = 'block';
        }
    }

    // 2. GOLEADORES
    const tbodyGoleadores = document.getElementById('tbody-goleadores');
    const noGoleadoresMensaje = document.getElementById('no-goleadores-mensaje');
    function calcularYRenderizarGoleadores() {
        const todosLosGoles = {};
        partidos.forEach(partido => {
            partido.goles_detalle?.forEach(g => {
                const jugador = jugadores.find(j => j.id === g.jugador_id);
                if (jugador) {
                    todosLosGoles[jugador.nombre] = (todosLosGoles[jugador.nombre] || 0) + g.cantidad;
                }
            });
        });
        const listaGoleadores = Object.entries(todosLosGoles).map(([nombre, goles]) => ({ nombre, goles }));
        listaGoleadores.sort((a, b) => b.goles - a.goles || a.nombre.localeCompare(b.nombre));

        tbodyGoleadores.innerHTML = '';
        noGoleadoresMensaje.style.display = listaGoleadores.filter(g => g.goles > 0).length === 0 ? 'block' : 'none';
        let rank = 0;
        listaGoleadores.forEach(g => {
            if (g.goles > 0) {
                rank++;
                const tr = document.createElement('tr');
                tr.innerHTML = `<td>${rank}</td><td>${g.nombre}</td><td>${g.goles}</td>`;
                tbodyGoleadores.appendChild(tr);
            }
        });
    }

    // 3. ASISTENTES
    const tbodyAsistentes = document.getElementById('tbody-asistentes');
    const noAsistentesMensaje = document.getElementById('no-asistentes-mensaje');
    function calcularYRenderizarAsistentes() {
        const todasLasAsistencias = {};
        partidos.forEach(partido => {
            partido.asistencias_detalle?.forEach(a => {
                const jugador = jugadores.find(j => j.id === a.jugador_id);
                if (jugador) {
                    todasLasAsistencias[jugador.nombre] = (todasLasAsistencias[jugador.nombre] || 0) + a.cantidad;
                }
            });
        });
        const listaAsistentes = Object.entries(todasLasAsistencias).map(([nombre, asistencias]) => ({ nombre, asistencias }));
        listaAsistentes.sort((a, b) => b.asistencias - a.asistencias || a.nombre.localeCompare(b.nombre));

        tbodyAsistentes.innerHTML = '';
        noAsistentesMensaje.style.display = listaAsistentes.filter(a => a.asistencias > 0).length === 0 ? 'block' : 'none';
        let rank = 0;
        listaAsistentes.forEach(a => {
            if (a.asistencias > 0) {
                rank++;
                const tr = document.createElement('tr');
                tr.innerHTML = `<td>${rank}</td><td>${a.nombre}</td><td>${a.asistencias}</td>`;
                tbodyAsistentes.appendChild(tr);
            }
        });
    }
    
    // 4. TARJETAS
    const tbodyTarjetas = document.getElementById('tbody-tarjetas');
    const noTarjetasMensaje = document.getElementById('no-tarjetas-mensaje');
    function calcularYRenderizarTarjetas() {
        const todasLasTarjetas = {}; 
        partidos.forEach(partido => {
            partido.tarjetas_detalle?.forEach(t => {
                const jugador = jugadores.find(j => j.id === t.jugador_id);
                if (jugador) {
                    if (!todasLasTarjetas[jugador.nombre]) todasLasTarjetas[jugador.nombre] = { TA: 0, TR: 0 };
                    if (t.tipo === 'TA') todasLasTarjetas[jugador.nombre].TA++;
                    else if (t.tipo === 'TR') todasLasTarjetas[jugador.nombre].TR++;
                }
            });
        });
        const listaTarjetas = Object.entries(todasLasTarjetas)
                                .map(([nombre, counts]) => ({ nombre, TA: counts.TA, TR: counts.TR }))
                                .filter(t => t.TA > 0 || t.TR > 0); 
        
        tbodyTarjetas.innerHTML = '';
        noTarjetasMensaje.style.display = listaTarjetas.length === 0 ? 'block' : 'none';
        listaTarjetas.forEach(t => {
            const tr = document.createElement('tr');
            tr.innerHTML = `<td>${t.nombre}</td><td>${t.TA}</td><td>${t.TR}</td>`;
            tbodyTarjetas.appendChild(tr);
        });
    }

    // --- SECCIÓN: SANCIONES (Con Selector de Jugador) ---
    const formSancion = document.getElementById('form-sancion');
    const sancionIdInput = document.getElementById('sancion-id');
    const sancionJugadorIdSelect = document.getElementById('sancion-jugador-id');
    const tbodySanciones = document.getElementById('tbody-sanciones');
    const btnGuardarSancion = document.getElementById('btn-guardar-sancion');
    const btnCancelarSancion = document.getElementById('btn-cancelar-sancion');
    const noSancionesMensaje = document.getElementById('no-sanciones-mensaje');

    function renderizarSanciones() {
        tbodySanciones.innerHTML = '';
        noSancionesMensaje.style.display = sanciones.length === 0 ? 'block' : 'none';
        sanciones.forEach((sancion) => {
            const tr = document.createElement('tr');
            const jugador = jugadores.find(j => j.id === sancion.jugador_id);
            const nombreJugador = jugador ? jugador.nombre : 'Jugador Desconocido';
            tr.innerHTML = `
                <td>${nombreJugador}</td><td>${sancion.confirmados}</td>
                <td>${sancion.asistidos}</td><td>${sancion.faltas}</td>
                <td class="actions-cell">
                    <button class="edit-btn" data-type="sancion" data-id="${sancion.id}" title="Editar"><i class="fas fa-edit"></i></button>
                    <button class="delete-btn" data-type="sancion" data-id="${sancion.id}" title="Eliminar"><i class="fas fa-trash-alt"></i></button>
                </td>`;
            tbodySanciones.appendChild(tr);
        });
        addEventListenersToTableButtons();
    }
    formSancion.addEventListener('submit', (e) => {
        e.preventDefault();
        const data = {
            id: sancionIdInput.value || Date.now().toString(),
            jugador_id: sancionJugadorIdSelect.value, // Guardar el ID del jugador
            confirmados: parseInt(formSancion.elements['sancion-confirmados'].value) || 0,
            asistidos: parseInt(formSancion.elements['sancion-asistidos'].value) || 0,
            faltas: parseInt(formSancion.elements['sancion-faltas'].value) || 0,
        };
        if (!data.jugador_id) { alert('Debe seleccionar un jugador.'); return; }
        const existingIndex = sanciones.findIndex(s => s.id === data.id);
        if (existingIndex > -1 && sancionIdInput.value) sanciones[existingIndex] = data;
        else sanciones.push(data);
        guardarSanciones(); renderizarSanciones();
        resetForm(formSancion, sancionIdInput, btnGuardarSancion, btnCancelarSancion, 'Guardar Sanción');
    });
    btnCancelarSancion.addEventListener('click', () => resetForm(formSancion, sancionIdInput, btnGuardarSancion, btnCancelarSancion, 'Guardar Sanción'));


    // --- FUNCIÓN PARA ACTUALIZAR TODAS LAS TABLAS CALCULADAS ---
    function actualizarTodasLasTablasCalculadas() {
        calcularYRenderizarStatsGlobales();
        calcularYRenderizarGoleadores();
        calcularYRenderizarAsistentes();
        calcularYRenderizarTarjetas();
    }

    // --- MANEJADORES GENERALES PARA BOTONES EDITAR/ELIMINAR ---
    function handleEditAction(type, id) {
        let item, form, idInput, submitBtn, cancelBtn, updateText, dataArray;
        switch(type) {
            case 'jugador': dataArray = jugadores; item = dataArray.find(j => j.id === id); form = formJugador; idInput = jugadorIdInput;
                            submitBtn = btnGuardarJugador; cancelBtn = btnCancelarEdicionJugador; updateText = 'Actualizar Jugador'; break;
            case 'partido': dataArray = partidos; item = dataArray.find(p => p.id === id); form = formPartido; idInput = partidoIdInput;
                            submitBtn = btnGuardarPartido; cancelBtn = btnCancelarPartido; updateText = 'Actualizar Partido'; break;
            case 'sancion': dataArray = sanciones; item = dataArray.find(s => s.id === id); form = formSancion; idInput = sancionIdInput;
                            submitBtn = btnGuardarSancion; cancelBtn = btnCancelarSancion; updateText = 'Actualizar Sanción'; break;
            default: return;
        }
        if (item) loadDataToForm(item, form, idInput, submitBtn, cancelBtn, updateText);
    }

    function handleDeleteAction(type, id) {
        if (!confirm('¿Estás seguro de que quieres eliminar este registro?')) return;
        let dataArray, saveFn, renderFn, form, idInput, submitBtn, cancelBtn, resetText;
        let wasEditingThisItem = false;

        switch(type) {
            case 'jugador': 
                dataArray = jugadores; const jIdx = dataArray.findIndex(j=>j.id===id); 
                if(jIdx>-1) { wasEditingThisItem = (jugadorIdInput.value === id); dataArray.splice(jIdx,1); }
                saveFn = guardarJugadores; renderFn = renderizarJugadores;
                form = formJugador; idInput = jugadorIdInput; submitBtn = btnGuardarJugador; cancelBtn = btnCancelarEdicionJugador; resetText = 'Guardar Jugador';
                break;
            case 'partido': 
                dataArray = partidos; const pIdx = dataArray.findIndex(p=>p.id===id); 
                if(pIdx>-1) { wasEditingThisItem = (partidoIdInput.value === id); dataArray.splice(pIdx,1); }
                saveFn = guardarPartidos; renderFn = renderizarPartidos;
                form = formPartido; idInput = partidoIdInput; submitBtn = btnGuardarPartido; cancelBtn = btnCancelarPartido; resetText = 'Guardar Partido';
                break;
            case 'sancion': 
                dataArray = sanciones; const sIdx = dataArray.findIndex(s=>s.id===id); 
                if(sIdx>-1) { wasEditingThisItem = (sancionIdInput.value === id); dataArray.splice(sIdx,1); }
                saveFn = guardarSanciones; renderFn = renderizarSanciones;
                form = formSancion; idInput = sancionIdInput; submitBtn = btnGuardarSancion; cancelBtn = btnCancelarSancion; resetText = 'Guardar Sanción';
                break;
            default: return;
        }
        saveFn(); renderFn(); 
        if (wasEditingThisItem) {
             resetForm(form, idInput, submitBtn, cancelBtn, resetText);
        }
    }
    
    function addEventListenersToTableButtons() {
        document.querySelectorAll('.edit-btn').forEach(btn => {
            btn.removeEventListener('click', processEditClick); btn.addEventListener('click', processEditClick);
        });
        document.querySelectorAll('.delete-btn').forEach(btn => {
            btn.removeEventListener('click', processDeleteClick); btn.addEventListener('click', processDeleteClick);
        });
    }
    function processEditClick(event) { handleEditAction(event.currentTarget.dataset.type, event.currentTarget.dataset.id); }
    function processDeleteClick(event) { handleDeleteAction(event.currentTarget.dataset.type, event.currentTarget.dataset.id); }

    // --- RENDERIZADO INICIAL ---
    renderizarJugadores(); 
    renderizarPartidos();  
    renderizarSanciones(); 
});
</script>
</body>
</html>
