---
title: 'Usar migração de lote em pastas herdadas no Office 365 e Exchange Online'
TOCTitle: Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63763692
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2018-03-26_

**Resumo:**  Use estes procedimentos para migrar suas pastas públicas do Exchange 2007 e do Exchange 2010 para o Office 365.

Este tópico descreve como migrar suas pastas públicas em uma migração rápida ou em estágios do Pacote Cumulativo de Atualizações 8 para Exchange Server 2010 Service Pack 3 (SP3) ou do Pacote Cumulativo de Atualizações 15 para Exchange 2007 SP3 para o Office 365 ou o Exchange Online.

Este tópico chama os servidores Exchange 2010 SP3 RU8 e Exchange 2007 SP3 RU15 de *servidores Exchange herdados*. Da mesma forma, as etapas deste tópico podem ser aplicadas ao Exchange Online e ao Office 365. Os termos podem ser usados de maneira intercambiável nesse tópico.


> [!NOTE]
> O método de migração em lotes descrito neste artigo é o único método com suporte para migrar pastas públicas legadas para o Office 365 e o Exchange Online. O método antigo de migração em série para migrar pastas públicas está se tornando obsoleto e já não tem mais o suporte da Microsoft.



Recomendamos que você não use o recurso de exportação de PST do Outlook para migrar pastas públicas para o Office 365 ou o Exchange Online. O crescimento da caixa de correio de pastas públicas do Office 365 e do Exchange Online é gerenciado por meio de um recurso de divisão automática que divide a caixa de correio de pastas públicas quando ela excede as cotas de tamanho. A divisão automática não pode lidar com o crescimento repentino de caixas de correio de pastas públicas quando você usa a exportação de PST para migrar suas pastas públicas, e talvez você precise esperar até duas semanas para que a divisão automática migre os dados da caixa de correio principal. Recomendamos o uso das instruções baseadas em cmdlet neste documento para migrar pastas públicas para o Office 365 e o Exchange Online. No entanto, se você optar por migrar pastas públicas usando a exportação de PST, confira a seção Migrar pastas públicas para o Office 365 usando exportação de PST do Outlook mais adiante neste tópico.

