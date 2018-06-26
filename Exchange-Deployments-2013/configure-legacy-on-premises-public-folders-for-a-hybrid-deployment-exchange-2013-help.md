---
title: 'Configurar pastas públicas locais herdadas para uma implantação híbrida: Exchange 2013 Help'
TOCTitle: Configurar pastas públicas locais herdadas para uma implantação híbrida
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54913433
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar pastas públicas locais herdadas para uma implantação híbrida

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2018-05-22_

**Resumo:** Use as etapas deste artigo para sincronizar pastas públicas entre o Office 365 e a implantação local do Exchange 2007 ou do Exchange 2010.

Em uma implantação híbrida, os usuários podem estar no Exchange Online, no local ou em ambos e as pastas públicas podem estar no Exchange Online ou no local. As pastas públicas podem residir apenas em um local, por isso, você deve decidir se elas estarão no Exchange Online ou no local. Elas não podem ficar nos dois locais. As caixas de correio de pastas públicas são sincronizadas com o Exchange Online pelo Serviço de Sincronização de Diretórios. No entanto, as pastas públicas habilitadas para email não são sincronizadas nos locais.

Este tópico descreve como sincronizar pastas públicas habilitadas para email quando os usuários estão no Office 365 e as pastas públicas do Exchange 2010 SP3 ou do pacote cumulativo de atualizações 10 do Exchange 2007 SP3 estão no local. No entanto, um usuário do Office 365 que não esteja representado por um objeto MailUser no local (local da hierarquia de pastas públicas de destino) não terá acesso a pastas públicas locais herdadas ou do Exchange 2013.


> [!TIP]
> Este tópico chama os servidores Exchange 2010 SP3 e Exchange 2007 SP3 RU10 de <EM>servidores Exchange herdados</EM>.



Você sincronizará suas pastas públicas habilitadas para email com os seguintes scripts, que são iniciados por uma tarefa do Windows que é executada no ambiente local:

1.  `Sync-MailPublicFolders.ps1`   Esse script sincroniza objetos de pastas públicas habilitadas para email da implantação local do Exchange com o Office 365. Ele usa a implantação local do Exchange como mestre para determinar quais alterações devem ser aplicadas ao Office 365. O script cria, atualiza ou exclui objetos de pastas públicas habilitadas para email no Azure Active Directory para Office 365, com base no conteúdo existente na implantação local do Exchange.

2.  `SyncMailPublicFolders.strings.psd1`   Este é um arquivo de suporte usado pelo script de sincronização anterior e deve ser copiado para o mesmo local que esse script.

Quando você concluir o procedimento, os usuários locais e do Office 365 poderão acessar a mesma infraestrutura de pasta pública no local.

## Quais versões híbridas do Exchange funcionarão com pastas públicas?

A tabela a seguir descreve a versão e as combinações de locais de caixas de correio e pastas públicas do usuário que são suportadas. "Híbrida não aplicável" ainda é um cenário com suporte, mas não é considerado um cenário híbrido, pois tanto as pastas públicas quanto os usuários estão residindo no mesmo local.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Exchange 2007 no local ou caixa de correio do usuário do Exchange 2010</th>
<th>Caixa de correio do usuário do Exchange 2013 no local</th>
<th>Caixa de correio do usuário do Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pastas públicas do Exchange 2007 ou do Exchange 2010 no local</p></td>
<td><p>Híbrida não aplicável</p></td>
<td><p>Híbrida não aplicável</p></td>
<td><p>Com suporte</p></td>
</tr>
<tr class="even">
<td><p>Pastas públicas do Exchange 2013 no local</p></td>
<td><p>Híbrida não aplicável</p></td>
<td><p>Híbrida não aplicável</p></td>
<td><p>Com suporte</p></td>
</tr>
<tr class="odd">
<td><p>Pastas Públicas do Exchange Online</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Híbrida não aplicável</p></td>
</tr>
</tbody>
</table>


