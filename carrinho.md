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
        print("❌ Opção inválida.")

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
        print(f"✅ '{nome}' removido do carrinho.")
    else:
        print("❌ Opção inválida.")
