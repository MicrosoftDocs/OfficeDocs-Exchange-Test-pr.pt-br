---
title: 'Modificar a configuração do AD LDS: Exchange 2013 Help'
TOCTitle: Modificar a configuração do AD LDS
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61183348
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar a configuração do AD LDS

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o script **ConfigureAdam.ps1** (localizado em $env:CaminhoInstalaçãoExchange\\Scripts) para modificar a configuração padrão do Active Directory Lightweight Directory Services (AD LDS) em servidores de Transporte de Borda antes de inscrever o servidor de Transporte de Borda em sua organização do Exchange.


> [!IMPORTANT]
> O script <STRONG>ConfigureAdam.ps1</STRONG> chama o comando <STRONG>dsdbutil</STRONG> para alterar as configurações do Registro para o AD&nbsp;LDS. O comando <STRONG>dsdbutil</STRONG> é uma ferramenta de gerenciamento do AD&nbsp;LDS para ser usada somente por administradores experientes, o uso do <STRONG>ConfigureAdam.ps1</STRONG> é a maneira recomendada de alterar a configuração do AD&nbsp;LDS.



Os parâmetros da tabela a seguir estão disponíveis para o script **ConfigureAdam.ps1**. Você pode usar um, todos ou qualquer combinação desses parâmetros para modificar o AD LDS.

### Parâmetros disponíveis para o script ConfigureAdam.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>Altera a porta usada para comunicação LDAP. Por padrão, o servidor de Transporte de Borda usa a porta não-padrão 50389.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>Altera a porta usada para a comunicação LDAP segura. Por padrão, o servidor de Transporte de Borda usa a porta não-padrão 50636.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>Altera a localização do arquivo de log. Por padrão, o servidor de Transporte de Borda cria arquivos de log no caminho %CaminhoInstalaçãoExchange%Transport Roles\Data\adam</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>Altera a localização do arquivo de banco de dados de diretório. Por padrão, o servidor de Transporte de Borda armazena o banco de dados de diretório no caminho %CaminhoInstalaçãoExchange%Transport Roles\Data\adam</p></td>
</tr>
</tbody>
</table>


## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: cinco minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Servidores de Transporte de Borda" em [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Se você precisar fazer qualquer alteração na configuração do AD LDS do servidor de Transporte de Borda, faça antes de inscrever o servidor de Transporte de Borda para sua organização do Exchange. Se você alterar a configuração do AD LDS de um servidor de Transporte de Borda, será necessário inscrever novamente o servidor de Transporte de Borda na organização do Exchange.

  - Sempre use o script para alterar as configurações do Registro. Fazer alterações manuais ao registro na configuração do AD LDS pode tornar a instância do AD LDS indisponível.

  - Se você alterar a porta LDAP ou a porta SSL utilizada pelo AD LDS, primeiro verifique se a porta selecionada não está sendo usada por outro aplicativo. Use o comando **netstat** para exibir as portas em uso no servidor de Transporte de Borda.

  - Você só pode usar o Shell para executar esse procedimento.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Modificar a configuração do AD LDS em um servidor de Transporte de Borda

Este exemplo altera a porta LDAP usada pelo AD LDS para 5000. O E comercial (&) faz parte da sintaxe do comando.

```powershell
    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000
```

Este exemplo faz as seguintes alterações na configuração do AD LDS. O E comercial (&) faz parte da sintaxe do comando. Observe os dois pontos (:) usados entre cada parâmetro e seu valor:

  - Altera a porta LDAP para 5000

  - Altera a porta SSL para 500

  - Altera o caminho de log para D:\\Exchange Server\\Data\\ADLDS

  - Altera o caminho de dados para D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->
```powershell
    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"
```

