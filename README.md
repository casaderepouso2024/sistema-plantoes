[index.html](https://github.com/user-attachments/files/26897853/index.html)
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
        
        .field {
            margin-bottom: 12px;
        }
        
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
        
        .field textarea { resize: vertical; min-height: 60px; }
        
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
        
        .btn-sm {
            width: auto;
            padding: 6px 10px;
            font-size: 12px;
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
        
        .toast {
            display: none;
            padding: 12px;
            border-radius: 6px;
            margin-bottom: 12px;
            font-size: 12px;
            border-left: 4px solid;
        }
        
        .toast.show {
            display: block;
        }
        
        .toast.success {
            background: #f0fdf4;
            border-left-color: var(--success);
            color: #166534;
        }
        
        .toast.error {
            background: #fef2f2;
            border-left-color: var(--danger);
            color: #991b1b;
        }
        
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
        
        .list {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        
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
        
        .gate-btns {
            display: flex;
            gap: 8px;
        }
        
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
        
        .obs-box {
            background: #fffbeb;
            border-left: 3px solid var(--warning);
            padding: 8px;
            border-radius: 4px;
            margin-top: 8px;
            font-size: 11px;
            color: #92400e;
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏥 Plantões</h1>
            <p>Casa de Repouso</p>
        </div>
        
        <div class="nav">
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
                    <div id="toast-ci" class="toast"></div>
                    <div class="field">
                        <label>Funcionário</label>
                        <select id="ci-func"></select>
                    </div>
                    <div class="field">
                        <label>Tipo de plantão</label>
                        <select id="ci-tipo" onchange="onTipoChange()"></select>
                    </div>
                    <div class="field" id="campo-hosp" style="display:none;">
                        <label>Nome do hóspede</label>
                        <select id="ci-hosp"></select>
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
            </div>
            
            <div class="card">
                <h2>Últimos registros</h2>
                <div id="lista-rec"></div>
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
                    <div class="metric-val" style="color:var(--warning);">0</div>
                    <div class="metric-lbl">Pendentes</div>
                </div>
                <div class="metric">
                    <div class="metric-val" style="color:var(--success);">0</div>
                    <div class="metric-lbl">Aprovados</div>
                </div>
                <div class="metric">
                    <div class="metric-val" style="color:var(--danger);">0</div>
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
                <h2>📅 Calendário de Pagamentos</h2>
                <p style="font-size:12px;color:#666;margin-bottom:12px;">Clique em um dia para ver e liberar plantões para pagamento.</p>
                <div id="cal-wrapper"></div>
            </div>
        </div>
        
        <!-- PAGAMENTOS -->
        <div class="screen" id="screen-pagamentos">
            <div class="card">
                <h2>💰 Relatório de Pagamentos</h2>
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
                <label style="display:flex;align-items:center;gap:6px;font-size:12px;margin-top:8px;">
                    <input type="checkbox" id="tab-pagos" onchange="renderTab()">
                    Mostrar pagos também
                </label>
            </div>
            
            <div class="card">
                <div style="display:flex;justify-content:space-between;align-items:center;">
                    <div>
                        <div style="font-size:11px;color:#666;">Total selecionado</div>
                        <div style="font-size:20px;font-weight:600;color:var(--success);">R$0</div>
                    </div>
                    <button class="btn btn-success btn-sm" onclick="pagarSelecionados()">Processar</button>
                </div>
            </div>
            
            <div id="tab-lista"></div>
        </div>
        
        <!-- CADASTROS -->
        <div class="screen" id="screen-cadastros">
            <div class="card">
                <h2>Tipos de Plantão</h2>
                <div class="row2">
                    <div class="field" style="margin-bottom:0;">
                        <label>Nome</label>
                        <input id="cad-tn" placeholder="Ex: Plantão dia">
                    </div>
                    <div class="field" style="margin-bottom:0;">
                        <label>Valor R$</label>
                        <input id="cad-tv" type="number" placeholder="0">
                    </div>
                </div>
                <button class="btn btn-primary" style="margin-top:10px;" onclick="addTipo()">Adicionar tipo</button>
                <div id="lst-tipos" style="margin-top:12px;"></div>
            </div>
            
            <div class="card">
                <h2>Funcionários</h2>
                <div class="row2">
                    <div class="field" style="margin-bottom:0;">
                        <label>Nome</label>
                        <input id="cad-fn" placeholder="Nome">
                    </div>
                    <div class="field" style="margin-bottom:0;">
                        <label>Cargo</label>
                        <input id="cad-fc" placeholder="Cargo">
                    </div>
                </div>
                <button class="btn btn-primary" style="margin-top:10px;" onclick="addFunc()">Adicionar</button>
                <div id="lst-func" style="margin-top:12px;"></div>
            </div>
        </div>
    </div>
    
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script>
        // CONFIGURAÇÃO — MUDE AQUI
        var SHEET_ID = "1TVYsc9GnaK_T1YILkdgBOJSyDA4CZbEyvzk47Izr-go"
        
        var db = {
            tipos: [
                { nome: "Dia (12h)", valor: 180 },
                { nome: "Noite (12h)", valor: 220 },
                { nome: "24h", valor: 380 }
            ],
            funcionarios: [
                { nome: "Maria Silva", cargo: "Cuidadora" },
                { nome: "João Santos", cargo: "Técnico" }
            ],
            plantoes: [],
            nextId: 1
        };
        
        var hoje = new Date();
        
        // FUNÇÕES PRINCIPAIS
        function show(s) {
            document.querySelectorAll(".screen").forEach(el => el.classList.remove("active"));
            document.querySelector("#screen-" + s).classList.add("active");
            document.querySelectorAll(".nav button").forEach(el => el.classList.remove("active"));
            event.target.classList.add("active");
            
            if (s === "checkin") { resetGate(); populateCI(); renderRec(); }
            if (s === "enfermeira") { populateEnf(); renderEnf(); }
            if (s === "pagamentos") { initTabDates(); renderTab(); }
            if (s === "cadastros") { renderCad(); }
        }
        
        function resetGate() {
            document.getElementById("ci-gate").style.display = "block";
            document.getElementById("ci-aviso").style.display = "none";
            document.getElementById("ci-form").style.display = "none";
        }
        
        function ciGate(sim) {
            document.getElementById("ci-gate").style.display = "none";
            if (sim) {
                document.getElementById("ci-form").style.display = "block";
            } else {
                document.getElementById("ci-aviso").style.display = "block";
            }
        }
        
        function toast(msg, type = "success") {
            var el = document.getElementById("toast-ci");
            el.textContent = msg;
            el.className = "toast show " + type;
            setTimeout(() => el.className = "toast", 3000);
        }
        
        function populateCI() {
            var fs = document.getElementById("ci-func");
            fs.innerHTML = '<option value="">Selecione...</option>';
            db.funcionarios.forEach(f => {
                var opt = document.createElement("option");
                opt.value = f.nome;
                opt.textContent = f.nome;
                fs.appendChild(opt);
            });
            
            var ts = document.getElementById("ci-tipo");
            ts.innerHTML = '<option value="">Selecione...</option>';
            db.tipos.forEach(t => {
                var opt = document.createElement("option");
                opt.value = t.nome;
                opt.textContent = t.nome + " — R$" + t.valor;
                ts.appendChild(opt);
            });
        }
        
        function onTipoChange() {
            var campo = document.getElementById("campo-hosp");
            // Mostrar campo hóspede apenas para tipos específicos
            campo.style.display = "none";
        }
        
        function fazerCheckin() {
            var func = document.getElementById("ci-func").value;
            var tipo = document.getElementById("ci-tipo").value;
            
            if (!func || !tipo) {
                toast("Preencha todos os campos!", "error");
                return;
            }
            
            var t = db.tipos.find(x => x.nome === tipo);
            db.plantoes.unshift({
                id: db.nextId++,
                func: func,
                tipo: tipo,
                data: hoje.toLocaleDateString("pt-BR"),
                hora: hoje.toLocaleTimeString("pt-BR", { hour: "2-digit", minute: "2-digit" }),
                valor: t.valor,
                status: "pendente"
            });
            
            document.getElementById("ci-func").value = "";
            document.getElementById("ci-tipo").value = "";
            toast("Check-in registrado!");
            renderRec();
        }
        
        function renderRec() {
            var el = document.getElementById("lista-rec");
            var r = db.plantoes.slice(0, 4);
            
            if (!r.length) {
                el.innerHTML = '<p style="font-size:12px;color:#666;">Nenhum registro.</p>';
                return;
            }
            
            el.innerHTML = r.map(p => `
                <div class="item">
                    <div class="item-head">
                        <span class="item-name">${p.func}</span>
                        <span class="badge badge-${p.status === "pendente" ? "warn" : "ok"}">${p.status}</span>
                    </div>
                    <div class="item-sub">${p.tipo} · ${p.hora} · ${p.data}</div>
                </div>
            `).join("");
        }
        
        function populateEnf() {
            // Adicionar lista de aprovadores se necessário
        }
        
        function renderEnf() {
            var el = document.getElementById("lista-enf");
            var pend = db.plantoes.filter(p => p.status === "pendente");
            
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
            `).join("");
        }
        
        function aprovar(id) {
            db.plantoes.forEach(p => {
                if (p.id === id) p.status = "aprovado";
            });
            renderEnf();
        }
        
        function rejeitar(id) {
            db.plantoes.forEach(p => {
                if (p.id === id) p.status = "rejeitado";
            });
            renderEnf();
        }
        
        function initTabDates() {
            var de = document.getElementById("tab-de");
            var ate = document.getElementById("tab-ate");
            if (!de.value) {
                var y = hoje.getFullYear();
                var m = String(hoje.getMonth() + 1).padStart(2, "0");
                de.value = y + "-" + m + "-01";
                ate.value = hoje.toISOString().split("T")[0];
            }
        }
        
        function renderTab() {
            var el = document.getElementById("tab-lista");
            var lista = db.plantoes.filter(p => p.status === "aprovado");
            
            if (!lista.length) {
                el.innerHTML = '<div class="card"><p style="font-size:12px;color:#666;">Nenhum plantão aprovado.</p></div>';
                return;
            }
            
            var html = "";
            lista.forEach(p => {
                html += `
                    <div class="card">
                        <div style="display:flex;justify-content:space-between;align-items:center;">
                            <div>
                                <div class="item-name">${p.func}</div>
                                <div class="item-sub">${p.data} · ${p.tipo}</div>
                            </div>
                            <div style="text-align:right;">
                                <div style="font-size:14px;font-weight:600;color:var(--success);">R$${p.valor}</div>
                                <button class="btn btn-success btn-sm" onclick="marcarPago(${p.id})">Pagar</button>
                            </div>
                        </div>
                    </div>
                `;
            });
            
            el.innerHTML = html;
        }
        
        function marcarPago(id) {
            db.plantoes.forEach(p => {
                if (p.id === id) p.status = "pago";
            });
            renderTab();
        }
        
        function pagarSelecionados() {
            alert("Plantões marcados como pagos!");
        }
        
        function renderCad() {
            document.getElementById("lst-tipos").innerHTML = db.tipos.map((t, i) => `
                <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;border-bottom:1px solid var(--border);">
                    <div>
                        <div class="item-name">${t.nome}</div>
                        <div class="item-sub">R$ ${t.valor}</div>
                    </div>
                    <button onclick="db.tipos.splice(${i},1);renderCad();" style="background:var(--danger);color:white;border:none;padding:4px 8px;border-radius:4px;cursor:pointer;font-size:12px;">Deletar</button>
                </div>
            `).join("");
            
            document.getElementById("lst-func").innerHTML = db.funcionarios.map((f, i) => `
                <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;border-bottom:1px solid var(--border);">
                    <div>
                        <div class="item-name">${f.nome}</div>
                        <div class="item-sub">${f.cargo}</div>
                    </div>
                    <button onclick="db.funcionarios.splice(${i},1);renderCad();" style="background:var(--danger);color:white;border:none;padding:4px 8px;border-radius:4px;cursor:pointer;font-size:12px;">Deletar</button>
                </div>
            `).join("");
        }
        
        function addTipo() {
            var n = document.getElementById("cad-tn").value.trim();
            var v = parseInt(document.getElementById("cad-tv").value) || 0;
            if (!n) return;
            db.tipos.push({ nome: n, valor: v });
            document.getElementById("cad-tn").value = "";
            document.getElementById("cad-tv").value = "";
            renderCad();
        }
        
        function addFunc() {
            var n = document.getElementById("cad-fn").value.trim();
            var c = document.getElementById("cad-fc").value.trim();
            if (!n) return;
            db.funcionarios.push({ nome: n, cargo: c || "—" });
            document.getElementById("cad-fn").value = "";
            document.getElementById("cad-fc").value = "";
            renderCad();
        }
        
        // Inicializar
        populateCI();
        renderRec();
        renderCad();
    </script>
</body>
</html>
