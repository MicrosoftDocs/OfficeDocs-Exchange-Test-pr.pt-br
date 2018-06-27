---
title: 'Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online: Exchange 2013 Help'
TOCTitle: Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432748
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online

 

_**Tópico modificado em:**2018-03-26_

**Resumo:** Este artigo explica como mover modernas pastas públicas do Exchange 2013 para o Office 365.

Migrando suas pastas públicas do Exchange 2013 para Exchange Online requer o Exchange Server 2013 CU15 ou posterior esteja em execução no seu ambiente local.


> [!TIP]
> Se você tiver pastas públicas do Exchange 2013 e Exchange 2016 em sua organização e deseja movê-los todos para Exchange Online, use <A href="https://go.microsoft.com/fwlink/p/?linkid=845314">a versão do Exchange 2016 deste artigo</A> para planejar e executar a migração. Seus servidores Exchange 2013 ainda precisará ter CU15 ou posterior instalado.



## O que você precisa saber antes de começar?

  - Quando você atualiza para o Exchange Server 2013 CU15 ou posterior, você também deve preparar o Active Directory ou a migração de pasta pública falhará. Essa preparação do Active Directory garante que todos os cmdlets do PowerShell e parâmetros relevantes estão disponíveis para preparar e executar a migração. Consulte [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md) para obter mais informações.

  - No Exchange Online, você precisa ser membro do grupo de funções de gerenciamento da organização. Este grupo de função é diferente das permissões atribuídas a você quando você se inscreve para Office 365 ou Exchange Online. Para obter detalhes sobre como habilitar o grupo de funções de gerenciamento da organização, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - No Exchange Server 2013, você precisa ser membro dos grupos de função de gerenciamento da organização ou servidor de gerenciamento de RBAC. Para obter detalhes, consulte [Adicionar membros a um grupo de funções](https://go.microsoft.com/fwlink/?linkid=299212).

  - Antes de começar a migração de pasta pública, se qualquer pasta pública individual em sua organização tiver mais de 25 GB, recomendamos que você excluir o conteúdo dessa pasta para torná-lo menor ou divida a pasta pública conteúdo em várias, de pastas públicas menores. Observe que o limite de 25 GB citado aqui se aplica somente à pasta pública e não para qualquer filho ou subpastas que na pasta em questão pode ter. Se nenhuma das opções é viável, recomendamos que você não mover suas pastas públicas para o Exchange Online. Consulte [Limites do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=391188) para obter mais informações.
    

    > [!TIP]
    > Se menos de 25 GB suas atual cotas de pastas públicas no Exchange Online, você pode usar o <A href="https://go.microsoft.com/fwlink/p/?linkid=844062">cmdlet Set-OrganizationConfig</A> para aumentá-los com os parâmetros DefaultPublicFolderIssueWarningQuota e DefaultPublicFolderProhibitPostQuota.



  - No Office 365 e Exchange Online, você pode criar um máximo de caixas de correio de pasta pública de 1000.

  - Se você pretende migrar usuários para o Office 365, você deve concluir a migração de usuário antes de migrar suas pastas públicas. Para obter mais informações, consulte [maneiras para migrar várias contas de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=842798).

  - Proxy MRS deve ser ativado em pelo menos um servidor do Exchange, um servidor que também hospeda as caixas de correio de pasta pública. Consulte [Habilitar o ponto de extremidade do Proxy MRS para movimentações remotas](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md) para obter detalhes.

  - Para executar os procedimentos de migração neste artigo, você não pode usar o Centro de administração do Exchange (EAC). Em vez disso, você precisará usar o Shell de gerenciamento do Exchange em seus servidores Exchange 2013. No Exchange Online, você precisará usar o PowerShell do Exchange Online. Para obter mais informações, consulte [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=842801).

  - Migrando de itens excluídos e pastas excluídas do Exchange 2013 para o Exchange Online é suportada. Antes de começar a migração, é recomendável que você revise excluídas todas as pastas e itens da pasta e exclui permanentemente qualquer item que você não precisará no Exchange Online. Observe que quando algo é permanentemente excluído, não pode ser recuperado.
    
    Você pode usar os seguintes comandos para listar as pastas públicas excluídas presente no Exchange dumpster (em seu ambiente do Exchange no local):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    Para excluir permanentemente uma pasta específica, use o seguinte comando (Este exemplo usa uma pasta denominada 'Calendar2'):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - Antes de começar, leia este artigo mudada. Para algumas etapas há tempo de inatividade necessário. Durante esse tempo de inatividade, pastas públicas não será acessíveis por qualquer pessoa.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Etapa 1: Baixar os scripts de migração

1.  Baixe todos os scripts e arquivos de suporte de [Scripts de migração de pastas públicas do Exchange 2013/2016](https://go.microsoft.com/fwlink/p/?linkid=844893).

2.  Salve os scripts no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts. Verifique se que todos os scripts estão salvos no mesmo local.

Os scripts e arquivos que você estiver baixando os dados são:

  - `Sync-ModernMailPublicFolders.ps1` Esse script sincroniza os objetos de pasta pública habilitada para email entre seu ambiente do Exchange no local e o Office 365. Você vai executar esse script em um servidor Exchange 2013.

  - `SyncModernMailPublicFolders.strings.psd1` Esse arquivo de suporte é usado pelo script Sync-ModernMailPublicFolders.ps1 ps1 e deve ser baixado no mesmo local.

  - `Export-ModernPublicFolderStatistics.ps1` Esse script cria o tamanho da pasta de nome de pasta e arquivo de mapeamento de tamanho de item excluído. Você vai executar esse script no servidor Exchange 2013.

  - `Export-ModernPublicFolderStatistics.strings.psd1` Esse arquivo de suporte é usado pelo script Export-ModernPublicFolderStatistics.ps1 ps1 e deve ser baixado no mesmo local.

  - `ModernPublicFolderToMailboxMapGenerator.ps1` Esse script cria o arquivo de mapeamento de correio de pasta pública usando a saída do script Export-ModernPublicFolderStatistics.ps1. Você vai executar esse script em um servidor Exchange 2013.

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` Esse arquivo de suporte é usado pelo script ModernPublicFolderToMailboxMapGenerator.ps1 ps1 e deve ser baixado no mesmo local.

  - `SetMailPublicFolderExternalAddress.ps1` Esse script atualiza `ExternalEmailAddress` de pastas públicas habilitadas para email no seu ambiente local ao de seus colegas Online do Exchange. Isso garante que, após a migração, emails endereçados a pastas públicas habilitadas para email adequadamente são roteadas para o Exchange Online. Você precisa executar esse script em um servidor Exchange 2013.

  - `SetMailPublicFolderExternalAddress.strings.psd1` Esse arquivo de suporte é usado pelo script SetMailPublicFolderExternalAddress.ps1 ps1 e deve ser baixado no mesmo local.

## Etapa 2: Preparar-se para a migração

Execute todas as etapas de pré-requisito nas seções a seguir antes de iniciar a migração de pasta pública.

**Etapas gerais de pré-requisito**

Para a sua migração obter êxito, você deve:

  - Certifique-se de que não há nenhuma pasta pública órfão mail objetos no Active Directory. Esses são objetos do Active Directory sem um objeto correspondente do Exchange.

  - Confirme se os endereços de email SMTP configurados para pastas públicas no Active Directory correspondem os endereços de email SMTP em objetos do Exchange.

  - Confirme que não há nenhum objeto de pasta pública duplicados no Active Directory. Isso é necessário para evitar ter dois ou mais Active Directory objetos que estão apontando para a mesma pasta pública habilitada para email.

**Etapas de pré-requisito no ambiente de servidor local do Exchange 2013**

No Exchange Management Shell (local) execute as seguintes etapas:

1.  Depois que a migração estiver concluída, ele levarão algum tempo para caches DNS pela Internet mensagens direto para suas pastas públicas habilitadas para email no novo local no Exchange Online. Você pode garantir que suas pastas públicas recém-migrada habilitados para email recebem mensagens durante este período de transição de DNS criando um domínio aceito com um nome conhecido. Para fazer isso, execute o seguinte comando em seu ambiente do Exchange local. Neste exemplo, `target domain` é o seu domínio Office 365 ou Exchange Online, para o qual um conector de envio já foi configurado pelo Assistente de configuração híbrida.
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **Exemplo**:
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    Se o domínio aceito já existir no seu ambiente local, renomeie-o para `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` e deixe os outros atributos intactas.
    
    Para verificar se o domínio aceito já esteja presente no seu ambiente local:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    Para renomear o domínio aceito para `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`, execute o seguinte:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    

    > [!TIP]
    > Se suas pastas públicas habilitadas para email no Exchange Online para receber emails externos da Internet sejam os esperados, você precisa desabilitar Directory Based Edge bloqueando (DBEB) no Exchange Online e Exchange Online Protection (EOP). Consulte <A href="https://technet.microsoft.com/pt-br/library/dn600322(v=exchg.150)">Usar Bloqueio de Borda Baseado em Diretório para Rejeitar Mensagens Enviadas a Destinatários Inválidos</A> para obter mais informações.



2.  Se o nome de uma pasta pública contiver uma barra invertida **\\** ou uma barra invertida **/**, ele pode não obter migrado para sua caixa de correio designada durante o processo de migração. Antes de migrar, renomear qualquer uma dessas pastas para remover esses caracteres
    
    1.  Para localizar pastas públicas que possuem uma barra invertida no nome de usuário, execute o seguinte comando:
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  Se qualquer pasta pública for retornada, você poderá renomeá-la executando o seguinte comando:
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  Siga as seguintes etapas para confirmar que não existe um registro de uma migração bem-sucedida anterior em sua organização. Se houver, você precisará definir esse valor com `$false`.
    
    Antes de alterar os valores, confirme que a tentativa de migração anterior pode ser descartada para que você acidentalmente não realizar uma migração segunda.
    
    1.  Execute o seguinte comando para verificar se há qualquer migrações anteriores e o status dessas migrações:
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        

        > [!TIP]
        > Se o <CODE>PublicFoldersLockedforMigration</CODE> ou <CODE>PublicFolderMigrationComplete</CODE> parâmetros <CODE>$true</CODE>, significa que você migrou pastas públicas herdadas em algum momento. Certifique-se de que qualquer banco de dados de pasta pública herdado foi descomissionar antes de passar para a etapa 3b.

    
    2.  Se qualquer uma das perguntas acima é retornado com um valor definido como `$true`, torná-los `$false` executando:
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  Para fins de verificar o êxito da migração após a sua conclusão, recomendamos que você execute os seguintes comandos em todos os servidores Exchange 2013 apropriados. Isso levará instantâneos da sua implantação atual de pasta pública que podem ser usados para comparar com suas pastas públicas recém-migrada posteriormente.
    

    > [!TIP]
    > Dependendo do tamanho da sua organização do Exchange, ela pode levar algum tempo para executar esses comandos.

    
      - Execute o seguinte comando para obter um instantâneo da estrutura de pastas original.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - Execute o seguinte comando para obter um instantâneo de estatísticas de pastas públicas, como contagem de itens, tamanho e proprietário.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - Execute o seguinte comando para obter um instantâneo das permissões de pasta pública.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - Execute o seguinte comando para obter um instantâneo das suas pastas públicas habilitadas para email:
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - Salve os arquivos gerados dos comandos anteriores em um local seguro para tornar uma comparação no final da migração.

5.  Se você estiver usando o Microsoft Azure Active Directory Connect (conectar do Azure AD) para sincronizar seus diretórios no local com o Windows Azure Active Directory, você deve executar as seguintes ações (se você não estiver usando Connect do Azure AD, você pode ignorar esta etapa):
    
    1.  Em um computador local, abra o Microsoft Azure Active Directory Connect e, em seguida, selecione **Configurar**.
    
    2.  Na tela **tarefas adicionais**, selecione **Personalizar opções de sincronização** e, em seguida, clique em **Avançar**.
    
    3.  Na tela **conectar ao AD do Windows Azure**, digite as credenciais apropriadas e clique em **Avançar**. Uma vez conectado, continue clicando em **Avançar** até que você esteja na tela **Recursos opcionais** .
    
    4.  Certifique-se de que as **Pastas públicas de email do Exchange** não está selecionada. Se ainda não estiver selecionada, você pode continuar na próxima seção, *etapas de pré-requisito no Exchange Online*. Se ela estiver selecionada, clique para desmarcar a caixa de seleção e, em seguida, clique em **Avançar**.
        

        > [!TIP]
        > Se você não vir a <STRONG>Pastas públicas do Exchange Mail</STRONG> como uma opção na tela <STRONG>Recursos opcionais</STRONG>, você pode sair do Microsoft Azure Active Directory Connect e prossiga para a próxima seção, <EM>etapas de pré-requisito no Exchange Online</EM>.

    
    5.  Após você ter desmarcado a seleção de **Pastas públicas do Exchange Mail**, mantenha a clicar em **Avançar** até que você esteja na tela **pronto para configurar** e, em seguida, clique em **Configurar**.

**Etapas de pré-requisito no Exchange Online**

No PowerShell do Exchange Online, faça o seguinte:

1.  Verifique se não há nenhuma solicitação de migração de pasta pública existente. Se houver, desmarque-los ou seu próprio solicitação de migração falhará. Esta etapa só será necessária se você acha que pode haver uma solicitação de migração existente no pipeline (que falhou ou que desejar anular).
    
    Uma solicitação de migração existente pode ser um dos dois tipos: lote de migração ou serial. Os comandos para detectar e removendo, cada tipo de solicitação são os seguintes.
    
    O exemplo a seguir detectará quaisquer solicitações de migração serial existente:
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    O exemplo a seguir remove quaisquer solicitações de série de migração de pasta pública existente:
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    O exemplo a seguir detectará quaisquer solicitações de migração de lote existente:
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    O exemplo a seguir remove quaisquer solicitações de migração de lote de pasta pública existente:
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  Você precisa ter o recurso de migração **PAW** habilitados para o locatário do Office 365. Você pode verificar isso executando o seguinte comando no PowerShell do Exchange Online:
    
        Get-MigrationConfig
    
    Se a saída em **recursos** tiver **PAW**, em seguida, o recurso está habilitado e você pode continuar para a próxima etapa.
    
    Se PATA ainda não foi habilitado para seu locatário, poderia ser porque você precisou alguns lotes de migração existentes, lotes lotes de pasta pública ou de usuário. Esses lotes poderia ser qualquer estado, incluindo concluído. Se este for o caso, preencha e remover qualquer lotes de migração até que os registros não forem retornados quando você executar `Get-MigrationBatch`. Depois que todos os lotes existentes são removidos, PATA deve obter habilitada automaticamente. Observe que a alteração pode não refletir no `Get-MigrationConfig` imediatamente, mas que é okey. No caso de migrações do usuário, você pode continuar a criação de novos lotes depois que essa etapa for concluída.

3.  Verifique se que não há pastas públicas nem caixas de correio de pasta pública no Exchange Online. Se você descobrir pastas públicas no Exchange Online após executar as etapas abaixo, é importantes para determinar o que eles são e quem na sua organização tiver iniciado uma hierarquia de pasta pública antes de começar a remoção de pastas públicas e a pasta pública caixas de correio.
    
    1.  No Office 365 ou no Exchange Online PowerShell, execute o seguinte comando para ver se existem caixas de correio de pastas públicas.
        
            Get-Mailbox -PublicFolder
    
    2.  Se o comando não retorna qualquer caixa de correio de pasta pública, continuar etapa 3: gerar os arquivos. csv. Se o comando retornar qualquer caixa de correio de pastas públicas, execute o seguinte comando para ver se existem pastas públicas:
        
            Get-PublicFolder -Recurse
    
    3.  Se você tiver alguma pasta pública no Office 365 ou Exchange Online, execute o seguinte comando do PowerShell para removê-los (depois de confirmar que eles não são necessários). Certifique-se de que você salvou todas as informações nessas pastas públicas antes de excluí-los, porque todas as informações serão permanentemente excluídas quando você remover as pastas públicas.
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Depois que as pastas públicas são removidas, execute os seguintes comandos para remover todas as caixas de correio de pasta pública:
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## Etapa 3: Gerar os arquivos. csv

Use os scripts baixados anteriormente para gerar os arquivos. csv que serão usados na migração.

1.  No Shell de gerenciamento do Exchange (no local), execute o script de `Export-ModernPublicFolderStatistics.ps1` para criar o arquivo de mapeamento de nome para a pasta de tamanho de pasta. Você deve ter permissões de administrador local para executar esse script. O arquivo resultante conterá três colunas: **FolderName**, **FolderSize** e **DeletedItemSize**. Os valores para as colunas **FolderSize** e **DeletedItemSize** serão exibidos em bytes. Por exemplo, **\\PublicFolder01,10240, 100** significa que a pasta pública na raiz da sua hierarquia chamada PublicFolder01 é 10240 bytes ou 10.240 MB, tamanho e existem 100 bytes de itens recuperáveis nela.
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **Exemplo**:
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  Execute o script `ModernPublicFolderToMailboxMapGenerator.ps1` para criar um arquivo. csv que mapeie a pastas públicas do código-fonte para caixas de correio de pasta pública em seu destino do Exchange Online. Esse arquivo é usado para calcular o número correto de caixas de correio de pasta pública no Exchange Online.
    

    > [!TIP]
    > O arquivo gerado pela <CODE>ModernPublicFolderToMailboxMapGenerator.ps1</CODE> não conterá o nome de cada pasta pública em sua organização. Ele irá conter referências às pastas pai de maiores árvores de pasta ou os nomes das pastas que sozinhos são significativamente grandes. Você pode considerar esse arquivo como um arquivo de "exceção" usado para se certificar de que certos árvores de pasta e pastas maiores obtém colocadas no correio de pasta pública específicacaixas. É normal que você não verá a cada uma das suas pastas públicas neste arquivo. Pastas filhas de qualquer pasta listados nesse arquivo de mapeamento também serão migradas para a mesma caixa de correio de pasta pública como sua pasta pai (a menos que explicitamente mencionado em outra linha dentro do arquivo de mapeamento que direciona-los para uma caixa de correio de pasta pública diferentes).

    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` é a quantidade máxima de dados que você deseja migrar em qualquer caixa de correio única de pasta pública no Exchange Online. O tamanho máximo desse campo está atualmente 50 GB, mas recomendamos que você use um tamanho menor, como 50% do tamanho máximo, para permitir o crescimento futuro.
    
      - `Maximum mailbox recoverable items size in bytes` é a cota de itens recuperáveis em suas caixas de correio do Exchange Online. O tamanho máximo de caixas de correio de pasta pública no Exchange Online no momento é 50 GB. Recomendamos a configuração` RecoverableItemsQuota` para 15 GB ou menos.
    
      - `Folder-to-size map path` é o caminho de arquivo do arquivo. csv criado quando você executou o script de `Export-ModernPublicFolderStatistics.ps1` .
    
      - `Folder-to-mailbox map path` é o caminho de arquivo do arquivo. csv de correio de pasta que você está criando nesta etapa. Se você especificar apenas um nome de arquivo, o arquivo será gerado no diretório atual do PowerShell no computador local.

**Exemplo**:

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv


> [!TIP]
> Não há suporte para migração de pastas públicas para o Exchange Online se o número de caixas de correio de pasta pública exclusivo no Exchange Online for maior que 100.



## Etapa 4: Criar as caixas de correio de pasta pública no Exchange Online

Em seguida, no Exchange Online PowerShell, crie as caixas de correio de pasta pública de destino que conterão suas pastas públicas migradas.

1.  Execute o seguinte script para criar as caixas de correio de pasta pública de destino. O script criará uma caixa de correio de destino para cada caixa de correio no arquivo. csv que você gerou anteriormente no *etapa 3: gerar os arquivos. csv*, quando executou o script `ModernPublicFoldertoMailboxMapGenerator.ps1` .
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` é o caminho de arquivo do arquivo. csv de correio de pasta que foi gerado pelo script `ModernPublicFoldertoMailboxMapGenerator.ps1`*etapa 3: gerar os arquivos. csv*.

## Etapa 5: Iniciar a solicitação de migração

Um número de comandos agora precisa ser executado em seu ambiente do Exchange 2013 no local e no Exchange Online.

1.  De qualquer um dos seus servidores Exchange 2013 hospedar caixas de correio de pasta pública, execute o seguinte script. Esse script sincronizará habilitados para email a pastas públicas do seu Active Directory local para o Exchange Online. Certifique-se de que você baixou a versão mais recente desse script e que você está executando-lo do Shell de gerenciamento do Exchange.
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` é o seu nome de usuário administrativo Exchange Online e a senha.
    
      - `CsvSummaryFile` é o caminho do arquivo para onde você deseja que seu arquivo de log das operações de sincronização e erros localizados. O log será no formato. csv.

2.  No servidor Exchange 2013, localize o proxy MRS servidor de ponto de extremidade e anote-lo. Você precisará dessas informações para executar a solicitação de migração. Salve essas informações para a etapa 3b abaixo.

3.  No PowerShell do Exchange Online, execute os seguintes comandos para passar informações de credenciais e as informações de MRS da etapa anterior para as variáveis de cmdlet que serão usados na solicitação de migração.
    
    1.  Passe a credencial de um usuário que possui permissões de administrador no ambiente Exchange 2013 local para a variável `$Source_Credential`. A solicitação de migração que você execute no Exchange Online usará essa credencial para acessar os servidores do Exchange 2013 local para copiar a conteúdo através de pasta pública para o Exchange Online.
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Siga as informações do MRS Proxy Server do ambiente do Exchange 2013 que você encontrou na etapa 2 acima e passe-o para a variável:
        
            $Source_RemoteServer = "<paste the value here>"

4.  No PowerShell do Exchange Online, execute os seguintes comandos para criar o ponto de extremidade de migração de pasta pública e a solicitação de migração de pasta pública:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    

    > [!TIP]
    > Separe os vários endereços de email com vírgulas.

    
    Onde `folder_mapping.csv` é o arquivo de mapa gerado na *etapa 3: Crie os arquivos. csv*. Certifique-se de fornecer o caminho completo do arquivo. Se o arquivo de mapa foi movido por qualquer motivo, certifique-se de usar o novo local.

5.  Finalmente, inicie a migração usando o seguinte comando no PowerShell do Exchange Online:
    
        Start-MigrationBatch PublicFolderMigration

Enquanto as migrações de lote precisam ser criadas usando o cmdlet New-MigrationBatch no PowerShell do Exchange Online, o andamento e a conclusão da migração podem ser exibidos e gerenciados no EAC ou executando o cmdlet Get-MigrationBatch. O cmdlet New-MigrationBatch inicia uma solicitação de migração de caixa de correio para cada caixa de correio de pasta pública e você pode exibir o status dessas solicitações usando a página de migração de caixa de correio.

Para ir até a página de migração de caixa de correio:

1.  Faça logon no Exchange Online e abra o EAC.

2.  Navegue até **destinatários** e selecione **migração**.

3.  Selecione a solicitação de migração que acabou de criar e, no painel de **detalhes**, selecione **Exibir detalhes**.

Antes de mover o logon em *etapa 6: bloquear as pastas públicas no servidor Exchange 2013*, verifique se que todos os dados foi copiado e que não há nenhum erro na migração. Depois de confirmar que o lote foi transferida para o estado de **sincronizado**, execute os comandos mencionados na *etapa 2: preparar para a migração*, em final etapa em **etapas de pré-requisito no ambiente de servidor do Exchange 2013 local**, como obter um instantâneo das pastas públicas no local. Após tem executar esses comandos, você poderá prosseguir para a próxima etapa. Observe que esses comandos pode demorar um pouco para ser concluído dependendo do número de pastas que você tem.

## Etapa 6: Bloquear as pastas públicas no ambiente do Exchange 2013 para a migração final (tempo de inatividade pasta pública necessário)

Até esse ponto no processo de migração, os usuários têm sido capazes de acessar suas pastas públicas do local. As etapas a seguir serão agora logoff logoff de usuários de pastas públicas do Exchange 2013 e bloquear as pastas que o processo de migração for concluída seu sincronização final. Os usuários não poderão acessar pastas públicas durante esse tempo, e todas as mensagens enviadas para essas pastas públicas habilitadas para email serão enfileiradas e permanecem não entregues até que a migração de pasta pública seja concluída.

Antes de executar o comando `PublicFolderMailboxesLockedForNewConnections` conforme descrito abaixo, certifique-se de que todos os trabalhos estejam no estado **sincronizado**. Você pode fazer isso executando o comando `Get-PublicFolderMailboxMigrationRequest` . Continue com esta etapa somente depois de verificar que todos os trabalhos estejam no estado **sincronizado**.

Em seu ambiente local, execute o seguinte comando para bloquear as pastas públicas do Exchange 2013 para finalização.

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true


> [!TIP]
> Se você não puder acessar o parâmetro <CODE>-PublicFolderMailboxesLockedForNewConnections</CODE> , talvez seja porque seu Active Directory não foi preparado durante a atualização de UC, como podemos aconselhado acima <EM>o que você precisa saber antes de começar?</EM> Consulte <A href="prepare-active-directory-and-domains-exchange-2013-help.md">Preparar o Active Directory e domínios</A> para obter mais informações.<BR>Também Observe que todos os usuários que precisam de acesso a pastas públicas devem ser migrados em primeiro lugar, <STRONG>antes de</STRONG> migrar as pastas públicas sozinhos.



Se sua organização tiver caixas de correio de pasta pública em vários servidores Exchange 2013, você precisará aguardar até que a replicação do AD foi concluída. Após a conclusão, você pode confirmar que todas as caixas de correio de pasta pública tiverem buscadas o sinalizador `PublicFolderMailboxesLockedForNewConnections` e que quaisquer alterações feitos recentemente suas pastas públicas de usuários têm convergiu em toda a organização pendentes. Tudo isso pode levar várias horas.

## Etapa 7: Finalizar a migração de pasta pública (tempo de inatividade pasta pública necessário)

Antes de concluir a migração de pasta pública, você precisa confirmar que não há nenhuma outra caixa de correio de pasta pública move ou movimentações de pastas públicas contínuas em seu ambiente do Exchange local. Para fazer isso, use os cmdlets `Get-MoveRequest` e `Get-PublicFolderMoveRequest` para listar qualquer pasta pública existente move. Se houver qualquer movimento em andamento ou no estado **concluído**, removê-los.

Em seguida, para concluir a migração de pasta pública, execute o seguinte comando no PowerShell do Exchange Online:

    Complete-MigrationBatch PublicFolderMigration

Quando você executar esse comando, o Exchange fará uma sincronização final entre sua organização do Exchange no local e o Exchange Online. Durante esse período, o status do lote de migração será alterado de **sincronizado** para **Concluindo** e depois finalmente como **concluído**. Se a sincronização final for bem-sucedida, as pastas públicas no Exchange Online serão bloqueadas.

É comum para o lote de migração demorar algumas horas antes da alteração do status de **sincronizado** a **Concluindo**, no momento em que a sincronização final será iniciada.

## Etapa 8: Testar e desbloquear a pastas públicas no Exchange Online

Uma vez concluída a migração de pasta pública, siga estas etapas para testar o êxito da migração e oficialmente verificar sua conclusão. Essas tarefas finais permitem que você teste a hierarquia de pasta pública migrados antes de alternar permanentemente sua organização para pastas públicas do Exchange Online.

1.  No PowerShell do Exchange Online, atribua algumas teste caixas de correio de usuário para usar um dos sua caixa de correio de pasta pública recém-migrada como suas caixas de correio de pasta pública padrão.:
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    Certifique-se de que os usuários de teste tenham as permissões necessárias para criar pastas públicas.

2.  Faça logon no Outlook com o usuário de teste que você designados na etapa anterior e, em seguida, execute os seguintes testes de pasta pública. Observe que pode levar 15 a 30 minutos para que as alterações entrem em vigor. Depois que o Outlook está ciente das alterações, ele poderá solicitar a reinicialização algumas vezes.
    
    1.  Visualize a hierarquia.
    
    2.  Verifique as permissões.
    
    3.  Criar algumas pastas públicas e, em seguida, excluí-los.
    
    4.  Publique conteúdo e exclua conteúdo, de uma pasta pública.
    
    Se você tiver algum problema e determinar que não está pronto para alternar pastas públicas da sua organização inteiramente para o Exchange Online, consulte [Reverter uma migração de pasta pública do Exchange 2013 para o Exchange Online](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md).

3.  Execute o seguinte comando no Exchange Online PowerShell para desbloquear suas pastas públicas no Exchange Online. Após executar o comando, pode levar aproximadamente 15 a 30 minutos para que as alterações entrem em vigor. Depois que o Outlook fica atento as alterações, ele pode solicitar seus usuários para reiniciar o programa várias vezes.
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Etapa 9: Finalizar a migração no local

Para habilitar os e-mails para pastas públicas habilitadas para email no local, siga estas etapas:

1.  Em seu ambiente local, execute o seguinte script para certificar-se de que todos os emails para pastas públicas habilitadas para email corretamente são roteadas para o Exchange Online. O script irá carimbar pastas públicas habilitadas para email com uma `ExternalEmailAddress` que os direciona a seus colegas Online do Exchange:
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  Se o teste for bem-sucedido, em seu ambiente local, execute o seguinte comando para indicar que a migração de pasta pública está concluída:
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## Como saber se funcionou?

No etapa 2: preparar para a migração, você desempenhou instantâneos de sua estrutura de pasta pública no local, estatísticas e permissões. As etapas a seguir ajudará você a verificar que sua migração de pasta pública foi bem-sucedida, de acordo com os mesmos instantâneos no Exchange Online após a migração. Compare os dados em ambos os arquivos para verificar o sucesso.

1.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo da nova estrutura de pastas:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo das estatísticas de pastas públicas, incluindo a contagem de itens, tamanho e proprietário:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo das permissões:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  No PowerShell do Exchange Online, execute o seguinte comando para obter um instantâneo das pastas públicas habilitadas para email:
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## Problemas conhecidos

A seguir estão problemas comuns de migração de pasta pública que podem ocorrer na sua organização.

  - Não há suporte para migração de pastas públicas para o Exchange Online se o número de caixas de correio de pasta pública exclusivo no Exchange Online for maior que 100.

  - Permissões de pasta pública raiz e a pasta EFORMS REGISTRY não serão migrados para o Exchange Online e você terá que manualmente aplicarão-las no Exchange Online. Para fazer isso, execute o seguinte comando no seu PowerShell do Exchange Online. Execute o comando uma vez para cada entrada de permissão que esteja presente no local, mas ausente no Exchange Online:
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - Alguns migrações de pasta pública falhará se algumas caixas de correio de pasta pública não estão atendendo a hierarquia de pasta pública. Isso significa que o parâmetro `IsExcludedFromServingHierarchy` em uma ou mais caixas de correio é definido como `$true`. Para evitar isso, defina todas as caixas de correio no Exchange Online para atender a hierarquia.

  - Permissões **Enviar como** e **Enviar em nome** não serão migradas para o Exchange Online. Se isso acontecer com sua migração, use os seguintes comandos em seu ambiente local observar quem tem essas permissões.
    
    Para ver quais pastas públicas possuem permissões Enviar como local:
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    Para ver quais pastas públicas tenha enviar em nome permissões no local:
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Para adicionar a permissão Enviar como para uma pasta pública habilitada para email no Exchange Online, no Exchange Online PowerShell digite:
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **Exemplo**:
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Para adicionar o envio na permissão do nome para uma pasta pública habilitada para email no Exchange Online, no Exchange Online PowerShell digite:
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **Exemplo**:
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - Ter mais de 10.000 pastas sob a pasta "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" pode causar falha na migração. Portanto, verifique a pasta "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" para ver se há mais de 10.000 pastas diretamente sob ele (filhos imediatos). Você pode usar o seguinte comando para encontrar o número de pastas públicas no local:
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    O Exchange Online não suporta mais de 10.000 subpastas, por isso, migrações de mais de 10.000 pastas falhará. Estamos atualmente desenvolvendo um script para desbloquear tais configurações. Enquanto isso, sugerimos aguardando para migrar suas pastas públicas.

  - Trabalhos de migração não estão fazendo progresso ou estão paralisados. Isso pode acontecer se houver muitos trabalhos em execução em paralelo, causando trabalhos falha com erros intermitentes. Você pode reduzir o número de trabalhos simultâneos modificando `MaxConcurrentMigrations` e `MaxConcurrentIncrementalSyncs` para um número menor. Use o exemplo a seguir para definir esses valores:
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - Trabalhos de migração falharem com o erro "Erro: Dumpster da pasta Dumpster." Se você vir esse erro, ele deve ser resolvido se você parar o lote e, em seguida, reiniciá-lo.

  - Trabalhos de migração falhar e gerar um "solicitação foi colocada em quarentena devido ao seguinte erro: A chave fornecida não estava presente no dicionário" mensagem de erro. Isso acontece quando um item corrompido estiver presente em uma pasta em que os trabalhos de migração não é possível copiar. Para contornar esse problema:
    
    1.  Pare o lote de migração.
    
    2.  Identifique a pasta que contém o item inválido. O relatório de migração deve incluir referências para a pasta em que estava sendo copiados quando o erro ocorreu.
    
    3.  Em seu ambiente local, mova a pasta afetada para a caixa de correio de pasta pública principal. Você pode usar o cmdlet `New-PublicFolderMoveRequest` para mover pastas.
    
    4.  Aguarde a movimentação de pasta para a conclusão. Quando ela for concluída, remova a solicitação de movimentação. Em seguida, reinicie o lote de migração.

## Remover caixas de correio de pasta pública do seu ambiente local do Exchange

Após a migração estiver concluída e você verificou que suas pastas públicas no Exchange Online estão funcionando conforme o esperado e contenham dados todos os esperados, você pode remover as suas caixas de correio de pasta pública no local.

Lembre-se de que esta etapa é irreversível, porque depois de caixas de correio de pasta pública forem excluídas, eles não podem ser recuperados. Portanto, é altamente recomendável que, além de verificar o sucesso da sua migração, você também monitorar suas pastas públicas do Exchange Online para algumas semanas antes de remover as caixas de correio de pasta pública no local.

