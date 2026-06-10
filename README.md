[plantoes_v9.html](https://github.com/user-attachments/files/28799527/plantoes_v9.html)
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
        
        .btn-info { background: var(--info); color: white; }
        .btn-info:hover { opacity: 0.9; }
        
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
        .badge-paid { background: #dcfce7; color: #166534; border: 2px solid #16a34a; }
        
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
        
        .payment-table tr.pago {
            background: #f0fdf4;
            opacity: 0.7;
        }

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
        
        .qr-code-display img {
            display: block;
            margin: 0 auto;
            width: 200px;
            height: 200px;
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
            border: 2px solid var(--border);
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 12px;
        }
        
        .link-card h4 {
            font-size: 14px;
            margin-bottom: 8px;
            color: var(--primary);
            font-weight: 600;
        }
        
        .link-card p {
            font-size: 11px;
            color: #666;
            margin-bottom: 8px;
        }
        
        input[type="checkbox"] {
            width: 18px;
            height: 18px;
            cursor: pointer;
        }
        
        input[type="checkbox"]:disabled {
            cursor: not-allowed;
        }
        
        /* TELA DE LOGIN */
        #login-screen {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: #fafafa;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
        }
        
        #login-screen.hidden {
            display: none;
        }
        
        .login-box {
            background: white;
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 32px 24px;
            width: 100%;
            max-width: 340px;
            box-shadow: 0 4px 24px rgba(0,0,0,0.08);
        }
        
        .login-logo {
            text-align: center;
            margin-bottom: 24px;
        }
        
        .login-logo h1 { font-size: 22px; color: var(--primary); }
        .login-logo p  { font-size: 12px; color: #666; margin-top: 4px; }
        
        .login-error {
            background: #fee2e2;
            color: var(--danger);
            border-radius: 6px;
            padding: 8px 12px;
            font-size: 12px;
            margin-bottom: 12px;
            display: none;
        }
        .dash-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 16px;
        }
        
        .dash-card {
            background: white;
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 16px;
            text-align: center;
        }
        
        .dash-val {
            font-size: 32px;
            font-weight: 700;
            line-height: 1.1;
        }
        
        .dash-lbl {
            font-size: 11px;
            color: #666;
            margin-top: 4px;
        }
        
        .logout-btn {
            background: none;
            border: 1px solid rgba(255,255,255,0.5);
            color: white;
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 11px;
            cursor: pointer;
            float: right;
            margin-top: -2px;
        }
        
        .logout-btn:hover { background: rgba(255,255,255,0.15); }
    </style>
