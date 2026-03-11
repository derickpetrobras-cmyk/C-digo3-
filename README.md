from datetime import date


def verificar_idade():
    try:
        idade = int(input("Digite sua idade: "))
        if idade < 18:
            print('Você é menor de idade.')
        elif idade < 60:
            print("Você é adulto.")
        else:
            print("Você é idoso.")
    except ValueError:
        print("Erro: Por favor, digite um número inteiro.")


def calcular_idade_atual():
    try:
        ano_nascimento = int(input("Digite seu ano de nascimento (4 dígitos): "))
        ano_atual = date.today().year
        idade = ano_atual - ano_nascimento

        if idade < 0:
            print("O ano de nascimento não pode ser no futuro!")
        else:
            print(f"Você tem (ou fará) {idade} anos de idade.")
    except ValueError:
        print("Erro: Digite um ano válido com 4 números.")


def menu():
    while True:
        print("\n=== MENU ===")
        print("1. Verificar categoria por idade")
        print("2. Calcular idade pelo ano de nascimento")
        print("3. Sair")

        opcao = input("Escolha uma opção: ")  # Corrigido: Removido parêntese extra

        if opcao == "1":
            verificar_idade()
        elif opcao == "2":
            calcular_idade_atual()
        elif opcao == "3":
            print("Encerrando o programa...")
            break
        else:
            print("Opção Inválida.")


if __name__ == '__main__':
    menu()