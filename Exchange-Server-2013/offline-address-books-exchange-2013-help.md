---
title: 'Catálogos de endereços offline: Exchange 2013 Help'
TOCTitle: Catálogos de endereços offline
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50486331
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Catálogos de endereços offline

 

_**Aplica-se a:** Exchange Server 2010, Exchange Server 2013_

_**Tópico modificado em:** 2014-11-16_

Um catálogo de endereços offline (OAB) é uma cópia de uma coleção de lista de endereços que tenha sido baixada para que um usuário do Microsoft Outlook possa acessar o catálogo de endereços enquanto desconectado do servidor. Microsoft Exchange gera os novos arquivos OAB e compacta os arquivos e coloca-los em um compartilhamento de local. Você pode decidir quais listas de endereços são disponibilizadas para os usuários que trabalham offline, e você também pode configurar o método pelo qual os catálogos de endereços são distribuídos.

Para saber mais sobre listas de endereços, consulte [Listas de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-lists/address-lists).


> [!IMPORTANT]
> Dados OAB são produzidos pelo serviço Microsoft Exchange OABGen, que é um Assistente de caixa de correio. Se você usar o descritor de segurança para impedir que usuários exibindo certos destinatários no Active Directory, usuários que baixar o OAB será capazes de exibir os destinatários ocultos. Portanto, para ocultar um destinatário a partir de uma lista de endereços, defina o parâmetro de <EM>HiddenFromAddressListsEnabled</EM> à <A href="https://technet.microsoft.com/pt-br/library/aa998596(v=exchg.150)">Set-PublicFolder</A>, <A href="https://technet.microsoft.com/pt-br/library/aa995950(v=exchg.150)">Set-MailContact</A>, <A href="https://technet.microsoft.com/pt-br/library/aa995971(v=exchg.150)">Set-MailUser</A>, <A href="https://technet.microsoft.com/pt-br/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</A>, <A href="https://technet.microsoft.com/pt-br/library/bb123981(v=exchg.150)">Set-Mailbox</A>e <A href="https://technet.microsoft.com/pt-br/library/bb124955(v=exchg.150)">Set-DistributionGroup</A> cmdlets. Como alternativa, você pode criar um novo padrão OAB que não contêm os destinatários ocultos. Para obter detalhes sobre como adicionar ou remover listas de endereços de um OAB, consulte <A href="https://docs.microsoft.com/pt-br/exchange/address-books/offline-address-books/add-or-remove-an-address-list">Adicionar uma lista de endereços para ou remover uma lista de endereços do catálogo de endereços offline</A>.



