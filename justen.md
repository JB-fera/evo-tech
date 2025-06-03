import sys

# Banco de dados simulado (usuários cadastrados)
usuarios = {
    'gamer123': {'senha': 'senha123', 'nome': 'Carlos Gamer'},
    'proplayer': {'senha': 'pro2025', 'nome': 'Ana Pro'},
    'nostalgia90': {'senha': 'supermario', 'nome': 'João Retrô'}
}

# Usuário atualmente logado
usuario_logado = None

# Carrinho do usuário logado (dicionário com nome do jogo e quantidade)
carrinho = {}

# Dados do usuário para a compra
dados_entrega = {}

# Catálogo de jogos
jogos = [
    {"nome": "Elden Ring", "preço": 249.90},
    {"nome": "Cyberpunk 2077", "preço": 199.90},
    {"nome": "The Last of Us Part II", "preço": 229.90},
    {"nome": "God of War Ragnarok", "preço": 279.90},
]

def exibir_menu():
    print("\n=== E-commerce de Games Modernos ===")
    if usuario_logado:
        print(f"🔓 Logado como: {usuario_logado['nome']}")
        print("1. Ver catálogo de jogos")
        print("2. Ver carrinho")
        print("3. Logout")
    else:
        print("1. Login")
        print("2. Cadastrar novo usuário")
    print("0. Sair")

def login():
    global usuario_logado
    print("\n== Login ==")
    usuario = input("Usuário: ").strip()
    senha = input("Senha: ").strip()

    if usuario in usuarios and usuarios[usuario]['senha'] == senha:
        usuario_logado = {'usuario': usuario, 'nome': usuarios[usuario]['nome']}
        print(f"✅ Bem-vindo(a), {usuario_logado['nome']}!")
    else:
        print("❌ Usuário ou senha inválidos.")

def logout():
    global usuario_logado, carrinho, dados_entrega
    print(f"👋 Até logo, {usuario_logado['nome']}!")
    usuario_logado = None
    carrinho = {}  # limpa o carrinho no logout
    dados_entrega = {}

def cadastrar_usuario():
    print("\n== Cadastro de Novo Usuário ==")
    novo_usuario = input("Escolha um nome de usuário: ").strip()
    if novo_usuario in usuarios:
        print("⚠️ Esse nome de usuário já está em uso.")
        return
    nome = input("Seu nome completo: ").strip()
    senha = input("Crie uma senha: ").strip()

    usuarios[novo_usuario] = {'senha': senha, 'nome': nome}
    print("✅ Usuário cadastrado com sucesso!")
