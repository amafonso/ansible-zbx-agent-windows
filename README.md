## ansible-zbx-agent-windows

Nesta automação, foram criadas 3 Roles:

# Instalação do Agent Zabbix para Windows (MSI)
  - Instalar o Agente do Zabbix, conforme versão que for definido no arquvido Default.
  - Copiado as pastas de parametros e scripts, repositório Files
  - Configuração do .conf, repositório Templates

# Alteração de configurações:
  - Alterar o arquivo .conf
  - Copiado as pastas de parametros e scripts, repositório Files
  - Configuração do .conf, repositório Templates

# Solicitação de Restart do Serviço Zabbix
  - Apenas reiniciar o serviço.

# Adicionar Host no Zabbix
  - Adiciona o Host no Zabbix, dentro do Grupo e com Template. Mas para isso, vai precisar editar o arquvio roles/zbxregisterhost/defaults/main.yml e adicionar os dados de conexão, grupo e o template.

# Obs.: 
Todas as configurações do .conf é feito pelo Default/main.yml, se precisa alterar servidor, versão ou parametros do .conf.

- Foi adicionado o repositório files/zabbix_agentd.conf.d, para adicionar paramtros customizados, tudo que colocar na pasta será copiado para os clientes.

- O repositório files/scripts esta no caminho 'C:\Program Files\Zabbix Agent\scripts\', conforme descrição no default/main.yml

# Para o Ansible acessar o Servidores Windows, precisa ser executado o script abaixo como no Powershell como administrador:
- Script disponibilizado no site: https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html, para habilitar a comunicação HTTPS
'''$url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Install-WMF3Hotfix.ps1"
$file = "$env:temp\Install-WMF3Hotfix.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file -Verbose


$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file
'''

- A conexão com o servidores foi configurado como NTLM, dentro do repositório group_vars/windows, que esta fazendo referencia com o grupo Windows criado o arquivo de inventário hosts

### Importante, tente usar o ansible-vault no arquivo group_vars/windows, para manter a segurança.

