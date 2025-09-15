import json
from datetime import datetime

# Função para adicionar um paciente
def adicionar_paciente(pacientes):
    nome = input("Nome do Paciente: ")
    endereco = input("Endereço: ")
    data_agendamento = input("Data do Agendamento (DD/MM/AAAA): ")

    # Validar a data
    try:
        data_agendamento = datetime.strptime(data_agendamento, "%d/%m/%Y")
    except ValueError:
        print("Data inválida. Formato correto: DD/MM/AAAA")
        return

    paciente = {
        "nome": nome,
        "endereco": endereco,
        "data_agendamento": data_agendamento.strftime("%d/%m/%Y")
    }

    pacientes.append(paciente)
    print("Paciente adicionado com sucesso!")

# Função para visualizar todos os pacientes agendados
def visualizar_pacientes(pacientes):
    if not pacientes:
        print("Nenhum paciente agendado.")
    else:
        for i, paciente in enumerate(pacientes, start=1):
            print(f"\nPaciente {i}:")
            for chave, valor in paciente.items():
                print(f"{chave.capitalize()}: {valor}")

# Função para salvar pacientes em um arquivo JSON
def salvar_pacientes(pacientes, arquivo):
    with open(arquivo, 'w') as f:
        json.dump(pacientes, f)
    print("Pacientes salvos com sucesso!")

# Função principal
def main():
    pacientes = []
    arquivo = "pacientes.json"

    while True:
        print("\nMenu:")
        print("1. Adicionar Paciente")
        print("2. Visualizar Pacientes")
        print("3. Salvar Pacientes")
        print("4. Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            adicionar_paciente(pacientes)
        elif opcao == '2':
            visualizar_pacientes(pacientes)
        elif opcao == '3':
            salvar_pacientes(pacientes, arquivo)
        elif opcao == '4':
            print("Saindo do sistema...")
            break
        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    main()
