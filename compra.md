# ===== DADOS PARA ENTREGA =====
def coletar_dados_entrega():
    print("\n== Dados para entrega ==")
    nome = input("Nome completo: ").strip()
    endereco = input("Endereço completo: ").strip()
    telefone = input("Telefone para contato: ").strip()

    if not nome or not endereco or not telefone:
        print("❌ Todos os campos são obrigatórios.")
        return False

    dados_entrega['nome'] = nome
    dados_entrega['endereco'] = endereco
    dados_entrega['telefone'] = telefone
    return True


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
        print("❌ Opção inválida.")
        return escolher_metodo_pagamento()

def finalizar_compra():
    if not carrinho:
        print("O carrinho está vazio.")
        return

    if not coletar_dados_entrega():
        print("❌ Falha ao coletar dados de entrega. Cancelando compra.")
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
    print("✅ Compra finalizada com sucesso! Obrigado pela preferência.")

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
        print("🛒 Obrigado por visitar nosso e-commerce de games. Até mais!")
        sys.exit()
    else:
        print("❌ Opção inválida.")
