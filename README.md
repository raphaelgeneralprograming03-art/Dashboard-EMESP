
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EMESP - Sistema Embarcado de Alta Precisão | Visão Geral</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkbg: '#0a0e17',
                        cardbg: '#111827',
                        bordercolor: '#1f2937',
                        accentgreen: '#10b981',
                        accentcyan: '#06b6d4',
                        accentamber: '#f59e0b',
                        accentred: '#ef4444'
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome para Ícones -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .font-mono {
            font-family: 'JetBrains Mono', monospace;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0e17;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2937;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #374151;
        }
    </style>
</head>
<body class="bg-darkbg text-gray-100 min-h-screen flex flex-col selection:bg-cyan-500 selection:text-black">

    <!-- Header / Navbar Superior -->
    <header class="bg-cardbg border-b border-bordercolor px-6 py-4 flex items-center justify-between sticky top-0 z-50 shadow-lg">
        <div class="flex items-center space-x-4">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-cyan-600 to-emerald-500 flex items-center justify-center shadow-lg shadow-cyan-500/20">
                <i class="fa-solid fa-microchip text-white text-xl"></i>
            </div>
            <div>
                <div class="flex items-center space-x-2">
                    <h1 class="font-bold text-lg tracking-wider text-white">EMESP <span class="text-cyan-400 text-xs px-2 py-0.5 rounded bg-cyan-950 border border-cyan-800">v4.8 Core</span></h1>
                </div>
                <p class="text-xs text-gray-400">Sistema Embarcado de Alta Precisão — Telemetria e Diagnóstico Tático</p>
            </div>
        </div>

        <!-- Status Globais do Sistema -->
        <div class="hidden md:flex items-center space-x-6 text-xs font-mono">
            <div class="flex items-center space-x-2 bg-darkbg px-3 py-1.5 rounded-lg border border-bordercolor">
                <span class="w-2.5 h-2.5 rounded-full bg-emerald-500 animate-pulse"></span>
                <span class="text-gray-300">NÚCLEOS IA: <strong class="text-emerald-400">ONLINE</strong></span>
            </div>
            <div class="flex items-center space-x-2 bg-darkbg px-3 py-1.5 rounded-lg border border-bordercolor">
                <span class="w-2.5 h-2.5 rounded-full bg-cyan-500"></span>
                <span class="text-gray-300">LINK COFDM: <strong class="text-cyan-400">99.8%</strong></span>
            </div>
            <div class="flex items-center space-x-2 bg-darkbg px-3 py-1.5 rounded-lg border border-bordercolor">
                <i class="fa-solid fa-temperature-three-quarters text-amber-400"></i>
                <span class="text-gray-300">TEMP: <strong id="global-temp" class="text-amber-400">42.5°C</strong></span>
            </div>
            <div class="flex items-center space-x-2 bg-darkbg px-3 py-1.5 rounded-lg border border-bordercolor">
                <i class="fa-solid fa-bolt text-cyan-400"></i>
                <span class="text-gray-300">BARRAMENTO: <strong class="text-cyan-400">24.0V CC</strong></span>
            </div>
        </div>

        <div class="flex items-center space-x-3">
            <button onclick="toggleSystemMode()" id="mode-btn" class="px-4 py-2 text-xs font-semibold rounded-lg bg-emerald-600 hover:bg-emerald-500 text-white transition shadow-lg shadow-emerald-600/20 flex items-center space-x-2">
                <i class="fa-solid fa-play" id="mode-icon"></i>
                <span id="mode-text">SISTEMA ATIVO</span>
            </button>
        </div>
    </header>

    <!-- Corpo Principal -->
    <main class="flex-1 p-6 grid grid-cols-1 lg:grid-cols-12 gap-6 max-w-[1700px] w-full mx-auto">
        
        <!-- Coluna Esquerda: Componentes de Hardware & Controle Interativo (4 Colunas) -->
        <section class="lg:col-span-4 flex flex-col space-y-6">
            <div class="bg-cardbg border border-bordercolor rounded-2xl p-5 shadow-xl flex flex-col h-[calc(100vh-140px)]">
                <div class="flex items-center justify-between pb-4 border-b border-bordercolor">
                    <h2 class="font-semibold text-sm tracking-wide text-gray-200 flex items-center space-x-2">
                        <i class="fa-solid fa-server text-cyan-400"></i>
                        <span>ARQUITETURA DE HARDWARE EMESP</span>
                    </h2>
                    <span class="text-xs font-mono bg-darkbg px-2.5 py-1 rounded-md text-cyan-400 border border-bordercolor">6 Módulos</span>
                </div>

                <!-- Lista de Componentes Estilizada -->
                <div class="flex-1 overflow-y-auto pr-1 space-y-3 mt-4" id="component-list">
                    <!-- Gerado via JavaScript -->
                </div>
            </div>
        </section>

        <!-- Coluna Central/Direita: Canvas Dinâmico e Gráficos de Telemetria (8 Colunas) -->
        <div class="lg:col-span-8 flex flex-col space-y-6">
            
            <!-- Grid Superior com Canvas 2D Principal e Radar/Gimbal -->
            <div class="grid grid-cols-1 md:grid-cols-12 gap-6">
                
                <!-- Canvas 2D Telemetria Visual & Person Re-ID (8 Colunas) -->
                <div class="md:col-span-8 bg-cardbg border border-bordercolor rounded-2xl p-5 shadow-xl flex flex-col">
                    <div class="flex items-center justify-between mb-3">
                        <div class="flex items-center space-x-2">
                            <span class="w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                            <h3 class="text-xs font-semibold tracking-wider text-gray-300 uppercase">Visão Computacional & Matriz Homográfica (IA)</h3>
                        </div>
                        <div class="flex space-x-1.5">
                            <span class="text-[10px] font-mono px-2 py-0.5 rounded bg-cyan-950 text-cyan-300 border border-cyan-800">JETSON ORIN</span>
                            <span class="text-[10px] font-mono px-2 py-0.5 rounded bg-emerald-950 text-emerald-300 border border-emerald-800">60 FPS</span>
                        </div>
                    </div>
                    
                    <div class="relative w-full aspect-[16/10] bg-darkbg rounded-xl overflow-hidden border border-bordercolor shadow-inner">
                        <canvas id="visionCanvas" class="w-full h-full block cursor-crosshair"></canvas>
                        <div class="absolute bottom-3 left-3 bg-darkbg/80 backdrop-blur-md px-3 py-1.5 rounded-lg border border-bordercolor text-[11px] font-mono flex items-center space-x-3 pointer-events-none">
                            <span class="text-emerald-400">● ALVOS DETECTADOS: <strong id="target-count" class="text-white">3</strong></span>
                            <span class="text-gray-400">|</span>
                            <span class="text-cyan-400">LATÊNCIA: <strong class="text-white">4.2ms</strong></span>
                        </div>
                    </div>
                </div>

                <!-- Painel de Controle Pan/Tilt & Encoders (4 Colunas) -->
                <div class="md:col-span-4 bg-cardbg border border-bordercolor rounded-2xl p-5 shadow-xl flex flex-col justify-between">
                    <div>
                        <h3 class="text-xs font-semibold tracking-wider text-gray-300 uppercase mb-4 flex items-center space-x-2">
                            <i class="fa-solid fa-compass text-amber-400"></i>
                            <span>Posicionamento & Eixos Servo</span>
                        </h3>

                        <!-- Indicadores Angulares -->
                        <div class="space-y-4 font-mono text-xs">
                            <div class="bg-darkbg p-3 rounded-xl border border-bordercolor">
                                <div class="flex justify-between text-gray-400 mb-1">
                                    <span>EIXO PAN (AZIMUTE)</span>
                                    <span id="pan-val" class="text-cyan-400 font-bold">142.5°</span>
                                </div>
                                <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden">
                                    <div id="pan-bar" class="bg-cyan-500 h-full transition-all duration-150" style="width: 45%;"></div>
                                </div>
                            </div>

                            <div class="bg-darkbg p-3 rounded-xl border border-bordercolor">
                                <div class="flex justify-between text-gray-400 mb-1">
                                    <span>EIXO TILT (ELEVAÇÃO)</span>
                                    <span id="tilt-val" class="text-emerald-400 font-bold">-18.2°</span>
                                </div>
                                <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden">
                                    <div id="tilt-bar" class="bg-emerald-500 h-full transition-all duration-150" style="width: 60%;"></div>
                                </div>
                            </div>

                            <div class="bg-darkbg p-3 rounded-xl border border-bordercolor">
                                <div class="flex justify-between text-gray-400 mb-1">
                                    <span>ENCODER ÓPTICO (14-BITS)</span>
                                    <span class="text-amber-400 font-bold">16384 CPR</span>
                                </div>
                                <div class="text-[10px] text-gray-400 mt-1">Feedback de malha fechada FOC ativado em tempo real.</div>
                            </div>
                        </div>
                    </div>

                    <!-- Controles Manuais do Gimbal -->
                    <div class="mt-4 pt-4 border-t border-bordercolor">
                        <span class="text-[11px] font-medium text-gray-400 uppercase tracking-wider block mb-2">Comando Manual Rápido</span>
                        <div class="grid grid-cols-3 gap-2 text-center text-xs">
                            <button onclick="adjustGimbal('up')" class="bg-darkbg hover:bg-gray-800 border border-bordercolor py-2 rounded-lg transition active:bg-cyan-900"><i class="fa-solid fa-chevron-up"></i></button>
                            <button onclick="adjustGimbal('center')" class="bg-darkbg hover:bg-gray-800 border border-bordercolor py-2 rounded-lg transition text-cyan-400 font-bold">HOME</button>
                            <button onclick="adjustGimbal('down')" class="bg-darkbg hover:bg-gray-800 border border-bordercolor py-2 rounded-lg transition active:bg-cyan-900"><i class="fa-solid fa-chevron-down"></i></button>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Grid Inferior: Link COFDM & Logs de Sistema (Gráfico de Espectro / Telemetria) -->
            <div class="grid grid-cols-1 md:grid-cols-12 gap-6">
                
                <!-- Espectro COFDM e Link de Rádio (6 Colunas) -->
                <div class="md:col-span-6 bg-cardbg border border-bordercolor rounded-2xl p-5 shadow-xl flex flex-col">
                    <div class="flex items-center justify-between mb-3">
                        <h3 class="text-xs font-semibold tracking-wider text-gray-300 uppercase flex items-center space-x-2">
                            <i class="fa-solid fa-tower-broadcast text-emerald-400"></i>
                            <span>Módulo de Rádio COFDM (Link Criptografado)</span>
                        </h3>
                        <span class="text-[10px] font-mono text-emerald-400 bg-emerald-950 px-2 py-0.5 rounded border border-emerald-800">AES-256</span>
                    </div>
                    <div class="relative w-full h-36 bg-darkbg rounded-xl overflow-hidden border border-bordercolor">
                        <canvas id="cofdmCanvas" class="w-full h-full block"></canvas>
                    </div>
                    <div class="grid grid-cols-3 gap-2 mt-3 text-center text-xs font-mono">
                        <div class="bg-darkbg p-2 rounded-lg border border-bordercolor">
                            <span class="text-gray-500 block text-[10px]">FREQUÊNCIA</span>
                            <strong class="text-gray-200">2.45 GHz</strong>
                        </div>
                        <div class="bg-darkbg p-2 rounded-lg border border-bordercolor">
                            <span class="text-gray-500 block text-[10px]">LARGURA DE BANDA</span>
                            <strong class="text-cyan-400">20 MHz</strong>
                        </div>
                        <div class="bg-darkbg p-2 rounded-lg border border-bordercolor">
                            <span class="text-gray-500 block text-[10px]">TAXA DE DADOS</span>
                            <strong class="text-emerald-400">48.2 Mbps</strong>
                        </div>
                    </div>
                </div>

                <!-- Logs de Diagnóstico & Segurança em Nível de Hardware (6 Colunas) -->
                <div class="md:col-span-6 bg-cardbg border border-bordercolor rounded-2xl p-5 shadow-xl flex flex-col">
                    <div class="flex items-center justify-between mb-3">
                        <h3 class="text-xs font-semibold tracking-wider text-gray-300 uppercase flex items-center space-x-2">
                            <i class="fa-solid fa-shield-halved text-cyan-400"></i>
                            <span>Telemetria & Criptografia Embarcada</span>
                        </h3>
                        <span class="text-[10px] font-mono text-gray-400">LOG EM TEMPO REAL</span>
                    </div>
                    <div id="log-container" class="flex-1 h-36 bg-darkbg rounded-xl p-3 font-mono text-[11px] overflow-y-auto space-y-1.5 border border-bordercolor shadow-inner">
                        <!-- Logs gerados dinamicamente via JS -->
                    </div>
                </div>

            </div>

        </div>

    </main>

    <!-- Modal de Detalhes do Componente -->
    <div id="component-modal" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cardbg border border-bordercolor rounded-2xl max-w-lg w-full p-6 shadow-2xl relative animate-in fade-in zoom-in duration-200">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-400 hover:text-white transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="flex items-center space-x-3 mb-4">
                <div id="modal-icon-bg" class="w-12 h-12 rounded-xl flex items-center justify-center text-xl text-white"></div>
                <div>
                    <h3 id="modal-title" class="font-bold text-base text-white"></h3>
                    <span id="modal-badge" class="text-xs font-mono px-2 py-0.5 rounded border"></span>
                </div>
            </div>
            <div class="space-y-3 text-xs font-mono">
                <div class="bg-darkbg p-3 rounded-xl border border-bordercolor">
                    <span class="text-gray-400 block text-[10px] mb-1">FUNÇÃO ESTRATÉGICA NO EMESP</span>
                    <p id="modal-desc" class="text-gray-200 text-sm font-sans"></p>
                </div>
                <div class="bg-darkbg p-3 rounded-xl border border-bordercolor flex justify-between items-center">
                    <span class="text-gray-400">QUANTIDADE DE INSTALAÇÃO</span>
                    <strong id="modal-qty" class="text-cyan-400 text-sm"></strong>
                </div>
                <div class="bg-darkbg p-3 rounded-xl border border-bordercolor flex justify-between items-center">
                    <span class="text-gray-400">STATUS OPERACIONAL</span>
                    <span class="text-emerald-400 flex items-center space-x-1.5 font-bold">
                        <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                        <span>OPERACIONAL / SEGURO</span>
                    </span>
                </div>
            </div>
            <div class="mt-6 flex justify-end">
                <button onclick="closeModal()" class="px-5 py-2 rounded-xl bg-cyan-600 hover:bg-cyan-500 text-white text-xs font-semibold transition">FECHAR</button>
            </div>
        </div>
    </div>

    <!-- Script de Simulação e Renderização -->
    <script>
        // Dados Estruturais do EMESP (Excluindo total e absolutamente custos ou orçamentos)
        const emespComponents = [
            {
                id: 1,
                name: "NVIDIA Jetson Orin AGX 64GB",
                function: "Processamento local de IA de alta densidade, execução de Person Re-ID em tempo real e cálculo vetorial da Matriz Homográfica.",
                qty: 1,
                icon: "fa-microchip",
                color: "from-emerald-600 to-teal-700",
                textColor: "text-emerald-400",
                borderColor: "border-emerald-800"
            },
            {
                id: 2,
                name: "Servomotor Brushless Coreless (24V)",
                function: "Atuador mecânico de alta velocidade e resposta dinâmica para os eixos de movimentação Pan e Tilt.",
                qty: 2,
                icon: "fa-gears",
                color: "from-cyan-600 to-blue-700",
                textColor: "text-cyan-400",
                borderColor: "border-cyan-800"
            },
            {
                id: 3,
                name: "Encoder Óptico Absoluto de 14-bits",
                function: "Leitura de posicionamento angular de alta precisão real e feedback contínuo de malha fechada.",
                qty: 2,
                icon: "fa-bullseye",
                color: "from-amber-600 to-orange-700",
                textColor: "text-amber-400",
                borderColor: "border-amber-800"
            },
            {
                id: 4,
                name: "Módulo de Rádio Transmissão COFDM",
                function: "Link de dados sem fio de alta resiliência e criptografia em nível de hardware para comunicação segura com o drone.",
                qty: 1,
                icon: "fa-satellite-dish",
                color: "from-indigo-600 to-purple-700",
                textColor: "text-indigo-400",
                borderColor: "border-indigo-800"
            },
            {
                id: 5,
                name: "Driver de Servo Industrial FOC (400Hz)",
                function: "Controle vetorial avançado orientado por campo magnético (FOC) dos motores com latência operacional ultrabaixa.",
                qty: 2,
                icon: "fa-wave-square",
                color: "from-rose-600 to-pink-700",
                textColor: "text-rose-400",
                borderColor: "border-rose-800"
            },
            {
                id: 6,
                name: "Estrutura Mecânica em Fibra de Carbono",
                function: "Chassi estrutural ultraleve de alta rigidez mecânica para acoplamento físico do gimbal e armação de proteção.",
                qty: 1,
                icon: "fa-shield",
                color: "from-slate-600 to-gray-700",
                textColor: "text-gray-300",
                borderColor: "border-gray-700"
            }
        ];

        // Estado do Sistema
        let isSystemActive = true;
        let panAngle = 142.5;
        let tiltAngle = -18.2;
        let targets = [
            { x: 120, y: 90, vx: 0.8, vy: 0.5, id: "ID-01 [ALVO SEGURO]", color: "#10b981" },
            { x: 300, y: 180, vx: -0.5, vy: 0.7, id: "ID-02 [RASTREAMENTO]", color: "#06b6d4" },
            { x: 220, y: 240, vx: 0.6, vy: -0.4, id: "ID-03 [PERSON RE-ID]", color: "#f59e0b" }
        ];

        // Inicializar Lista de Componentes na Interface
        function renderComponents() {
            const container = document.getElementById('component-list');
            container.innerHTML = '';
            emespComponents.forEach(comp => {
                container.innerHTML += `
                    <div onclick="openModal(${comp.id})" class="bg-darkbg hover:bg-gray-800/80 border border-bordercolor hover:border-cyan-500/50 p-3.5 rounded-xl cursor-pointer transition flex items-center justify-between group">
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-lg bg-gradient-to-tr ${comp.color} flex items-center justify-center text-white shadow">
                                <i class="fa-solid ${comp.icon}"></i>
                            </div>
                            <div>
                                <h4 class="text-xs font-semibold text-gray-200 group-hover:text-cyan-400 transition">${comp.name}</h4>
                                <p class="text-[11px] text-gray-400 line-clamp-1 mt-0.5">${comp.function}</p>
                            </div>
                        </div>
                        <div class="text-right pl-2">
                            <span class="text-[10px] font-mono px-2 py-0.5 rounded bg-gray-900 ${comp.textColor} border ${comp.borderColor}">QTD: ${comp.qty}</span>
                        </div>
                    </div>
                `;
            });
        }

        // Modal Handlers
        function openModal(id) {
            const comp = emespComponents.find(c => c.id === id);
            if (!comp) return;
            document.getElementById('modal-title').innerText = comp.name;
            document.getElementById('modal-desc').innerText = comp.function;
            document.getElementById('modal-qty').innerText = `${comp.qty} Unidade(s)`;
            document.getElementById('modal-badge').innerText = `MOD-0${comp.id} // EMESP`;
            document.getElementById('modal-badge').className = `text-xs font-mono px-2 py-0.5 rounded border ${comp.textColor} ${comp.borderColor}`;
            
            const iconBg = document.getElementById('modal-icon-bg');
            iconBg.className = `w-12 h-12 rounded-xl flex items-center justify-center text-xl text-white bg-gradient-to-tr ${comp.color} shadow-lg`;
            iconBg.innerHTML = `<i class="fa-solid ${comp.icon}"></i>`;

            document.getElementById('component-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('component-modal').classList.add('hidden');
        }

        // Alternar Estado do Sistema
        function toggleSystemMode() {
            isSystemActive = !isSystemActive;
            const btn = document.getElementById('mode-btn');
            const icon = document.getElementById('mode-icon');
            const text = document.getElementById('mode-text');

            if (isSystemActive) {
                btn.className = "px-4 py-2 text-xs font-semibold rounded-lg bg-emerald-600 hover:bg-emerald-500 text-white transition shadow-lg shadow-emerald-600/20 flex items-center space-x-2";
                icon.className = "fa-solid fa-play";
                text.innerText = "SISTEMA ATIVO";
                addLog("Sistema EMESP reativado com sucesso. Malha fechada FOC estabilizada.");
            } else {
                btn.className = "px-4 py-2 text-xs font-semibold rounded-lg bg-rose-600 hover:bg-rose-500 text-white transition shadow-lg shadow-rose-600/20 flex items-center space-x-2";
                icon.className = "fa-solid fa-pause";
                text.innerText = "SISTEMA EM PAUSA";
                addLog("Aviso: Sistema colocado em modo de espera manual.");
            }
        }

        // Logs Dinâmicos do Sistema
        const systemLogs = [
            "Jetson Orin AGX: Matriz Homográfica calculada a 60 FPS.",
            "Encoder Óptico 14-bits: Sincronização angular perfeita.",
            "Driver FOC: Corrente vetorial estável em 2.4A.",
            "Link COFDM: Taxa de erro de pacotes (PER) < 0.01%.",
            "Servomotor Brushless Coreless: Temperatura nominal (39.2°C)."
        ];

        function addLog(customText) {
            const container = document.getElementById('log-container');
            const time = new Date().toLocaleTimeString();
            const text = customText || systemLogs[Math.floor(Math.random() * systemLogs.length)];
            container.innerHTML += `<div class="text-gray-300"><span class="text-cyan-500">[${time}]</span> ${text}</div>`;
            container.scrollTop = container.scrollHeight;
            if (container.children.length > 25) {
                container.removeChild(container.firstChild);
            }
        }

        // Canvas 1: Visão Computacional / Matriz Homográfica (Jetson Orin Simulation)
        const visionCanvas = document.getElementById('visionCanvas');
        const vCtx = visionCanvas.getContext('2d');
        
        // Canvas 2: Espectro COFDM
        const cofdmCanvas = document.getElementById('cofdmCanvas');
        const cCtx = cofdmCanvas.getContext('2d');

        function resizeCanvas() {
            visionCanvas.width = visionCanvas.parentElement.clientWidth;
            visionCanvas.height = visionCanvas.parentElement.clientHeight;
            cofdmCanvas.width = cofdmCanvas.parentElement.clientWidth;
            cofdmCanvas.height = cofdmCanvas.parentElement.clientHeight;
        }

        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // Loop de Anulação e Desenho
        let waveOffset = 0;
        function animate() {
            if (isSystemActive) {
                // Atualizar ângulos aleatórios suaves
                panAngle += (Math.random() - 0.5) * 0.4;
                tiltAngle += (Math.random() - 0.5) * 0.3;
                document.getElementById('pan-val').innerText = panAngle.toFixed(1) + '°';
                document.getElementById('pan-bar').style.width = Math.min(100, Math.max(10, (panAngle + 180) / 3.6)) + '%';
                
                document.getElementById('tilt-val').innerText = tiltAngle.toFixed(1) + '°';
                document.getElementById('tilt-bar').style.width = Math.min(100, Math.max(10, (tiltAngle + 90) / 1.8)) + '%';

                // Temperatura flutuante
                const tempVal = 41 + Math.sin(Date.now() / 2000) * 2;
                document.getElementById('global-temp').innerText = tempVal.toFixed(1) + '°C';
            }

            // Renderizar Visão Computacional (Canvas 1)
            vCtx.fillStyle = '#070b12';
            vCtx.fillRect(0, 0, visionCanvas.width, visionCanvas.height);

            // Grade Homográfica Estilo Tático / Militar
            vCtx.strokeStyle = 'rgba(6, 182, 212, 0.12)';
            vCtx.lineWidth = 1;
            const gridSize = 35;
            for (let x = 0; x < visionCanvas.width; x += gridSize) {
                vCtx.beginPath(); vCtx.moveTo(x, 0); vCtx.lineTo(x, visionCanvas.height); vCtx.stroke();
            }
            for (let y = 0; y < visionCanvas.height; y += gridSize) {
                vCtx.beginPath(); vCtx.moveTo(0, y); vCtx.lineTo(visionCanvas.width, y); vCtx.stroke();
            }

            // Linhas de Mira do Gimbal
            vCtx.strokeStyle = 'rgba(16, 185, 129, 0.4)';
            vCtx.setLineDash([4, 4]);
            vCtx.beginPath();
            vCtx.moveTo(visionCanvas.width / 2, 0); vCtx.lineTo(visionCanvas.width / 2, visionCanvas.height);
            vCtx.moveTo(0, visionCanvas.height / 2); vCtx.lineTo(visionCanvas.width, visionCanvas.height / 2);
            vCtx.stroke();
            vCtx.setLineDash([]);

            // Atualizar e Desenhar Alvos de IA (Person Re-ID)
            if (isSystemActive) {
                targets.forEach(t => {
                    t.x += t.vx;
                    t.y += t.vy;
                    if (t.x < 30 || t.x > visionCanvas.width - 30) t.vx *= -1;
                    if (t.y < 30 || t.y > visionCanvas.height - 30) t.vy *= -1;

                    // Caixa delimitadora de IA (Bounding Box)
                    vCtx.strokeStyle = t.color;
                    vCtx.lineWidth = 2;
                    const bw = 55;
                    const bh = 85;
                    vCtx.strokeRect(t.x - bw/2, t.y - bh/2, bw, bh);

                    // Cantos da caixa tática
                    const cornerLen = 10;
                    vCtx.fillStyle = t.color;
                    // Superior esquerdo
                    vCtx.fillRect(t.x - bw/2, t.y - bh/2, cornerLen, 3);
                    vCtx.fillRect(t.x - bw/2, t.y - bh/2, 3, cornerLen);
                    // Superior direito
                    vCtx.fillRect(t.x + bw/2 - cornerLen, t.y - bh/2, cornerLen, 3);
                    vCtx.fillRect(t.x + bw/2 - 3, t.y - bh/2, 3, cornerLen);

                    // Rótulo do Alvo
                    vCtx.font = '10px "JetBrains Mono"';
                    vCtx.fillStyle = t.color;
                    vCtx.fillText(t.id, t.x - bw/2, t.y - bh/2 - 6);
                });
            }

            // Renderizar Espectro COFDM (Canvas 2)
            cCtx.fillStyle = '#070b12';
            cCtx.fillRect(0, 0, cofdmCanvas.width, cofdmCanvas.height);

            cCtx.strokeStyle = 'rgba(16, 185, 129, 0.2)';
            cCtx.lineWidth = 1;
            for (let y = 0; y < cofdmCanvas.height; y += 20) {
                cCtx.beginPath(); cCtx.moveTo(0, y); cCtx.lineTo(cofdmCanvas.width, y); cCtx.stroke();
            }

            cCtx.strokeStyle = '#10b981';
            cCtx.lineWidth = 2;
            cCtx.beginPath();
            waveOffset += 0.08;
            for (let x = 0; x < cofdmCanvas.width; x++) {
                const freq = 0.02;
                const amplitude = 25 + Math.sin(x * 0.01 + waveOffset * 2) * 10;
                const y = cofdmCanvas.height / 2 + Math.sin(x * freq + waveOffset) * amplitude + (Math.random() - 0.5) * 4;
                if (x === 0) cCtx.moveTo(x, y);
                else cCtx.lineTo(x, y);
            }
            cCtx.stroke();

            requestAnimationFrame(animate);
        }

        // Controles Manuais
        function adjustGimbal(dir) {
            if (dir === 'up') tiltAngle += 5;
            if (dir === 'down') tiltAngle -= 5;
            if (dir === 'center') { panAngle = 0; tiltAngle = 0; }
            addLog(`Comando manual executado no Gimbal: Ajuste de eixo aplicado.`);
        }

        // Inicialização Geral
        window.onload = function() {
            renderComponents();
            setInterval(() => {
                if (isSystemActive) addLog();
            }, 4000);
            animate();
        };
    </script>
</body>
</html>
