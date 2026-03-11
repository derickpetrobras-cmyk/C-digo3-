from datetime import date

# Dicionário global para armazenar os dados dos contribuintes
contribuintes = {}

def adicionar_contribuinte():
    nome = input("Nome completo: ").strip().title()
    cpf = input("CPF (somente números): ").strip()
    try:
        renda_input = input("Renda mensal (R$): ").replace(',', '.')
        renda = float(renda_input)
        contribuintes[cpf] = {"nome": nome, "renda": renda}
        print(f"{nome} cadastrado(a) com sucesso!")
    except ValueError:
        print("Erro: Digite um valor numérico válido para a renda.")

def calcular_ir(renda):
    if renda <= 2112:
        return 0
    elif renda <= 2826.65:
        return renda * 0.075 - 158.40
    elif renda <= 3751.05:
        return renda * 0.15 - 370.40
    elif renda <= 4664.68:
        return renda * 0.225 - 651.73
    else:
        return renda * 0.275 - 884.96

def ver_contribuintes():
    print("\n--- Lista de Contribuintes ---")
    if not contribuintes:
        print("Nenhum contribuinte cadastrado.")
    else:
        for cpf, dados in contribuintes.items():
            print(f"Nome: {dados['nome']} | CPF: {cpf} | Renda: R$ {dados['renda']:.2f}")

def calcular_ir_contribuinte():
    cpf = input("Digite o CPF para cálculo: ").strip()
    if cpf in contribuintes:
        renda = contribuintes[cpf]["renda"]
        nome = contribuintes[cpf]["nome"]
        imposto = calcular_ir(renda)
        print(f"\nContribuinte: {nome}")
        print(f"Renda: R$ {renda:.2f} -> Imposto Devido: R$ {imposto:.2f}")
    else:
        print("CPF não localizado.")

def verificar_idade():
    try:
        idade = int(input("Digite sua idade: "))
        if idade < 18:
            print("Categoria: Menor de idade.")
        elif idade < 60:
            print("Categoria: Adulto.")
        else:
            print("Categoria: Idoso.")
    except ValueError:
        print("Erro: Digite um número inteiro.")

def calcular_idade_pelo_ano():
    try:
        ano_nasc = int(input("Ano de nascimento (4 dígitos): "))
        ano_atual = date.today().year
        print(f"Você tem (ou fará) {ano_atual - ano_nasc} anos.")
    except ValueError:
        print("Erro: Digite um ano válido.")

def menu():
    while True:
        print("\n========== MENU ==========")
        print("1. Adicionar Contribuinte")
        print("2. Ver Lista")
        print("3. Calcular IR")
        print("4. Verificar Categoria de Idade")
        print("5. Calcular Idade pelo Ano")
        print("6. Sair")
        print("==========================")
        
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            adicionar_contribuinte()
        elif opcao == "2":
            ver_contribuintes()
        elif opcao == "3":
            calcular_ir_contribuinte()
        elif opcao == "4":
            verificar_idade()
        elif opcao == "5":
            calcular_idade_pelo_ano()
        elif opcao == "6":
            print("Encerrando programa...")
            break
        else:
            print("Opção inválida!")

if __name__ == "__main__":
    menu()