Uma configuração híbrida com pastas públicas do Exchange 2003 não é suportada. Se você estiver executando o Exchange 2003 em sua organização, deverá mover todos os bancos de dados de pasta pública e réplicas para o Exchange 2007 SP3 RU10 ou posterior. Nenhuma réplica de pasta pública pode permanecer no Exchange 2003.


> [!TIP]
> O Outlook 2016 não tem suporte para o acesso de pastas públicas herdadas do Exchange 2007. Caso tenha usuários com o Outlook 2016, você deverá migrar as pastas públicas para uma versão mais recente do Exchange. Para saber mais sobre a compatibilidade do Outlook 2016 e do Office 2016 com o Exchange 2007 e versões anteriores, confira <A href="https://go.microsoft.com/fwlink/p/?linkid=849053">este artigo</A>.



## Etapa 1 – O que você precisa saber para começar?

1.  Estas instruções pressupõem que você tenha usado o Assistente de Configuração Híbrida para configurar e sincronizar seus ambientes do Exchange Online e no local e que os registros DNS usados ​​para a Descoberta Automática da maioria dos usuários façam referência a um ponto de extremidade no local. Para obter mais informações, consulte [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

2.  As instruções pressupõem que o Outlook em Qualquer Lugar esteja habilitado e funcional em servidores Exchange herdados no local. Para saber mais sobre como habilitar o Outlook em Qualquer Lugar, confira [Outlook em Qualquer Lugar](https://technet.microsoft.com/pt-br/library/bb123741\(v=exchg.150\)).

3.  Implementar a coexistência de pasta pública herdada para uma implantação híbrida do Exchange com o Office 365 pode exigir a correção de conflitos durante o procedimento de importação. Os conflitos podem acontecer devido a um endereço de e-mail sem possibilidade de roteamento atribuído a pastas públicas habilitadas para email, conflitos com outros usuários e grupos no Office 365 e outros atributos.

4.  Estas instruções pressupõem que sua organização do Exchange Online tenha sido atualizada para uma versão que dê suporte a pastas públicas.

5.  No Exchange Online, você precisa ser membro do grupo de funções Gerenciamento de Organização. Esse grupo de funções é diferente das permissões atribuídas quando você assina o Exchange Online. Para obter detalhes sobre como habilitar o grupo de funções Gerenciamento de Organização, consulte [Gerenciar grupos de função](https://technet.microsoft.com/pt-br/library/jj657480\(v=exchg.150\)).

6.  No Exchange 2010, você deve ser membro dos grupos de função Gerenciamento de Organização ou RBAC de Gerenciamento de Servidor. Confira os detalhes em [Adicionar membros a um grupo de função](https://go.microsoft.com/fwlink/?linkid=299212)

7.  No Exchange 2007, você deve ter a função Administrador da Organização do Exchange ou Administrador do Exchange Server atribuída. Além disso, você deve ter a função Administrador de Pasta Pública e o grupo local Administradores atribuídos para o servidor de destino. Confira os detalhes em [Como adicionar um usuário ou um grupo a uma função de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779)

8.  Se estiver usando o Exchange Server 2007 no Windows Server 2008 x64, você deverá atualizar para o [Windows PowerShell 2.0 e WinRM 2.0 para Windows Server 2008 x64 Edition (KB968930)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930). Se estiver usando o Exchange Server 2007 no Windows Server 2003 x64, você deverá atualizar para o Windows PowerShell 2.0. Para saber mais, confira [Atualização do Windows Server 2003 x64 Edition (KB968930)](https://www.microsoft.com/pt-br/download/details.aspx?id=10512).

9.  Para acessar as pastas públicas entre locais, os usuários devem atualizar seus clientes do Outlook para a atualização pública de novembro de 2012 do Outlook ou posterior.
    
    1.  Para baixar a atualização do Outlook de novembro de 2012 para Outlook 2010, confira [Atualização do Microsoft Outlook 2010 (KB2687623) Edição de 32 bits](https://www.microsoft.com/pt-br/download/details.aspx?id=35702).
    
    2.  Para baixar a atualização do Outlook de novembro de 2012 para Outlook 2007, confira [Atualização para o Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/pt-br/download/details.aspx?id=35718).

10. O Outlook 2016 para Mac (e versões anteriores) e o Outlook para Mac para Office 365 não têm suporte para pastas públicas herdadas entre instalações. Os usuários devem estar no mesmo local que as pastas públicas para acessá-las com o Outlook para Mac ou com o Outlook para Mac para Office 365. Além disso, os usuários cujas caixas de correio estão no Exchange Online não terão acesso às pastas públicas no local usando o Outlook Web App.

11. Depois de seguir as instruções do artigo para configurar as pastas públicas no local para uma implantação híbrida, os usuários externos da organização não poderão enviar mensagens para as pastas públicas no local, a menos que você realize outros procedimentos. Você pode definir o domínio aceito para as pastas públicas como Retransmissão Interna (para saber mais, confira [Gerenciar domínios aceitos no Exchange Online](https://technet.microsoft.com/pt-br/library/jj945194\(v=exchg.150\))) ou desabilitar o DBEB (Bloqueio de Borda Baseado em Diretório), conforme descrito no tópico [Usar Bloqueio de Borda Baseado em Diretório para Rejeitar Mensagens Enviadas a Destinatários Inválidos](https://technet.microsoft.com/pt-br/library/dn600322\(v=exchg.150\)).

## Etapa 2 – Tornar pastas públicas remotas detectáveis

1.  Se as pastas públicas estiverem no Exchange 2010 ou em servidores posteriores, você deverá instalar a função de servidor Acesso para Cliente em todos os servidores de caixa de correio que tiverem um banco de dados de pasta pública. Dessa forma, é possível executar o serviço RpcClientAccess do Microsoft Exchange, para que todos os clientes possam acessar as pastas públicas. Os servidores de pastas públicas do Exchange 2007 não exigem a função de Acesso para Cliente, portanto, esta etapa não é necessária. Para saber mais, confira o artigo [Instalar o Exchange Server 2010](https://technet.microsoft.com/pt-br/library/bb124778\(v=exchg.141\).aspx). Esta etapa não é necessária para pastas públicas do Exchange 2007.
    

    > [!TIP]
    > Este servidor não precisa fazer parte do balanceamento de carga de acesso para cliente. Para saber mais, confira o artigo <A href="https://technet.microsoft.com/pt-br/library/ff625247(v=exchg.141).aspx">Noções básicas sobre balanceamento de carga no Exchange 2010</A>.



2.  Crie um banco de dados de caixa de correio vazio em cada servidor de pasta pública.
    
    Para o Exchange 2010, execute o seguinte comando. Este comando exclui o banco de dados de caixa de correio do balanceador de carga de provisionamento de caixa de correio. Isso evita que novas caixas de correio sejam automaticamente adicionadas a esse banco de dados.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    Para o Exchange 2007, execute o seguinte comando:
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!TIP]
    > Recomendamos que a única caixa de correio que você adicionar a esse banco de dados seja a caixa de correio de proxy que você criará na etapa 3. Nenhuma outra caixa de correio deve ser criada nesse banco de dados de caixa de correio.



3.  Crie uma caixa de correio de proxy no novo banco de dados de caixa de correio e oculte a caixa de correio do catálogo de endereços. O SMTP desta caixa de correio será devolvido pela Descoberta Automática como o SMTP *DefaultPublicFolderMailbox*, de modo que, ao resolver esse SMTP, o cliente possa acessar o servidor Exchange herdado para acesso à pasta pública.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Para o Exchange 2010, habilite a Descoberta Automática para retornar as caixas de correio de pasta pública de proxy. Esta etapa não é necessária para o Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Repita as etapas anteriores para cada servidor de pasta pública em sua organização.

## Etapa 3 – Baixar os scripts

1.  Baixe os seguintes arquivos de [Pastas públicas habilitadas para email – Script de sincronização de diretórios](https://www.microsoft.com/pt-br/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Salve os arquivos no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts.

## Etapa 4 – Configurar a sincronização de diretórios

O serviço de Sincronização de Diretório não sincroniza pastas públicas habilitadas para email. Executar o script a seguir sincronizará as pastas públicas habilitadas para email nos locais. As permissões especiais atribuídas a pastas públicas habilitadas para emails devem ser recriadas na nuvem, já que as permissões entre instalações não têm suporte nos cenários de implantação híbrida. Para saber mais, confira o tópico [Implantação híbrida do Exchange Server 2013](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!TIP]
> As pastas públicas habilitadas para email sincronizadas serão exibidas como objetos de contato de email para fins de fluxo de emails e não serão exibidas no Centro de administração do Exchange. Veja o comando Get-MailPublicFolder. Para recriar as permissões SendAs na nuvem, use o comando Add-RecipientPermission.



1.  No servidor Exchange herdado, execute o seguinte comando para sincronizar as pastas públicas habilitadas para email do Microsoft Active Directory local com o Office 365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Em que `Credential` é o nome de usuário e a senha do Office 365 e `CsvSummaryFile` é o caminho no qual você deseja registrar erros e operações de sincronização no formato .CSV.


> [!TIP]
> Antes de executar o script, recomendamos primeiro simular as ações que ele executaria no ambiente, o que pode ser feito executando-o com o parâmetro <CODE>-WhatIf</CODE>, conforme descrito acima.<BR>Recomendamos também executar esses scripts diariamente a fim de sincronizar as pastas públicas habilitadas para email.



## Etapa 5 – Configurar os usuários do Exchange Online para acessar pastas públicas no local

A etapa final deste procedimento consiste em configurar a organização do Exchange Online e permitir o acesso a pastas públicas locais herdadas.

Habilite a organização do Exchange Online para acessar as pastas públicas no local. Você deve apontar para todas as caixas de correio de pasta pública de proxy que criou na Etapa 2 – Tornar pastas públicas remotas detectáveis.

Execute o seguinte comando no **Windows PowerShell**:

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

Você deve esperar a conclusão da sincronização do ActiveDirectory para ver as alterações. Pode levar até três horas para concluir esse processo. Caso prefira não esperar pelas sincronizações recorrentes que ocorrem a cada três horas, você pode forçar a sincronização de diretórios a qualquer momento. Confira as etapas detalhadas sobre como forçar a sincronização de diretórios em [Forçar sincronização de diretórios](http://technet.microsoft.com/pt-br/library/jj151771.aspx). O Office 365 seleciona aleatoriamente uma das caixas de correio de pasta pública fornecidas neste comando.


> [!IMPORTANT]
> Um usuário do Office 365 que não esteja representado por um objeto MailUser no local (local da hierarquia de pastas públicas de destino) não terá acesso a pastas públicas locais herdadas ou do Exchange 2013. Confira a solução no artigo da Base de Dados de Conhecimento <A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Os usuários do Exchange Online não podem acessar pastas públicas locais herdadas</A>.



## Como saber se funcionou?

1.  Faça logon no Outlook para um usuário que esteja no Exchange Online e execute os seguintes testes de pasta pública:
    
      - Visualize a hierarquia.
    
      - Verifique as permissões
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

## Começando a usar o Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="O ícone pequeno do LinkedIn Learning" alt="O ícone pequeno do LinkedIn Learning" /> <strong>Começando a usar o Office 365?</strong><br />
Descubra cursos em vídeo gratuitos para <a href="https://support.office.com/pt-br/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, oferecidos pelo LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

