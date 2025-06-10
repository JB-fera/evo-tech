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

# Catálogo de jogos (com classificação e tamanho)
jogos = [
    {"nome": "Elden Ring", "preço": 249.90, "classificacao": "16+", "tamanho_gb": 50},
    {"nome": "Cyberpunk 2077", "preço": 199.90, "classificacao": "18+", "tamanho_gb": 70},
    {"nome": "The Last of Us Part II", "preço": 229.90, "classificacao": "18+", "tamanho_gb": 78},
    {"nome": "God of War Ragnarok", "preço": 279.90, "classificacao": "18+", "tamanho_gb": 90},
]

# ===== DADOS (login, cadastro e logout) =====
def exibir_menu():
    print("\n=== E-commerce de Games Modernos ===")
    if usuario_logado:
        print(f" Logado como: {usuario_logado['nome']}")
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
        print(f" Bem-vindo(a), {usuario_logado['nome']}!")
    else:
        print(" Usuário ou senha inválidos.")

def logout():
    global usuario_logado, carrinho, dados_entrega
    print(f" Até logo, {usuario_logado['nome']}!")
    usuario_logado = None
    carrinho.clear()  # limpa o carrinho no logout
    dados_entrega.clear()

def cadastrar_usuario():
    print("\n== Cadastro de Novo Usuário ==")
    novo_usuario = input("Escolha um nome de usuário: ").strip()
    if novo_usuario in usuarios:
        print("Esse nome de usuário já está em uso.")
        return
    nome = input("Seu nome completo: ").strip()
    senha = input("Crie uma senha: ").strip()

    usuarios[novo_usuario] = {'senha': senha, 'nome': nome}
    print("Usuário cadastrado com sucesso!")

# ===== CATÁLOGO =====
def ver_catalogo():
    print("\n Catálogo de Jogos Modernos:")
    for i, jogo in enumerate(jogos, 1):
        print(f"{i}. {jogo['nome']} - R$ {jogo['preço']:.2f} | Classificação: {jogo['classificacao']} | Tamanho: {jogo['tamanho_gb']} GB")
    print("0. Voltar")

    while True:
        escolha = input("Digite o número do jogo para adicionar ao carrinho ou 0 para voltar: ").strip()
        if escolha == "0":
            break
        if escolha.isdigit() and 1 <= int(escolha) <= len(jogos):
            index = int(escolha) - 1
            adicionar_ao_carrinho(jogos[index])
        else:
            print("Opção inválida.")

# ===== DADOS PARA ENTREGA =====
def coletar_dados_entrega():
    print("\n== Dados para entrega ==")
    nome = input("Nome completo: ").strip()
    endereco = input("Endereço completo: ").strip()
    telefone = input("Telefone para contato: ").strip()

    if not nome or not endereco or not telefone:
        print("Todos os campos são obrigatórios.")
        return False

    dados_entrega['nome'] = nome
    dados_entrega['endereco'] = endereco
    dados_entrega['telefone'] = telefone
    return True

# ===== CARRINHO =====
def ver_carrinho():
    print("\n🛒 Seu Carrinho:")
    if not carrinho:
        print("O carrinho está vazio.")
        return

    total = 0
    for i, (nome, info) in enumerate(carrinho.items(), 1):
        subtotal = info['preço'] * info['quantidade']
        total += subtotal
        print(f"{i}. {nome} - R$ {info['preço']:.2f} x {info['quantidade']} = R$ {subtotal:.2f}")

    print(f"\nTotal: R$ {total:.2f}")
    print("1. Remover item")
    print("2. Finalizar compra")
    print("0. Voltar")

    escolha = input("Escolha uma opção: ").strip()
    if escolha == "1":
        remover_item_carrinho()
    elif escolha == "2":
        finalizar_compra()
    elif escolha == "0":
        return
    else:
        print("Opção inválida.")

def remover_item_carrinho():
    if not carrinho:
        print("O carrinho está vazio.")
        return
    print("\nItens no carrinho:")
    nomes = list(carrinho.keys())
    for i, nome in enumerate(nomes, 1):
        print(f"{i}. {nome} - Quantidade: {carrinho[nome]['quantidade']}")

    escolha = input("Digite o número do item para remover (ou 0 para cancelar): ").strip()
    if escolha == "0":
        return
    if escolha.isdigit() and 1 <= int(escolha) <= len(nomes):
        nome = nomes[int(escolha) - 1]
        del carrinho[nome]
        print(f" '{nome}' removido do carrinho.")
    else:
        print("Opção inválida.")

def adicionar_ao_carrinho(jogo):
    nome = jogo['nome']
    if nome in carrinho:
        carrinho[nome]['quantidade'] += 1
    else:
        carrinho[nome] = {'preço': jogo['preço'], 'quantidade': 1}
    print(f" '{nome}' adicionado ao carrinho. Quantidade: {carrinho[nome]['quantidade']}")

# ===== FINALIZAR COMPRA =====
def escolher_metodo_pagamento():
    print("\n== Métodos de Pagamento ==")
    print("1. Cartão de Crédito")
    print("2. Boleto Bancário")
    print("3. Pix")
    print("0. Cancelar compra")

    escolha = input("Escolha o método de pagamento: ").strip()
    if escolha == "1":
        return "Cartão de Crédito"
    elif escolha == "2":
        return "Boleto Bancário"
    elif escolha == "3":
        return "Pix"
    elif escolha == "0":
        return None
    else:
        print("Opção inválida.")
        return escolher_metodo_pagamento()

def finalizar_compra():
    if not carrinho:
        print("O carrinho está vazio.")
        return

    if not coletar_dados_entrega():
        print("Falha ao coletar dados de entrega. Cancelando compra.")
        return

    metodo = escolher_metodo_pagamento()
    if metodo is None:
        print("Compra cancelada pelo usuário.")
        return

    total = sum(info['preço'] * info['quantidade'] for info in carrinho.values())

    print("\n=== Resumo da Compra ===")
    print(f"Nome: {dados_entrega['nome']}")
    print(f"Endereço: {dados_entrega['endereco']}")
    print(f"Telefone: {dados_entrega['telefone']}")
    print(f"Método de pagamento: {metodo}")
    print(f"Total a pagar: R$ {total:.2f}")
    print("Compra finalizada com sucesso! Obrigado pela preferência.")

    # Limpa carrinho e dados após compra
    carrinho.clear()
    dados_entrega.clear()

# Loop principal
while True:
    exibir_menu()
    escolha = input("Escolha uma opção: ").strip()

    if escolha == "1":
        if usuario_logado:
            ver_catalogo()
        else:
            login()
    elif escolha == "2":
        if usuario_logado:
            ver_carrinho()
        else:
            cadastrar_usuario()
    elif escolha == "3" and usuario_logado:
        logout()
    elif escolha == "0":
        print("Obrigado por visitar nosso e-commerce de games. Até mais!")
        sys.exit()
    else:
        print("Opção inválida.")
