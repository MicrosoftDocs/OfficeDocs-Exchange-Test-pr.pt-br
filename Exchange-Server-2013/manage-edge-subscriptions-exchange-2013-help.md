---
title: 'Gerenciar inscrições de borda: Exchange 2013 Help'
TOCTitle: Gerenciar inscrições de borda
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61183347
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar inscrições de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-04-16_

Este tópico oferece informações detalhadas sobre várias tarefas de gerenciamento de Inscrição de Borda.

**Sumário**

Subscribe an Edge Transport server

Remove an Edge subscription

Resubscribe an Edge Transport Server

Add or remove a Mailbox Server

Run EdgeSync manually

Verify EdgeSync results

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "EdgeSync" e seção "Servidores de Transporte de Borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você precisa ter um Servidor de borda inscrito em seu site do Active Directory voltado para a Internet. Para obter mais informações, consulte [Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Inscrever-se em um servidor de Transporte de Borda

Você pode se inscrever em um ou mais servidores de Transporte de Borda em um único site do Active Directory. Se você implantar servidores de Transporte de Borda adicionais em sua rede de perímetro e inscrevê-los no mesmo site do Active Directory em que uma Inscrição de Borda já exista, as seguintes ações ocorrerão:

  - Um novo objeto de Inscrição de Borda será criado no Active Directory.

  - Contas ESRA adicionais serão criadas para cada servidor de Caixa de Correio no site do Active Directory. Essas contas serão replicadas para o Active Directory Lightweight Directory Services (AD LDS) e usadas pelo processo de sincronização do EdgeSync durante a sincronização com o novo servidor.

  - A nova Inscrição de Borda é adicionada à lista de servidores de origem do Conector de Envio automático para a Internet. As mensagens enviadas a esse conector para processamento sofrerão um balanceamento de carga entre os servidores de Transporte de Borda inscritos.

  - Um Conector de envio de entrada é criado automaticamente no servidor de Transporte de Borda para a organização do Exchange.

  - A sincronização EdgeSync para o servidor de Transporte de Borda será iniciada.

## Remover uma Inscrição de Borda

Talvez ocasionalmente você queira remover uma Inscrição de Borda da organização do Exchange ou da organização do Exchange e do servidor de Transporte de Borda. Se mais tarde você planeja inscrever novamente o servidor de Transporte de Borda na organização do Exchange, não remova a Inscrição de Borda do servidor de Transporte de Borda. Quando você remove a Inscrição de Borda de um servidor de Transporte de Borda, todos os dados replicados são excluídos do AD LDS. Isso poderá levar muito tempo se houver muitos dados de destinatários.

Para remover completamente uma Inscrição de Borda, você precisa executar este procedimento no servidor de Transporte de Borda que deseja remover em um servidor de Caixa de Correio do Exchange 2013 no site do Active Directory em que o servidor de Transporte de Borda está inscrito.

Depois que você remover a Inscrição de Borda, a sincronização de informações do AD LDS será interrompida. Todas as contas armazenadas no AD LDS são removidas e o servidor de Transporte de Borda é removido da lista de servidores de origem de qualquer Conector de envio. Você não poderá mais usar os recursos do servidor de Transporte de Borda que se baseiam nos dados do Active Directory.

1.  Para remover a Inscrição de Borda do servidor de Transporte de Borda, use a sintaxe a seguir.
    
    ```powershell
Remove-EdgeSubscription <EdgeTransportServerIdentity>
```
    
    Por exemplo, para remover a Inscrição de Borda do servidor de Transporte de Borda chamado Edge01, execute o comando a seguir.
    
    ```powershell
Remove-EdgeSubscription Edge01
```

2.  Para remover a Inscrição de Borda do servidor de Caixa de Correio, use a sintaxe a seguir.
    
    ```powershell
Remove-EdgeSubscription <MailboxServerIdentity>
```
    
    Por exemplo, para remover a Inscrição de Borda do servidor de Caixa de Correio chamado Mailbox01, execute o comando a seguir.
    
    ```powershell
Remove-EdgeSubscription Mailbox01
```

Será necessário remover a Inscrição de Borda se:

  - Você não deseja mais que o servidor de Transporte de Borda participe da sincronização do EdgeSync. Será necessário remover a Inscrição de Borda tanto do servidor de Transporte de Borda como da organização do Exchange.

  - Um servidor de Transporte de Borda está sendo descomissionado. Neste cenário, só é necessário remover a Inscrição de Borda da organização do Exchange. Se você desinstalar a função de servidor de Transporte de Borda do computador, a instância do AD LDS e todos os dados do Active Directory armazenados no AD LDS também serão removidos.

  - Você deseja alterar a associação de site do Active Directory para a Inscrição de Borda. Só é necessário remover a Inscrição de Borda da organização do Exchange. Após a remoção da Inscrição de Borda da organização do Exchange, é possível inscrever-se novamente no servidor de Transporte de Borda em um site diferente do Active Directory.

Quando você remove uma Inscrição de borda da organização do Exchange:

  - A sincronização de informações do Active Directory para o AD LDS é interrompida.

  - As contas ESRA são removidas do Active Directory e do AD LDS.

  - O servidor de Transporte de Borda é removido da propriedade *SourceTransportServers* de qualquer Conector de envio.

  - O Conector de envio de entrada automático do servidor de Transporte de Borda para a organização do Exchange é removido do AD LDS.