Você realizará a migração usando os cmdlets **\*-MigrationBatch**, além dos seguintes scripts PowerShell:

  - `Export-PublicFolderStatistics.ps1`   Esse script cria o arquivo de mapeamento de nome da pasta para tamanho de pasta. Você deve executar esse script no servidor Exchange herdado.

  - `Export-PublicFolderStatistics.psd1`   Esse arquivo de suporte é usado pelo script `Export-PublicFolderStatistics.ps1` e deve ser baixado no mesmo local.

  - `PublicFolderToMailboxMapGenerator.ps1`   Esse script cria o arquivo de mapeamento de pasta pública para caixa de correio usando a saída do script `Export-PublicFolderStatistics.ps1`. Você deve executar esse script no servidor Exchange herdado.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   Esse arquivo de suporte é usado pelo script `PublicFolderToMailboxMapGenerator.ps1` e deve ser baixado no mesmo local.

  - `Create-PublicFolderMailboxesForMigration.ps1` Esse script cria as caixas de correio de pastas públicas de destino para a migração. Além disso, esse script calcula o número de caixas de correio necessário para lidar com a carga de usuários estimada, com base nas orientações referentes ao número de logons de usuário por caixa de correio de pastas públicas recomendado em [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Esse arquivo de suporte é usado pelo script Create-PublicFolderMailboxesForMigration.ps1 e deve ser baixado no mesmo local.

  - `Sync-MailPublicFolders.ps1`  Esse script sincroniza objetos de pasta pública habilitados para email entre a sua implantação local do Exchange e o Office 365. Você deve executar esse script no servidor Exchange herdado.

  - `SyncMailPublicFolders.strings.psd1`   Este é um arquivo de suporte usado pelo script `Sync-MailPublicFolders.ps1` e deve ser copiado para o mesmo local que os scripts anteriores.

Etapa 1: Baixar os scripts de migração fornece detalhes sobre onde baixar esses scripts. Certifique-se de que todos os scripts sejam baixados para o mesmo local.

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## Quais versões do Exchange oferecem suporte à migração de pastas públicas para o Office 365 e o Exchange Online?

O Exchange oferece suporte à movimentação das suas pastas públicas para o Office 365 e o Exchange Online a partir das seguintes versões herdadas do Exchange Server:

  - Exchange 2010 SP3 RU8 ou versão posterior

  - Exchange 2007 SP3 RU15 ou versão posterior

Se você precisar mover suas pastas públicas para o Exchange Online, mas seus servidores locais não estiverem executando as versões mínimas com suporte do Exchange 2010 ou do Exchange 2007, recomendamos atualizar seus servidores locais e usar a migração em lotes, que é o único método de migração de pastas públicas com suporte.

Não é possível migrar pastas públicas diretamente do Exchange 2003. Se você estiver executando o Exchange 2003 na sua organização, precisará migrar todos os bancos de dados de pastas públicas e réplicas para o Exchange 2010 SP3 RU8 ou versão posterior ou para o Exchange 2007 SP3 RU10 ou versão posterior. Nenhuma réplica de pasta pública pode permanecer no Exchange 2003. Além disso, as mensagens destinadas a uma pasta pública do Exchange 2013 não podem ser roteadas por meio de um servidor Exchange 2003.

## O que você precisa saber antes de começar?

  - O servidor Exchange Server 2010 precisa estar executando o Exchange 2010 SP3 RU8 ou versão posterior.

  - O servidor Exchange Server 2007 precisa estar executando o Exchange 2007 SP3 RU15 ou versão posterior.

  - No Office 365 e no Exchange Online, você precisa ser membro do grupo de função Gerenciamento da Organização. Esse grupo de função é diferente das permissões atribuídas quando você assina o Office 365 ou o Exchange Online. Para obter detalhes sobre como habilitar o grupo de função Gerenciamento da Organização, confira [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - No Exchange 2010, você deve ser membro dos grupos de função RBAC Gerenciamento da Organização ou Gerenciamento de Servidor. Para obter detalhes, confira o tópico sobre como [adicionar membros a um grupo de função](https://go.microsoft.com/fwlink/?linkid=299212).

  - No Exchange 2007, você precisa ter a função Administrador da Organização do Exchange ou a função Administrador do Exchange Server atribuída. Além disso, você deve ter a função Administrador de Pasta Pública e o grupo local Administradores atribuídos para o servidor de destino. Para obter detalhes, confira o tópico sobre [Como adicionar um usuário ou grupo a uma função de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - No servidor Exchange 2007, atualize para o [Windows PowerShell 2.0 e o WinRM 2.0 para Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Antes da migração, se alguma pasta pública na sua organização for maior do que 2 GB, recomendamos que você exclua o conteúdo dessa pasta ou divida esse conteúdo em várias pastas públicas. Se uma dessas opções não for possível, recomendamos que não mova suas pastas públicas para o Office 365 ou o Exchange Online.

  - No Office 365 e no Exchange Online, você pode criar um máximo de mil caixas de correio de pastas públicas.

  - Antes de migrar suas pastas públicas, recomendamos que todas as caixas de correio de usuários sejam movidas para o Office 365 e o Exchange Online. Para obter mais detalhes, confira as [Maneiras de migrar várias contas de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

  - O Outlook em Qualquer Lugar precisa estar habilitado no servidor Exchange herdado. Para obter detalhes sobre como habilitar o Outlook em Qualquer Lugar em servidores Exchange 2010, confira o tópico sobre como [Habilitar o Outlook em Qualquer Lugar](https://go.microsoft.com/fwlink/p/?linkid=187249). Para obter detalhes sobre como habilitar o Outlook em Qualquer Lugar em servidores Exchange 2007, confira o tópico sobre [Como habilitar o Outlook em Qualquer Lugar](https://go.microsoft.com/fwlink/p/?linkid=167210).

  - Não é possível usar o EAC (Centro de administração do Exchange) ou o EMC (Console de gerenciamento do Exchange) para realizar esse procedimento. Nos servidores Exchange herdados, você precisa usar o Shell de Gerenciamento do Exchange. Para o Exchange Online, você precisa usar o PowerShell do Exchange Online. Para mais informações, confira [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)).

  - Antes de começar, recomendamos a leitura integral deste tópico, pois um certo tempo de inatividade é necessário para algumas etapas.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Veja o que acontece em cada etapa: Baixar os scripts de migração

1.  Baixe todos os scripts e arquivos de suporte de [Scripts de migração de pastas públicas](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Salve os scripts no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts. Verifique se que todos os scripts estão salvos no mesmo local.

3.  Baixe os seguintes arquivos de [Pastas públicas habilitadas para email – script de sincronização de diretórios](https://go.microsoft.com/fwlink/p/?linkid=532376):
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  Salve os scripts no mesmo local que da etapa 2. Por exemplo, C:\\PFScripts.

## Etapa 2: Preparar-se para a migração

Realize as seguintes etapas de pré-requisitos antes de iniciar a migração.

**Etapas gerais de pré-requisito**

  - Certifique-se de que não haja nenhum objeto de email de pasta pública órfão no Active Directory, ou seja, objetos no Active Directory sem um objeto do Exchange correspondente.

  - Confirme se o endereço de email SMTP configurado para pastas públicas no Active Directory corresponde aos endereços de email SMTP nos objetos do Exchange.

  - Certifique-se de que não há nenhum objeto de pasta pública duplicado no Active Directory, para evitar uma situação em que dois ou mais objetos do Active Directory apontam para a mesma pasta pública habilitada para email.

**Etapas de pré-requisitos no servidor Exchange herdado**

1.  No servidor Exchange herdado, certifique-se de que o roteamento para as pastas públicas habilitadas para email que estarão no Office 365 e no Exchange Online continue em funcionamento até que todos os caches de DNS na cache sejam atualizados para apontar para os DNS do Exchange Online, onde sua organização reside agora. Para fazer isso, execute o seguinte comando para configurar um domínio aceito com um nome conhecido que irá rotear corretamente as mensagens de email para o domínio do Office 365 ou do Exchange Online.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  Se o nome de uma pasta pública contiver uma barra invertida **\\**, as pastas públicas serão criadas na pasta pública pai quando a migração ocorrer. Antes de migrar, recomendamos que você renomeie todas as pastas públicas que tiverem uma barra invertida no nome.
    
    1.  No Exchange 2010, para localizar pastas públicas que possuem uma barra invertida no nome, execute o seguinte comando:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  No Exchange 2007, para localizar pastas públicas que possuem uma barra invertida no nome, execute o seguinte comando:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Se qualquer pasta pública for retornada, você poderá renomeá-la executando o seguinte comando:
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Verifique se não existe um registro anterior de uma migração bem-sucedida. Em caso afirmativo, você precisará definir esse valor como `$false`. Se o valor for definido como `$true`, a solicitação de migração falhará.
    
    1.  O exemplo a seguir verifica o status de migração de pasta pública.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  Se o status das propriedades *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* for `$true`, execute o seguinte comando para definir o valor como `$false`.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!CAUTION]
    > Depois de redefinir essas propriedades, você deverá aguardar até que o Exchange detecte as novas configurações. Isso pode demorar até duas horas.



4.  Para fins de verificação no final da migração, recomendamos que você primeiro execute os seguintes comandos Shell de Gerenciamento do Exchange no servidor Exchange herdado para tirar instantâneos da sua implantação de pastas públicas atual.
    
    1.  Execute o seguinte comando para obter um instantâneo da estrutura de pastas original.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  Execute o seguinte comando para obter um instantâneo de estatísticas de pastas públicas, como contagem de itens, tamanho e proprietário.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  Execute o seguinte comando para obter um instantâneo das permissões.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Salve as informações dos comandos anteriores para comparação no final da migração.

5.  Se você estiver usando o Microsoft Azure Active Directory Connect (conectar do Azure AD) para sincronizar seus diretórios no local com o Windows Azure Active Directory, você precisará fazer o seguinte (se você não estiver usando Connect do Azure AD, você pode ignorar esta etapa):
    
    1.  Em um computador local, abra o Microsoft Azure Active Directory Connect e, em seguida, selecione **Configurar**.
    
    2.  Na tela **tarefas adicionais**, selecione **Personalizar opções de sincronização** e, em seguida, clique em **Avançar**.
    
    3.  Na tela **conectar ao AD do Windows Azure**, digite as credenciais apropriadas e clique em **Avançar**. Uma vez conectado, continue clicando em **Avançar** até que você esteja na tela **Recursos opcionais** .
    
    4.  Certifique-se de que as **Pastas públicas de email do Exchange** não está selecionada. Se ainda não estiver selecionado, você poderá continuar na próxima seção, *que etapas de pré-requisito no Office 365 ou Exchange Online*. Se ela estiver selecionada, clique para desmarcar a caixa de seleção e, em seguida, clique em **Avançar**.
        

        > [!TIP]
        > Se você não vir a <STRONG>Pastas públicas do Exchange Mail</STRONG> como uma opção na tela <STRONG>Recursos opcionais</STRONG>, você pode sair do Microsoft Azure Active Directory Connect e prossiga para a próxima seção, <EM>que etapas de pré-requisito no Office 365 ou Exchange Online</EM>.

    
    5.  Após você ter desmarcado a seleção de **Pastas públicas do Exchange Mail**, mantenha a clicar em **Avançar** até que você esteja na tela **pronto para configurar** e, em seguida, clique em **Configurar**.

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [New-AcceptedDomain](https://technet.microsoft.com/pt-br/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/pt-br/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/pt-br/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/pt-br/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/pt-br/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/pt-br/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Etapas de pré-requisito no Office 365 ou Exchange Online**

1.  Certifique-se de que não haja solicitações de migração de pastas públicas. Se elas existirem, apague-as, ou sua própria solicitação de migração falhará. Essa etapa não é necessária em todos os casos; ela apenas será obrigatória se você achar que pode haver uma solicitação de migração no pipeline.
    
    Uma solicitação de migração existente pode ser um destes dois tipos: migração em lotes ou migração em série. Os comandos para detectar solicitações para cada tipo e para a remoção de solicitações de cada tipo são da seguinte forma.
    

    > [!IMPORTANT]
    > Antes de remover uma solicitação de migração, é importante compreender por que havia uma existente. Executar os comandos a seguir determinará quando foi feita uma solicitação anterior e ajudará a diagnosticar problemas que podem ter ocorrido. Talvez você precise se comunicar com outros administradores na sua organização para determinar por que a alteração foi feita.

    
    O exemplo a seguir descobrirá todas as solicitações de migração em série existentes.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    O exemplo a seguir remove todas as solicitações de migração em série de pastas públicas existentes.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    O exemplo a seguir descobrirá todas as solicitações de migração em lotes existentes.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    O exemplo a seguir remove todas as solicitações de migração em lotes de pastas públicas existentes.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Verifique se não há pastas públicas nem caixas de correio de pasta pública no Office 365.
    

    > [!IMPORTANT]
    > Se você vir as pastas públicas no Office 365 ou Exchange Online, é importante determinar o que eles são e quem na sua organização tiver iniciado uma hierarquia de pasta pública antes de remover as pastas públicas e caixas de correio de pasta pública.

    
    1.  No Office 365 ou no Exchange Online PowerShell, execute o seguinte comando para ver se existem caixas de correio de pastas públicas.
        
            Get-Mailbox -PublicFolder 
    
    2.  Se o comando não retornou nenhuma caixa de correio de pastas públicas, continue até Etapa 3: Gerar os arquivos .csv. Se o comando retornou alguma caixa de correio de pastas públicas, execute o seguinte comando para ver se existem pastas públicas:
        
            Get-PublicFolder
    
    3.  Se você tiver alguma pasta pública no Office 365 ou no Exchange Online, execute o seguinte comando do PowerShell para removê-las. Verifique se você salvou todas as informações que estavam nas pastas públicas no Office 365. Todas as informações contidas nas pastas públicas serão excluídas permanentemente quando você remover as pastas públicas.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Depois que as pastas públicas forem removidas, execute os seguintes comandos para remover todas as caixas de correio de pastas públicas.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/pt-br/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/pt-br/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/pt-br/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/pt-br/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/pt-br/library/aa995948\(v=exchg.150\))

## Etapa 3: Gerar os arquivos .csv

1.  No servidor Exchange herdado, execute o script `Export-PublicFolderStatistics.ps1` para criar o arquivo de mapeamento de nome de pasta para tamanho de pasta. Esse script sempre deve ser executado por um administrador local. O arquivo conterá duas colunas: **FolderName** e **FolderSize**. Os valores da coluna **FolderSize** serão exibidos em bytes. Por exemplo, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* equivale ao nome de domínio totalmente qualificado do servidor de Caixa de Correio no qual a hierarquia da pastas públicas está hospedada.
    
      - *Folder to size map path* equivale ao nome do arquivo e ao caminho em uma pasta de rede compartilhada na qual você deseja salvar o arquivo .csv. Mais adiante neste tópico, você precisará usar o PowerShell do Exchange Online para acessar este arquivo. Se você especificar apenas o nome de arquivo, o arquivo será gerado no diretório atual do PowerShell no computador local.
    
      - Se necessário, remova todas as pastas do sistema habilitadas para email da saída do script antes de continuar.

2.  Execute o script `PublicFolderToMailboxMapGenerator.ps1` para criar o arquivo de mapeamento de pastas públicas para caixas de correio. Esse arquivo é usado para calcular o número correto de caixas de correio de pasta pública no Exchange Online.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > O arquivo de mapeamento de correio de pasta pública não deve exceder 1.000 linhas. Se esse arquivo exceder 1.000 linhas, sua estrutura de pasta pública deve ser simplificado. Prosseguir com um arquivo de mais de 1.000 linhas não é recomendado e pode causar erros de migração.

    
      - Antes de executar o script, use o seguinte cmdlet para verificar os limites de pasta pública atual no seu locatário do Exchange Online. Em seguida, observe os valores de cota atual para pastas públicas. `Get-OrganizationConfig | fl *quota*`
        
        No Exchange Online, o valor padrão é 1.7 GB para **DefaultPublicFolderIssueWarningQuota** e 2 GB para **DefaultPublicFolderProhibitPostQuota**.
    
      - *Maximum mailbox size in bytes* equivale ao tamanho máximo que você deseja definir para novas caixas de correio de pasta pública. No Exchange Online, o tamanho máximo de caixas de correio de pasta pública é de 100 GB. Recomendamos que você use uma configuração de 15 GB para que cada caixa de correio de pasta pública tenha espaço para crescer. O Exchange Online tem uma cota de "Proibir postagem" de pasta pública padrão de 2 GB. Se você tiver pastas públicas individuais que são maiores do que 2 GB, você pode usar qualquer uma das seguintes opções para corrigir esse problema:
        
          - Antes de iniciar o lote de migração, aumente a cota de "Proibir postagem" da pasta pública padrão executando o seguinte cmdlet:
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - Antes de iniciar o lote de migração, exclua o conteúdo para reduzir o tamanho do conteúdo para 2 GB ou menos de pasta pública.
        
          - Antes de iniciar o lote de migração, divida a pasta pública em várias pastas públicas que tenham cada 2 GB ou menos.
        

        > [!TIP]
        > Se a pasta pública for maior do que 30 GB, e se ele não for viável para excluir conteúdo ou dividi-lo em várias pastas públicas, recomendamos que você não move suas pastas públicas para o Exchange Online.

    
      - *Folder to size map path* é igual o caminho do arquivo do arquivo. csv que você criou quando executou o script `Export-PublicFolderStatistics.ps1` .
    
      - é igual a *Folder to mailbox map path* , o nome de arquivo e caminho do arquivo. csv de correio de pasta que você criado nesta etapa. Se você especificar apenas o nome do arquivo, o arquivo é gerado no diretório atual do PowerShell no computador local.


> [!TIP]
> Depois que os scripts são executados e os arquivos. csv são gerados, quaisquer novas pastas públicas ou atualizações para pastas públicas existentes não serão coletadas.



## Etapa 4: Criar as caixas de correio de pasta pública no Exchange Online

1.  Execute o seguinte comando para criar as caixas de correio de pastas públicas de destino. O script criará uma caixa de correio de destino para cada caixa de correio no arquivo .csv que você gerou anteriormente na Etapa 3, executando o script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* é o arquivo gerado pelo script PublicFoldertoMailboxMapGenerator.ps1 na Etapa 3. O número estimado de conexões de usuários simultâneas navegando em uma hierarquia de pastas públicas é geralmente menor que o número total de usuários em uma organização.

## Etapa 5: Iniciar a solicitação de migração

1.  No servidor Exchange herdado, execute o seguinte comando para sincronizar pastas públicas habilitadas para email do seu Active Directory local para o Exchange Online.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` é seu nome de usuário do Office 365 e a senha. `CsvSummaryFile` é o caminho de arquivo no qual você deseja registrar, no formato .CSV, erros e operações de sincronização.
    

    > [!TIP]
    > Recomendamos que você primeiro simule as ações que o script executaria antes de realmente executá-lo, o que pode ser feito executando o script com um parâmetro <CODE>-WhatIf</CODE>.



2.  No servidor Exchange herdado, obtenha as seguintes informações que são necessárias para executar a solicitação de migração:
    
    1.  Encontre o `LegacyExchangeDN` da conta do usuário que é um membro da função de Administrador de Pasta Pública. Este será o mesmo usuário de cujas credenciais você precisa na etapa 3 desse procedimento.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Encontre o `LegacyExchangeDN` de qualquer servidor de caixa de correio que tenha um banco de dados de pastas públicas.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Encontre o FQDN do nome de host do Outlook em Qualquer Lugar. Se tiver várias instâncias do Outlook em Qualquer Lugar, recomendamos que você selecione a instância que seja a mais próxima do ponto de extremidade de migração ou a que seja a mais próxima das réplicas de pasta pública na organização do Exchange herdado. O seguinte comando encontrará todas as instâncias do Outlook em Qualquer Lugar:
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  No PowerShell do Office 365, execute os seguintes comandos para passar as informações retornadas na etapa anterior para as variáveis que serão utilizadas na solicitação de migração.
    
    1.  Passe a credencial de um usuário que tem permissões administrativas no servidor Exchange herdado para a variável `$Source_Credential`. A solicitação de migração executada no Exchange Online usará essa credencial para obter acesso aos seus servidores Exchange herdados a fim de copiar o conteúdo.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  Use o `ExchangeLegacyDN` do usuário de migração no servidor herdado do Exchange encontrado na etapa 2a e passe-o para a variável `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  Use o `ExchangeLegacyDN` do servidor de pasta pública que encontrado na etapa 2b acima e passe-o para a variável `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  Use o Nome de Host Externo do Outlook em Qualquer Lugar que você encontrou na etapa 2c acima e passe-o para a variável `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  Por fim, no PowerShell do Exchange Online, execute os seguintes comandos para criar a solicitação de migração.
    

    > [!TIP]
    > O método de autenticação no exemplo de Shell de Gerenciamento do Exchange a seguir precisa corresponder às configurações do seu Outlook em Qualquer Lugar, caso contrário, o comando falhará.

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    Onde o arquivo \<*folder\_mapping.csv*\> é o arquivo gerado na Step 3: Generate the .csv files.

5.  Inicie a migração usando o seguinte comando:
    
        Start-MigrationBatch PublicFolderMigration

Embora as migrações em lotes precisem ser criadas usando o cmdlet **New-MigrationBatch** no Shell de Gerenciamento do Exchange, o andamento e a conclusão da migração podem ser visualizados e gerenciados no EAC. Como o cmdlet **New-MigrationBatch** inicia uma solicitação de migração de caixa de correio para cada caixa de correio de pastas públicas, você pode visualizar o status dessas solicitações usando a página de migração de caixas de correio. Você pode acessar a página de migração de caixa de correio e criar relatórios de migração que podem ser enviados por email para você fazendo o seguinte:

1.  Faça logon no Exchange Online e abra o EAC.

2.  Navegue até **Caixa de Correio** \> **Migração**.

3.  Selecione a solicitação de migração que você acabou de criar e clique em **Exibir Detalhes** no painel **Detalhes**.

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/pt-br/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/pt-br/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/pt-br/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/pt-br/library/jj218697\(v=exchg.150\))

## Etapa 6: Bloquear as pastas públicas no servidor Exchange herdado para a migração final (tempo de inatividade necessário)

Até este ponto na migração, os usuários eram capazes de acessar pastas públicas. As próximas etapas farão o logoff dos usuários das pastas públicas legadas e as bloqueará enquanto a migração realiza sua sincronização final. Os usuários não conseguirão acessar as pastas públicas durante esse processo. Além disso, os emails enviados para pastas públicas habilitadas para email serão enfileirados e não serão entregues até a conclusão da migração das pastas públicas.

Antes de executar o comando `PublicFoldersLockedForMigration` conforme descrito abaixo, certifique-se de que todos os trabalhos estejam no estado **sincronizado**. Você pode fazer isso executando o comando `Get-PublicFolderMailboxMigrationRequest` . Continue com esta etapa somente depois de verificar que todos os trabalhos estejam no estado **sincronizado**.

No servidor Exchange herdado, execute o seguinte comando para bloquear as pastas públicas herdadas para finalização.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

Se a sua organização tiver vários bancos de dados de pastas públicas, você terá que aguardar a conclusão da replicação de pastas públicas para confirmar que todos os bancos de dados de pastas públicas selecionaram o sinalizador `PublicFoldersLockedForMigration` e que todas as alterações pendentes feitas recentemente pelos usuários foram convergidas em pastas para pastas têm convergidas por toda a organização. Isso pode levar várias horas.

## Etapa 7: Finalizar a migração de pasta pública (tempo de inatividade necessário)

Execute o comando a seguir para concluir a migração das pastas públicas:

    Complete-MigrationBatch PublicFolderMigration

Quando você concluir a migração, o Exchange executará uma sincronização final entre o servidor Exchange herdado e o Exchange Online. Se a sincronização final for bem-sucedida, as pastas públicas no Exchange Online serão bloqueadas, e o status do lote de migração será alterado como **concluído**. É comum para o lote de migração demorar algumas horas antes da alteração do status de **sincronizado** a **Concluindo**, no momento em que a sincronização final será iniciada.

Se você configurou uma implantação híbrida entre seus servidores Exchange locais e o Office 365, será necessário executar o seguinte comando no PowerShell do Exchange Online após a conclusão da migração:

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Etapa 8: Testar e desbloquear a migração de pastas públicas

Depois de finalizar a migração de pastas públicas, você deve executar o seguinte teste para garantir que a migração foi bem-sucedida. Isso permite que você teste a hierarquia de pastas públicas migradas antes de alternar para o uso de pastas públicas do Office 365 ou Exchange Online.

1.  No Office 365 ou no Exchange Online PowerShell, atribua algumas caixas de correio de teste para usar qualquer caixa de correio de pasta pública recém-migrada como a caixa de correio de pasta pública padrão.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Faça logon no Outlook 2007 ou versão posterior com o usuário de teste identificado na etapa anterior e, em seguida, realize os seguintes testes de pastas públicas:
    
      - Visualize a hierarquia.
    
      - Verifique as permissões.
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

3.  Se você tiver quaisquer problemas, consulte Reverter a migração , mais adiante neste tópico. Se o conteúdo de pasta pública e a hierarquia é aceitáveis e funciona como esperado, prossiga para a próxima etapa.

4.  No servidor Exchange herdado, execute o seguinte comando para indicar que a migração de pastas públicas está concluída:
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Depois de verificar se a migração está concluída, execute o seguinte comando no PowerShell do Exchange Online para garantir que o parâmetro *PublicFoldersEnabled* em **Set-OrganizationConfig** esteja definido como `Local`:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

[Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\))

## Como saber se funcionou?

Na Step 2: Prepare for the migration, você recebeu instruções para obter instantâneos da estrutura de pastas públicas, de estatísticas e de permissões antes do início da migração. As etapas seguintes ajudarão a verificar se a migração de pastas públicas foi bem-sucedida, obtendo os mesmos instantâneos após a conclusão da migração. Dessa forma, você pode comparar os dados em ambos os arquivos para verificar o êxito da operação.

1.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo da nova estrutura de pastas.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo das estatísticas de pasta pública, como total de itens, tamanho e proprietário.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo das permissões.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Remover bancos de dados de pastas públicas dos servidores Exchange herdados

Após a conclusão da migração, e depois de ter verificado que suas pastas públicas do Exchange Online estão funcionando conforme o esperado, remova os bancos de dados de pasta pública dos servidores Exchange herdados.


> [!IMPORTANT]
> Como todas as suas caixas de correio foram migradas para o Office 365 antes da migração de pastas públicas, convém direcionar o tráfego pelo Office 365 (fluxo de emails descentralizado) em vez do fluxo de emails centralizado por meio do seu ambiente local. Se você optar por manter o fluxo de emails centralizado, isso poderá causar problemas de entrega para as suas pastas públicas, já que você removeu os bancos de dados de caixa de correio de pastas públicas da sua organização local.



  - Para mais detalhes sobre como remover bancos de dados de pastas públicas de servidores Exchange 2007, confira o tópico sobre como [remover bancos de dados de pastas públicas](https://go.microsoft.com/fwlink/?linkid=123678).

  - Para mais detalhes sobre como remover bancos de dados de pastas públicas de servidores Exchange 2010, confira o tópico sobre como [remover bancos de dados de pastas públicas](https://go.microsoft.com/fwlink/?linkid=81409).

## Reverter a migração

Se você encontrar problemas com a migração e precisar reativar suas pastas públicas do Exchange herdadas, realize as etapas a seguir.


> [!WARNING]
> Se você reverter sua migração para os servidores Exchange herdados, perderá todos os emails que foram enviados para as pastas públicas habilitadas para email ou todo o conteúdo que foi postado em pastas públicas após a migração. Para salvar esse conteúdo, exporte o conteúdo da pasta pública para um arquivo .pst e, em seguida importe-o para as pastas públicas herdadas quando a reversão estiver concluída.



1.  No servidor Exchange herdado, execute o seguinte comando para desbloquear as pastas públicas herdadas do Exchange. Esse processo pode levar várias horas.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  No PowerShell do Exchange Online, execute os seguintes comandos para remover todas as pastas públicas do Exchange Online.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  No servidor Exchange herdado, execute o seguinte comando para definir o sinalizador `PublicFolderMigrationComplete` como `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Migrar pastas públicas para o Office 365 usando exportação de PST do Outlook

Recomendamos que você não use o recurso de exportação de PST do Outlook para migrar pastas públicas para o Office 365 ou Exchange Online caso a hierarquia de pastas públicas no local seja maior do que 30 GB. O crescimento da caixa de correio de pasta pública do Office 365 online é gerenciado por meio de um recurso de divisão automática, que divide a caixa de correio de pasta pública quando ela excede as cotas de tamanho. A divisão automática não poderá cuidar do crescimento repentino de caixas de correio de pasta pública se você usar a exportação PST para migrar as pastas públicas, e você talvez precise esperar até duas semanas para que a divisão automática mova os dados da caixa de correio principal. Além disso, considere o seguinte antes de usar o recurso de PST do Outlook para exportar pastas públicas para o Office 365 ou Exchange Online:

  - As permissões de pasta pública serão perdidas durante esse processo. Capture as permissões vigentes antes de migrar e as adicione manualmente, assim que a migração estiver concluída.

  - Se suar permissões complexas ou houver muitas pastas a serem migradas, recomendamos que você use o método de cmdlet para migração.

  - Qualquer alteração de item e pasta feita nas pastas públicas de origem durante a exportação PST será perdida. Portanto, recomendamos que você use o método de cmdlet se esse processo de exportação e importação demorar muito para ser concluído.

Se ainda quiser migrar suas pastas públicas usando arquivos PST, execute essas etapas para garantir o êxito da migração.

1.  Use as instruções em Etapa 1: Baixar os scripts de migração para baixar os scripts de migração. Você só precisa baixar o arquivo `PublicFolderToMailboxMapGenerator.ps1`.

2.  Execute a etapa 2 de Step 3: Generate the .csv files para criar o arquivo de mapeamento de pasta para caixa de correio. Esse arquivo é usado para calcular o número correto de caixas de correio de pasta pública no Exchange Online.

3.  Crie as caixas de correio de pasta pública necessárias com base no arquivo de mapeamento. Para saber mais, veja [Criar uma caixa de correio de pasta pública](create-a-public-folder-mailbox-exchange-2013-help.md).

4.  Use o cmdlet New-PublicFolder para criar a pasta pública de nível superior em cada uma das caixas de correio de pasta pública usando o parâmetro *Mailbox*.

5.  Exporte e importe os arquivos PST usando o Outlook.

6.  Defina as permissões nas pastas públicas usando o EAC. Para saber mais, execute a [Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) no tópico [Configurar pastas públicas em uma nova organização](set-up-public-folders-in-a-new-organization-exchange-2013-help.md).


> [!WARNING]
> Se já tiver iniciado uma migração PST e tiver encontrado um problema de caixa de correio principal cheia, você terá duas opções para recuperar a migração PST: 
> <OL>
> <LI>
> <P>Esperar até que a divisão automática mova os dados da caixa de correio principal. Isso pode levar até duas semanas. Entretanto, todas as pastas públicas em uma caixa de correio de pasta pública totalmente preenchida não poderão receber novo conteúdo enquanto a divisão automática não estiver concluída.</P>
> <LI>
> <P><A href="create-a-public-folder-mailbox-exchange-2013-help.md">Criar uma caixa de correio de pasta pública</A> e então use o cmdlet <STRONG>New-PublicFolder</STRONG> com o parâmetro <EM>Mailbox</EM> para criar as demais pastas públicas na caixa de correio de pasta pública secundária. Este exemplo cria uma nova pasta pública, chamada PF201, na caixa de correio de pasta pública secundária.</P><PRE><CODE>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</CODE></PRE></LI></OL>



## Começando a usar o Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="O ícone pequeno do LinkedIn Learning" alt="O ícone pequeno do LinkedIn Learning" /> <strong>Começando a usar o Office 365?</strong><br />
Descubra cursos em vídeo gratuitos para <a href="https://support.office.com/pt-br/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, oferecidos pelo LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

