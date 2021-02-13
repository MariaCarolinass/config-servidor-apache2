# Tutorial 1

Configurando um servidor Apache2 em uma máquina virtual.

## Instalação da máquina virtual: VirtualBox

O VirtualBox é um virtualizador completo de uso geral. É um ambiente virtual que simula a experiência de usar um sistema operacional sem precisar fazer a sua instalação na máquina física. 

- [Link para instalação do VirtualBox](https://www.virtualbox.org/wiki/Downloads).

## Instalação da imagem do sistema operacional: Debian

Para configurar o VirtualBox precisamos baixar uma imagem de algum sistema operacional. 

O Projeto Debian é uma associação de indivíduos que têm como causa comum criar um sistema operacional livre. O sistema operacional criado é chamado Debian. Os sistemas Debian atualmente usam o kernel Linux ou o kernel FreeBSD.

- [Link para instalação do Debian](https://www.debian.org/distrib/).
- [Saiba mais sobre o Debian](https://www.debian.org/).
- [Saiba mais sobre Linux em geral: Guia Foca Linux](https://www.guiafoca.org/guiaonline/iniciante/).

## Criação da máquina virtual mais instalação do Debian no VirtualBox

### Criando a máquina virtual

1. Clicar em "Novo" para criar a máquina virtual.
2. Escolher o nome do sistema operacional, tipo de sistema operacional "Linux" e a versão da imagem escolhida "Debian 32-bit" ou "Debian 64-bit".
3. O tamanho da memória deve continuar na opção recomendada de 1024MB para um computador com 2GB ou mais de memória.
4. Deixar marcado “Criar um novo disco rígido virtual agora”.
5. Escolher um arquivo do tipo "VDI (VirtualBox Disk Image)" para a criação do disco rígido.
6. Para otimização de processamento, o armazenamento em disco rígido físico será de tamanho fixo.
7. O disco criado terá o tamanho recomendado de 8GB.
8. Por fim, a máquina será criada e após a sua finalização devemos clicar em "Iniciar" da máquina virtual.

### Instalando o Debian na máquina virtual criada

1. Ao iniciar a máquina virtual pela primeira vez, clique na pasta amarela e "Acrescente" o arquivo da imagem do Deabian que foi baixada anteriomente. Depois ao escolher corretamente o arquivo, clique em "Iniciar".
2. Aperte “Enter” para escolher a opção “Graphical install”.
3. Selecione o idioma “Portuguese (Brazil)”.
4. Logo em seguida, a localidade “Brasil”.
5. Selecione o mapeamento do teclado “Português Brasileiro” e aguarde.
6. Defina o nome da máquina.
7. O nome de domínio fica em branco.
8. Defina a senha de root. LEMBRE-SE DA SENHA.
9. Digite a senha novamente, para confirmar.
10. Digite o nome completo do usuário.
11. Digite o nome de usuário para acessar o computador.
12. Defina a senha para o usuário. LEMBRE-SE DA SENHA.
13. Confirme a senha do usuário.
14. Selecione a localidade para configurar o relógio.
15. Selecione a opção de Particionamento do Disco “Assistido - usar o disco inteiro”.
16. Selecione o disco disponível.
17. Selecione a opção “Todos os arquivos em uma partição (para iniciantes)”.
18. Selecione a opção “Finalizar o particionamento e escrever as mudanças no disco”.
19. Confirme a ação "Sim" e aguarde a instalação do sistema básico.
20. Selecione “Não” para não adicionar novos CDs ou DVDs.
21. Escolha o país mais próximo para configurar o servidor "Brasil".
22. Escolha um servidor "deb.debian.org".
23. Não é necessário fazer configuração de proxy. Aperte “Enter” e aguarde a instalação.
24. Selecione a opção “Não” para participar do concurso de instalação de pacotes.
25. Utilizando as setas e a tecla “Espaço”, marque as opções "Xfce", "servidor de impressão", "utilitários de sistema padrão" e aperte “Enter”.
26. Selecione “Sim” para instalar o GRUB para inicializar o Sistema Operacional.
27. Indique o dispositivo na lista "/dev/sda", para instalação do carregador.
28. Selecione “Continuar” para encerrar a instalação.


## Configurando e instalando o servidor web Apache 2

Com a máquina virtual devidamente criada no VirtualBox e funcionando com o sistema operacional Debian. Inicialize a máquina virtual e abra o terminal para começar a instalação do servidor Apache.

1. Entre como usuário (root) administrador digitando o comando abaixo e logo após, digite sua senha:

`$ su`

2. Instale o servidor Apache:

`# apt-get install apache2`

3. Para verificar se o Apache está funcionando:

`# systemctl status`

4. Na máquina virtual, clique em "configurações" > Rede > Altere a rede para Conectado a: Host-only. Depois volte ao terminal, para atualizar as configurações de rede:

`# /sbin/dhclient`

5. Verifique qual é o endereço IP da sua máquina com o comando abaixo:

`# ip addr`

O seu endereço IP está na linha "inet".

6. Acesse o seu endereço IP, digitando ele em seu navegador web de preferência e confira se irá aparecer a página inicial do Apache.

### Editando a página inicial

No terminal, entre para o seguinte diretório:

`# cd /var/www/html`

Mova o arquivo "index.html":

`# mv index.html _index.html`

Agora edite o arquivo "_index.html". Obs: Você precisa editá-lo como um usuário administrador, no seu editor de texto de preferência. Utilizei o editor "gedit", caso ele não esteja instalado: `# apt-get install gedit`.

Apague todo o código html no arquivo _index.html e digite um novo. Por exemplo:

```
<html>
<header><title>Teste</title></header>
<body><h1>Editando um site</h1></body>
</html>
```

Finalmente, verifique se a página foi editada digitando o endereço IP da máquina em um navegador web. Caso seja preciso, reiniciei o Apache: `systemctl restart apache2`.
