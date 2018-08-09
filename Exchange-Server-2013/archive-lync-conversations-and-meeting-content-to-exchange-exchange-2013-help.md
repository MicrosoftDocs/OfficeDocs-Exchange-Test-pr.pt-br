---
title: 'Arquivar conversas do Lync e o conteúdo da reunião para o Exchange'
TOCTitle: Arquivar conversas do Lync e o conteúdo da reunião para o Exchange
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678849
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arquivar conversas do Lync e o conteúdo da reunião para o Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Você pode arquivar conteúdo de Lync Online, como conversas de mensagens Instantâneas, caixa de correio do usuário em Exchange Online. Em implantações de local, você pode arquivar conteúdo Lync 2013 às caixas de correio Exchange 2013. Em ambos online e ambientes locais, isso requer a colocação de um litígio ou um bloqueio In-loco na caixa de correio do usuário. Quando o conteúdo do Lync é permanentemente excluído por um usuário cuja caixa de correio está em espera, o Lync arquivado conteúdo é preservado na pasta itens recuperáveis na caixa de correio do usuário. Não é visível para os usuários, mas ele está incluído nas pesquisas de descoberta eletrônica.

Quando você coloca uma caixa de correio em retenção de litígio, todos os tipos de conteúdo, incluindo os itens do Lync, são preservados. Por padrão, isso também é o caso quando você cria um bloqueio In-loco. No entanto, se desejar usar um bloqueio In-loco para preservar apenas itens do Lync, você pode usar a opção **Selecionar tipos de mensagens** através do Assistente de **Descoberta eletrônica In-loco & bloqueio** para selecionar **itens do Lync**, conforme mostrado na captura de tela abaixo.

![Colocar itens do Lync em espera](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Colocar itens do Lync em espera")


> [!TIP]
> Você também pode configurar um bloqueio In-loco para excluir itens do Lync. Por exemplo, organizações talvez prefira preservar itens da caixa postal e mensagem instantânea para um período de tempo menor outros tipos de conteúdo. Para implementar esse tipo de política de retenção, você criará um bloqueio In-loco para preservar o conteúdo por um longo período de tempo (por exemplo, sete anos) e excluir itens do Lync desta isenção. Em seguida, você cria outra In-Place Hold com uma duração de espera menor que preserva apenas itens do Lync. Você também pode especificar por quanto tempo o conteúdo deve ser preservado. Para obter mais informações sobre a criação de uma isenção com uma duração específica, consulte <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Retenção local e Retenção de litígio</A>.



Consulte os tópicos a seguir para obter instruções passo a passo para colocar um usuário em espera:

  - [Criar ou remover um bloqueio In-loco](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [Colocar uma caixa de correio em Retenção de Litígio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

Para tarefas de gerenciamento adicionais relacionadas a arquivamento, consulte:

  - [Habilitar ou desabilitar uma caixa de correio de arquivo morto no Exchange Online](https://technet.microsoft.com/pt-br/library/jj984357\(v=exchg.150\))

  - [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## Mais informações

  - Arquivamento de conteúdo do Lync ocorre no servidor, independente de se o usuário tem o cliente Lync configurado para [Salvar as conversas de IM do Lync na pasta Histórico da conversa](https://go.microsoft.com/fwlink/p/?linkid=400589).

  - Arquivamento do conteúdo do Lync começa após o usuário é colocado em retenção de litígio ou bloqueio in-loco. Para garantir Lync do usuário comunicações são arquivadas desde o momento em que sua conta é criada, local, a conta em espera imediatamente após sua criação.

Além disso, em implantações em instalações Exchange 2013 e Lync 2013:

  - Você deve configurar a autenticação OAuth entre o Lync 2013 e Exchange 2013. Para obter detalhes, consulte [Integração com o SharePoint e o Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

  - Você também pode arquivar Lync 2013 conteúdo para Exchange 2013 independentemente se um usuário é colocado em espera. Isso é feito definindo a diretiva de arquivamento do Exchange do usuário. Use o cmdlet de `Set-CsUser` no servidor Lync 2013 para definir a propriedade de *ExchangeArchivingPolicy* do usuário Lync como `ArchivingToExchange`.

  - Para obter mais detalhes sobre o conteúdo do Lync em implantações em instalações de arquivamento, consulte [Planning for Archiving](https://go.microsoft.com/fwlink/p/?linkid=400590) na documentação de Lync 2013.

