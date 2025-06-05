jogos = [
    {"nome": "Elden Ring", "preço": 249.90, "classificacao": "16+", "tamanho_gb": 50},
    {"nome": "Cyberpunk 2077", "preço": 199.90, "classificacao": "18+", "tamanho_gb": 70},
    {"nome": "The Last of Us Part II", "preço": 229.90, "classificacao": "18+", "tamanho_gb": 78},
    {"nome": "God of War Ragnarok", "preço": 279.90, "classificacao": "18+", "tamanho_gb": 90},
]
def ver_catalogo():
    print("\n🎮 Catálogo de Jogos Modernos:")
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
            print("❌ Opção inválida.")
