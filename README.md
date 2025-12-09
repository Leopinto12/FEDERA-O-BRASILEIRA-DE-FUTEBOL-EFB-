<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>SUPERLIGA - Rede Social</title>
    <style>
        /* [Seção de Estilos CSS] (Mantidos, com pequenas adaptações) */
        body { margin: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #050b16; color: #ffffff; line-height: 1.6; }
        header { text-align: center; padding: 40px 20px 60px; background: linear-gradient(180deg, #06142e, #050b16); border-bottom: 3px solid #00ff96; }
        .logo { width: 180px; filter: drop-shadow(0 0 15px #00ff96); }
        h1 { margin-top: 15px; font-size: 2.8rem; text-transform: uppercase; letter-spacing: 3px; text-shadow: 0 0 15px #00ff96; color: #ffffff; }
        nav { display: flex; justify-content: center; gap: 40px; padding: 20px; background: #06142e; position: sticky; top: 0; z-index: 1000; border-bottom: 2px solid #00ff96; }
        nav a { color: #00ff96; text-decoration: none; font-size: 1.2rem; font-weight: bold; transition: 0.3s ease-in-out; padding: 5px 10px; border-radius: 5px; position: relative; }
        nav a:hover { color: #f2c94c; text-shadow: 0 0 10px #f2c94c; transform: scale(1.05); background: rgba(242, 201, 76, 0.1); }
        .container { width: 90%; max-width: 1200px; margin: 30px auto; padding: 0 10px; }
        .card { background: rgba(255,255,255,0.08); border: 1px solid rgba(0,255,150,0.5); padding: 25px; border-radius: 16px; margin-bottom: 35px; box-shadow: 0 0 15px rgba(0,255,150,0.3); transition: transform 0.3s ease; }
        .title { font-size: 2rem; margin-bottom: 20px; color: #00ff96; text-shadow: 0 0 10px #00ff96; border-bottom: 2px dashed rgba(0,255,150,0.4); padding-bottom: 10px; }
        table { width: 100%; border-collapse: collapse; margin-top: 15px; font-size: 1.05rem; }
        th, td { padding: 15px; text-align: center; border-bottom: 1px solid rgba(255,255,255,0.15); }
        th { background: rgba(0,255,150,0.25); color: #ffffff; font-size: 1.15rem; text-transform: uppercase; }
        tr:nth-child(even) { background: rgba(255,255,255,0.02); }
        tr:hover { background: rgba(0,255,150,0.1); cursor: pointer; }
        .team-link { cursor: pointer; color: #f2c94c; font-weight: bold; text-shadow: 0 0 3px #f2c94c; transition: color 0.2s; }
        .action-button { width: 100%; padding: 15px; background: #00ff96; border: none; border-radius: 10px; margin-top: 5px; font-size: 1.1rem; font-weight: bold; color: #050b16; box-shadow: 0 0 15px #00ff96; cursor: pointer; transition: background 0.3s, transform 0.2s; }
        .link-switch { color:#f2c94c; text-decoration:none; cursor: pointer; font-weight: bold; transition: color 0.2s; }

        /* Estilo dos Posts e Formulário de Publicação */
        .post { background: #0a1324; border: 1px solid rgba(255,255,255,0.1); padding: 20px; border-radius: 10px; margin-bottom: 15px; }
        .post-header { display: flex; align-items: center; margin-bottom: 10px; }
        .post-author { font-weight: bold; color: #00ff96; margin-right: 10px; }
        .post-date { font-size: 0.8em; color: #999; }
        .post-content { color: #ccc; }
        #post-form textarea { width: 96%; padding: 10px; background: #0a1324; border: 1px solid #00ff96; border-radius: 8px; color: white; resize: vertical; min-height: 80px; }

        /* Modal de Login/Cadastro/Perfil/Admin (Mantido) */
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; overflow-y: auto; background: rgba(5, 11, 22, 0.95); z-index: 9999; padding-bottom: 60px; backdrop-filter: blur(5px); }
        .login-box { background:rgba(255,255,255,0.05); border:1px solid #00ff96; width:85%; max-width:420px; margin:auto; padding:35px; border-radius:14px; box-shadow:0 0 25px rgba(0,255,150,0.4); }
        .login-input { width:90%; padding:15px; background:#0a1324; border:1px solid #00ff96; border-radius:8px; color:white; margin-bottom:20px; font-size: 1rem; }
    </style>
</head>
<body>
    <header>
        <img src="A_logo_for_\"SUPERLIGA\"_is_presented_in_a_digital_v.png" class="logo" alt="Logo Superliga" />
        <h1>SUPERLIGA BRASILEIRA</h1>
        <button onclick="openLogin()" id="header-login-button" style="margin-top: 20px; padding: 10px 20px; background: #f2c94c; border: none; border-radius: 8px; font-weight: bold; color: #050b16; cursor: pointer; box-shadow: 0 0 10px #f2c94c; transition: background 0.3s;">
            ACESSAR CONTA
        </button>
        <button onclick="openAdminPanel()" id="admin-panel-button" style="display:none; margin-top: 20px; padding: 10px 20px; background: #ff004c; border: none; border-radius: 8px; font-weight: bold; color: #ffffff; cursor: pointer; box-shadow: 0 0 10px #ff004c; margin-left: 10px; transition: background 0.3s;">
            PAINEL ADMIN
        </button>
    </header>

    <nav>
        <a href="#feed">Feed</a>
        <a href="#series">Séries A e B</a>
        <a href="#times">Times Cadastrados</a>
        <a href="#" onclick="openLogin()">Login/Cadastro</a>
    </nav>

    <div class="container" id="feed">
        <div class="card">
            <div class="title">📸 Feed Oficial</div>

            <div id="post-form-container" style="display:none; margin-bottom: 30px; padding: 15px; background: #06142e; border-radius: 10px; border: 1px solid #f2c94c;">
                <h3 style="color:#f2c94c;">O que está acontecendo na Superliga?</h3>
                <textarea id="post-input" placeholder="Publique uma notícia ou atualização do seu time..." maxlength="300"></textarea>
                <button onclick="publishPost()" class="action-button" style="width: auto; padding: 10px 20px; margin-top: 10px;">Publicar</button>
            </div>

            <div id="feed-posts">
                </div>
        </div>
    </div>

    <div class="container" id="series">
        <div class="card">
            <div class="title">🏆 Série A — Classificação</div>
            <p id="series-a-status">Nenhum time na Série A.</p>
            <table id="tabela-serie-a" style="display:none;">
                <tr>
                    <th>Time</th>
                    <th>Pontos</th>
                    <th>Vitórias</th>
                    <th>Saldo</th>
                </tr>
            </table>
        </div>

        <div class="card">
            <div class="title">💠 Série B — Classificação</div>
            <p id="series-b-status">Nenhum time na Série B.</p>
            <table id="tabela-serie-b" style="display:none;">
                <tr>
                    <th>Time</th>
                    <th>Pontos</th>
                    <th>Vitórias</th>
                    <th>Saldo</th>
                </tr>
            </table>
        </div>
    </div>

    <div class="container" id="times">
        <div class="card">
            <div class="title">🛡️ Times Cadastrados</div>
            <div id="times-list">
                <p>Nenhum time cadastrado além do administrador.</p>
            </div>
        </div>
    </div>

    <div class="container" id="jogadores" style="display:none;">
        </div>

    <footer>
        SUPERLIGA © 2025 — O Campeonato Futurista do Brasil
    </footer>

<div id="perfil-time" class="modal">
    <div class="modal-header">
        <img id="perfil-time-logo" src="" class="modal-logo" alt="Logo do Time" />
        <h2 id="perfil-time-nome" style="margin-top:15px; font-size:2rem; color:white; text-shadow:0 0 10px #000;"></h2>
        <p id="perfil-time-serie" style="color:#f2c94c; font-weight: bold;"></p>
    </div>

    <div class="modal-content">
        <div class="modal-card">
            <h3 class="modal-title">📊 Estatísticas</h3>
            <div id="perfil-time-stats">Nenhuma estatística disponível.</div>
        </div>

        <div class="modal-card">
            <h3 class="modal-title">📰 Posts Recentes</h3>
            <div id="perfil-time-feed">Nenhum post deste time.</div>
        </div>

        <button onclick="closePerfilTime()" class="action-button">Voltar à Liga</button>
    </div>
</div>

<div id="login" class="modal" style="padding-top:120px; text-align:center;">
    <div class="login-box">
        <img src="A_logo_for_\"SUPERLIGA\"_is_presented_in_a_digital_v.png" style="width:140px; filter:drop-shadow(0 0 10px #00ff96); margin-bottom:20px;" alt="Logo Superliga" />
        <h2 style="color:#00ff96; text-shadow:0 0 10px #00ff96; margin-bottom:25px;">ACESSO DE MEMBRO</h2>

        <input type="text" placeholder="Usuário/E-mail" id="login-user" class="login-input" />
        <input type="password" placeholder="Senha" id="login-pass" class="login-input" />

        <button onclick="fazerLogin()" class="action-button">ENTRAR</button>

        <p style="font-size:0.9rem; margin-top:20px; color: #ccc;">
            Ainda não tem conta? <a class="link-switch" onclick="openRegister()">Cadastre-se aqui</a>.
        </p>
        <button onclick="closeLogin()" style="padding: 10px 20px; background: transparent; border: 1px solid #00ff96; border-radius: 8px; font-weight: bold; color: #00ff96; cursor: pointer; margin-top: 15px; transition: background 0.3s;">
            Cancelar
        </button>
    </div>
</div>

<div id="register" class="modal" style="padding-top:120px; text-align:center;">
    <div class="login-box">
        <img src="A_logo_for_\"SUPERLIGA\"_is_presented_in_a_digital_v.png" style="width:140px; filter:drop-shadow(0 0 10px #00ff96); margin-bottom:20px;" alt="Logo Superliga" />
        <h2 style="color:#00ff96; text-shadow:0 0 10px #00ff96; margin-bottom:25px;">CADASTRO DE NOVO TIME</h2>

        <input type="text" placeholder="Nome do Time (Será seu Nome de Usuário)" id="register-user" class="login-input" />
        <input type="email" placeholder="E-mail do Responsável" id="register-email" class="login-input" />
        <input type="password" placeholder="Senha (Mínimo 6 caracteres)" id="register-pass" class="login-input" />

        <button onclick="fazerCadastro()" class="action-button">CADASTRAR TIME</button>

        <p style="font-size:0.9rem; margin-top:20px; color: #ccc;">
            Já é membro? <a class="link-switch" onclick="openLogin()">Voltar ao Login</a>.
        </p>
        <button onclick="closeRegister()" style="padding: 10px 20px; background: transparent; border: 1px solid #00ff96; border-radius: 8px; font-weight: bold; color: #00ff96; cursor: pointer; margin-top: 15px; transition: background 0.3s;">
            Cancelar
        </button>
    </div>
</div>

<div id="admin-panel" class="modal" style="padding-top:60px;">
    <div class="modal-content">
        <div class="card">
            <h2 class="title" style="border-color: #ff004c;">⚙️ PAINEL DE ADMINISTRAÇÃO</h2>
            <p style="color: #ff004c; font-weight: bold;">Gerencie a alocação dos times nas Séries A e B.</p>

            <div id="admin-teams-list">
                </div>

            <button onclick="closeAdminPanel()" class="action-button" style="background: #ff004c;">Fechar Painel</button>
        </div>
    </div>
</div>

<script>
    // Usuário logado atual
    let loggedInUser = null;

    // --- Data Storage (Simulação de DB com localStorage) ---
    // Estrutura de times/usuários
    let usuariosCadastrados = JSON.parse(localStorage.getItem('superligaUsers')) || {
        'admin': { email: 'admin@superliga.br', senha: '123', isAdmin: true, teamName: 'Administrador', series: null, stats: null, logo: null }
    };

    // Estrutura de posts
    let posts = JSON.parse(localStorage.getItem('superligaPosts')) || [
        { author: 'admin', content: 'Bem-vindo à nova SUPERLIGA! Cadastre seu time e aguarde a aprovação do admin para entrar nas Séries A ou B!', date: new Date().toLocaleDateString('pt-BR') }
    ];

    // --- Funções de Ajuda ---
    function saveUsers() {
        localStorage.setItem('superligaUsers', JSON.stringify(usuariosCadastrados));
    }
    function savePosts() {
        localStorage.setItem('superligaPosts', JSON.stringify(posts));
    }
    function getAllTeams() {
        // Retorna todos os usuários que não são o 'admin' e não têm status de 'isAdmin'
        return Object.keys(usuariosCadastrados)
            .filter(user => user !== 'admin' && !usuariosCadastrados[user].isAdmin)
            .map(user => ({ username: user, ...usuariosCadastrados[user] }));
    }

    // --- Funções de Renderização Inicial ---
    document.addEventListener('DOMContentLoaded', () => {
        renderFeed();
        renderClassificationTables();
        renderTeamsList();
    });

    function renderFeed() {
        const feedContainer = document.getElementById('feed-posts');
        feedContainer.innerHTML = ''; // Limpa o feed

        const sortedPosts = posts.sort((a, b) => new Date(b.date) - new Date(a.date)); // Ordena do mais novo para o mais antigo

        if (sortedPosts.length === 0) {
            feedContainer.innerHTML = '<p style="text-align:center; color:#999;">Ainda não há publicações no Feed.</p>';
            return;
        }

        sortedPosts.forEach(post => {
            const postElement = document.createElement('div');
            postElement.className = 'post';
            postElement.innerHTML = `
                <div class="post-header">
                    <span class="post-author">${post.author}</span>
                    <span class="post-date"> - ${post.date}</span>
                </div>
                <p class="post-content">${post.content}</p>
            `;
            feedContainer.appendChild(postElement);
        });
    }

    function renderClassificationTables() {
        const teams = getAllTeams().filter(team => team.series);
        const serieA = teams.filter(t => t.series === 'Série A').sort((a, b) => b.stats.Pontos - a.stats.Pontos);
        const serieB = teams.filter(t => t.series === 'Série B').sort((a, b) => b.stats.Pontos - a.stats.Pontos);

        const renderTable = (series, data) => {
            const tableElement = document.getElementById(`tabela-serie-${series.toLowerCase().replace('é', 'e')}`);
            const statusElement = document.getElementById(`series-${series.toLowerCase().replace('é', 'e')}-status`);
            const tbody = tableElement.tBodies.length ? tableElement.tBodies[0] : tableElement.createTBody();
            tbody.innerHTML = '';

            if (data.length === 0) {
                tableElement.style.display = 'none';
                statusElement.style.display = 'block';
                return;
            }

            tableElement.style.display = 'table';
            statusElement.style.display = 'none';

            data.forEach(team => {
                const row = tbody.insertRow();
                row.setAttribute('data-team', team.username);
                row.onclick = () => openPerfilTime(team.username);
                row.innerHTML = `
                    <td><span class="team-link">${team.teamName}</span></td>
                    <td>${team.stats.Pontos}</td>
                    <td>${team.stats.Vitórias}</td>
                    <td>${team.stats.Saldo}</td>
                `;
            });
        };

        renderTable('Série A', serieA);
        renderTable('Série B', serieB);
    }

    function renderTeamsList() {
        const listContainer = document.getElementById('times-list');
        listContainer.innerHTML = '';
        const teams = getAllTeams();

        if (teams.length === 0) {
            listContainer.innerHTML = '<p>Nenhum time cadastrado além do administrador.</p>';
            return;
        }

        teams.forEach(team => {
            const status = team.series ? `(${team.series})` : '(Aguardando alocação)';
            listContainer.innerHTML += `
                <p>
                    <span class="team-link" onclick="openPerfilTime('${team.username}')">
                        • ${team.teamName}
                    </span> ${status}
                </p>
            `;
        });
    }

    // --- Funções de Publicação ---
    function publishPost() {
        const input = document.getElementById('post-input');
        const content = input.value.trim();

        if (!loggedInUser) {
            alert('Você deve estar logado para publicar.');
            return;
        }

        if (content.length < 5) {
            alert('A publicação deve ter no mínimo 5 caracteres.');
            return;
        }

        const newPost = {
            author: usuariosCadastrados[loggedInUser].teamName, // Usa o nome do time/usuário logado
            content: content,
            date: new Date().toLocaleDateString('pt-BR')
        };

        posts.unshift(newPost); // Adiciona no início
        savePosts();
        input.value = ''; // Limpa o campo
        renderFeed();
        alert('Publicação enviada com sucesso!');
    }


    // --- Funções de Login/Cadastro/Logout ---
    function openLogin() {
        document.getElementById('register').style.display = 'none';
        document.getElementById('login').style.display = 'block';
        document.body.style.overflow = 'hidden';
    }

    function closeLogin() {
        document.getElementById('login').style.display = 'none';
        document.body.style.overflow = 'auto';
        document.getElementById('login-user').value = '';
        document.getElementById('login-pass').value = '';
    }

    function updateHeaderButtons(user) {
        const loginBtn = document.getElementById('header-login-button');
        const adminBtn = document.getElementById('admin-panel-button');

        if (user) {
            // Logado
            loginBtn.textContent = `LOGOUT (${usuariosCadastrados[user].teamName})`;
            loginBtn.onclick = fazerLogout;
            // Admin Check
            if (usuariosCadastrados[user].isAdmin) {
                adminBtn.style.display = 'inline-block';
            } else {
                adminBtn.style.display = 'none';
            }
            // Mostrar formulário de postagem
            document.getElementById('post-form-container').style.display = 'block';

        } else {
            // Deslogado
            loginBtn.textContent = 'ACESSAR CONTA';
            loginBtn.onclick = openLogin;
            adminBtn.style.display = 'none';
            document.getElementById('post-form-container').style.display = 'none';
        }
    }

    function fazerLogin() {
        const user = document.getElementById('login-user').value.trim();
        const pass = document.getElementById('login-pass').value.trim();

        const userFound = Object.keys(usuariosCadastrados).find(key => key === user || usuariosCadastrados[key].email === user);

        if (userFound && usuariosCadastrados[userFound].senha === pass) {
            loggedInUser = userFound;
            closeLogin();
            updateHeaderButtons(loggedInUser);
            alert(`✅ Login bem-sucedido! Bem-vindo(a), ${usuariosCadastrados[loggedInUser].teamName}.`);
        } else {
            alert('❌ Credenciais incorretas. Verifique seu Usuário/E-mail e Senha.');
        }
    }

    function fazerLogout() {
        loggedInUser = null;
        updateHeaderButtons(null);
        alert('Você foi desconectado(a) com sucesso.');
    }

    function fazerCadastro() {
        const user = document.getElementById('register-user').value.trim();
        const email = document.getElementById('register-email').value.trim();
        const pass = document.getElementById('register-pass').value.trim();

        if (!user || !email || !pass || pass.length < 6) {
            alert('🚨 Por favor, preencha todos os campos e use uma senha de no mínimo 6 caracteres.');
            return;
        }

        const isUserTaken = Object.keys(usuariosCadastrados).includes(user);
        const isEmailTaken = Object.values(usuariosCadastrados).some(u => u.email === email);

        if (isUserTaken) {
            alert('❌ Nome de time/usuário já cadastrado.');
            return;
        }
        if (isEmailTaken) {
            alert('❌ E-mail já cadastrado. Tente fazer login.');
            return;
        }

        // Novo Time/Usuário Padrão
        usuariosCadastrados[user] = {
            email: email,
            senha: pass,
            isAdmin: false,
            teamName: user, // Nome do Time é o nome de usuário
            series: null, // Começa sem Série
            logo: 'https://via.placeholder.com/130/06142e/00ff96?text=LOGO', // Logo Placeholder
            stats: { Pontos: 0, Vitórias: 0, Saldo: 0 } // Estatísticas iniciais
        };

        saveUsers();
        alert(`🎉 Time "${user}" cadastrado com sucesso! O administrador irá alocá-lo em uma Série em breve.`);
        closeRegister();
        openLogin();
    }

    // --- Funções de Perfil de Time (Visualização) ---
    function openPerfilTime(username) {
        const perfilModal = document.getElementById('perfil-time');
        const team = usuariosCadastrados[username];

        if (!team) {
            alert(`Dados do time ${username} não encontrados.`);
            return;
        }

        document.getElementById('perfil-time-nome').textContent = team.teamName;
        document.getElementById('perfil-time-logo').src = team.logo || 'https://via.placeholder.com/130/06142e/00ff96?text=LOGO';
        document.getElementById('perfil-time-serie').textContent = team.series ? `Série: ${team.series}` : 'Série: Aguardando Alocação';

        // Estatísticas
        let statsHtml = team.stats ? `
            <p>Pontos: <b>${team.stats.Pontos}</b></p>
            <p>Vitórias: <b>${team.stats.Vitórias}</b></p>
            <p>Saldo de Gols: <b>${team.stats.Saldo}</b></p>
        ` : 'Nenhuma estatística disponível.';
        document.getElementById('perfil-time-stats').innerHTML = statsHtml;

        // Feed do Time (filtra posts por autor)
        const teamPosts = posts.filter(post => post.author === team.teamName);
        let feedHtml = '';
        if (teamPosts.length > 0) {
            feedHtml = teamPosts.map(post =>
                `<div style="background:#0a1324; padding:10px; border-radius:8px; margin-bottom:10px; border:1px solid rgba(255,255,255,0.1);"><p style="font-size:0.9em;">${post.content}</p><p style="font-size:0.7em; color:#999; text-align:right;">${post.date}</p></div>`
            ).join('');
        } else {
            feedHtml = '<p style="color:#999;">Nenhum post recente deste time.</p>';
        }
        document.getElementById('perfil-time-feed').innerHTML = feedHtml;

        perfilModal.style.display = 'block';
        document.body.style.overflow = 'hidden';
    }

    function closePerfilTime() {
        document.getElementById('perfil-time').style.display = 'none';
        document.body.style.overflow = 'auto';
    }

    // --- Funções do Painel de Administração ---
    function openAdminPanel() {
        if (!loggedInUser || !usuariosCadastrados[loggedInUser].isAdmin) {
            alert('Acesso negado.');
            return;
        }

        renderAdminTeamList();
        document.getElementById('admin-panel').style.display = 'block';
        document.body.style.overflow = 'hidden';
    }

    function closeAdminPanel() {
        document.getElementById('admin-panel').style.display = 'none';
        document.body.style.overflow = 'auto';
        renderClassificationTables(); // Atualiza as tabelas após fechar o painel
        renderTeamsList();
    }

    function renderAdminTeamList() {
        const adminList = document.getElementById('admin-teams-list');
        adminList.innerHTML = '';
        const teams = getAllTeams();

        if (teams.length === 0) {
            adminList.innerHTML = '<p style="color:#ccc;">Não há times para gerenciar.</p>';
            return;
        }

        teams.forEach(team => {
            const currentSeries = team.series || 'Nenhuma';
            const teamElement = document.createElement('div');
            teamElement.style.cssText = 'background: #0a1324; padding: 15px; border-radius: 8px; margin-bottom: 10px; border-left: 5px solid #00ff96; display: flex; justify-content: space-between; align-items: center;';

            teamElement.innerHTML = `
                <div>
                    <strong style="color: #00ff96;">${team.teamName}</strong> (Usuário: ${team.username})
                    <p style="margin: 5px 0 0; font-size: 0.9em; color: #ccc;">Série Atual: <b>${currentSeries}</b></p>
                </div>
                <select id="select-${team.username}" onchange="changeTeamSeries('${team.username}', this.value)">
                    <option value="Nenhuma" ${currentSeries === 'Nenhuma' || !currentSeries ? 'selected' : ''}>Nenhuma</option>
                    <option value="Série A" ${currentSeries === 'Série A' ? 'selected' : ''}>Série A</option>
                    <option value="Série B" ${currentSeries === 'Série B' ? 'selected' : ''}>Série B</option>
                </select>
            `;
            adminList.appendChild(teamElement);
        });
    }

    function changeTeamSeries(username, newSeries) {
        if (newSeries === 'Nenhuma') {
            usuariosCadastrados[username].series = null;
        } else {
            usuariosCadastrados[username].series = newSeries;
        }
        saveUsers();
        alert(`Time ${usuariosCadastrados[username].teamName} alocado para ${newSeries}.`);
        renderAdminTeamList(); // Re-renderiza a lista para refletir a mudança
    }

</script>
</body>
</html>
