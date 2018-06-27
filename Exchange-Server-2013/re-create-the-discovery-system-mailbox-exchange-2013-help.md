---
title: 'Recriar a caixa de correio do sistema de descoberta: Exchange 2013 Help'
TOCTitle: Recriar a caixa de correio do sistema de descoberta
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50485674
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recriar a caixa de correio do sistema de descoberta

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2018-01-17_

Descoberta eletrônica in-loco usa uma caixa de correio do sistema para armazenar metadados de pesquisa de descoberta eletrônica In-loco. Esta caixa de correio do sistema de descoberta tem o nome de exibição **SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**. Como caixas de correio do sistema não são visíveis no Centro de administração do Exchange (EAC) ou em listas de endereços Exchange, eles raramente são excluídos inadvertidamente.

No entanto, se a caixa de correio do sistema de descoberta for excluída acidentalmente, gerentes de descoberta será capaz de realizar pesquisas de descoberta eletrônica In-loco ou gerenciar as pesquisas existentes. Nesse caso, para habilitar a funcionalidade de descoberta eletrônica, você deverá recriar a caixa de correio do sistema de descoberta.

## Você deve saber antes de começar

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use o Shell para recriar a caixa de correio do sistema de descoberta

1.  Exclua a conta de usuário SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} Active Directory, se ela existir. Por padrão, Exchange Server 2013 a instalação cria a caixa de correio no contêiner usuários Active Directory. Para obter detalhes sobre como excluir uma conta de usuário de Active Directory, consulte [Excluir uma conta de usuário](https://go.microsoft.com/fwlink/p/?linkid=215850).

2.  Use o Shell para habilitar a caixa de correio do sistema de descoberta.
    

    > [!TIP]
    > Você não pode usar o EAC para habilitar a caixa de correio do sistema de descoberta.<BR>O comando a seguir deve ser executado do mesmo diretório onde você extraiu da mídia de instalação do Exchange.

    
    Para recriar a caixa de correio do sistema de descoberta, execute o seguinte comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## Como saber se funcionou?

Para verificar se você criou com êxito novamente a caixa de correio do sistema de descoberta, use o cmdlet **Get-Mailbox** com a opção *Arbitration* para recuperar caixas de correio do sistema. Exiba os resultados do comando para verificar se a caixa de correio do sistema `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` foi criado novamente.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


