---
title: 'Testar a conectividade do Outlook em qualquer lugar: Exchange 2013 Help'
TOCTitle: Testar a conectividade do Outlook em qualquer lugar
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50556143
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testar a conectividade do Outlook em qualquer lugar

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Você pode testar a conectividade do Outlook Anywhere do cliente de ponta a ponta usando o Shell ou o Analisador de Conectividade Remota do Exchange (ExRCA). Isso inclui o teste de conectividade do serviço Descoberta Automática, da criação de um perfil de usuário e do logon na caixa de correio do usuário. Todos os valores obrigatórios são obtidos do serviço Descoberta Automática.

Para outras tarefas de gerenciamento relacionadas ao Outlook Anywhere, consulte [Outlook em Qualquer Lugar](outlook-anywhere-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Outlook Anywhere" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para testar a conectividade do Outlook em Qualquer Lugar

Para usar o Shell para testar a conectividade do Outlook Anywhere, use o cmdlet **Test-OutlookConnectivity**.

Execute o seguinte comando.

```powrshell
    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com
```

> [!NOTE]
> O valor de parâmetro <EM>OutlookMailboxDeepTestProbe</EM> testa a conectividade do servidor de Caixa de Correio. Para testar a conectividade do servidor de Acesso para Cliente, use <EM>OutlookMailboxCTPProbe</EM> para o valor de parâmetro <EM>ProbeIdentity</EM>.



## Use o Analisador de Conectividade Remota do Exchange para testar a conectividade do Outlook Anywhere

O Exchange Remote Connectivity Analyzer (ExRCA) é uma ferramenta baseada na web projetada para testar a conectividade com uma variedade de protocolos do Exchange. Você pode acessar o ExRCA [aqui](https://go.microsoft.com/fwlink/p/?linkid=167905).

1.  No site do ExRCA, em **Testes de Conectividade do Microsoft Office Outlook**, selecione **Outlook Anywhere** e depois selecione Próximo na parte inferior da página.

2.  Insira as informações necessárias na próxima tela, incluindo endereço de email, domínio e nome de usuário e senha.

3.  Escolha se deseja usar a Descoberta Automática para detectar as configurações de servidor ou especificar manualmente as configurações de servidor.

4.  Aceite o aviso de isenção de responsabilidade, digite o código de verificação e, em seguida, selecione **Verificar**.

5.  Selecione **Realizar Teste**.

## Como saber se funcionou?

Quando o teste de ExRCA for concluído, os resultados serão exibidos na página da Web. Quaisquer falhas serão listadas.

