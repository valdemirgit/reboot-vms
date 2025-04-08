# reboot-vms
script Python que simule o pressionamento de um botão para reiniciar uma máquina remota, podemos usar bibliotecas como paramiko para conexão SSH e executar comandos no sistema remoto. O script a seguir é um exemplo básico de como isso pode ser feito. 
Pré-requisitos: 

    Certifique-se de ter o Python instalado.
    Instale a biblioteca paramiko usando o comando:
    bash
     
   

    pip install paramiko
     
     
    A máquina remota deve permitir conexões SSH e você precisa ter as credenciais de acesso (usuário e senha ou chave privada).
     

Código Python: Botão para Reiniciar Máquina Remota 
python
 


import paramiko
import sys

def reiniciar_maquina_remota(hostname, port, username, password):
    """
    Função para reiniciar uma máquina remota via SSH.

    try:
        # Criar uma instância do cliente SSH
        ssh_client = paramiko.SSHClient()
        
        # Configurar para aceitar chaves SSH desconhecidas automaticamente
        ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        
        # Conectar ao servidor remoto
        print(f"[INFO] Conectando ao servidor {hostname}:{port}...")
        ssh_client.connect(hostname, port=port, username=username, password=password)
        
        # Comando para reiniciar a máquina remota
        comando_reiniciar = "sudo reboot"
        print("[INFO] Enviando comando de reinicialização...")
        
        # Executar o comando no servidor remoto
        stdin, stdout, stderr = ssh_client.exec_command(comando_reiniciar)
        
        # Verificar se houve erros
        erro = stderr.read().decode()
        if erro:
            print(f"[ERRO] Falha ao reiniciar a máquina: {erro}")
        else:
            print("[INFO] Comando de reinicialização enviado com sucesso!")
        
        # Fechar a conexão SSH
        ssh_client.close()
        print("[INFO] Conexão SSH encerrada.")
    
    except Exception as e:
        print(f"[ERRO] Ocorreu um erro: {e}")

if __name__ == "__main__":
    # Configurações da máquina remota
    HOSTNAME = "192.168.1.100"  # Substitua pelo IP ou nome da máquina remota
    PORT = 22                  # Porta SSH padrão
    USERNAME = "usuario"       # Nome de usuário SSH
    PASSWORD = "senha"         # Senha SSH
    
    # Simular o pressionamento do botão para reiniciar
    print("Pressione ENTER para reiniciar a máquina remota...")
    input()  # Aguarda o usuário pressionar ENTER
    
    # Chamar a função para reiniciar a máquina remota
    reiniciar_maquina_remota(HOSTNAME, PORT, USERNAME, PASSWORD)
 
 
Como Funciona: 

    Conexão SSH : O script usa o paramiko para estabelecer uma conexão SSH com a máquina remota.
    Comando de Reinicialização : Após a conexão, o comando sudo reboot é enviado para reiniciar a máquina remota.
    Botão Virtual : O script aguarda o usuário pressionar ENTER para simular o pressionamento de um botão.
    Erros : Se houver problemas na conexão ou execução do comando, o script exibe mensagens de erro.
     

Observações: 

    Permissões de Superusuário : O comando sudo reboot requer permissões de superusuário. Certifique-se de que o usuário SSH tem essas permissões configuradas.
    Chave Privada : Se você usa autenticação por chave privada em vez de senha, ajuste o código para usar pkey no método connect.
    Segurança : Evite armazenar senhas diretamente no código. Use variáveis de ambiente ou arquivos de configuração seguros.
     

Exemplo de Uso: 

    Execute o script no terminal:
    bash
     
    python reiniciar_maquina.py
     
     
    Pressione ENTER quando solicitado para reiniciar a máquina remota.

Observações Importantes

🔹 Permissões: Certifique-se de que o usuário SSH tenha permissão para executar reboot/shutdown (geralmente requer sudo).
🔹 Chave SSH: Prefira autenticação por chave em vez de senha (mais seguro).
🔹 Logs: Se quiser registrar os resultados em um arquivo, adicione with open('log.txt', 'a') as f: f.write(...).
🔹 Alternativa sem Python: Se preferir, use pssh (Parallel SSH) para um comando direto:
bash
Copy

pssh -H "user@host1 user@host2" -i "sudo reboot"

Quer algum ajuste? Posso adaptar o script conforme sua necessidade! 🚀
     
