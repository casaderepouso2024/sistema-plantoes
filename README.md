[SISTEMA_CORRIGIDO_FINAL.html](https://github.com/user-attachments/files/27167661/SISTEMA_CORRIGIDO_FINAL.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Controle de Plantões</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        :root {
            --primary: #2563eb;
            --success: #16a34a;
            --danger: #dc2626;
            --warning: #f59e0b;
            --info: #0ea5e9;
            --light: #f5f5f5;
            --border: #e5e7eb;
            --text: #1f2937;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background: #fafafa;
            color: var(--text);
            line-height: 1.6;
        }
        
        .container { max-width: 600px; margin: 0 auto; padding: 12px; }
        
        .header {
            background: var(--primary);
            color: white;
            padding: 16px;
            border-radius: 8px;
            margin-bottom: 16px;
            text-align: center;
        }
        
        .header h1 { font-size: 20px; margin-bottom: 4px; }
        .header p { font-size: 12px; opacity: 0.9; }
        
        .access-banner {
            background: #dbeafe;
            border: 1px solid #0284c7;
            border-radius: 6px;
            padding: 10px 12px;
            margin-bottom: 12px;
            font-size: 11px;
            color: #0c4a6e;
            text-align: center;
            font-weight: 500;
        }
        
        .nav {
            display: flex;
            gap: 4px;
            margin-bottom: 16px;
            background: white;
            padding: 4px;
            border-radius: 8px;
            overflow-x: auto;
            border: 1px solid var(--border);
        }
        
        .nav.hidden { display: none; }
        
        .nav button {
            flex: 1;
            padding: 8px 6px;
            border: none;
            background: transparent;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 500;
            color: #666;
            cursor: pointer;
            transition: all 0.2s;
            white-space: nowrap;
        }
        
        .nav button.active {
            background: var(--primary);
            color: white;
        }
        
        .nav button:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }
        
        .screen { display: none; }
        .screen.active { display: block; }
        
        .card {
            background: white;
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 12px;
        }
        
        .card h2 { font-size: 16px; font-weight: 600; margin-bottom: 12px; }
        
        .field { margin-bottom: 12px; }
        
        .field label {
            display: block;
            font-size: 12px;
            color: #666;
            margin-bottom: 4px;
            font-weight: 500;
        }
        
        .field input,
        .field select,
        .field textarea {
            width: 100%;
            padding: 8px 10px;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 13px;
            font-family: inherit;
        }
        
        .btn {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            font-family: inherit;
        }
        
        .btn-primary { background: var(--primary); color: white; }
        .btn-primary:hover { opacity: 0.9; }
        
        .btn-success { background: var(--success); color: white; }
        .btn-success:hover { opacity: 0.9; }
        
        .btn-danger { background: var(--danger); color: white; }
        .btn-danger:hover { opacity: 0.9; }
        
        .btn-warning { background: var(--warning); color: white; }
        .btn-warning:hover { opacity: 0.9; }
        
        .btn-sm {
            width: auto;
            padding: 6px 12px;
            font-size: 12px;
            margin: 4px;
        }
        
        .badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
        }
        
        .badge-warn { background: #fef3c7; color: #92400e; }
        .badge-ok { background: #dcfce7; color: #166534; }
        .badge-danger { background: #fee2e2; color: #991b1b; }
        
        .item {
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 12px;
            margin-bottom: 8px;
        }
        
        .item-head {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 6px;
        }
        
        .item-name { font-weight: 600; font-size: 13px; }
        .item-sub { font-size: 11px; color: #666; margin-bottom: 4px; }
        
        .row2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }
        
        .gate-wrapper {
            text-align: center;
            padding: 24px 16px;
        }
        
        .gate-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: #dbeafe;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 16px;
            font-size: 32px;
        }
        
        .gate-q { font-size: 16px; font-weight: 600; margin-bottom: 8px; }
        .gate-sub { font-size: 12px; color: #666; margin-bottom: 16px; }
        
        .gate-btns { display: flex; gap: 8px; }
        .gate-btns button { flex: 1; }
        
        .alert {
            background: #fef3c7;
            border: 1px solid #fcd34d;
            border-radius: 6px;
            padding: 12px;
            text-align: center;
            margin-bottom: 12px;
        }
        
        .alert-title { font-weight: 600; font-size: 13px; margin-bottom: 6px; }
        .alert-text { font-size: 12px; color: #78350f; }
        
        .success-message {
            background: #dcfce7;
            border: 2px solid #16a34a;
            border-radius: 8px;
            padding: 24px;
            text-align: center;
        }
        
        .success-icon {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: #16a34a;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 16px;
            font-size: 48px;
        }
        
        .success-title {
            font-size: 20px;
            font-weight: 600;
            color: #166534;
            margin-bottom: 8px;
        }
        
        .success-text {
            font-size: 14px;
            color: #166534;
        }
        
        .metrics {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 12px;
        }
        
        .metric {
            background: var(--light);
            border-radius: 6px;
            padding: 12px;
            text-align: center;
        }
        
        .metric-val { font-size: 20px; font-weight: 600; }
        .metric-lbl { font-size: 10px; color: #666; margin-top: 4px; }
        
        .cal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 16px;
        }
        
        .cal-header button {
            background: var(--primary);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
        }
        
        .cal-header h3 { font-size: 16px; font-weight: 600; }
        
        .cal-days {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 4px;
            margin-bottom: 16px;
        }
        
        .cal-day-name {
            text-align: center;
            font-size: 11px;
            font-weight: 600;
            color: #666;
            padding: 8px 0;
        }
        
        .cal-day {
            aspect-ratio: 1;
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 6px;
            font-size: 12px;
            cursor: pointer;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }
        
        .cal-day:hover { border-color: var(--primary); }
        .cal-day.other-month { opacity: 0.3; }
        
        .cal-day .dot {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            margin-top: 4px;
        }
        
        .cal-day.pending .dot { background: #dc2626; }
        .cal-day.approved .dot { background: #f59e0b; }
        .cal-day.paid .dot { background: #16a34a; }
        
        .filter-group {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-bottom: 12px;
        }
        
        .filter-btn {
            padding: 6px 10px;
            border: 1px solid var(--border);
            border-radius: 6px;
            background: white;
            cursor: pointer;
            font-size: 12px;
            transition: all 0.2s;
        }
        
        .filter-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        
        .payment-table {
            border-collapse: collapse;
            width: 100%;
            font-size: 12px;
            margin-top: 12px;
        }
        
        .payment-table th {
            background: var(--light);
            padding: 10px;
            text-align: left;
            font-weight: 600;
            border-bottom: 1px solid var(--border);
        }
        
        .payment-table td {
            padding: 10px;
            border-bottom: 1px solid var(--border);
        }
        
        .payment-table tr:hover { background: #fafafa; }

        .loading {
            text-align: center;
            padding: 20px;
            font-size: 12px;
            color: #666;
        }
        
        .qr-section {
            background: white;
            border: 2px solid var(--primary);
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            margin: 20px 0;
        }
        
        .qr-section h3 {
            font-size: 16px;
            margin-bottom: 12px;
            color: var(--primary);
        }
        
        .qr-code-display {
            background: var(--light);
            padding: 20px;
            border-radius: 8px;
            margin: 16px auto;
            max-width: 250px;
        }
        
        .qr-code-display canvas {
            display: block;
            margin: 0 auto;
        }
        
        .url-display {
            background: var(--light);
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 12px;
            font-size: 11px;
            word-break: break-all;
            margin-top: 12px;
            font-family: monospace;
        }
        
        .link-card {
            background: white;
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 12px;
        }
        
        .link-card h4 {
            font-size: 14px;
            margin-bottom: 8px;
            color: var(--primary);
        }
        
        .link-card p {
            font-size: 11px;
            color: #666;
            margin-bottom: 8px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏥 Plantões</h1>
            <p>Casa de Repouso</p>
        </div>
        
        <div id="access-banner" class="access-banner"></div>
        
        <div class="nav" id="nav-container">
            <button class="active" onclick="show('checkin')">Check-in</button>
            <button onclick="show('enfermeira')">Enfermeira</button>
            <button onclick="show('calendario')">Calendário</button>
            <button onclick="show('pagamentos')">Pagamentos</button>
            <button onclick="show('cadastros')">Cadastros</button>
        </div>
        
        <!-- CHECK-IN -->
        <div class="screen active" id="screen-checkin">
            <div class="card">
                <div id="ci-gate" class="gate-wrapper">
                    <div class="gate-icon">⏰</div>
                    <div class="gate-q">Você está nesse plantão agora?</div>
                    <div class="gate-sub">Confirme apenas se você está presente neste momento.</div>
                    <div class="gate-btns">
                        <button class="btn btn-success" onclick="ciGate(true)">Sim, estou</button>
                        <button class="btn btn-danger" onclick="ciGate(false)">Não</button>
                    </div>
                </div>
                
                <div id="ci-aviso" style="display:none;">
                    <div class="alert">
                        <div class="alert-title">⚠️ Check-in não permitido</div>
                        <div class="alert-text">O preenchimento só pode ser realizado no momento do plantão. Favor entrar em contato com o RH no próximo dia útil para regularização.</div>
                    </div>
                </div>
                
                <div id="ci-form" style="display:none;">
                    <div class="field">
                        <label>Funcionário</label>
                        <select id="ci-func"></select>
                    </div>
                    <div class="field">
                        <label>Tipo de plantão</label>
                        <select id="ci-tipo"></select>
                    </div>
                    <div class="field">
                        <label>Motivo</label>
                        <select id="ci-motivo"></select>
                    </div>
                    <div class="field">
                        <label>Autorizado por</label>
                        <select id="ci-autor"></select>
                    </div>
                    <button class="btn btn-primary" onclick="fazerCheckin()">Confirmar chegada</button>
                </div>
                
                <div id="ci-sucesso" style="display:none;">
                    <div class="success-message">
                        <div class="success-icon">✓</div>
                        <div class="success-title">Obrigado!</div>
                        <div class="success-text">Bom plantão! 🏥</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- ENFERMEIRA -->
        <div class="screen" id="screen-enfermeira">
            <div class="card">
                <div class="field" style="margin-bottom:0;">
                    <label>Aprovando como:</label>
                    <select id="enf-quem"></select>
                </div>
            </div>
            
            <div class="metrics">
                <div class="metric">
                    <div class="metric-val" style="color:var(--warning);" id="m-pend">0</div>
                    <div class="metric-lbl">Pendentes</div>
                </div>
                <div class="metric">
                    <div class="metric-val" style="color:var(--success);" id="m-aprov">0</div>
                    <div class="metric-lbl">Aprovados</div>
                </div>
                <div class="metric">
                    <div class="metric-val" style="color:var(--danger);" id="m-rej">0</div>
                    <div class="metric-lbl">Rejeitados</div>
                </div>
            </div>
            
            <div class="card">
                <h2>Aguardando aprovação</h2>
                <div id="lista-enf"></div>
            </div>
        </div>
        
        <!-- CALENDÁRIO -->
        <div class="screen" id="screen-calendario">
            <div class="card">
                <h2>📅 Calendário de Plantões</h2>
                
                <div class="cal-header">
                    <button onclick="mesAnterior()">‹</button>
                    <h3 id="cal-mes-ano"></h3>
                    <button onclick="mesProximo()">›</button>
                </div>
                
                <div style="font-size:11px;color:#666;margin-bottom:12px;display:flex;gap:12px;">
                    <span>🔴 Pendente</span>
                    <span>🟡 Aprovado</span>
                    <span>🟢 Pago</span>
                </div>
                
                <div class="cal-days" id="cal-grid"></div>
                
                <div id="cal-detalhes" style="display:none;">
                    <div style="background:var(--light);border-radius:8px;padding:12px;margin-top:12px;">
                        <h3 style="font-size:14px;margin-bottom:10px;" id="det-data"></h3>
                        <div id="det-items"></div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- PAGAMENTOS -->
        <div class="screen" id="screen-pagamentos">
            <div class="card">
                <h2>💰 Relatório de Pagamentos</h2>
                
                <div style="margin-bottom:12px;">
                    <label style="font-size:12px;color:#666;font-weight:500;margin-bottom:6px;display:block;">Filtros rápidos:</label>
                    <div class="filter-group">
                        <button class="filter-btn" onclick="filtroRapido(7)">Últimos 7 dias</button>
                        <button class="filter-btn" onclick="filtroRapido('semana')">Semana passada</button>
                        <button class="filter-btn" onclick="filtroRapido('mes')">Mês atual</button>
                        <button class="filter-btn" onclick="filtroRapido('mes-ant')">Mês passado</button>
                        <button class="filter-btn" onclick="filtroRapido('tudo')">Todo período</button>
                    </div>
                </div>
                
                <div class="row2">
                    <div class="field" style="margin-bottom:0;">
                        <label>De</label>
                        <input type="date" id="tab-de" onchange="renderTab()">
                    </div>
                    <div class="field" style="margin-bottom:0;">
                        <label>Até</label>
                        <input type="date" id="tab-ate" onchange="renderTab()">
                    </div>
                </div>
            </div>
            
            <div id="tab-lista"></div>
        </div>
        
        <!-- CADASTROS -->
        <div class="screen" id="screen-cadastros">
            <div class="card">
                <h2>⚙️ Cadastros do Google Sheets</h2>
                
                <button class="btn btn-warning" onclick="carregarDados()" style="margin-bottom:12px;">🔄 Recarregar dados</button>
                
                <div id="cad-status"></div>
                <div id="cad-content"></div>
            </div>
            
            <!-- QR CODE E LINKS -->
            <div id="qr-generator-section" style="display:none;">
                <div class="qr-section">
                    <h3>📱 QR Code para Funcionários</h3>
                    <p style="font-size:12px;color:#666;margin-bottom:16px;">Gere o QR Code para os funcionários registrarem plantões</p>
                    
                    <button class="btn btn-primary btn-lg" onclick="gerarQRCode()" style="font-size:16px;padding:14px;">
                        🎨 GERAR QR CODE
                    </button>
                    
                    <div id="qr-display" style="display:none;margin-top:20px;">
                        <div class="qr-code-display">
                            <div id="qrcode"></div>
                        </div>
                        
                        <button class="btn btn-success" onclick="baixarQRCode()">
                            ⬇️ Baixar QR Code (PNG)
                        </button>
                        
                        <div class="url-display" id="qr-url"></div>
                    </div>
                </div>
                
                <div class="link-card">
                    <h4>💉 Link para Enfermeira</h4>
                    <p>Compartilhe este link com a enfermeira responsável pela aprovação:</p>
                    <div class="url-display" id="url-enf"></div>
                    <button class="btn btn-sm btn-primary" onclick="copiarURL('enfermeira')">📋 Copiar Link</button>
                </div>
                
                <div class="link-card">
                    <h4>👨‍💼 Link para Gestor</h4>
                    <p>Seu link de acesso administrativo completo:</p>
                    <div class="url-display" id="url-gest"></div>
                    <button class="btn btn-sm btn-primary" onclick="copiarURL('gestor')">📋 Copiar Link</button>
                </div>
            </div>
        </div>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
    <script>
        var SHEET_ID = "1TVYsc9GnaK_T1YILkdgBOJSyDA4CZbEyvzk47Izr-go";
        var API_KEY = AIzaSyC2Vb-uj16w6NnlSk6sOAm6S1Uj5HpIh40
        var BASE_URL = window.location.origin + window.location.pathname;
        
        var urlParams = new URLSearchParams(window.location.search);
        var tipoAcesso = urlParams.get('tipo') || 'gestor';
        
        var db = {
            funcionarios: [],
            tipos: [],
            autorizadores: [],
            aprovadores: [],
            motivos: [],
            plantoes: JSON.parse(localStorage.getItem('plantoes')) || []
        };
        
        var hoje = new Date();
        var calMes = hoje.getMonth();
        var calAno = hoje.getFullYear();
        var qrCodeCanvas = null;
        
        async function carregarDados() {
            var statusEl = document.getElementById('cad-status');
            statusEl.innerHTML = '<div class="loading">🔄 Carregando dados do Google Sheets...</div>';
            
            try {
                var urlFunc = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/Funcionários?key=${API_KEY}`;
                var respFunc = await fetch(urlFunc);
                var dataFunc = await respFunc.json();
                
                if (dataFunc.error) throw new Error(dataFunc.error.message);
                
                db.funcionarios = [];
                if (dataFunc.values && dataFunc.values.length > 1) {
                    for (var i = 1; i < dataFunc.values.length; i++) {
                        if (dataFunc.values[i][0]) {
                            db.funcionarios.push({
                                nome: dataFunc.values[i][0],
                                cargo: dataFunc.values[i][1] || ''
                            });
                        }
                    }
                }
                
                var urlConf = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/Configurações?key=${API_KEY}`;
                var respConf = await fetch(urlConf);
                var dataConf = await respConf.json();
                
                db.tipos = [];
                if (dataConf.values && dataConf.values.length > 1) {
                    for (var i = 1; i < dataConf.values.length; i++) {
                        if (dataConf.values[i][0]) {
                            db.tipos.push({
                                nome: dataConf.values[i][0],
                                valor: parseFloat(dataConf.values[i][1]) || 0
                            });
                        }
                    }
                }
                
                var urlAut = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/Autorizadores?key=${API_KEY}`;
                var respAut = await fetch(urlAut);
                var dataAut = await respAut.json();
                
                db.autorizadores = [];
                if (dataAut.values && dataAut.values.length > 1) {
                    for (var i = 1; i < dataAut.values.length; i++) {
                        if (dataAut.values[i][0]) {
                            db.autorizadores.push({
                                nome: dataAut.values[i][0],
                                funcao: dataAut.values[i][1] || ''
                            });
                        }
                    }
                }
                
                var urlApr = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/Aprovadores?key=${API_KEY}`;
                var respApr = await fetch(urlApr);
                var dataApr = await respApr.json();
                
                db.aprovadores = [];
                if (dataApr.values && dataApr.values.length > 1) {
                    for (var i = 1; i < dataApr.values.length; i++) {
                        if (dataApr.values[i][0]) {
                            db.aprovadores.push({
                                nome: dataApr.values[i][0],
                                funcao: dataApr.values[i][1] || ''
                            });
                        }
                    }
                }
                
                var urlPlant = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/Plantões?key=${API_KEY}`;
                var respPlant = await fetch(urlPlant);
                var dataPlant = await respPlant.json();
                
                db.motivos = [];
                if (dataPlant.values && dataPlant.values.length > 1) {
                    for (var i = 1; i < dataPlant.values.length; i++) {
                        if (dataPlant.values[i][4] && dataPlant.values[i][4].trim()) {
                            var motivo = dataPlant.values[i][4].trim();
                            if (db.motivos.indexOf(motivo) === -1) {
                                db.motivos.push(motivo);
                            }
                        }
                    }
                }
                
                if (db.motivos.length === 0) {
                    db.motivos = ['Agitação noturna', 'Intercorrência médica', 'Reforço de equipe'];
                }
                
                statusEl.innerHTML = '<div style="background:#dcfce7;color:#166534;padding:10px;border-radius:6px;font-size:12px;">✅ Dados carregados com sucesso!</div>';
                
                populateSelects();
                renderCad();
                
            } catch (error) {
                statusEl.innerHTML = '<div style="background:#fee2e2;color:#991b1b;padding:10px;border-radius:6px;font-size:12px;">❌ Erro: ' + error.message + '</div>';
                
                db.funcionarios = [{nome: "Maria Silva", cargo: "Cuidadora"}];
                db.tipos = [{nome: "Dia (12h)", valor: 180}];
                db.autorizadores = [{nome: "Dr. Roberto", funcao: "Médico"}];
                db.aprovadores = [{nome: "Enf. Carla", funcao: "Enfermeira"}];
                db.motivos = ["Agitação noturna"];
                
                populateSelects();
                renderCad();
            }
        }
        
        window.addEventListener('DOMContentLoaded', function() {
            configurarAcesso();
            carregarDados();
            renderCal();
            if (tipoAcesso === 'gestor') {
                document.getElementById('qr-generator-section').style.display = 'block';
                mostrarURLs();
            }
        });
        
        function configurarAcesso() {
            var banner = document.getElementById('access-banner');
            var nav = document.getElementById('nav-container');
            var buttons = document.querySelectorAll('.nav button');
            
            if (tipoAcesso === 'funcionario') {
                banner.textContent = '👤 Acesso Funcionário — Check-in de Plantão';
                nav.classList.add('hidden');
            } else if (tipoAcesso === 'enfermeira') {
                banner.textContent = '💉 Acesso Enfermeira — Aprovação de Plantões';
                buttons[0].disabled = true;
                buttons[1].disabled = false;
                buttons[2].disabled = true;
                buttons[3].disabled = true;
                buttons[4].disabled = true;
                show('enfermeira');
            } else {
                banner.textContent = '👨‍💼 Acesso Gestor — Controle Total';
            }
        }
        
        function show(s) {
            if (tipoAcesso === 'funcionario' && s !== 'checkin') return;
            if (tipoAcesso === 'enfermeira' && s !== 'enfermeira') return;
            
            document.querySelectorAll('.screen').forEach(el => el.classList.remove('active'));
            document.querySelector('#screen-' + s).classList.add('active');
            document.querySelectorAll('.nav button').forEach(el => el.classList.remove('active'));
            
            var tabs = ['checkin', 'enfermeira', 'calendario', 'pagamentos', 'cadastros'];
            var idx = tabs.indexOf(s);
            if (idx >= 0) document.querySelectorAll('.nav button')[idx].classList.add('active');
            
            if (s === 'checkin') resetGate();
            if (s === 'enfermeira') renderEnf();
            if (s === 'calendario') renderCal();
            if (s === 'pagamentos') { initDates(); renderTab(); }
        }
        
        function resetGate() {
            document.getElementById('ci-gate').style.display = 'block';
            document.getElementById('ci-aviso').style.display = 'none';
            document.getElementById('ci-form').style.display = 'none';
            document.getElementById('ci-sucesso').style.display = 'none';
        }
        
        function ciGate(sim) {
            document.getElementById('ci-gate').style.display = 'none';
            if (sim) {
                document.getElementById('ci-form').style.display = 'block';
            } else {
                document.getElementById('ci-aviso').style.display = 'block';
            }
        }
        
        function populateSelects() {
            var fs = document.getElementById('ci-func');
            fs.innerHTML = '<option value="">Selecione...</option>';
            db.funcionarios.forEach(f => {
                var opt = document.createElement('option');
                opt.value = f.nome;
                opt.textContent = f.nome;
                fs.appendChild(opt);
            });
            
            var ts = document.getElementById('ci-tipo');
            ts.innerHTML = '<option value="">Selecione...</option>';
            db.tipos.forEach(t => {
                var opt = document.createElement('option');
                opt.value = t.nome;
                opt.textContent = t.nome + ' — R$' + t.valor;
                ts.appendChild(opt);
            });
            
            var ms = document.getElementById('ci-motivo');
            ms.innerHTML = '<option value="">Opcional...</option>';
            db.motivos.forEach(m => {
                var opt = document.createElement('option');
                opt.value = m;
                opt.textContent = m;
                ms.appendChild(opt);
            });
            
            var as = document.getElementById('ci-autor');
            as.innerHTML = '<option value="">Selecione...</option>';
            db.autorizadores.forEach(a => {
                var opt = document.createElement('option');
                opt.value = a.nome;
                opt.textContent = a.nome;
                as.appendChild(opt);
            });
            
            var es = document.getElementById('enf-quem');
            es.innerHTML = '<option value="">Selecione...</option>';
            db.aprovadores.forEach(a => {
                var opt = document.createElement('option');
                opt.value = a.nome;
                opt.textContent = a.nome;
                es.appendChild(opt);
            });
        }
        
        function fazerCheckin() {
            var func = document.getElementById('ci-func').value;
            var tipo = document.getElementById('ci-tipo').value;
            
            if (!func || !tipo) {
                alert('Por favor, preencha funcionário e tipo de plantão!');
                return;
            }
            
            var t = db.tipos.find(x => x.nome === tipo);
            var p = {
                id: Date.now(),
                func: func,
                tipo: tipo,
                motivo: document.getElementById('ci-motivo').value || null,
                data: hoje.toLocaleDateString('pt-BR'),
                dataObj: new Date(hoje.getFullYear(), hoje.getMonth(), hoje.getDate()),
                hora: hoje.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' }),
                valor: t ? t.valor : 0,
                status: 'pendente',
                autor: document.getElementById('ci-autor').value || null
            };
            
            db.plantoes.unshift(p);
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            
            document.getElementById('ci-form').style.display = 'none';
            document.getElementById('ci-sucesso').style.display = 'block';
        }
        
        function renderEnf() {
            var pend = db.plantoes.filter(p => p.status === 'pendente');
            var aprov = db.plantoes.filter(p => p.status === 'aprovado');
            var rej = db.plantoes.filter(p => p.status === 'rejeitado');
            
            document.getElementById('m-pend').textContent = pend.length;
            document.getElementById('m-aprov').textContent = aprov.length;
            document.getElementById('m-rej').textContent = rej.length;
            
            var el = document.getElementById('lista-enf');
            
            if (!pend.length) {
                el.innerHTML = '<p style="font-size:12px;color:#666;">Nenhum pendente.</p>';
                return;
            }
            
            el.innerHTML = pend.map(p => `
                <div class="item">
                    <div class="item-head">
                        <span class="item-name">${p.func}</span>
                        <span class="badge badge-warn">Pendente</span>
                    </div>
                    <div class="item-sub">${p.tipo} · ${p.data} · R$${p.valor}</div>
                    <div style="display:flex;gap:8px;margin-top:8px;">
                        <button class="btn btn-success btn-sm" style="flex:1;" onclick="aprovar(${p.id})">Aprovar</button>
                        <button class="btn btn-danger btn-sm" style="flex:1;" onclick="rejeitar(${p.id})">Rejeitar</button>
                    </div>
                </div>
            `).join('');
        }
        
        function aprovar(id) {
            db.plantoes = db.plantoes.map(p => 
                p.id === id ? {...p, status: 'aprovado'} : p
            );
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            renderEnf();
            renderCal();
        }
        
        function rejeitar(id) {
            db.plantoes = db.plantoes.map(p => 
                p.id === id ? {...p, status: 'rejeitado'} : p
            );
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            renderEnf();
            renderCal();
        }
        
        function renderCal() {
            var meses = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
            document.getElementById('cal-mes-ano').textContent = meses[calMes] + ' ' + calAno;
            
            var primeiro = new Date(calAno, calMes, 1).getDay();
            var diasMes = new Date(calAno, calMes + 1, 0).getDate();
            var diasMesAnt = new Date(calAno, calMes, 0).getDate();
            
            var dows = ['Dom', 'Seg', 'Ter', 'Qua', 'Qui', 'Sex', 'Sáb'];
            var html = dows.map(d => '<div class="cal-day-name">' + d + '</div>').join('');
            
            for (var i = primeiro - 1; i >= 0; i--) {
                html += '<div class="cal-day other-month">' + (diasMesAnt - i) + '</div>';
            }
            
            for (var d = 1; d <= diasMes; d++) {
                var plantoesDia = db.plantoes.filter(p => 
                    p.dataObj && p.dataObj.getFullYear() === calAno && 
                    p.dataObj.getMonth() === calMes && 
                    p.dataObj.getDate() === d
                );
                
                var statusClass = '';
                if (plantoesDia.some(p => p.status === 'pago')) statusClass = 'paid';
                else if (plantoesDia.some(p => p.status === 'aprovado')) statusClass = 'approved';
                else if (plantoesDia.some(p => p.status === 'pendente')) statusClass = 'pending';
                
                html += '<div class="cal-day ' + statusClass + '" onclick="selecionarDia(' + d + ')">' + d;
                if (plantoesDia.length > 0) html += '<div class="dot"></div>';
                html += '</div>';
            }
            
            for (var i = 1; i < (42 - primeiro - diasMes); i++) {
                html += '<div class="cal-day other-month">' + i + '</div>';
            }
            
            document.getElementById('cal-grid').innerHTML = html;
        }
        
        function mesAnterior() {
            calMes--;
            if (calMes < 0) { calMes = 11; calAno--; }
            renderCal();
        }
        
        function mesProximo() {
            calMes++;
            if (calMes > 11) { calMes = 0; calAno++; }
            renderCal();
        }
        
        function selecionarDia(d) {
            var plantoesDia = db.plantoes.filter(p => 
                p.dataObj && p.dataObj.getFullYear() === calAno && 
                p.dataObj.getMonth() === calMes && 
                p.dataObj.getDate() === d
            );
            
            var det = document.getElementById('cal-detalhes');
            if (!plantoesDia.length) {
                det.style.display = 'none';
                return;
            }
            
            det.style.display = 'block';
            var meses = ['jan', 'fev', 'mar', 'abr', 'mai', 'jun', 'jul', 'ago', 'set', 'out', 'nov', 'dez'];
            document.getElementById('det-data').textContent = d + ' de ' + meses[calMes] + ' · ' + plantoesDia.length + ' plantão(ões)';
            document.getElementById('det-items').innerHTML = plantoesDia.map(p => `
                <div class="item">
                    <div class="item-head">
                        <span class="item-name">${p.func}</span>
                        <span class="badge badge-${p.status === 'pendente' ? 'warn' : p.status === 'aprovado' ? 'ok' : 'danger'}">${p.status}</span>
                    </div>
                    <div class="item-sub">${p.tipo} · ${p.hora} · R$${p.valor}</div>
                </div>
            `).join('');
        }
        
        function initDates() {
            if (!document.getElementById('tab-de').value) {
                document.getElementById('tab-de').valueAsDate = new Date(hoje.getFullYear(), hoje.getMonth(), 1);
                document.getElementById('tab-ate').valueAsDate = hoje;
            }
        }
        
        function filtroRapido(tipo) {
            var de = new Date();
            var ate = new Date();
            
            if (tipo === 7) de.setDate(ate.getDate() - 7);
            else if (tipo === 'mes') de = new Date(ate.getFullYear(), ate.getMonth(), 1);
            else if (tipo === 'tudo') de = new Date(2000, 0, 1);
            
            document.getElementById('tab-de').valueAsDate = de;
            document.getElementById('tab-ate').valueAsDate = ate;
            renderTab();
        }
        
        function renderTab() {
            var el = document.getElementById('tab-lista');
            var filtrados = db.plantoes.filter(p => p.status === 'aprovado' || p.status === 'pago');
            
            if (!filtrados.length) {
                el.innerHTML = '<div class="card"><p style="font-size:12px;color:#666;">Nenhum plantão aprovado.</p></div>';
                return;
            }
            
            var html = '<div class="card">';
            html += '<table class="payment-table">';
            html += '<thead><tr><th>Data</th><th>Funcionário</th><th>Tipo</th><th>Valor</th><th style="text-align:center;">Pago?</th></tr></thead>';
            html += '<tbody>';
            
            filtrados.forEach(p => {
                var isPago = p.status === 'pago';
                var checkboxHtml = isPago 
                    ? '<input type="checkbox" checked disabled style="cursor:not-allowed;">' 
                    : '<input type="checkbox" onchange="marcarPago(' + p.id + ', this.checked)">';
                
                var rowStyle = isPago ? 'opacity:0.6;' : '';
                
                html += '<tr style="' + rowStyle + '">';
                html += '<td>' + p.data + '</td>';
                html += '<td>' + p.func + '</td>';
                html += '<td>' + p.tipo + '</td>';
                html += '<td><strong>R$' + p.valor + '</strong></td>';
                html += '<td style="text-align:center;">' + checkboxHtml + '</td>';
                html += '</tr>';
            });
            
            html += '</tbody></table>';
            
            var totalGeral = filtrados.reduce((s, p) => s + p.valor, 0);
            var totalPago = filtrados.filter(p => p.status === 'pago').reduce((s, p) => s + p.valor, 0);
            var totalAPagar = totalGeral - totalPago;
            
            html += '<div style="margin-top:16px;padding-top:16px;border-top:2px solid var(--border);">';
            html += '<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;font-size:13px;">';
            html += '<div><span style="color:#666;">Total Geral:</span><br><strong style="font-size:16px;">R$' + totalGeral + '</strong></div>';
            html += '<div><span style="color:#666;">Total Pago:</span><br><strong style="font-size:16px;color:var(--success);">R$' + totalPago + '</strong></div>';
            html += '<div><span style="color:#666;">A Pagar:</span><br><strong style="font-size:16px;color:var(--warning);">R$' + totalAPagar + '</strong></div>';
            html += '</div></div>';
            
            html += '</div>';
            
            el.innerHTML = html;
        }
        
        function marcarPago(id, checked) {
            db.plantoes = db.plantoes.map(p => {
                if (p.id === id) {
                    return {...p, status: checked ? 'pago' : 'aprovado'};
                }
                return p;
            });
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            renderTab();
            renderCal();
        }
        
        function renderCad() {
            var html = '<div style="background:#f9fafb;border:1px solid var(--border);border-radius:6px;padding:12px;font-size:11px;font-family:monospace;max-height:200px;overflow-y:auto;">';
            html += '<strong>Funcionários (' + db.funcionarios.length + '):</strong><br>';
            db.funcionarios.forEach(f => html += '- ' + f.nome + '<br>');
            html += '<br><strong>Tipos (' + db.tipos.length + '):</strong><br>';
            db.tipos.forEach(t => html += '- ' + t.nome + ' (R$' + t.valor + ')<br>');
            html += '</div>';
            
            document.getElementById('cad-content').innerHTML = html;
        }
        
        function mostrarURLs() {
            document.getElementById('url-enf').textContent = BASE_URL + '?tipo=enfermeira';
            document.getElementById('url-gest').textContent = BASE_URL + '?tipo=gestor';
        }
        
        function gerarQRCode() {
            var url = BASE_URL + '?tipo=funcionario';
            var qrDiv = document.getElementById('qrcode');
            qrDiv.innerHTML = '';
            
            try {
                // Criar elemento canvas
                var canvas = document.createElement('canvas');
                
                // Usar a biblioteca QRCode
                if (typeof QRCode !== 'undefined' && QRCode.toCanvas) {
                    QRCode.toCanvas(canvas, url, { width: 200, margin: 2 }, function(error) {
                        if (error) {
                            alert('Erro ao gerar QR Code: ' + error);
                            return;
                        }
                        qrDiv.appendChild(canvas);
                        qrCodeCanvas = canvas;
                        document.getElementById('qr-display').style.display = 'block';
                        document.getElementById('qr-url').textContent = url;
                    });
                } else {
                    alert('Biblioteca QR Code ainda não carregou. Aguarde alguns segundos e tente novamente.');
                }
            } catch (e) {
                alert('Erro ao gerar QR Code: ' + e.message);
            }
        }
        
        function baixarQRCode() {
            if (!qrCodeCanvas) {
                alert('Gere o QR Code primeiro!');
                return;
            }
            
            var link = document.createElement('a');
            link.download = 'qrcode-funcionarios.png';
            link.href = qrCodeCanvas.toDataURL();
            link.click();
        }
        
        function copiarURL(tipo) {
            var url = tipo === 'enfermeira' ? BASE_URL + '?tipo=enfermeira' : BASE_URL + '?tipo=gestor';
            navigator.clipboard.writeText(url).then(() => alert('✅ Link copiado!'));
        }
    </script>
</body>
</html>
