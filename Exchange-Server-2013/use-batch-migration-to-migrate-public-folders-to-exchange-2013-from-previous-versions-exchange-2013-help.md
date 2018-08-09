---
title: 'Usar migração de lote para migrar pastas de versões prévias para Exchange 2013'
TOCTitle: Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64131809
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-03-26_

**Resumo:**  Este artigo explica como mover pastas públicas do Exchange 2007 ou Exchange 2010 para o Exchange 2013.

Este artigo descreve como migrar suas pastas públicas do Exchange Server 2010 SP3 RU8 ou RU15 do Exchange 2007 SP3 para o Microsoft Exchange Server 2013 CU7 ou posterior dentro da mesma floresta.

Nos referimos os servidores Exchange 2010 SP3 RU8 e Exchange 2007 SP3 RU15 como o *servidor Exchange herdado*.


> [!TIP]
> O método de migração de lote descrito neste artigo é o único método suportado para migração de pastas públicas herdada para o Exchange 2013. O método de migração serial antigo para migração de pastas públicas está sendo preterido e não é mais suportado pela Microsoft.



Você realizará a migração usando os cmdlets **\*MigrationBatch** e os cmdlets **\*PublicFolderMigrationRequest** para solução de problemas. Além disso, você usará os seguintes scripts PowerShell:

  - `Export-PublicFolderStatistics.ps1` Esse script cria o arquivo de mapeamento de nome para a pasta de tamanho de pasta.

  - ` Export-PublicFolderStatistics.psd1` Esse arquivo de suporte é usado pelo script Export-PublicFolderStatistics.ps1 ps1 e deve ser baixado no mesmo local.

  - `PublicFolderToMailboxMapGenerator.ps1` Esse script cria o arquivo de mapeamento de correio de pasta pública.

  - `PublicFolderToMailboxMapGenerator.strings.psd1` Esse arquivo de suporte é usado pelo script Publicfoldertomailboxmapgenerator ps1 e deve ser baixado no mesmo local.

  - `Create-PublicFolderMailboxesForMigration.ps1` Esse script cria as caixas de correio de pastas públicas de destino para a migração. Além disso, esse script calcula o número de caixas de correio necessário para lidar com a carga de usuários estimada, com base nas orientações referentes ao número de logons de usuário por caixa de correio de pastas públicas recomendado em [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Esse arquivo de suporte é usado pelo script Create-PublicFolderMailboxesForMigration.ps1 e deve ser baixado no mesmo local.

Etapa 1: baixar os scripts de migração fornece detalhes sobre onde baixar esses scripts. Certificar-se de que todos os scripts são baixados no mesmo local.

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## Quais são as versões do Exchange com suporte para a migração de pastas públicas para o Exchange 2013?

O Exchange dá suporte para a movimentação de pastas públicas a partir das seguintes versões herdadas do Exchange Server:

  - Exchange 2010 SP3 RU8 ou versão posterior

  - Exchange 2007 SP3 RU15 ou versão posterior

Se você precisar mover suas pastas públicas para o Exchange 2013, mas os servidores no local não estejam executando as versões de suporte mínimo do Exchange 2010 ou Exchange 2007, confira [Use serial migração para migrar pastas públicas para o Exchange 2013 de versões anteriores](https://technet.microsoft.com/pt-br/library/jj150486\(v=exchg.150\)). Durante a migração serial for uma opção, é altamente recomendável que você atualize os servidores no local e usar a migração de lote. Migração de lote permite significativamente mais rápida e maior confiabilidade.

Não é possível migrar pastas públicas diretamente do Exchange 2003. Se você estiver executando o Exchange 2003 em sua organização, você precisará mover todos os bancos de dados de pasta pública e réplicas para RU8 do Exchange 2010 SP3 ou posterior, ou para RU15 do Exchange 2007 SP3 ou posterior. Não há réplicas de pasta pública podem permanecer no Exchange 2003. Além disso, as mensagens destinadas a uma pasta pública do Exchange 2013 não podem ser roteadas por meio de um servidor Exchange 2003.

## O que você precisa saber antes de começar?

  - Antes de começar, recomendamos a leitura integral deste tópico, pois um certo tempo de inatividade é necessário para algumas etapas.

  - O servidor Exchange Server 2010 precisa estar executando o Exchange 2010 SP3 RU8 ou versão posterior.

  - O servidor Exchange Server 2007 precisa estar executando o Exchange 2007 SP3 RU15 ou versão posterior.

  - O número máximo de pastas públicas que podem ser migradas para o Exchange 2013 em uma única migração é 500.000.

  - No Exchange 2013, você precisa ser membro do grupo de funções de gerenciamento da organização. Para obter detalhes sobre como habilitar o grupo de funções de gerenciamento da organização, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - No Exchange 2010, você deve ser membro dos grupos de função RBAC Gerenciamento da Organização ou Gerenciamento de Servidor. Para obter detalhes, confira o tópico sobre como [adicionar membros a um grupo de função](https://go.microsoft.com/fwlink/?linkid=299212).

  - No Exchange 2007, você precisa ter a função Administrador da Organização do Exchange ou a função Administrador do Exchange Server atribuída. Além disso, você deve ter a função Administrador de Pasta Pública e o grupo local Administradores atribuídos para o servidor de destino. Para obter detalhes, confira o tópico sobre [Como adicionar um usuário ou grupo a uma função de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - No servidor Exchange 2007, atualize para o [Windows PowerShell 2.0 e o WinRM 2.0 para Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Antes de migrar, considere os [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

  - Antes de migrar, mova todas as caixas de correio do usuário para o Exchange 2013, porque os usuários com caixas de correio do Exchange 2007 ou Exchange 2010 não terão acesso a pastas públicas no Exchange 2013. Para obter detalhes, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Em um ambiente de vários domínios, o pastas públicas habilitadas para email irá parar de funcionar após a migração para o Exchange 2013, se estiver executando o Exchange em um domínio filho. Isso acontece porque no Exchange 2013, objetos de pasta pública habilitada para email deverão ser sob o domínio raiz. Para resolver esse problema, você precisa desabilitar email suas pastas públicas habilitadas para email e, em seguida, habilitar email-los novamente, que permitirá que você transfira-os para o local de domínio correto.

  - Após a migração é concluída, que se desejar que os remetentes externos para enviar emails para as pastas públicas habilitadas para email migradas, o usuário **anônimo** precisa ser concedida pelo menos a permissão de **Criar itens**. Se você não fizer isso, remetentes externos receberá uma notificação de falha de entrega e as mensagens não será entregue à pasta pública habilitada para email migrada. Para ler mais sobre como definir permissões em que o usuário anônimo, consulte [Email habilitar ou desabilitar email uma pasta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Veja o que acontece em cada etapa: Baixar os scripts de migração

1.  Baixe todos os scripts e arquivos de suporte de [Scripts de migração de pastas públicas](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Salve os scripts no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts. Verifique se que todos os scripts estão salvos no mesmo local.

## Etapa 2: Preparar-se para a migração

Realize as seguintes etapas de pré-requisitos antes de iniciar a migração.

**Etapas de pré-requisitos no servidor Exchange herdado**

1.  Para fins de verificação no final da migração, recomendamos que você primeiro execute os comandos a seguir no servidor Exchange herdado para tirar instantâneos de sua implantação de pasta pública atual:
    
      - Execute o seguinte comando para obter um instantâneo da estrutura de pasta de origem original:
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
      - Execute o seguinte comando para obter um instantâneo de estatísticas de pasta pública, como contagem de itens, tamanho e proprietário:
        
            Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
      - Execute o seguinte comando para obter um instantâneo das permissões:
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Salve as informações dos comandos anteriores para fins de comparação no final da migração.

2.  Se o nome de uma pasta pública contiver uma barra invertida **\\**, as pastas públicas serão criadas na pasta pública pai quando a migração ocorrer. Antes de migrar, recomendamos que você renomeie todas as pastas públicas que tiverem uma barra invertida no nome.
    
    1.  No Exchange 2010, para localizar pastas públicas que possuem uma barra invertida no nome, execute o seguinte comando:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  No Exchange 2007, para localizar pastas públicas que possuem uma barra invertida no nome, execute o seguinte comando:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Se qualquer pasta pública for retornada, você poderá renomeá-la executando o seguinte comando:
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Verifique se que não há um registro anterior de uma migração bem-sucedida.
    
    1.  O exemplo a seguir verifica o status de migração de pasta pública.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        
        Se houve uma migração bem-sucedida anterior, o valor das propriedades *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* é `$true`. Use o comando na etapa 3b para definir o valor como `$false`. Se o valor é definido como `$true`, sua solicitação de migração falhará.
    
    2.  Se o status das propriedades *PublicFoldersLockedforMigration* ou *PublicFolderMigrationComplete* for `$true`, execute o seguinte comando para definir o valor como `$false`.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > Depois de redefinir essas propriedades, você deverá aguardar até que o Exchange detecte as novas configurações. Isso pode demorar até duas horas.



Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-PublicFolder](https://technet.microsoft.com/pt-br/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/pt-br/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/pt-br/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/pt-br/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/pt-br/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Etapas de pré-requisitos no servidor Exchange 2013**

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

2.  Verifique se não há pastas públicas nem caixas de correio de pasta pública pública nos servidores Exchange 2013.
    
    1.  Execute o seguinte comando para ver se existem de qualquer caixas de correio de pastas públicas.
        
            Get-Mailbox -PublicFolder 
    
    2.  Se o comando não retornou nenhum caixas de correio de pasta pública, continuar etapa 3: gerar os arquivos. csv. Se o comando retornado quaisquer pastas públicas, execute o seguinte comando para ver se existem pastas públicas:
        
            Get-PublicFolder
    
    3.  Se você tiver alguma pasta pública, execute os seguintes comandos do PowerShell para removê-los. Certifique-se de que você salvou qualquer informação que estava nas pastas públicas.
        

        > [!TIP]
        > Todas as informações contidas nas pastas públicas serão permanentemente excluídas quando você removê-los.

        
        ```
            Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        ```        
            Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```

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

1.  No servidor Exchange herdado, execute o script de `Export-PublicFolderStatistics.ps1` para criar o arquivo de mapeamento de nome para a pasta de tamanho de pasta. Este script deve ser executado por um administrador local. O arquivo conterá duas colunas: **FolderName** e **FolderSize**. Os valores da coluna **FolderSize** serão exibidos em bytes. Por exemplo, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* equivale ao nome de domínio totalmente qualificado do servidor de Caixa de Correio no qual a hierarquia da pastas públicas está hospedada.
    
      - é igual a *Folder to size map path* , o nome de arquivo e caminho em uma pasta compartilhada da rede onde deseja que o arquivo. csv salvo. Neste tópico, você precisará acessar esse arquivo a partir do servidor Exchange 2013. Se você especificar apenas o nome do arquivo, o arquivo será gerado no diretório atual do PowerShell no computador local.

2.  Execute o script `PublicFolderToMailboxMapGenerator.ps1` para criar o arquivo de mapeamento de correio de pasta pública. Esse arquivo é usado para calcular o número correto de caixas de correio de pasta pública no servidor de caixa de correio do Exchange 2013.
    

    > [!TIP]
    > Se o nome de uma pasta pública contiver uma barra invertida <STRONG>\</STRONG>, as pastas públicas serão criadas na pasta pública pai. Recomendamos que você revise o arquivo. csv e editar quaisquer nomes que contêm uma barra invertida.

    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes* equivale ao tamanho máximo que você deseja definir para novas caixas de correio de pasta pública. Ao especificar essa configuração, certifique-se de que permitem a expansão para a caixa de correio de pasta pública tenha espaço para crescer.
    
      - *Folder to size map path* iguala o caminho de arquivo do arquivo .csv criado quando o script `Export-PublicFolderStatistics.ps1` foi executado.
    
      - *Folder to mailbox map path* equivale ao nome e ao caminho do arquivo .csv de pasta para caixa de correio que você criará com essa etapa. Se você especificar apenas o nome de arquivo, o arquivo será gerado no diretório atual do PowerShell no computador local.

## Etapa 4: Criar as caixas de correio de pasta pública no Exchange 2013

1.  Execute o seguinte comando para criar as caixas de correio de pastas públicas de destino. O script criará uma caixa de correio de destino para cada caixa de correio no arquivo .csv que você gerou anteriormente na Etapa 3, executando o script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* é o arquivo gerado pelo script PublicFoldertoMailboxMapGenerator.ps1 na Etapa 3. O número estimado de conexões de usuários simultâneas navegando em uma hierarquia de pastas públicas é geralmente menor que o número total de usuários em uma organização.

## Etapa 5: Iniciar a solicitação de migração

As etapas para migrar pastas públicas do Exchange 2007 são diferentes das etapas para migrar pastas públicas do Exchange 2010.


> [!TIP]
> Se a migração do Exchange 2007 ou Exchange 2010, depois que as solicitações de migração de lote são criadas com o cmdlet apropriado, você pode visualizar as solicitações e gerenciá-los no EAC.



**Migrar pastas públicas do Exchange 2007**

1.  Pastas públicas do sistema herdado como OWAScratchPad e a subárvore da pasta raiz de esquema no Exchange 2007 não ser reconhecido pelo Exchange 2013 e, portanto, serão tratadas como "não satisfatório" itens. Isso fará com que a falha na migração. Como parte da solicitação de migração, você deve especificar um valor para o parâmetro `BadItemLimit` . Esse valor irá variar dependendo do número de bancos de dados de pasta pública que você tem. Os comandos a seguir determinarão bancos de dados de pasta pública quantos você e calcular o `BadItemLimit` para a solicitação de migração.
    
```
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
```
```    
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)
```

2.  No servidor Exchange 2013, execute o seguinte comando:
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  Inicie a migração usando o seguinte comando:
    
        Start-MigrationBatch PFMigration

**Migrar pastas públicas do Exchange 2010**

1.  No servidor Exchange 2013, execute o seguinte comando.
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    O parâmetro `NotificationEmails` é opcional.

2.  Inicie a migração usando o seguinte comando:
    
        Start-MigrationBatch PFMigration
    
    Ou:
    
    Você pode iniciar a migração no EAC.
    
    1.  Faça logon no Exchange Online e abra o EAC.
    
    2.  Navegue até **destinatários** \> **migração**.
    
    3.  Selecione o lote de migração que você acabou de criar e, em seguida, clique no botão Iniciar.

A coluna **Status** mostrará o status do lote inicial como **Criado**. O status é alterado para **Sincronizando** durante a migração. Quando a solicitação de migração for concluída, o status será **Sincronizado**. Clique duas vezes em um lote para exibir o status de caixas de correio individuais dentro do lote. Os trabalhos de caixa de correio começam com um status **Enfileirado**. Quando o trabalho é iniciado, o status é **Sincronizando** e, quando a `InitialSync` é concluída, o status exibe **Sincronizado**.

O progresso e conclusão da migração podem ser exibidos e gerenciados no EAC. Porque o cmdlet **New-MigrationBatch** inicia uma solicitação de migração de caixa de correio para cada caixa de correio de pasta pública, você pode exibir o status dessas solicitações usando a página de migração de caixa de correio. Você pode chegar à página de migração de caixa de correio e criar relatórios de migração que podem ser enviados para você, fazendo o seguinte:

1.  Faça logon no Exchange Online e abra o EAC.

2.  Navegue até **Caixa de Correio** \> **Migração**.

3.  Selecione a solicitação de migração que você acabou de criar e clique em **Exibir Detalhes** no painel **Detalhes**.

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/pt-br/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/pt-br/library/jj218697\(v=exchg.150\))

## Etapa 6: Bloquear as pastas públicas no servidor Exchange herdado para a migração final (tempo de inatividade necessário)

Até este ponto na migração, os usuários foram capazes de acessar pastas públicas. As próximas etapas farão o logoff dos usuários das pastas públicas herdadas e as bloqueará enquanto a migração realiza sua sincronização final. Os usuários não conseguirão acessar as pastas públicas durante esse processo. Além disso, os emails enviados para pastas públicas habilitadas para email serão enfileirados e não serão entregues até a conclusão da migração de pastas públicas.

Antes de executar o comando `PublicFoldersLockedForMigration` conforme descrito abaixo, certifique-se de que todos os trabalhos estejam no estado **sincronizado**. Você pode fazer isso executando o comando `Get-PublicFolderMailboxMigrationRequest` . Continue com esta etapa somente depois de verificar que todos os trabalhos estejam no estado **sincronizado**.

No servidor Exchange herdado, execute o seguinte comando para bloquear as pastas públicas herdadas para finalização.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true


> [!TIP]
> Se por algum motivo o lote de migração arquivo não finalizar (exibe do<STRONG>PublicFolderMigrationComplete</STRONG> <STRONG>False</STRONG>,) no servidor herdado, reinicie o repositório de informações (IS).



Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

Se a sua organização tiver vários bancos de dados de pastas públicas, você terá que aguardar a conclusão da replicação de pastas públicas para confirmar que todos os bancos de dados de pastas públicas selecionaram o sinalizador `PublicFoldersLockedForMigration` e que todas as alterações pendentes feitas recentemente pelos usuários foram convergidas em pastas para pastas têm convergidas por toda a organização. Isso pode levar várias horas.

## Etapa 7: Finalizar a migração de pasta pública (tempo de inatividade necessário)

Primeiro, execute o seguinte cmdlet para alterar o tipo de implantação do Exchange 2013 para **remoto**:

    Set-OrganizationConfig -PublicFoldersEnabled Remote

Depois disso, você poderá concluir a migração de pastas públicas executando o comando a seguir:

    Complete-MigrationBatch PublicFolderMigration

Ou, no EAC, você poderá concluir a migração clicando em **Concluir este lote de migração**.

Quando você concluir a migração, o Exchange executará uma sincronização final entre o servidor Exchange herdado e o Exchange 2013. Se a sincronização final for bem-sucedida, as pastas públicas no servidor Exchange 2013 serão bloqueadas e o status do lote de migração será alterado para **Concluindo** e, em seguida, **concluído**. É comum para o lote de migração demorar algumas horas antes da alteração do status de **sincronizado** a **Concluindo**, no momento em que a sincronização final será iniciada.

## Etapa 8: Testar e desbloquear a migração de pastas públicas

Depois de finalizar a migração de pastas públicas, você deve executar o seguinte teste para garantir que a migração foi bem-sucedida. Isso permite testar a hierarquia de pastas públicas migradas antes de você passar a usar pastas públicas do Exchange 2013.

1.  No PowerShell, execute o seguinte comando para atribuir algumas caixas de correio de teste para usar qualquer caixa de correio de pasta pública recém-migrada como a caixa de correio de pasta pública padrão.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Faça logon no Outlook 2007 ou versão posterior com o usuário de teste identificado na etapa anterior e, em seguida, realize os seguintes testes de pastas públicas:
    
      - Visualize a hierarquia.
    
      - Verifique as permissões.
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

3.  Se você tiver quaisquer problemas, consulte Reverter a migração , mais adiante neste tópico. Se o conteúdo de pasta pública e a hierarquia é aceitáveis e funciona como esperado, execute o seguinte comando para desbloquear as pastas públicas para todos os outros usuários.
    
        Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    

    > [!IMPORTANT]
    > Não use o parâmetro <EM>IsExcludedFromServingHierarchy</EM> após a validação da migração inicial for concluída, pois este parâmetro é utilizado pelo serviço de gerenciamento de armazenamento automatizado do Exchange Online.



4.  No servidor Exchange herdado, execute o seguinte comando para indicar que a migração de pastas públicas está concluída:
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Depois de confirmar que a migração estiver concluída, execute o seguinte comando:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

6.  Finalmente, se desejar que os remetentes externos para enviar emails para as pastas públicas habilitadas para email migradas, o usuário **anônimo** deve ser concedida pelo menos a permissão de **Criar itens**. Se você não fizer isso, remetentes externos receberá uma notificação de falha de entrega e as mensagens não será entregue à pasta pública habilitada para email migrada.
    
    Você pode usar o Shell ou o Outlook para definir as permissões do usuário anônimo. Para ler mais sobre como definir permissões em que o usuário anônimo, consulte [Email habilitar ou desabilitar email uma pasta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

## Como saber se funcionou?

No etapa 2: preparar para a migração, que foram instruído tirar instantâneos de estrutura de pasta pública, as estatísticas e as permissões antes que a migração foi iniciada. As etapas a seguir o ajudarão a verificar se a migração de pasta pública foi bem-sucedida, de acordo com os instantâneos mesmos após a migração estiver concluída. Em seguida, você pode comparar os dados em ambos os arquivos para verificar o sucesso.

1.  Execute o comando a seguir para obter um instantâneo da estrutura de pastas original.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  Execute o seguinte comando para obter um instantâneo de estatísticas de pastas públicas, como contagem de itens, tamanho e proprietário.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  Execute o seguinte comando para obter um instantâneo das permissões.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Remover bancos de dados de pastas públicas dos servidores Exchange herdados

Após a conclusão da migração e depois que você tiver confirmado que as suas pastas públicas do Exchange 2013 estão funcionando conforme o esperado, será necessário remover os bancos de dados de pastas públicas nos servidores Exchange herdados.

  - Para mais detalhes sobre como remover bancos de dados de pastas públicas de servidores Exchange 2007, confira o tópico sobre como [remover bancos de dados de pastas públicas](https://go.microsoft.com/fwlink/?linkid=123678).

  - Para mais detalhes sobre como remover bancos de dados de pastas públicas de servidores Exchange 2010, confira o tópico sobre como [remover bancos de dados de pastas públicas](https://go.microsoft.com/fwlink/?linkid=81409).

## Reverter a migração

Se você encontrar problemas com a migração e precisar reativar suas pastas públicas do Exchange herdadas, realize as etapas a seguir.


> [!WARNING]
> Se você reverter a migração para servidores Exchange herdados, você perderá qualquer email que foi enviada para pastas públicas habilitadas para email ou o conteúdo que foi lançado em pastas públicas no Exchange 2013 após a migração. Para salvar esse conteúdo, você precisa exportar o conteúdo de pasta pública para um arquivo. pst e importá-lo para as pastas públicas herdadas quando a reversão for concluída.



1.  No servidor Exchange herdado, execute o seguinte comando para desbloquear as pastas públicas herdadas do Exchange. Esse processo pode levar várias horas.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  No servidor Exchange 2013, execute os seguintes comandos para remover as caixas de correio de pasta pública.
    
```
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
```
```        
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
```

3.  No servidor Exchange herdado, execute o seguinte comando para definir o sinalizador `PublicFolderMigrationComplete` como `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

