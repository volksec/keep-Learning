# [Informações do Sistema]
Obter informações do sistema operacional
Verificar o PATH, alguma pasta gravável?
Verificar variáveis de ambiente, algum detalhe sensível?
Procurar por exploits no kernel usando scripts (DirtyCow?)
Verificar se a versão do sudo é vulnerável
Falha na verificação de assinatura do Dmesg
Mais enumeração do sistema (data, estatísticas do sistema, informações da CPU, impressoras)
Enumerar mais defesas

# [Unidades]
Listar unidades montadas
Alguma unidade desmontada?
Alguma credencial em fstab?

# [Softwares Instalados]
Verificar software útil instalado
Verificar software vulnerável instalado

# [Processos]
Algum software desconhecido em execução?
Algum software em execução com mais privilégios do que deveria?
Procurar exploits em processos em execução (especialmente a versão em execução).
É possível modificar o binário de algum processo em execução?
Monitorar processos e verificar se algum processo interessante está sendo executado frequentemente.
É possível ler a memória de algum processo interessante (onde senhas poderiam estar salvas)?

# [Tarefas Agendaddas - Cron Jobs]
O PATH está sendo modificado por algum cron e você pode escrever nele?
Algum caractere curinga em uma tarefa cron?
Algum script modificável está sendo executado ou está dentro de uma pasta modificável?
Você detectou que algum script pode estar sendo executado muito frequentemente? (a cada 1, 2 ou 5 minutos)

# [Serviços]
Algum arquivo .service gravável?
Algum binário gravável executado por um serviço?
Alguma pasta gravável no PATH do systemd?

# [Timers]
Algum temporizador gravável?
Sockets
Algum arquivo .socket gravável?
É possível se comunicar com algum socket?
Sockets HTTP com informações interessantes?

# [D-Bus]
É possível se comunicar com algum D-Bus?
Rede
Enumerar a rede para saber onde você está
Portas abertas que você não conseguia acessar antes de obter acesso à máquina?
É possível interceptar o tráfego usando tcpdump?

# [Usuários]
Enumeração genérica de usuários/grupos
Você tem um UID muito grande? A máquina é vulnerável?
É possível escalar privilégios devido a um grupo ao qual você pertence?
Dados da área de transferência?
Política de senha?
Tentar usar todas as senhas conhecidas que você descobriu anteriormente para fazer login com cada usuário possível. Tente fazer login também sem senha.

# [Path Gravável]
Se você tiver privilégios de gravação sobre alguma pasta no PATH, pode ser possível escalar privilégios
Comandos SUDO e SUID
É possível executar algum comando com sudo? Pode usá-lo para LER, ESCREVER ou EXECUTAR qualquer coisa como root? 

# [GTFOBins]
Existe algum binário SUID explorável? (GTFOBins)
Os comandos sudo são limitados pelo caminho? É possível burlar as restrições?
Binário SUDO/SUID sem caminho indicado?
Binário SUID especificando caminho? Bypass
Vulnerabilidade LD_PRELOAD
Falta de biblioteca .so em binário SUID de uma pasta gravável?
Tokens SUDO disponíveis? É possível criar um token SUDO?
É possível ler ou modificar arquivos sudoers?
É possível modificar /etc/ld.so.conf.d/?
Comando OpenBSD DOAS

# [Capabilities]
Algum binário tem alguma capacidade inesperada?

# [ACLs]
Algum arquivo tem alguma ACL inesperada?

# [SEssões de Shell Abertas]
screen
tmux

# [SSH]
Debian OpenSSL Predictable PRNG - CVE-2008-0166
Valores de configuração interessantes no SSH

# [Arquivos Interessantes]
Arquivos de perfil - Ler dados sensíveis? Escrever para escalonamento de privilégios?
Arquivos passwd/shadow - Ler dados sensíveis? Escrever para escalonamento de privilégios?
Verificar pastas comumente interessantes para dados sensíveis
Arquivos em locais/especificados estranhos, que você pode acessar ou alterar arquivos executáveis
Modificado nos últimos minutos
Arquivos de banco de dados SQLite
Arquivos ocultos
Scripts/binários no PATH
Arquivos da web (senhas?)
Backups?
Arquivos conhecidos que contêm senhas: Use Linpeas e LaZagne
Pesquisa genérica

# [ARQUIVOS Graváveis]
Modificar biblioteca Python para executar comandos arbitrários?
É possível modificar arquivos de log? Explorar o exploit Logtotten
É possível modificar /etc/sysconfig/network-scripts/? Explorar a vulnerabilidade no Centos/Redhat
É possível escrever em arquivos ini, int.d, systemd ou rc.d?
Outros truques
É possível abusar do NFS para escalar privilégios?
É necessário escapar de um shell restritivo?