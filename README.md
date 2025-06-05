# Modelo Tradicional de Venda de Jogos

O **modelo tradicional de venda de jogos** envolve a comercialização de jogos em **formato físico**, sendo o principal meio de consumo de jogos até o avanço da internet de alta velocidade e das plataformas digitais. Esse modelo apresenta várias características marcantes:

## Características Principais

- **Mídia Física**: Os jogos são distribuídos em mídias como:
  - CDs ou DVDs (PC, PlayStation, Xbox)
  - Cartuchos (Nintendo)
- **Embalagens Personalizadas**: Acompanha caixa física, manual de instruções, e em alguns casos, itens colecionáveis.
- **Venda em Lojas Físicas**: 
  - Grandes redes de varejo (ex: Americanas, Lojas Americanas, Saraiva)
  - Lojas especializadas em games (ex: GameStop, UZ Games)
- **Distribuição e Logística**: Envolve transporte, estoque e prateleiras físicas.
- **Sem Dependência de Internet**: Não exige conexão para jogar, exceto em casos de atualizações ou multiplayer.

## Vantagens

- **Propriedade Física**: O jogador possui o produto em mãos.
- **Revenda e Troca**: Jogos podem ser vendidos, trocados ou emprestados.
- **Itens Colecionáveis**: Alguns jogos vêm com edições especiais, brindes ou livros de arte.

## Desvantagens

- **Custo com Logística**: Transporte, armazenamento e distribuição encarecem o produto.
- **Espaço Físico**: Requer local para armazenar os jogos.
- **Desgaste da Mídia**: CDs e cartuchos podem arranhar ou estragar com o tempo.
- **Acesso Limitado**: Depende da disponibilidade em estoque ou localização da loja.

## Exemplo de Consoles que Usam Esse Modelo

- **PlayStation 2 / 3 / 4** (com leitor de disco)
- **Xbox 360 / One**
- **Nintendo Wii / Switch (cartucho)**

## Situação Atual

Apesar do crescimento do mercado digital, o modelo tradicional ainda é valorizado por **colecionadores**, **jogadores nostálgicos** e em regiões com acesso limitado à internet. Algumas edições especiais continuam sendo lançadas em formato físico para atender esse público.


# 🧾 Funcionalidades do E-commerce de Games Modernos

Este sistema simula um e-commerce de jogos digitais no terminal, com foco em jogos modernos. Abaixo estão suas funcionalidades organizadas por seção:

---

## 1. Autenticação e Usuário

- **`usuarios`**: Dicionário que simula um banco de dados de usuários cadastrados.
- **`login()`**: Permite o acesso do usuário com verificação de credenciais.
- **`cadastrar_usuario()`**: Cadastra um novo usuário com nome completo, nome de usuário e senha.
- **`logout()`**: Encerra a sessão atual e limpa o carrinho e os dados de entrega.

---

## 2. Catálogo de Jogos

- **`jogos`**: Lista de jogos modernos, cada um com:
  - `nome`: título do jogo
  - `preço`: valor do jogo
  - `classificacao`: faixa etária recomendada (ex: "18+")
  - `tamanho_gb`: espaço necessário em GB

- **`ver_catalogo()`**: Exibe a lista de jogos com informações detalhadas (nome, preço, classificação, tamanho) e permite ao usuário adicionar jogos ao carrinho.

---

## 3. Carrinho de Compras

- **`carrinho`**: Dicionário que armazena os jogos adicionados ao carrinho e suas quantidades.
- **`adicionar_ao_carrinho(jogo)`**: Adiciona um jogo ao carrinho ou incrementa sua quantidade.
- **`ver_carrinho()`**: Exibe os itens do carrinho, seus preços e quantidades, e o valor total. Oferece opções para:
  - Remover itens
  - Finalizar compra

- **`remover_item_carrinho()`**: Remove um item específico do carrinho com base na escolha do usuário.

---

## 4. Dados para Entrega

- **`dados_entrega`**: Dicionário que armazena informações do comprador.
- **`coletar_dados_entrega()`**: Solicita nome completo, endereço e telefone, e valida se os campos estão preenchidos.

---

## 5. Finalização da Compra

- **`escolher_metodo_pagamento()`**: Exibe opções de pagamento e retorna a escolha do usuário:
  - Cartão de Crédito
  - Boleto Bancário
  - Pix

- **`finalizar_compra()`**:
  - Valida se o carrinho não está vazio
  - Coleta os dados de entrega
  - Solicita o método de pagamento
  - Exibe o resumo da compra
  - Limpa o carrinho e os dados de entrega após a compra

---

## 6. Interface e Loop Principal

- **`exibir_menu()`**: Exibe o menu principal com base no estado de login do usuário.
- **`while True`**:
  - Mantém o programa em execução contínua
  - Controla a navegação entre login, cadastro, catálogo, carrinho, logout e sair do sistema.

---

## ✅ Pontos Positivos

- Interface simples e intuitiva via terminal
- Simulação realista de e-commerce (cadastro, catálogo, carrinho, compra)
- Validação de entrada de dados
- Estrutura clara, organizada em funções independentes
- Carrinho persistente durante a sessão do usuário
- Exibição de informações úteis nos jogos (preço, classificação etária, tamanho)

---

## 🚀 Sugestões para Evolução

- **Salvar usuários e pedidos em arquivos JSON ou banco de dados**
- **Adicionar autenticação com verificação de senha mais segura**
- **Permitir editar quantidade no carrinho sem precisar remover**
- **Incluir categorias ou filtros no catálogo**
- **Adicionar um modo administrador para gerenciar jogos no catálogo**
- **Transformar em app web com Flask ou Django**
