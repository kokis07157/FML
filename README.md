<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farmacia Moderna Lety</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .sync-status {
            background: #d4edda;
            border: 1px solid #c3e6cb;
            color: #155724;
            padding: 10px;
            text-align: center;
            font-size: 0.9em;
        }

        .sync-status.syncing {
            background: #fff3cd;
            border-color: #ffeaa7;
            color: #856404;
        }

        .role-selector {
            display: flex;
            justify-content: center;
            gap: 20px;
            padding: 30px;
            background: #f8f9fa;
        }

        .role-btn {
            padding: 15px 30px;
            border: 2px solid #4facfe;
            background: white;
            color: #4facfe;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            text-align: center;
        }

        .role-btn:hover, .role-btn.active {
            background: #4facfe;
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.3);
        }

        .content-section {
            padding: 30px;
            display: none;
        }

        .content-section.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e1e5e9;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #4facfe;
            box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
        }

        textarea {
            height: 100px;
            resize: vertical;
        }

        .btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            width: 100%;
            margin-bottom: 10px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.3);
        }

        .btn.secondary {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            color: #333;
        }

        .password-section {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .records-list {
            max-height: 400px;
            overflow-y: auto;
            border: 1px solid #e9ecef;
            border-radius: 10px;
            padding: 20px;
        }

        .record-item {
            background: #f8f9fa;
            border: 1px solid #e9ecef;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
        }

        .patient-name {
            font-size: 1.1em;
            font-weight: 600;
            color: #333;
            margin-bottom: 5px;
        }

        .record-date {
            color: #666;
            font-size: 0.9em;
            margin-bottom: 10px;
        }

        .export-section {
            background: #d1ecf1;
            border: 1px solid #b6d4da;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-number {
            font-size: 1.8em;
            font-weight: bold;
            color: #333;
        }

        .instructions {
            background: #e7f3ff;
            border: 1px solid #b8daff;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .success-message {
            background: #d4edda;
            border: 1px solid #c3e6cb;
            color: #155724;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            display: none;
        }

        .staff-password-section {
            background: #f8d7da;
            border: 1px solid #f5c6cb;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .turn-info {
            background: #e8f5e8;
            border: 2px solid #4facfe;
            padding: 20px;
            border-radius: 10px;
            margin: 15px 0;
            text-align: center;
        }

        .turn-number {
            font-size: 2em;
            font-weight: bold;
            color: #4facfe;
            margin: 10px 0;
        }

        .database-status {
            background: #e8f4fd;
            border: 1px solid #b8daff;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
        }

        @media (max-width: 768px) {
            .role-selector {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏥 Farmacia Moderna Lety</h1>
            <p>Sistema multi-rol sincronizado para registro y gestión de pacientes</p>
            <small>Turnos desde las 7:00 AM - 20 minutos por consulta</small>
        </div>

        <div class="sync-status" id="syncStatus">
            🔄 Sistema sincronizado - Próximo turno disponible: <span id="nextTurnNumber">1</span>
        </div>

        <div class="role-selector">
            <div class="role-btn" onclick="selectRole('patient')">
                👤 Soy Paciente
            </div>
            <div class="role-btn" onclick="selectRole('staff')">
                👨‍💼 Personal Médico
            </div>
            <div class="role-btn" onclick="selectRole('doctor')">
                👨‍⚕️ Doctor
            </div>
        </div>

        <!-- SECCIÓN PACIENTE -->
        <div id="patient-section" class="content-section">
            <h2>📝 Registro de Paciente</h2>
            <div class="instructions">
                <strong>Instrucciones:</strong> Complete el formulario con sus datos. Su información será registrada de forma segura y se le asignará un turno automáticamente.
                <br><strong>Horarios:</strong> Los turnos inician a las 7:00 AM y duran 20 minutos cada uno.
            </div>
            
            <div class="database-status">
                📊 <strong>Turnos asignados hoy:</strong> <span id="todayTurnsCount">0</span> | 
                <strong>Próximo turno:</strong> #<span id="patientNextTurn">1</span>
            </div>
            
            <form id="patientForm">
                <div class="form-group">
                    <label for="patientName">Nombre Completo *</label>
                    <input type="text" id="patientName" required placeholder="Ingrese su nombre completo">
                </div>

                <div class="form-group">
                    <label for="patientMotivo">Motivo de la Consulta *</label>
                    <textarea id="patientMotivo" required placeholder="Describa el motivo de su consulta..."></textarea>
                </div>

                <div class="form-group">
                    <label for="patientPriority">Urgencia</label>
                    <select id="patientPriority">
                        <option value="Normal">Normal</option>
                        <option value="Alta">Alta</option>
                        <option value="Urgente">Urgente</option>
                    </select>
                </div>

                <button type="submit" class="btn">✅ Registrar y Obtener Turno</button>
                <div class="success-message" id="patientSuccess">
                    <div id="turnInfo"></div>
                </div>
            </form>
        </div>

        <!-- SECCIÓN PERSONAL MÉDICO -->
        <div id="staff-section" class="content-section">
            <h2>👨‍💼 Registro por Personal Médico</h2>
            
            <div class="staff-password-section">
                <label for="staffPassword">Contraseña de Acceso Personal Médico:</label>
                <input type="password" id="staffPassword" placeholder="Ingrese la contraseña">
                <button class="btn" onclick="authenticateStaff()">🔓 Acceder</button>
            </div>

            <div id="staff-content" style="display: none;">
                <div class="instructions">
                    <strong>Personal autorizado:</strong> Registre pacientes durante las consultas o citas. Los turnos se asignan automáticamente iniciando a las 7:00 AM.
                </div>
                
                <div class="database-status">
                    📊 <strong>Turnos hoy:</strong> <span id="staffTodayCount">0</span> | 
                    <strong>Próximo turno:</strong> #<span id="staffNextTurn">1</span>
                </div>
                
                <form id="staffForm">
                    <div class="form-group">
                        <label for="staffPatientName">Nombre del Paciente *</label>
                        <input type="text" id="staffPatientName" required placeholder="Nombre completo del paciente">
                    </div>

                    <div class="form-group">
                        <label for="staffPhone">Teléfono (opcional)</label>
                        <input type="tel" id="staffPhone" placeholder="Número de contacto">
                    </div>

                    <div class="form-group">
                        <label for="staffMotivo">Motivo de la Consulta *</label>
                        <textarea id="staffMotivo" required placeholder="Motivo de la consulta..."></textarea>
                    </div>

                    <div class="form-group">
                        <label for="staffPriority">Prioridad</label>
                        <select id="staffPriority">
                            <option value="Normal">Normal</option>
                            <option value="Alta">Alta</option>
                            <option value="Urgente">Urgente</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="staffNotes">Notas del Personal</label>
                        <textarea id="staffNotes" placeholder="Observaciones adicionales..."></textarea>
                    </div>

                    <button type="submit" class="btn">💾 Registrar Paciente</button>
                    <button type="button" class="btn secondary" onclick="logoutStaff()">🚪 Cerrar Sesión</button>
                    <div class="success-message" id="staffSuccess">
                        <div id="staffTurnInfo"></div>
                    </div>
                </form>
            </div>
        </div>

        <!-- SECCIÓN DOCTOR -->
        <div id="doctor-section" class="content-section">
            <h2>👨‍⚕️ Panel del Doctor</h2>
            
            <div class="password-section">
                <label for="doctorPassword">Contraseña de Acceso:</label>
                <input type="password" id="doctorPassword" placeholder="Ingrese la contraseña">
                <button class="btn" onclick="authenticateDoctor()">🔓 Acceder</button>
            </div>

            <div id="doctor-content" style="display: none;">
                <div class="stats">
                    <div class="stat-card">
                        <div class="stat-number" id="totalRecords">0</div>
                        <div>Total Registros</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="todayRecords">0</div>
                        <div>Registros Hoy</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="urgentRecords">0</div>
                        <div>Urgentes</div>
                    </div>
                </div>

                <div class="database-status">
                    <strong>Estado del Sistema:</strong> Base de datos central activa | 
                    <strong>Último turno asignado:</strong> #<span id="lastTurnAssigned">0</span>
                </div>

                <div class="form-group">
                    <input type="text" id="searchPatients" placeholder="🔍 Buscar pacientes...">
                </div>

                <div class="records-list" id="patientRecords">
                    <div style="text-align: center; color: #666; padding: 20px;">
                        No hay registros para mostrar
                    </div>
                </div>

                <div class="export-section">
                    <h3>📊 Exportar Datos</h3>
                    <button class="btn secondary" onclick="exportToJSON()">📄 Exportar como JSON</button>
                    <button class="btn secondary" onclick="exportToCSV()">📋 Exportar como CSV</button>
                    <button class="btn secondary" onclick="resetDailyTurns()" style="background: #ffa502;">🔄 Resetear Turnos del Día</button>
                    <button class="btn secondary" onclick="clearAllData()" style="background: #ff4757;">🗑️ Limpiar Datos</button>
                    <button class="btn secondary" onclick="logoutDoctor()">🚪 Cerrar Sesión</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Sistema de base de datos centralizada simulada
        class CentralDatabase {
            constructor() {
                this.dbKey = 'farmacia_lety_central_db';
                this.counterKey = 'farmacia_lety_turn_counter';
                this.lastResetKey = 'farmacia_lety_last_reset';
                this.init();
            }

            init() {
                // Verificar si necesitamos resetear el contador diario
                this.checkDailyReset();
            }

            checkDailyReset() {
                const today = new Date().toDateString();
                const lastReset = this.getFromStorage(this.lastResetKey);
                
                if (lastReset !== today) {
                    // Nuevo día, resetear contador de turnos
                    this.setInStorage(this.counterKey, { 
                        dailyCounter: 0, 
                        date: today 
                    });
                    this.setInStorage(this.lastResetKey, today);
                }
            }

            getFromStorage(key) {
                try {
                    // Simulamos una base de datos central usando una clave única
                    return JSON.parse(window.name || '{}')[key];
                } catch {
                    return null;
                }
            }

            setInStorage(key, value) {
                try {
                    let storage = {};
                    try {
                        storage = JSON.parse(window.name || '{}');
                    } catch {}
                    storage[key] = value;
                    window.name = JSON.stringify(storage);
                    
                    // También guardamos en localStorage como respaldo
                    window.localStorage?.setItem(key, JSON.stringify(value));
                } catch (e) {
                    // Fallback a variables de memoria
                    if (!window.farmaciaStorage) window.farmaciaStorage = {};
                    window.farmaciaStorage[key] = value;
                }
            }

            getPatients() {
                let patients = this.getFromStorage(this.dbKey);
                if (!patients) {
                    // Intentar cargar desde localStorage
                    try {
                        patients = JSON.parse(window.localStorage?.getItem(this.dbKey) || '[]');
                    } catch {
                        patients = [];
                    }
                }
                return patients || [];
            }

            savePatients(patients) {
                this.setInStorage(this.dbKey, patients);
            }

            getNextTurnNumber() {
                const today = new Date().toDateString();
                let counter = this.getFromStorage(this.counterKey);
                
                if (!counter || counter.date !== today) {
                    counter = { dailyCounter: 0, date: today };
                }
                
                counter.dailyCounter++;
                this.setInStorage(this.counterKey, counter);
                
                return counter.dailyCounter;
            }

            getCurrentTurnCount() {
                const today = new Date().toDateString();
                const counter = this.getFromStorage(this.counterKey);
                
                if (!counter || counter.date !== today) {
                    return 0;
                }
                
                return counter.dailyCounter;
            }

            resetDailyCounter() {
                const today = new Date().toDateString();
                this.setInStorage(this.counterKey, { 
                    dailyCounter: 0, 
                    date: today 
                });
                this.setInStorage(this.lastResetKey, today);
            }
        }

        // Inicializar base de datos central
        const centralDB = new CentralDatabase();
        let patientDatabase = centralDB.getPatients();

        const DOCTOR_PASSWORD = "Consulta150";
        const STAFF_PASSWORD = "Son1970ia";
        const CONSULTATION_DURATION = 20;
        const START_HOUR = 7;
        const END_HOUR = 17;

        // Actualizar contadores en la interfaz
        function updateTurnCounters() {
            const currentCount = centralDB.getCurrentTurnCount();
            const nextTurn = currentCount + 1;
            
            // Actualizar todos los elementos que muestran el contador
            document.getElementById('nextTurnNumber').textContent = nextTurn;
            document.getElementById('todayTurnsCount').textContent = currentCount;
            document.getElementById('patientNextTurn').textContent = nextTurn;
            document.getElementById('staffTodayCount').textContent = currentCount;
            document.getElementById('staffNextTurn').textContent = nextTurn;
            document.getElementById('lastTurnAssigned').textContent = currentCount;
        }

        // Inicializar contadores
        updateTurnCounters();

        function calculateConsultationTime(turnNumber) {
            const minutesFromStart = (turnNumber - 1) * CONSULTATION_DURATION;
            const consultationHour = START_HOUR + Math.floor(minutesFromStart / 60);
            const consultationMinutes = minutesFromStart % 60;
            
            const consultationDate = new Date();
            consultationDate.setHours(consultationHour, consultationMinutes, 0, 0);
            
            if (consultationHour >= END_HOUR) {
                consultationDate.setDate(consultationDate.getDate() + 1);
                const newMinutesFromStart = (turnNumber - 1 - Math.floor((END_HOUR - START_HOUR) * 60 / CONSULTATION_DURATION)) * CONSULTATION_DURATION;
                consultationDate.setHours(START_HOUR + Math.floor(newMinutesFromStart / 60), newMinutesFromStart % 60, 0, 0);
            }
            
            return {
                time: consultationDate.toLocaleTimeString('es-MX', {
                    hour: '2-digit',
                    minute: '2-digit',
                    hour12: false
                }),
                date: consultationDate.toLocaleDateString('es-MX')
            };
        }

        function selectRole(role) {
            document.querySelectorAll('.role-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.content-section').forEach(section => section.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(role + '-section').classList.add('active');
            
            // Actualizar contadores cuando se selecciona un rol
            updateTurnCounters();
        }

        function authenticateStaff() {
            const password = document.getElementById('staffPassword').value;
            if (password === STAFF_PASSWORD) {
                document.getElementById('staff-content').style.display = 'block';
                document.querySelector('.staff-password-section').style.display = 'none';
                document.getElementById('staffPassword').value = '';
                updateTurnCounters();
            } else {
                alert('Contraseña incorrecta');
                document.getElementById('staffPassword').value = '';
            }
        }

        function logoutStaff() {
            if (confirm('¿Cerrar sesión?')) {
                document.getElementById('staff-content').style.display = 'none';
                document.querySelector('.staff-password-section').style.display = 'block';
                document.getElementById('staffForm').reset();
                hideSuccess('staffSuccess');
            }
        }

        document.getElementById('patientForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Mostrar estado de sincronización
            document.getElementById('syncStatus').className = 'sync-status syncing';
            document.getElementById('syncStatus').innerHTML = '🔄 Sincronizando con base de datos central...';
            
            setTimeout(() => {
                const turnNumber = centralDB.getNextTurnNumber();
                const consultationInfo = calculateConsultationTime(turnNumber);
                
                const patient = {
                    id: Date.now() + Math.random(), // ID único
                    turnNumber: turnNumber,
                    name: document.getElementById('patientName').value.trim(),
                    motivo: document.getElementById('patientMotivo').value.trim(),
                    priority: document.getElementById('patientPriority').value,
                    consultationTime: consultationInfo.time,
                    consultationDate: consultationInfo.date,
                    registeredBy: 'Paciente',
                    date: new Date().toISOString(),
                    displayDate: new Date().toLocaleDateString('es-MX', {
                        year: 'numeric',
                        month: 'long',
                        day: 'numeric',
                        hour: '2-digit',
                        minute: '2-digit'
                    })
                };

                patientDatabase.push(patient);
                centralDB.savePatients(patientDatabase);
                updateTurnCounters();
                this.reset();
                
                const turnInfo = document.getElementById('turnInfo');
                turnInfo.innerHTML = `
                    <div class="turn-info">
                        <h3>🎫 ¡Registro Exitoso!</h3>
                        <div class="turn-number">Turno #${turnNumber}</div>
                        <p><strong>📅 Fecha:</strong> ${consultationInfo.date}</p>
                        <p><strong>🕐 Hora de consulta:</strong> <span style="color: #4facfe; font-weight: bold; font-size: 1.2em;">${consultationInfo.time}</span></p>
                        <p><strong>⏱️ Duración:</strong> 20 minutos</p>
                        <p><em>Por favor llegue 10 minutos antes de su hora asignada.</em></p>
                    </div>
                `;
                showSuccess('patientSuccess');
                
                // Restaurar estado de sincronización
                document.getElementById('syncStatus').className = 'sync-status';
                document.getElementById('syncStatus').innerHTML = `🔄 Sistema sincronizado - Próximo turno disponible: <span id="nextTurnNumber">${centralDB.getCurrentTurnCount() + 1}</span>`;
            }, 1000);
        });

        document.getElementById('staffForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const turnNumber = centralDB.getNextTurnNumber();
            const consultationInfo = calculateConsultationTime(turnNumber);
            
            const patient = {
                id: Date.now() + Math.random(),
                turnNumber: turnNumber,
                name: document.getElementById('staffPatientName').value.trim(),
                phone: document.getElementById('staffPhone').value.trim(),
                motivo: document.getElementById('staffMotivo').value.trim(),
                priority: document.getElementById('staffPriority').value,
                consultationTime: consultationInfo.time,
                consultationDate: consultationInfo.date,
                notes: document.getElementById('staffNotes').value.trim(),
                registeredBy: 'Personal Médico',
                date: new Date().toISOString(),
                displayDate: new Date().toLocaleDateString('es-MX', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                })
            };

            patientDatabase.push(patient);
            centralDB.savePatients(patientDatabase);
            updateTurnCounters();
            this.reset();
            
            const staffTurnInfo = document.getElementById('staffTurnInfo');
            staffTurnInfo.innerHTML = `
                <div class="turn-info">
                    <strong>✅ Paciente registrado:</strong> ${patient.name}<br>
                    <strong>🎫 Turno #${turnNumber}</strong><br>
                    <strong>📅 Fecha:</strong> ${consultationInfo.date}<br>
                    <strong>🕐 Hora:</strong> <span style="color: #4facfe; font-weight: bold;">${consultationInfo.time}</span>
                </div>
            `;
            showSuccess('staffSuccess');
        });

        function authenticateDoctor() {
            const password = document.getElementById('doctorPassword').value;
            if (password === DOCTOR_PASSWORD) {
                document.getElementById('doctor-content').style.display = 'block';
                document.querySelector('.password-section').style.display = 'none';
                updateDoctorPanel();
                document.getElementById('doctorPassword').value = '';
            } else {
                alert('Contraseña incorrecta');
                document.getElementById('doctorPassword').value = '';
            }
        }

        function logoutDoctor() {
            if (confirm('¿Cerrar sesión?')) {
                document.getElementById('doctor-content').style.display = 'none';
                document.querySelector('.password-section').style.display = 'block';
                document.getElementById('searchPatients').value = '';
            }
        }

        function updateDoctorPanel() {
            // Recargar datos desde la base de datos central
            patientDatabase = centralDB.getPatients();
            updateStats();
            displayPatientRecords();
            updateTurnCounters();
            
            document.getElementById('searchPatients').addEventListener('input', function() {
                displayPatientRecords(this.value.toLowerCase());
            });
        }

        function updateStats() {
            const today = new Date().toDateString();
            const todayCount = patientDatabase.filter(p => 
                new Date(p.date).toDateString() === today
            ).length;
            const urgentCount = patientDatabase.filter(p => 
                p.priority === 'Urgente' || p.priority === 'Alta'
            ).length;

            document.getElementById('totalRecords').textContent = patientDatabase.length;
            document.getElementById('todayRecords').textContent = todayCount;
            document.getElementById('urgentRecords').textContent = urgentCount;
        }

        function displayPatientRecords(searchTerm = '') {
            const container = document.getElementById('patientRecords');
            let filtered = patientDatabase;

            if (searchTerm) {
                filtered = patientDatabase.filter(p =>
                    p.name.toLowerCase().includes(searchTerm) ||
                    p.motivo.toLowerCase().includes(searchTerm)
                );
            }

            if (filtered.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #666; padding
