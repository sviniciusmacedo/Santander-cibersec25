# Santander-cibersec25

# OBJETIVOS
<<<<<<< HEAD
[ ] Configurar duas VMs (Kali e Metasplotable2) host-only
[ ] Brute force FTP
[ ] Script form web DVWA
[ ] Pswd spraying
[ ] SMB enum
=======

- [ ] Configurar duas VMs (Kali e Metasplotable2) host-only
- [ ] Brute force FTP
- [ ] Script form web DVWA
- [ ] Pswd spraying
- [ ] SMB enum
>>>>>>> b84193135abbc6bf6d60dc1fe8ce7a121b7323bb

Ao tentar levantar Metasploitable2 na VM está apresentando kernel panic, como nao consegui resolver irei documentar o processo de aprendizado.

![Kernel panic metasploitable2](<erro metasploit kernel panic-1.png>)


## BRUTE FORCE MEDUSA
Para realizar o brute force com Medusa preciso garantir que a porta FTP esteja aberta, portanto é necessario usar o NMAP para verificar a vulnerabilidade realizando as seguintes etapas:
1) Estando na mesma rede do dispositivo verificar a conexao via ping
2) nmap -sV -p (portas para escanear), se a porta 21/tcp estiver open é possivel explorar a vulnerabilidade
3) executar o ftp (ip alvo, no caso a VM metasploitable2)
4) Se bem sucedido ele irá conectar e pedir usuario e senha.

### INICIA O BRUTE FORCE
<<<<<<< HEAD

=======
>>>>>>> b84193135abbc6bf6d60dc1fe8ce7a121b7323bb
1) Criar os arquivos txt de usuario e senha para ser combinados pelo Medusa
2) medusa -h (ip alvo) -U (usuarios.txt) -P (senhas.txt) -M ftp (metodo) -t(numero de treads)
Com esse comando vai ser realizada a combinaçao de usuarios-senhas fornecidos, a combinaçao correta apresentara SUCESS


## AUTOMATIZAÇAO TENTATIVAS EM FORM WEB (DVWA)
<<<<<<< HEAD
---------
=======

>>>>>>> b84193135abbc6bf6d60dc1fe8ce7a121b7323bb
A criaçao dos arquivos txt é basicamente a mesma, o que mudará é o comando para automatizaçao, ficará assim:
medusa -h (ip alvo) -U (usuarios.txt) -P (senhas.txt) -M http \
-m PAGE: '/dvwa/login.php' \
-m FORM: 'username=^USER^&password='^PASS^&Login=Login' \
-m 'FAIL=Login failed' -t6

Nesse caso o -M alterou pos mudou o modulo. O -m PAGE aponta a pagina e o -m FORM o caminho do formulario, e o -m FAIL é para verificar se for DIFERENTE de fail é porque obteve sucesso.


## ENUM + PASSWORD SPRAYING VIA SMB
<<<<<<< HEAD
---------
=======

>>>>>>> b84193135abbc6bf6d60dc1fe8ce7a121b7323bb
Com acesso a rede é possivel realizar o ataque que se segue dessa maneira
1) Realizar a enumeraçao de usuarios: 
    enum4linux -a (ip alvo) 'tee enum4_output.txt'
2) Apos ser gerado o output neste arquivo com diversas infos temos que buscar info dos usuarios tem um formato parecido com: user:[] rid:[]. 
Assim, sabendo os usuarios do sistema o password spraying fica mais "escondido" de ser detectado pelo sistema.
3) Apos ter os arquivos com usuario do sistema e senhas verificar se tem acesso de fato aquele usuario, ou seja, se ao por o usuario nao apresentar erro e passar direto para senha, foi estabelecido conexao
4) Ao passar o Medusa com a combinaçao usuario e senha com o comando:
 medusa -h (ip alvo) -U (usuarios) -P (senhas) -M SMBNT -t 2 -T50
 Perceba q o modulo mudou, o t= quantidade de usuarios e o T= limite de hosts em paralelo.
 5) Para testar o acesso...
    smbclient -L // (ip alvo) -U(usuario) 