Procurando tarefas de gerenciamento relacionadas a OABs? Consulte [Procedimentos do catálogo de endereços offline](https://docs.microsoft.com/pt-br/exchange/address-books/offline-address-books/offline-address-book-procedures).

**Sumário**

Movendo OABs entre versões do Exchange

Versão 4 do OAB e clientes do Outlook

Distribuição baseada na Web

Considerações do OAB

## Movendo OABs entre versões do Exchange

No Exchange 2007 e Exchange 2010, você pode usar o cmdlet **Move-OfflineAddressBook** para mover a geração do OAB para outro servidor de caixa de correio. Exchange 2013 suporta apenas o OAB (versão 4). Essa é a mesma versão que era o padrão no Exchange 2010. Você não pode configurar o Exchange 2013 para gerar as outras versões do OAB e a geração do OAB ocorre no servidor de caixa de correio em que a caixa de correio da organização reside. Portanto, para mover a geração do OAB no Exchange 2013, você deve mover a caixa de correio da organização. Você só pode mover a geração do OAB para outro banco de dados de caixa de correio do Exchange 2013. Você não pode mover a geração do OAB para uma versão anterior do Exchange. Para localizar a caixa de correio de organização do Exchange 2013 OAB, execute o seguinte comando no Shell:

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

Então, você pode usar os cmdlets **MoveRequest** para mover a caixa de correio.

## Versão 4 do OAB e clientes do Outlook

Exchange 2013 suporta apenas o OAB versão 4. OAB versão 4 foi introduzido no Exchange 2003 Service Pack 2 (SP2) e é suportada pela Outlook 2007, Outlook 2010 e Outlook 2013. Este OAB Unicode permite que os computadores cliente para receber atualizações diferenciais em vez de downloads de OAB completo e um tamanho de arquivo reduzido.

## Clientes do Outlook que usam o OAB versão 4

Para o Outlook 2013, Outlook 2010, Outlook 2007 e os clientes que usam o OAB versão 4, se o tamanho dos arquivos Changes for metade o tamanho (ou mais) dos arquivos OAB inteiros, Outlook inicia um OAB completo Baixe.

## Distribuição baseada na Web

*Distribuição baseada na Web* é o método de distribuição por quais Outlook 2013, Outlook 2010 ou Outlook 2007 clientes que estão trabalhando offline podem acessar o OAB.

Existem diversas vantagens em usar a distribuição baseada na Web, incluindo:

  - Suporte de computadores de clientes mais simultâneos.

  - Redução no uso de largura de banda.

  - Mais controle sobre os pontos de distribuição do OAB. Com a distribuição baseada na Web, o ponto de distribuição é o endereço da web HTTPS, onde os computadores cliente podem baixar o OAB.

Para se beneficiar mais distribuição baseada na Web, os computadores cliente devem estar executando o Outlook 2013, Outlook 2010 ou Outlook 2007.

Para funcionar corretamente, a distribuição baseada na Web depende os seguintes componentes:

  - **Processo de geração do OAB**   Este é o processo pelo qual Exchange cria e atualiza o OAB. Para criar e atualizar o OAB, o serviço de OABGen é executado no servidor de caixa de correio no qual a caixa de correio da organização está localizada. Para suportar a distribuição do OAB, esse servidor deve ser um servidor de caixa de correio Exchange.

  - **Distribuição do OAB**   Se um cliente inicia a solicitação de distribuição do OAB, a solicitação direcionado através de um servidor de acesso para cliente. Servidor acesso para cliente, em seguida, encaminha a solicitação no servidor de caixa de correio que está hospedando os arquivos OAB. Os arquivos OAB serão distribuídos diretamente do servidor de caixa de correio para o cliente.

  - **Diretório virtual do OAB**   O diretório virtual do OAB é o ponto de distribuição usado pelo método distribuição baseada na Web. Por padrão, quando Exchange estiver instalado, um novo diretório virtual chamado **OAB** é criado no site interno padrão no serviços de informações da Internet (IIS). Se você tiver usuários do cliente que se conectam ao Outlook de fora do firewall da organização, você poderá adicionar um site externo. Como alternativa, quando você executar o cmdlet **New-OABVirtualDirectory** no Shell, um novo diretório virtual chamado OAB é criado no site do IIS padrão no servidor de acesso para cliente local Exchange. Para obter informações, consulte [Criar um diretório virtual do catálogo de endereços offline](https://docs.microsoft.com/pt-br/exchange/address-books/offline-address-books/create-virtual-directory).

  - **Serviço de descoberta automática**   Esse é um recurso disponível no Outlook 2013, Outlook 2010, Outlook 2007 e em alguns dispositivos móveis que configuram automaticamente os clientes para o acesso a Exchange. O serviço é executado em um servidor de acesso para cliente e retorna a URL correta do OAB para uma conexão de cliente específico.

## Considerações de OAB

Como prática recomendada, se você usar um OAB único ou vários OABs, considere os fatores a seguir ao planejar e implementar sua estratégia de OAB:

  - Tamanho de cada OAB em sua organização. Para obter mais informações, consulte Considerações de tamanho OAB posteriormente neste tópico.

  - Número de downloads do OAB.

  - Número e a frequência das alterações de nome distinguida pai.

  - Diferenças de endereço SMTP.

  - Número total de alterações feitas no diretório.

## Considerações de tamanho do OAB

Para algumas organizações, o OAB é um arquivo pequeno que usuários remotos ocasionalmente baixarem. Para essas empresas, baixar o OAB normalmente não é uma preocupação. No entanto, algumas organizações grandes que possuem grandes diretórios, ou para organizações que implantaram Outlook 2003 no cache Exchange modo, ele pode ser uma preocupação, especialmente se as organizações têm consolidados Exchange servidores em um datacenter regional.

Tamanhos OAB podem variar de alguns megabytes a algumas centenas de megabytes. Os seguintes fatores podem afetar o tamanho do OAB:

  - Uso de certificados em uma empresa. A infraestrutura de chave mais pública (PKI) certificados, quanto maior o OAB. Os certificados de PKI variam de 1 quilobyte (KB) a 3 KB. Eles são os maiores colaboradores individuais para o tamanho do OAB.

  - Número de destinatários de email em Active Directory.

  - Número de grupos de distribuição em Active Directory.

  - Informações de uma empresa adiciona a Active Directory para cada caixa de correio habilitada ou objeto habilitado para email. Por exemplo, algumas organizações preenchem as propriedades de cada usuário; outros não.