Quando você remove a Inscrição de Borda de um servidor de Transporte de Borda:

  - Não poderá mais usar os recursos de servidor de Transporte de Borda que se baseiam nos dados do Active Directory.

  - Os dados replicados são removidos do AD LDS.

  - As tarefas que foram desabilitadas quando a Inscrição de Borda foi criada são reabilitadas novamente para permitir a configuração local.

## Inscrever-se novamente um servidor de Transporte de Borda

Ocasionalmente, talvez seja necessário inscrever-se novamente um servidor de Transporte de Borda em um site do Active Directory. Quando a Inscrição de Borda é recriada, novas credenciais são geradas e o processo completo de Inscrição de Borda deve ser seguido. É necessário cancelar a inscrição de um servidor de Transporte de Borda se:

  - Você adicionar novos servidores de Caixa de Correio no site do Active Directory inscrito e quiser que o novo servidor de Caixa de Correio participe da sincronização do EdgeSync.

  - Você aplicou a chave de licença ao servidor de Transporte de Borda após a criação da Inscrição de Borda. As informações de licenciamento para o servidor de Transporte de Borda são capturadas quando a Inscrição de Borda é criada. Os servidores de Transporte de Borda inscritos só aparecerão como licenciados se estiverem inscritos na organização do Exchange depois de a chave de licença já ter sido aplicada no servidor de Transporte de Borda. Se a chave de licença for aplicada ao servidor de Transporte de Borda depois que você executar o processo de Inscrição de Borda, as informações de licença não serão atualizadas na organização do Exchange e você deverá inscrever novamente o servidor de Transporte de Borda.

  - As credenciais de ESRA estão comprometidas.
    

    > [!IMPORTANT]
    > Para inscrever novamente um servidor de Transporte de Borda, exporte um novo arquivo de Inscrição de Borda para o servidor de Transporte de Borda e, então, importe o arquivo XML em um servidor de Caixa de Correio. Será necessário inscrever novamente o servidor de Transporte de Borda no mesmo site do Active Directory onde ele foi originalmente inscrito. Não é necessário remover primeiro a Inscrição de Borda original; o novo processo de inscrição substituirá a Inscrição de Borda existente.



## Adicionar ou remover um servidor de Caixa de Correio

Se você adicionar um servidor de Caixa de Correio a um site do Active Directory que já tenha um servidor de Transporte de Borda inscrito, o novo servidor de Caixa de Correio não participa automaticamente da sincronização do EdgeSync. Para permitir que um servidor de Caixa de Correio recém implantado participe do processo de sincronização do EdgeSync, será necessário inscrever novamente cada servidor de Transporte de Borda no site do Active Directory.

Remover um servidor de Caixa de Correio de um site do Active Directory em que um servidor de Transporte de Borda esteja inscrito não afetará a sincronização do EdgeSync, a menos que o servidor de Caixa de Correio seja o único servidor de Caixa de Correio nesse site. Se você remover todos os servidores de Caixa de Correio do site do Active Directory em que um servidor de Transporte de Borda esteja inscrito, os servidores de Transporte de Borda inscritos ficarão órfãos.

## Executar o EdgeSync manualmente

Talvez você queira executar manualmente o EdgeSync se tiver feito alterações significativas nas configurações ou nos destinatários do Active Directory e quiser que suas alterações sejam sincronizadas imediatamente. É possível executar uma sincronização total ou sincronizar somente as alterações feitas desde a última replicação.

Um EdgeSync manual redefine a programação de sincronização do EdgeSync. A próxima sincronização automática baseia-se em quando você executou a sincronização manual.

Para executar manualmente o EdgeSync, use a sintaxe a seguir.

    Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]

O exemplo a seguir inicia o EdgeSync com as seguintes opções:

  - A sincronização foi iniciada do servidor de Caixa de Correio do Exchange 2013 chamado Mailbox01.

  - Todos os servidores de Transporte de Borda são sincronizados.

  - Somente as alterações desde a última replicação são sincronizadas.

<!-- end list -->

```powershell
Start-EdgeSynchronization -Server Mailbox01
```

Este exemplo inicia o EdgeSync com as seguintes opções:

  - A sincronização foi iniciada do servidor de Caixa de Correio local.

  - Somente o servidor de Transporte de Borda chamado Edge03 é sincronizado.

  - Todos os dados de configuração e destinatário são totalmente sincronizados.

<!-- end list -->

```powershell
Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync
```

## Verificar os resultados do EdgeSync

Você pode usar o cmdlet **Test-EdgeSynchronization** para verificar se a sincronização de Borda está funcionando. Esse cmdlet gera um relatório do status de sincronização dos servidores de Transporte de Borda inscritos.

A saída criada por esse cmdlet permite que você veja quais objetos não foram sincronizados no servidor de Transporte de Borda. A tarefa compara os dados armazenados no Active Directory aos dados armazenados no AD LDS e informa qualquer inconsistência de dados.

É possível usar o parâmetro *ExcludeRecipientTest* com o cmdlet **Test-EdgeSynchronization** para excluir a validação da sincronização de dados de destinatário. Se você incluir esse parâmetro, somente a sincronização de objetos de configuração será validada. A validação dos dados de destinatários demorará mais do que validar somente os dados de configuração.

## Verificar resultados do EdgeSync para um único destinatário

Para verificar resultados do EdgeSync para um único destinatário, use a sintaxe a seguir no servidor de Caixa de Correio no site Active Directory inscrito.

```powershell
Test-EdgeSynchronization -VerifyRecipient <emailaddress>
```

Este exemplo verifica resultado do EdgeSync para a usuária kate@contoso.com.

```powershell
Test-EdgeSynchronization -VerifyRecipient kate@contoso.com
```

Voltar ao início