</head>
<body>

    <!-- TELA DE LOGIN -->
    <div id="login-screen">
        <div class="login-box">
            <div class="login-logo">
                <h1>🏥 Plantões</h1>
                <p>Casa de Repouso</p>
            </div>
            <div id="login-error" class="login-error">Usuário ou senha incorretos.</div>
            <div class="field">
                <label>Usuário</label>
                <input type="text" id="login-user" placeholder="Digite seu usuário..." autocomplete="username" />
            </div>
            <div class="field">
                <label>Senha</label>
                <input type="password" id="login-pass" placeholder="Digite sua senha..."
                    autocomplete="current-password"
                    onkeydown="if(event.key==='Enter') fazerLogin()" />
            </div>
            <button class="btn btn-primary" onclick="fazerLogin()">Entrar</button>
        </div>
    </div>

    <div class="container">
        <div class="header">
            <button class="logout-btn" id="btn-logout" onclick="fazerLogout()" style="display:none;">Sair ↩</button>
            <h1>🏥 Plantões</h1>
            <p>Casa de Repouso</p>
            <p id="usuario-logado" style="font-size:11px;opacity:0.8;margin-top:2px;"></p>
        </div>
        
        <div id="access-banner" class="access-banner"></div>
        
        <div class="nav" id="nav-container">
            <button onclick="show('dashboard')">Dashboard</button>
            <button onclick="show('checkin')">Check-in</button>
            <button onclick="show('enfermeira')">Enfermeira</button>
            <button onclick="show('calendario')">Calendário</button>
            <button onclick="show('pagamentos')">Pagamentos</button>
            <button onclick="show('historico')">Histórico</button>
            <button onclick="show('cadastros')">Cadastros</button>
        </div>
        
        <!-- DASHBOARD -->
        <div class="screen" id="screen-dashboard">
            <div class="card">
                <h2>📊 Dashboard — Resumo do Mês</h2>
                <p style="font-size:11px;color:#666;margin-bottom:16px;" id="dash-periodo"></p>
                <div class="dash-grid">
                    <div class="dash-card">
                        <div class="dash-val" style="color:var(--primary);" id="dash-total">0</div>
                        <div class="dash-lbl">Total de Plantões</div>
                    </div>
                    <div class="dash-card">
                        <div class="dash-val" style="color:var(--warning);" id="dash-pendentes">0</div>
                        <div class="dash-lbl">Pendentes de Aprovação</div>
                    </div>
                    <div class="dash-card">
                        <div class="dash-val" style="color:var(--success);" id="dash-aprovados">0</div>
                        <div class="dash-lbl">Aprovados</div>
                    </div>
                    <div class="dash-card">
                        <div class="dash-val" style="color:var(--danger);" id="dash-rejeitados">0</div>
                        <div class="dash-lbl">Rejeitados</div>
                    </div>
                </div>
                <div class="dash-grid">
                    <div class="dash-card" style="border-color:var(--success);">
                        <div class="dash-val" style="color:var(--success);font-size:22px;" id="dash-val-pago">R$0</div>
                        <div class="dash-lbl">Total Pago</div>
                    </div>
                    <div class="dash-card" style="border-color:var(--warning);">
                        <div class="dash-val" style="color:var(--warning);font-size:22px;" id="dash-val-apagar">R$0</div>
                        <div class="dash-lbl">A Pagar</div>
                    </div>
                </div>
                <h3 style="font-size:13px;font-weight:600;margin-bottom:10px;">Por Funcionário este mês:</h3>
                <div id="dash-por-func"></div>
            </div>
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
                        <select id="ci-tipo" onchange="verificarHospede()"></select>
                    </div>
                    <div class="field">
                        <label>Motivo</label>
                        <select id="ci-motivo"></select>
                    </div>
                    <div id="ci-hospede-field" class="field" style="display:none;">
                        <label>Nome do hóspede <span style="color:var(--danger);">*</span></label>
                        <input type="text" id="ci-hospede" placeholder="Digite o nome completo do hóspede..." />
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
                        <div id="ci-localizacao" style="margin-top:12px;font-size:12px;color:#166534;"></div>
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
        
        <!-- HISTÓRICO -->
        <div class="screen" id="screen-historico">
            <div class="card">
                <h2>📋 Histórico Completo de Plantões</h2>
                <p style="font-size:12px;color:#666;margin-bottom:12px;">Todos os plantões registrados no sistema</p>
                
                <button class="btn btn-success" onclick="exportarXLS()" style="margin-bottom:12px;">
                    📥 EXPORTAR PARA EXCEL (XLS)
                </button>
                
                <div id="historico-lista"></div>
            </div>
        </div>
        
        <!-- CADASTROS -->
        <div class="screen" id="screen-cadastros">
            <div class="card">
                <h2>⚙️ Cadastros do Google Sheets</h2>
                
                <button class="btn btn-warning" onclick="carregarDados()" style="margin-bottom:12px;">🔄 Recarregar dados</button>
                
                <div id="cad-status"></div>
                <div id="cad-content"></div>
            </div>
            
            <!-- LINKS DE ACESSO -->
            <div id="links-section" style="display:none;">
                <div class="card" style="background:#e0f2fe;border:2px solid var(--info);">
                    <h2 style="color:var(--info);">🔗 Links de Acesso ao Sistema</h2>
                    <p style="font-size:12px;color:#0c4a6e;margin-bottom:16px;">Copie e compartilhe os links conforme o perfil de acesso</p>
                </div>
                
                <div class="link-card" style="border-color:var(--success);">
                    <h4 style="color:var(--success);">👤 LINK FUNCIONÁRIO</h4>
                    <p>Acesso apenas para registrar plantões (check-in)</p>
                    <div class="url-display" id="url-func"></div>
                    <button class="btn btn-sm btn-success" onclick="copiarURL('funcionario')">📋 Copiar Link Funcionário</button>
                </div>
                
                <div class="link-card" style="border-color:var(--warning);">
                    <h4 style="color:var(--warning);">💉 LINK ENFERMEIRA</h4>
                    <p>Acesso apenas para aprovar plantões</p>
                    <div class="url-display" id="url-enf"></div>
                    <button class="btn btn-sm btn-warning" onclick="copiarURL('enfermeira')">📋 Copiar Link Enfermeira</button>
                </div>
                
                <div class="link-card" style="border-color:var(--primary);">
                    <h4 style="color:var(--primary);">👨‍💼 LINK GESTOR</h4>
                    <p>Acesso completo a todas as funcionalidades</p>
                    <div class="url-display" id="url-gest"></div>
                    <button class="btn btn-sm btn-primary" onclick="copiarURL('gestor')">📋 Copiar Link Gestor</button>
                </div>
            </div>
            
            <!-- QR CODE -->
            <div id="qr-generator-section" style="display:none;">
                <div class="qr-section">
                    <h3>📱 QR Code para Funcionários</h3>
                    <p style="font-size:12px;color:#666;margin-bottom:16px;">Gere o QR Code para os funcionários registrarem plantões</p>
                    
                    <button class="btn btn-primary" onclick="gerarQRCode()" style="font-size:16px;padding:14px;">
                        🎨 GERAR QR CODE
                    </button>
                    
                    <div id="qr-display" style="display:none;margin-top:20px;">
                        <div class="qr-code-display">
                            <div id="qrcode" style="display:flex;justify-content:center;"></div>
                        </div>
                        
                        <button class="btn btn-success" onclick="baixarQRCode()">
                            ⬇️ Baixar QR Code (PNG)
                        </button>
                        
                        <div class="url-display" id="qr-url"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script>
        var SHEET_ID = "1TVYsc9GnaK_T1YILkdgBOJSyDA4CZbEyvzk47Izr-go";
        var API_KEY = "AIzaSyC2Vb-uj16w6NnlSk6sOAm6S1Uj5HpIh40";
        var BASE_URL = window.location.origin + window.location.pathname;
        // Firebase Realtime Database - banco compartilhado gratuito entre todos os dispositivos
        var FIREBASE_URL = 'https://plantoes-casa-repouso-default-rtdb.firebaseio.com';
        var usuarioLogado = '';
        
        var urlParams = new URLSearchParams(window.location.search);
        var tipoAcesso = urlParams.get('tipo') || 'gestor';
        
        var _plantoesSalvos = JSON.parse(localStorage.getItem('plantoes')) || [];
        _plantoesSalvos = _plantoesSalvos.map(function(p) {
            if (p.dataObj && typeof p.dataObj === 'string') {
                p.dataObj = new Date(p.dataObj);
            }
            return p;
        });
        
        var db = {
            funcionarios: [],
            tipos: [],
            autorizadores: [],
            aprovadores: [],
            motivos: [],
            plantoes: _plantoesSalvos
        };
        
        var hoje = new Date();
        var calMes = hoje.getMonth();
        var calAno = hoje.getFullYear();
        
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
                                valor: parseFloat(dataConf.values[i][1]) || 0,
                                requerHospede: (dataConf.values[i][2] || '').trim().toLowerCase() === 'sim'
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
        
        // ── USUÁRIOS E SENHAS ──────────────────────────────────────────────────
        function fazerLogout() {
            usuarioLogado = '';
            tipoAcesso = '';
            document.getElementById('usuario-logado').textContent = '';
            document.getElementById('btn-logout').style.display = 'none';
            document.getElementById('login-screen').classList.remove('hidden');
            document.getElementById('login-user').value = '';
            document.getElementById('login-pass').value = '';
        }
        
        var USUARIOS = [
            { login: 'Michele',   senha: '4748', perfil: 'enfermeira' },
            { login: 'Enfermagem', senha: '0664', perfil: 'enfermeira' },
            { login: 'Thiago',    senha: '0034', perfil: 'gestor'     },
            { login: 'Luciane',   senha: '1186', perfil: 'gestor'     }
        ];
        
        function fazerLogin() {
            var user = document.getElementById('login-user').value.trim();
            var pass = document.getElementById('login-pass').value;
            var erro = document.getElementById('login-error');
            
            var encontrado = USUARIOS.find(function(u) {
                return u.login.toLowerCase() === user.toLowerCase() && u.senha === pass;
            });
            
            if (!encontrado) {
                erro.style.display = 'block';
                document.getElementById('login-pass').value = '';
                return;
            }
            
            // Login OK: esconde tela de login e define perfil
            erro.style.display = 'none';
            document.getElementById('login-screen').classList.add('hidden');
            tipoAcesso = encontrado.perfil;
            usuarioLogado = encontrado.login;
            // Mostrar nome do usuário e botão logout no header
            document.getElementById('usuario-logado').textContent = 'Olá, ' + usuarioLogado;
            document.getElementById('btn-logout').style.display = 'inline-block';
            configurarAcesso();
            carregarDados();
            renderCal();
            if (tipoAcesso === 'gestor') {
                document.getElementById('qr-generator-section').style.display = 'block';
                document.getElementById('links-section').style.display = 'block';
                mostrarURLs();
                renderDashboard();
            }
        }
        
        window.addEventListener('DOMContentLoaded', function() {
            if (tipoAcesso === 'funcionario') {
                // Funcionário entra direto pelo QR Code, sem login
                document.getElementById('login-screen').classList.add('hidden');
                configurarAcesso();
                carregarDados();
                renderCal();
            }
            // Enfermeira e gestor ficam na tela de login
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
                buttons[5].disabled = true;
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
            
            var tabs = ['checkin', 'enfermeira', 'calendario', 'pagamentos', 'historico', 'cadastros'];
            var idx = tabs.indexOf(s);
            if (idx >= 0) document.querySelectorAll('.nav button')[idx].classList.add('active');
            
            if (s === 'dashboard') renderDashboard();
            if (s === 'checkin') resetGate();
            if (s === 'enfermeira') renderEnf();
            if (s === 'calendario') renderCal();
            if (s === 'pagamentos') { initDates(); renderTab(); }
            if (s === 'historico') renderHistorico();
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
                // Valor R$ nunca aparece no dropdown de check-in
                opt.textContent = t.nome;
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
        
        function verificarHospede() {
            var tipoNome = document.getElementById('ci-tipo').value;
            var t = db.tipos.find(function(x) { return x.nome === tipoNome; });
            var campo = document.getElementById('ci-hospede-field');
            var input = document.getElementById('ci-hospede');
            if (t && t.requerHospede) {
                campo.style.display = 'block';
                input.required = true;
            } else {
                campo.style.display = 'none';
                input.required = false;
                input.value = '';
            }
        }
        
        function fazerCheckin() {
            var func = document.getElementById('ci-func').value;
            var tipo = document.getElementById('ci-tipo').value;
            
            if (!func || !tipo) {
                alert('Por favor, preencha funcionário e tipo de plantão!');
                return;
            }
            
            // Validar hóspede se tipo exigir
            var tSel = db.tipos.find(function(x) { return x.nome === tipo; });
            var hospede = document.getElementById('ci-hospede').value.trim();
            if (tSel && tSel.requerHospede && !hospede) {
                alert('Por favor, informe o nome do hóspede para este tipo de plantão.');
                return;
            }
            
            var agora = new Date();
            var t = db.tipos.find(x => x.nome === tipo);
            var p = {
                id: Date.now(),
                func: func,
                tipo: tipo,
                motivo: document.getElementById('ci-motivo').value || '',
                data: agora.toLocaleDateString('pt-BR'),
                dataObj: new Date(agora.getFullYear(), agora.getMonth(), agora.getDate()),
                dataISO: agora.toISOString(),
                hora: agora.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' }),
                valor: t ? t.valor : 0,
                status: 'pendente',
                autor: document.getElementById('ci-autor').value || '',
                hospede: hospede || '',
                endereco: ''
            };
            
            // Esconde form e mostra sucesso já (com localização pendente)
            document.getElementById('ci-form').style.display = 'none';
            document.getElementById('ci-sucesso').style.display = 'block';
            var locDiv = document.getElementById('ci-localizacao');
            locDiv.textContent = '📍 Obtendo localização...';
            
            function salvarPlantao(endereco) {
                p.endereco = endereco || '';
                db.plantoes.unshift(p);
                localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
                // Salva no Firebase (compartilhado entre TODOS os dispositivos)
                fetch(FIREBASE_URL + '/plantoes/' + p.id + '.json', {
                    method: 'PUT',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(p)
                }).then(function(r) {
                    if (!r.ok) console.warn('Firebase: erro ao salvar plantão');
                }).catch(function(e) {
                    console.warn('Firebase offline, salvo apenas localmente:', e);
                });
            }
            
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    function(pos) {
                        var lat = pos.coords.latitude;
                        var lon = pos.coords.longitude;
                        // Reverse geocode via OpenStreetMap Nominatim (gratuito)
                        fetch('https://nominatim.openstreetmap.org/reverse?format=json&lat=' + lat + '&lon=' + lon, {
                            headers: { 'Accept-Language': 'pt-BR' }
                        })
                        .then(function(r) { return r.json(); })
                        .then(function(geo) {
                            var ad = geo.address || {};
                            var partes = [];
                            if (ad.road) partes.push(ad.road);
                            if (ad.suburb || ad.neighbourhood) partes.push(ad.suburb || ad.neighbourhood);
                            if (ad.city || ad.town || ad.village) partes.push(ad.city || ad.town || ad.village);
                            if (ad.state) partes.push(ad.state);
                            var endereco = partes.join(', ');
                            locDiv.textContent = '📍 ' + endereco;
                            salvarPlantao(endereco);
                        })
                        .catch(function() {
                            var coords = lat.toFixed(5) + ', ' + lon.toFixed(5);
                            locDiv.textContent = '📍 ' + coords;
                            salvarPlantao(coords);
                        });
                    },
                    function() {
                        // Usuário negou ou erro de GPS
                        locDiv.textContent = '📍 Localização não disponível';
                        salvarPlantao('');
                    },
                    { timeout: 10000 }
                );
            } else {
                locDiv.textContent = '';
                salvarPlantao('');
            }
        }
        
        function renderEnfUI() {
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
                    ${p.motivo ? '<div class="item-sub">Motivo do funcionário: ' + p.motivo + '</div>' : ''}
                    ${p.hospede ? '<div class="item-sub" style="color:#0369a1;font-weight:500;">🛏️ Hóspede: ' + p.hospede + '</div>' : ''}
                    <div style="margin-top:10px;">
                        <label style="font-size:11px;font-weight:600;color:#374151;display:block;margin-bottom:4px;">
                            Justificativa da enfermeira <span style="color:var(--danger);">*</span>
                        </label>
                        <textarea
                            id="motivo-enf-${p.id}"
                            placeholder="Descreva a justificativa para aprovação (mínimo 10 caracteres)..."
                            oninput="verificarMotivoEnf(${p.id})"
                            style="width:100%;padding:8px;border:1px solid var(--border);border-radius:6px;font-size:12px;font-family:inherit;resize:vertical;min-height:64px;"
                        ></textarea>
                        <div id="aviso-enf-${p.id}" style="font-size:10px;color:var(--danger);margin-top:2px;display:none;">
                            Mínimo de 10 caracteres para aprovar.
                        </div>
                    </div>
                    <div style="display:flex;gap:8px;margin-top:8px;">
                        <button
                            id="btn-aprovar-${p.id}"
                            class="btn btn-success btn-sm"
                            style="flex:1;opacity:0.4;cursor:not-allowed;"
                            disabled
                            onclick="aprovar(${p.id})"
                        >Aprovar</button>
                        <button class="btn btn-danger btn-sm" style="flex:1;" onclick="rejeitar(${p.id})">Rejeitar</button>
                    </div>
                </div>
            `).join('');
        }
        
        function verificarMotivoEnf(id) {
            var textarea = document.getElementById('motivo-enf-' + id);
            var btn = document.getElementById('btn-aprovar-' + id);
            var aviso = document.getElementById('aviso-enf-' + id);
            if (!textarea || !btn) return;
            var val = textarea.value.trim();
            if (val.length >= 10) {
                btn.disabled = false;
                btn.style.opacity = '1';
                btn.style.cursor = 'pointer';
                aviso.style.display = 'none';
            } else {
                btn.disabled = true;
                btn.style.opacity = '0.4';
                btn.style.cursor = 'not-allowed';
                if (val.length > 0) {
                    aviso.style.display = 'block';
                } else {
                    aviso.style.display = 'none';
                }
            }
        }
        
        function renderEnf() {
            // Busca SEMPRE do Firebase (banco compartilhado entre todos os dispositivos)
            document.getElementById('lista-enf').innerHTML = '<p style="font-size:12px;color:#666;">🔄 Buscando plantões...</p>';
            fetch(FIREBASE_URL + '/plantoes.json')
                .then(function(r) { return r.json(); })
                .then(function(dados) {
                    if (dados && typeof dados === 'object') {
                        var remotos = Object.values(dados);
                        // Reconstrói db.plantoes com dados do Firebase (fonte da verdade)
                        db.plantoes = remotos.map(function(r) {
                            r.dataObj = r.dataISO ? new Date(r.dataISO) : new Date(r.data.split('/').reverse().join('-'));
                            r.valor = parseFloat(r.valor) || 0;
                            return r;
                        });
                        // Ordena do mais recente pro mais antigo
                        db.plantoes.sort(function(a, b) { return b.id - a.id; });
                        localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
                    }
                    renderEnfUI();
                })
                .catch(function() {
                    renderEnfUI();
                });
        }
        
        function aprovar(id) {
            var textarea = document.getElementById('motivo-enf-' + id);
            var motivoEnf = textarea ? textarea.value.trim() : '';
            // Segurança extra: não aprova se menos de 10 caracteres
            if (motivoEnf.length < 10) return;
            
            // 1. Atualiza localmente IMEDIATO (UI responde na hora)
            var agora = new Date();
            var aprovadoEm = agora.toLocaleDateString('pt-BR') + ' ' + agora.toLocaleTimeString('pt-BR', {hour:'2-digit', minute:'2-digit'});
            db.plantoes = db.plantoes.map(p => 
                p.id === id ? {...p, status: 'aprovado', motivoEnf: motivoEnf, aprovadoPor: usuarioLogado, aprovadoEm: aprovadoEm} : p
            );
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            
            // 2. Renderiza UI imediatamente com dado local (sem esperar Firebase)
            renderEnfUI();
            renderCal();
            
            // 3. Salva no Firebase em segundo plano (não bloqueia a UI)
            fetch(FIREBASE_URL + '/plantoes/' + id + '/status.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify('aprovado')
            }).catch(function() {});
            fetch(FIREBASE_URL + '/plantoes/' + id + '/motivoEnf.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(motivoEnf)
            }).catch(function() {});
            fetch(FIREBASE_URL + '/plantoes/' + id + '/aprovadoPor.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(usuarioLogado)
            }).catch(function() {});
            fetch(FIREBASE_URL + '/plantoes/' + id + '/aprovadoEm.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(aprovadoEm)
            }).catch(function() {});
        }
        
        function rejeitar(id) {
            db.plantoes = db.plantoes.map(p => 
                p.id === id ? {...p, status: 'rejeitado'} : p
            );
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            // Atualiza status no Firebase
            fetch(FIREBASE_URL + '/plantoes/' + id + '/status.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify('rejeitado')
            }).catch(function() {});
            renderEnf();
            renderCal();
        }
        
        function renderDashboard() {
            var meses = ['Janeiro','Fevereiro','Março','Abril','Maio','Junho','Julho','Agosto','Setembro','Outubro','Novembro','Dezembro'];
            var agora = new Date();
            var mes = agora.getMonth();
            var ano = agora.getFullYear();
            
            document.getElementById('dash-periodo').textContent = meses[mes] + ' de ' + ano;
            
            // Filtrar plantões do mês atual
            var doMes = db.plantoes.filter(function(p) {
                var d = p.dataObj instanceof Date ? p.dataObj : new Date(p.dataObj);
                return d.getMonth() === mes && d.getFullYear() === ano;
            });
            
            var pendentes  = doMes.filter(function(p) { return p.status === 'pendente'; });
            var aprovados  = doMes.filter(function(p) { return p.status === 'aprovado' || p.status === 'pago'; });
            var rejeitados = doMes.filter(function(p) { return p.status === 'rejeitado'; });
            var pagos      = doMes.filter(function(p) { return p.status === 'pago'; });
            var aprovApagar = doMes.filter(function(p) { return p.status === 'aprovado'; });
            
            var totalPago   = pagos.reduce(function(s,p){ return s + p.valor; }, 0);
            var totalApagar = aprovApagar.reduce(function(s,p){ return s + p.valor; }, 0);
            
            document.getElementById('dash-total').textContent     = doMes.length;
            document.getElementById('dash-pendentes').textContent  = pendentes.length;
            document.getElementById('dash-aprovados').textContent  = aprovados.length;
            document.getElementById('dash-rejeitados').textContent = rejeitados.length;
            document.getElementById('dash-val-pago').textContent   = 'R$' + totalPago.toFixed(2);
            document.getElementById('dash-val-apagar').textContent = 'R$' + totalApagar.toFixed(2);
            
            // Por funcionário
            var grupos = {};
            doMes.forEach(function(p) {
                if (!grupos[p.func]) grupos[p.func] = { total: 0, valor: 0 };
                grupos[p.func].total++;
                grupos[p.func].valor += p.valor;
            });
            
            var html = '';
            Object.keys(grupos).sort().forEach(function(nome) {
                var g = grupos[nome];
                html += '<div style="display:flex;justify-content:space-between;align-items:center;';
                html += 'padding:8px 12px;background:var(--light);border-radius:6px;margin-bottom:6px;font-size:13px;">';
                html += '<span>👤 ' + nome + '</span>';
                html += '<span><strong>' + g.total + '</strong> plantão(ões) · <strong>R$' + g.valor.toFixed(2) + '</strong></span>';
                html += '</div>';
            });
            
            document.getElementById('dash-por-func').innerHTML = html || '<p style="font-size:12px;color:#666;">Nenhum plantão este mês.</p>';
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
                var plantoesDia = db.plantoes.filter(function(p) {
                    if (!p.dataObj) return false;
                    var dt = (p.dataObj instanceof Date) ? p.dataObj : new Date(p.dataObj);
                    return dt.getFullYear() === calAno && dt.getMonth() === calMes && dt.getDate() === d;
                });
                
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
            var plantoesDia = db.plantoes.filter(function(p) {
                if (!p.dataObj) return false;
                var dt = (p.dataObj instanceof Date) ? p.dataObj : new Date(p.dataObj);
                return dt.getFullYear() === calAno && dt.getMonth() === calMes && dt.getDate() === d;
            });
            
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
                        <span class="badge badge-${p.status === 'pendente' ? 'warn' : p.status === 'aprovado' ? 'ok' : p.status === 'pago' ? 'paid' : 'danger'}">${p.status}</span>
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
        
        function toInputDate(d) {
            var mm = String(d.getMonth() + 1).padStart(2, '0');
            var dd = String(d.getDate()).padStart(2, '0');
            return d.getFullYear() + '-' + mm + '-' + dd;
        }
        
        function filtroRapido(tipo) {
            var agora = new Date();
            var de, ate;
            
            if (tipo === 7) {
                ate = new Date(agora);
                de = new Date(agora);
                de.setDate(agora.getDate() - 7);
            } else if (tipo === 'semana') {
                // Semana passada Domingo a Sabado
                ate = new Date(agora);
                ate.setDate(agora.getDate() - agora.getDay() - 1);
                de = new Date(ate);
                de.setDate(ate.getDate() - 6);
            } else if (tipo === 'mes') {
                de = new Date(agora.getFullYear(), agora.getMonth(), 1);
                ate = new Date(agora);
            } else if (tipo === 'mes-ant') {
                de = new Date(agora.getFullYear(), agora.getMonth() - 1, 1);
                ate = new Date(agora.getFullYear(), agora.getMonth(), 0);
            } else if (tipo === 'tudo') {
                de = new Date(2000, 0, 1);
                ate = new Date(agora);
            }
            
            document.getElementById('tab-de').value = toInputDate(de);
            document.getElementById('tab-ate').value = toInputDate(ate);
            renderTab();
        }
        
        function renderTab() {
            var el = document.getElementById('tab-lista');
            var deVal = document.getElementById('tab-de').value;
            var ateVal = document.getElementById('tab-ate').value;
            var de = deVal ? new Date(deVal + 'T00:00:00') : null;
            var ate = ateVal ? new Date(ateVal + 'T23:59:59') : null;
            
            // Filtrar por status e por intervalo de datas
            var filtrados = db.plantoes.filter(function(p) {
                if (p.status !== 'aprovado' && p.status !== 'pago') return false;
                if (!p.dataObj) return false;
                var dataP = p.dataObj instanceof Date ? p.dataObj : new Date(p.dataObj);
                if (de && dataP < de) return false;
                if (ate && dataP > ate) return false;
                return true;
            });
            
            if (!filtrados.length) {
                el.innerHTML = '<div class="card"><p style="font-size:12px;color:#666;">Nenhum plantão aprovado neste período.</p></div>';
                return;
            }
            
            // Agrupar por funcionário
            var grupos = {};
            filtrados.forEach(function(p) {
                if (!grupos[p.func]) grupos[p.func] = [];
                grupos[p.func].push(p);
            });
            
            var html = '';
            var totalGeralGlobal = 0;
            var totalPagoGlobal = 0;
            
            Object.keys(grupos).sort().forEach(function(nome) {
                var plantoesFunc = grupos[nome];
                var somaFunc = plantoesFunc.reduce(function(s, p) { return s + p.valor; }, 0);
                var somaPagoFunc = plantoesFunc.filter(function(p) { return p.status === 'pago'; }).reduce(function(s, p) { return s + p.valor; }, 0);
                totalGeralGlobal += somaFunc;
                totalPagoGlobal += somaPagoFunc;
                
                html += '<div class="card" style="margin-bottom:12px;">';
                html += '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;padding-bottom:8px;border-bottom:2px solid var(--primary);">';
                html += '<strong style="font-size:14px;color:var(--primary);">👤 ' + nome + '</strong>';
                html += '<span style="font-size:13px;font-weight:600;">Total: R$' + somaFunc.toFixed(2) + '</span>';
                html += '</div>';
                
                html += '<table class="payment-table"><thead><tr><th>Data</th><th>Tipo</th><th>Valor</th><th style="text-align:center;width:72px;">✅ Pago?</th></tr></thead><tbody>';
                
                plantoesFunc.forEach(function(p) {
                    var isPago = p.status === 'pago';
                    html += '<tr class="' + (isPago ? 'pago' : '') + '">';
                    html += '<td>' + p.data + '</td>';
                    html += '<td style="font-size:11px;">' + p.tipo + '</td>';
                    html += '<td><strong>R$' + p.valor + '</strong></td>';
                    html += '<td style="text-align:center;">';
                    if (isPago) {
                        html += '<input type="checkbox" checked disabled style="cursor:not-allowed;">';
                    } else {
                        html += '<input type="checkbox" onchange="marcarPago(' + p.id + ', this.checked)">';
                    }
                    html += '</td></tr>';
                });
                
                html += '</tbody></table>';
                
                // Subtotal por funcionário
                var apagarFunc = somaFunc - somaPagoFunc;
                html += '<div style="margin-top:10px;padding-top:10px;border-top:1px solid var(--border);display:grid;grid-template-columns:1fr 1fr;gap:8px;font-size:12px;">';
                html += '<div>Pago: <strong style="color:var(--success);">R$' + somaPagoFunc.toFixed(2) + '</strong></div>';
                html += '<div>A Pagar: <strong style="color:var(--warning);">R$' + apagarFunc.toFixed(2) + '</strong></div>';
                html += '</div></div>';
            });
            
            // Totais globais
            var totalAPagarGlobal = totalGeralGlobal - totalPagoGlobal;
            html += '<div class="card" style="background:var(--light);">';
            html += '<strong style="font-size:13px;">📊 Totais do Período</strong>';
            html += '<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;font-size:13px;margin-top:10px;">';
            html += '<div><span style="color:#666;">Total Geral:</span><br><strong style="font-size:18px;">R$' + totalGeralGlobal.toFixed(2) + '</strong></div>';
            html += '<div><span style="color:#666;">Total Pago:</span><br><strong style="font-size:18px;color:var(--success);">R$' + totalPagoGlobal.toFixed(2) + '</strong></div>';
            html += '<div><span style="color:#666;">A Pagar:</span><br><strong style="font-size:18px;color:var(--warning);">R$' + totalAPagarGlobal.toFixed(2) + '</strong></div>';
            html += '</div></div>';
            
            el.innerHTML = html;
        }
        
        function marcarPago(id, checked) {
            var novoStatus = checked ? 'pago' : 'aprovado';
            db.plantoes = db.plantoes.map(p => {
                if (p.id === id) {
                    return {...p, status: novoStatus};
                }
                return p;
            });
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            // Atualiza status no Firebase
            fetch(FIREBASE_URL + '/plantoes/' + id + '/status.json', {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(novoStatus)
            }).catch(function() {});
            renderTab();
            renderCal();
            renderHistorico();
        }
        
        function renderHistorico() {
            var el = document.getElementById('historico-lista');
            
            if (!db.plantoes.length) {
                el.innerHTML = '<p style="font-size:12px;color:#666;text-align:center;padding:20px;">Nenhum plantão registrado ainda.</p>';
                return;
            }
            
            var html = '<table class="payment-table">';
            html += '<thead><tr><th>ID</th><th>Data</th><th>Hora</th><th>Funcionário</th><th>Tipo</th><th>Motivo</th><th>Hóspede</th><th>Autor.</th><th>Valor</th><th>Status</th><th>Aprovado por</th><th>Data Aprov.</th><th>Justificativa Enf.</th><th>Localização</th><th style="text-align:center;">Apagar</th></tr></thead>';
            html += '<tbody>';
            
            db.plantoes.forEach(p => {
                var statusBadge = '';
                if (p.status === 'pendente') statusBadge = '<span class="badge badge-warn">Pendente</span>';
                else if (p.status === 'aprovado') statusBadge = '<span class="badge badge-ok">Aprovado</span>';
                else if (p.status === 'pago') statusBadge = '<span class="badge badge-paid">✅ PAGO</span>';
                else if (p.status === 'rejeitado') statusBadge = '<span class="badge badge-danger">Rejeitado</span>';
                
                html += '<tr>';
                html += '<td style="font-size:10px;color:#666;">' + p.id + '</td>';
                html += '<td>' + p.data + '</td>';
                html += '<td>' + p.hora + '</td>';
                html += '<td>' + p.func + '</td>';
                html += '<td style="font-size:11px;">' + p.tipo + '</td>';
                html += '<td style="font-size:11px;">' + (p.motivo || '-') + '</td>';
                html += '<td style="font-size:11px;color:#0369a1;">' + (p.hospede || '-') + '</td>';
                html += '<td style="font-size:11px;">' + (p.autor || '-') + '</td>';
                html += '<td><strong>R$' + p.valor + '</strong></td>';
                html += '<td>' + statusBadge + '</td>';
                html += '<td style="font-size:11px;color:var(--success);">' + (p.aprovadoPor || '-') + '</td>';
                html += '<td style="font-size:11px;">' + (p.aprovadoEm || '-') + '</td>';
                html += '<td style="font-size:11px;font-style:italic;">' + (p.motivoEnf || '-') + '</td>';
                html += '<td style="font-size:10px;color:#666;">' + (p.endereco || '-') + '</td>';
                html += '<td style="text-align:center;"><button onclick="apagarPlantao(' + p.id + ')" style="background:var(--danger);color:white;border:none;border-radius:4px;padding:4px 8px;font-size:11px;cursor:pointer;">🗑️</button></td>';
                html += '</tr>';
            });
            
            html += '</tbody></table>';
            
            var total = db.plantoes.reduce((s, p) => s + p.valor, 0);
            var totalPago = db.plantoes.filter(p => p.status === 'pago').reduce((s, p) => s + p.valor, 0);
            
            html += '<div style="margin-top:16px;padding:12px;background:var(--light);border-radius:6px;">';
            html += '<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;font-size:13px;">';
            html += '<div><strong>Total Plantões:</strong> ' + db.plantoes.length + '</div>';
            html += '<div><strong>Valor Total:</strong> R$' + total.toFixed(2) + '</div>';
            html += '<div><strong>Total Pago:</strong> <span style="color:var(--success);">R$' + totalPago.toFixed(2) + '</span></div>';
            html += '</div></div>';
            
            el.innerHTML = html;
        }
        
        function apagarPlantao(id) {
            if (!confirm('Tem certeza que deseja apagar este lançamento? Esta ação não pode ser desfeita.')) return;
            // Remove localmente
            db.plantoes = db.plantoes.filter(function(p) { return p.id !== id; });
            localStorage.setItem('plantoes', JSON.stringify(db.plantoes));
            // Remove do Firebase
            fetch(FIREBASE_URL + '/plantoes/' + id + '.json', {
                method: 'DELETE'
            }).catch(function() {});
            // Atualiza telas
            renderHistorico();
            renderCal();
            renderTab();
        }
        
        function exportarXLS() {
            if (!db.plantoes.length) {
                alert('Não há plantões para exportar!');
                return;
            }
            
            var dados = db.plantoes.map(p => ({
                'ID': p.id,
                'Data': p.data,
                'Hora': p.hora,
                'Funcionário': p.func,
                'Tipo de Plantão': p.tipo,
                'Motivo': p.motivo || '',
                'Autorizado por': p.autor || '',
                'Valor (R$)': p.valor,
                'Status': p.status,
                'Pago?': p.status === 'pago' ? 'SIM' : 'NÃO'
            }));
            
            var ws = XLSX.utils.json_to_sheet(dados);
            var wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Plantões");
            
            var hoje = new Date();
            var filename = 'historico_plantoes_' + hoje.toLocaleDateString('pt-BR').replace(/\//g, '-') + '.xlsx';
            
            XLSX.writeFile(wb, filename);
        }
        
        function renderCad() {
            var html = '<div style="background:#f9fafb;border:1px solid var(--border);border-radius:6px;padding:12px;font-size:11px;font-family:monospace;max-height:200px;overflow-y:auto;">';
            html += '<strong>Funcionários (' + db.funcionarios.length + '):</strong><br>';
            db.funcionarios.forEach(f => html += '- ' + f.nome + ' (' + f.cargo + ')<br>');
            html += '<br><strong>Tipos (' + db.tipos.length + '):</strong><br>';
            db.tipos.forEach(t => html += '- ' + t.nome + ' (R$' + t.valor + ')<br>');
            html += '<br><strong>Motivos (' + db.motivos.length + '):</strong><br>';
            db.motivos.forEach(m => html += '- ' + m + '<br>');
            html += '</div>';
            
            document.getElementById('cad-content').innerHTML = html;
        }
        
        function mostrarURLs() {
            document.getElementById('url-func').textContent = BASE_URL + '?tipo=funcionario';
            document.getElementById('url-enf').textContent = BASE_URL + '?tipo=enfermeira';
            document.getElementById('url-gest').textContent = BASE_URL + '?tipo=gestor';
        }
        
        function gerarQRCode() {
            var url = BASE_URL + '?tipo=funcionario';
            var qrDiv = document.getElementById('qrcode');
            qrDiv.innerHTML = '';
            
            // qrcodejs: sintaxe new QRCode(element, opcoes)
            new QRCode(qrDiv, {
                text: url,
                width: 200,
                height: 200,
                colorDark: '#000000',
                colorLight: '#ffffff',
                correctLevel: QRCode.CorrectLevel.H
            });
            
            document.getElementById('qr-display').style.display = 'block';
            document.getElementById('qr-url').textContent = url;
        }
        
        function baixarQRCode() {
            var qrDiv = document.getElementById('qrcode');
            var canvas = qrDiv.querySelector('canvas');
            var img = qrDiv.querySelector('img');
            
            var link = document.createElement('a');
            link.download = 'qrcode-funcionarios.png';
            
            if (canvas) {
                link.href = canvas.toDataURL('image/png');
                link.click();
            } else if (img) {
                link.href = img.src;
                link.click();
            } else {
                alert('Gere o QR Code primeiro!');
            }
        }
        
        function copiarURL(tipo) {
            var url = '';
            if (tipo === 'funcionario') url = BASE_URL + '?tipo=funcionario';
            else if (tipo === 'enfermeira') url = BASE_URL + '?tipo=enfermeira';
            else if (tipo === 'gestor') url = BASE_URL + '?tipo=gestor';
            
            navigator.clipboard.writeText(url).then(() => {
                alert('✅ Link copiado com sucesso!');
            }).catch(() => {
                alert('❌ Erro ao copiar. Selecione e copie manualmente.');
            });
        }
    </script>
</body>
</html>
