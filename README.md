# DESAFIO DIO - KALI LINUX + MEDUSA
## Descrição do Desafio

Implementar, documentar e compartilhar um projeto prático utilizando  **Kali Linux**  e a ferramenta  **Medusa**, em conjunto com ambientes vulneráveis (por exemplo,  **Metasploitable 2**  e  **DVWA**), para simular cenários de ataque de força bruta e exercitar medidas de prevenção.

-   **Configurar o ambiente**: duas VMs (Kali Linux e Metasploitable 2) no VirtualBox, com rede interna (_host-only_).
    
-   **Executar ataques simulados**: força bruta em  **FTP**, automação de tentativas em  **formulário web (DVWA)**  e  **password spraying**  em  **SMB**  com enumeração de usuários.
    
-   **Documentar os testes**: wordlists simples, comandos utilizados, validação de acessos e recomendações de mitigação.

## CONFIGURAÇÃO DE AMBIENTE

 - Máquina Virtual de **Metasploitable** configurada com Placa de Rede **Host-only**
<img src="img\01.png">
 - Máquina Virtual de **Kali Linux** configurada com Placa de Rede **Host-only**
<img src="img\02.png">
 - Logar no Metasploitable com: 
 ```console
 metasploitable login: msfadmin
 Password: msfadmin
 ```
 - Executar o comando para a obtenção do endereço IP:
 ```console
 ip a
 ```
<img src="img\03.png">


## EXECUÇÃO DE ATAQUES SIMULADOS
### FORÇA BRUTA EM FTP

1. Teste de comunicação entre as duas máquinas
<img src="img\04.png">
<img src="img\05.png">

2. Comando "nmap" para verificação de portas abertas                        
<img src="img\06.png">

3. Criação de arquivos de textos com tentativas de usuários e senhas                         
<img src="img\07.png">
<img src="img\08.png">

4. Execução do comando "medusa -h 192.168.56.101 -U users.txt -P pass.txt -m ftp -t 6"               
<img src="img\09.png">

OBS: usuário e senha encontrada em: <img src="img\10.png">

5. Tentativa de conexão                 
<img src="img\11.png"> *"230 Login successful."*

### AUTOMAÇÃO DE TENTATIVAS EM FORMULÁRIO WEB
1. Entrar na URL "192.168.56.101/dvwa/login.php"
<img src="img\12.png">

2. Criação de wordlists (users.txt e pass.txt)
<img src="img\13.png">

3. Execução do comando de Medusa para o teste de combinações de usuários e senhas
<img src="img\14.png">
OBS: a resposta esperada era "2025-10-23 00:53:34 ACCOUNT FOUND: [http] Host: 192.168.56.101 User: **admin** Password: **password** [SUCCESS]"

4. Login no DVWA
<img src="img\15.png">
<img src="img\16.png">



### PASSWORD SPRAYING EM SMB
1. Executar o comando enum4linux para obter arquivo de enumeração do alvo                       
<img src="img\17.png">

2. Identificação de usuários com o comando "less enum4_output.txt"                          
<img src="img\18.png">

3. Criação da lista de usuários e senhas            
<img src="img\19.png">

4. Ataque com Medusa e identificação de login
<img src="img\20.png">

5. Login no "smbclient"             
<img src="img\21.png">

