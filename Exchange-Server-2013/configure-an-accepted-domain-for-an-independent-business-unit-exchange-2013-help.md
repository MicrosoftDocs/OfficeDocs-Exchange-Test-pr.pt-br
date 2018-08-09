---
title: 'Configurar um domínio aceito para uma unidade de negócios independente'
TOCTitle: Configurar um domínio aceito para uma unidade de negócios independente
ms:assetid: bc95dbdc-3669-4c06-ab94-90093bc0dbfd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657491(v=EXCHG.150)
ms:contentKeyID: 50486517
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um domínio aceito para uma unidade de negócios independente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-17_

Em algumas situações, você deverá configurar um domínio aceito para uma unidade de negócios independente com servidores de email fora da sua organização do Exchange. Em tais cenários, é possível configurar o domínio aceito como um domínio de retransmissão externo.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios aceitos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Se você tiver um servidor de Transporte de Borda inscrito em sua rede de perímetro, configure os domínios aceitos em um servidor de Caixa de Correio em sua organização do Exchange. A configuração de domínios aceitos é replicada para o servidor de Transporte de Borda durante a sincronização do EdgeSync. Para saber mais, confira [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - Não é possível criar um domínio aceito que possua o mesmo nome de um domínio remoto já configurado. Por exemplo, se você tiver configurado fabrikam.com como um domínio remoto, não poderá criar um domínio aceito para fabrikam.com.

  - Depois de configurar um domínio aceito, você deve verificar se um registro do recurso de MX do DNS (Sistema de Nome de Domínio) público desse namespace SMTP existe e se o registro de recurso de MX faz referência a um nome de servidor e a um endereço IP associado à sua organização do Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o EAC para configurar um domínio aceito como sendo domínio de retransmissão externo

Você deverá configurar um domínio aceito para uma unidade de negócios com servidores de email fora da sua organização do Exchange.

1.  No EAC, navegue até **Fluxo de mensagens** \> **Domínios aceitos**, selecione o domínio que deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  No campo **Nome**, insira o nome para exibição do domínio aceito. Cada domínio aceito para a sua organização deve ter um nome para exibição original. Esse nome pode ser diferente daquele do domínio aceito. Por exemplo, o domínio Contoso.com poderia ter como nome para exibição Domínio Contoso Aceito Localmente.

3.  Selecione **Domínio de Retransmissão Externo**. Essa opção é destinada a emails retransmitidos a servidores fora da organização do Exchange.

4.  Clique em **Salvar**.

## Como saber se funcionou?

Para verificar se você configurou com sucesso um domínio aceito como domínio de retransmissão externo, envie uma mensagem do domínio aceito configurado como domínio de retransmissão externo e confira se a mensagem foi recebida.

