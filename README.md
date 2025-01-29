# Bingo
import random

def gerar_cartela(modalidade):
    if modalidade == "rapido":
        cartela = []
        for _ in range(2):
            linha = []
            for _ in range(3):
                if _ == 0:
                    linha.append(random.randint(1, 10))
                elif _ == 1:
                    linha.append(random.randint(11, 20))
                else:
                    linha.append(random.randint(21, 30))
            cartela.append(linha)
        return cartela
    elif modalidade == "demorado":
        cartela = []
        for _ in range(3):
            linha = []
            for _ in range(4):
                if _ == 0:
                    linha.append(random.randint(1, 10))
                elif _ == 1:
                    linha.append(random.randint(11, 20))
                elif _ == 2:
                    linha.append(random.randint(21, 30))
                else:
                    linha.append(random.randint(31, 40))
            cartela.append(linha)
        return cartela

def imprimir_cartela(cartela, dezenas_sorteadas, nome_jogador):
    print(f"Cartela de {nome_jogador}:")
    for linha in cartela:
        for dezena in linha:
            if dezena in dezenas_sorteadas:
                print(f"[X]", end=" ")
            else:
                print(f"{dezena:2d}", end=" ")
        print()

def simular_bingo(modalidade):
    if modalidade == "rapido":
        num_jogadores = 2
        num_dezenas = 30
    elif modalidade == "demorado":
        num_jogadores = 4
        num_dezenas = 40

    cartelas = []
    for _ in range(num_jogadores):
        cartela = gerar_cartela(modalidade)
        cartelas.append(cartela)

    dezenas_sorteadas = []
    while len(dezenas_sorteadas) < num_dezenas:
        dezena = random.randint(1, num_dezenas)
        if dezena not in dezenas_sorteadas:
            dezenas_sorteadas.append(dezena)
            print(f"\nÚltima dezena sorteada: {dezena}")
            print("Dezenas sorteadas até o momento:", sorted(dezenas_sorteadas))
            input("Digite ENTER para continuar o jogo:" ,)

            for i, cartela in enumerate(cartelas):
                imprimir_cartela(cartela, dezenas_sorteadas, f"Jogador {i+1}")

            vencedores = []
            for i, cartela in enumerate(cartelas):
                if all(dezena in dezenas_sorteadas for linha in cartela for dezena in linha):
                    vencedores.append(f"Jogador {i+1}")
            if vencedores:
                print(f"\nOs vencedores são: {', '.join(vencedores)}")
                break

def main():
    print("Bem-vindo ao simulador de bingo!")
    modalidade = input("Indique o modo de jogo: (0 - RÁPIDO 1 - DEMORADO): ")
    simular_bingo(modalidade)

if __name__ == "_main_":
    main()
