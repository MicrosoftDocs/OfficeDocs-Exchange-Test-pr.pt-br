---
title: 'Configurar um domínio aceito para uma unidade de negócios com caixas de correio fora da sua organização do Exchange: Exchange 2013 Help'
TOCTitle: Configurar um domínio aceito para uma unidade de negócios com caixas de correio fora da sua organização do Exchange
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50487091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um domínio aceito para uma unidade de negócios com caixas de correio fora da sua organização do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-08-06_

Em algumas instâncias, você pode configurar um domínio aceito para uma unidade de negócios em que alguns ou todos os destinatários no domínio não têm caixas de correio em sua organização do Exchange. Isso pode ocorrer, por exemplo, quando uma organização compartilha o mesmo endereço SMTP entre dois ou mais sistemas de email diferentes. Para esses cenários, você pode configurar um domínio aceito como um domínio de retransmissão interno.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios aceitos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Se você tiver um servidor de Transporte de Borda inscrito em sua rede de perímetro, configure os domínios aceitos em um servidor de Caixa de Correio em sua organização do Exchange. A configuração de domínios aceitos é replicada para o servidor de Transporte de Borda durante a sincronização do EdgeSync. Para saber mais, confira [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - Depois de configurar um domínio aceito, você deve verificar se um registro do recurso de MX do DNS (Sistema de Nome de Domínio) público desse namespace SMTP existe e se o registro de recurso de MX faz referência a um nome de servidor e a um endereço IP associado à sua organização do Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para configurar um domínio aceito como um domínio de retransmissão interno

1.  No EAC, navegue até **Fluxo de emails** \> **Domínios aceitos**, selecione o domínio que deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  No campo **Nome**, digite o nome de exibição do domínio aceito. Cada domínio aceito para a sua organização deve ter um nome de exibição exclusivo. Isso pode ser diferente em relação ao domínio aceito. Por exemplo, se o domínio Contoso.com puder ter um nome para exibição de Domínio Aceito Local Contoso.

3.  Selecione **Domínio de Retransmissão Interno**.

4.  Clique em **Salvar**.

## Como saber se funcionou?

Para verificar se você configurou com êxito o domínio aceito como domínio de retransmissão interno, envie uma mensagem do domínio de retransmissão interno para uma caixa de correio na sua organização do Exchange e verifique se ela foi recebida.

