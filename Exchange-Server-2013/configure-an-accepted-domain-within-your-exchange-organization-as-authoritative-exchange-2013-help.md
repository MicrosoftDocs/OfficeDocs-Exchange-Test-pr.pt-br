---
title: 'Configurar um domínio aceito na organização do Exchange como autoritativo'
TOCTitle: Configurar um domínio aceito na organização do Exchange como autoritativo
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50486882
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um domínio aceito na organização do Exchange como autoritativo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-17_

Se um domínio pertencente à sua organização hospedar caixas de correio para todos os destinatários em um namespace SMTP, esse domínio será considerado autoritativo. Por padrão, um domínio aceito é configurado como autoritativo para a organização do Exchange. Se a sua organização tiver mais de um namespace SMTP, você poderá configurar mais de um domínio aceito como autoritativo.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios aceitos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Se você tiver um servidor de Transporte de Borda inscrito em sua rede de perímetro, configure os domínios aceitos em um servidor de Caixa de Correio em sua organização do Exchange. A configuração de domínios aceitos é replicada para o servidor de Transporte de Borda durante a sincronização do EdgeSync. Para saber mais, confira [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - Não é possível criar um domínio aceito que possua o mesmo nome de um domínio remoto já configurado. Por exemplo, se você tiver configurado fabrikam.com como um domínio remoto, não poderá criar um domínio aceito para fabrikam.com.

  - Depois de configurar um domínio aceito, você deve verificar se um registro do recurso de MX do DNS (Sistema de Nome de Domínio) público desse namespace SMTP existe e se o registro de recurso de MX faz referência a um nome de servidor e a um endereço IP associado à sua organização do Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para configurar um domínio aceito como autoritativo

Se um domínio aceito para a sua organização do Exchange hospedar todas as caixas de correio de destinatários nesse namespace de SMTP de domínio, você poderá configurá-lo como um domínio autoritativo.

1.  No EAC, navegue até **Fluxo de emails** \> **Domínios aceitos** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No campo **Nome**, digite o nome de exibição do domínio aceito. Cada domínio aceito para a sua organização deve ter um nome para exibição exclusivo. Ele pode ser diferente do domínio aceito. Por exemplo, se o domínio contoso.com puder ter um nome para exibição de Domínio Aceito Local Contoso.

3.  No campo **Domínio aceito**, digite o domínio aceito. Especifique um namespace SMTP para o qual a organização aceita mensagens de email. (por exemplo, Contoso.com).

4.  Selecione **Domínio autoritativo**. Esta opção é para email retransmitido a servidores na sua organização do Exchange para um domínio aceito que hospeda caixas de correio para todos os destinatários em um namespace SMTP.

5.  Clique em **Salvar**.


> [!TIP]
> Para configurar um domínio aceito que já tenha sido criado, selecione o domínio da lista de domínios aceitos e clique em <STRONG>Editar</STRONG><IMG title="Ícone de edição" alt="Ícone de edição" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">. Você pode configurar mais de um domínio como autoritativo.



## Como saber se funcionou?

Seu novo domínio aceito aparecerá na lista de domínios aceitos no EAC. Para verificar se você configurou com êxito o domínio aceito como autoritativo, envie email ao domínio e verifique se ele é recebido.

