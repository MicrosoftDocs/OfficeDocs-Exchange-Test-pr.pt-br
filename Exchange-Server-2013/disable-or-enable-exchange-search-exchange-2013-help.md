---
title: 'Desabilitar ou habilitar a Pesquisa do Exchange: Exchange 2013 Help'
TOCTitle: Desabilitar ou habilitar a Pesquisa do Exchange
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52058792
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar ou habilitar a Pesquisa do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-05-07_

Por padrão, a Pesquisa do Exchange é habilitada para todos os novos bancos de dados de caixa de correio e não exige configuração adicional. Entretanto, se você quiser que a Pesquisa do Exchange pare de indexar o conteúdo da caixa de correio, você pode desabilitar a pesquisa para bancos de dados de caixas de correio individuais ou para todo um servidor de Caixa de Correio.


> [!CAUTION]
> Desabilitar a Pesquisa do Exchange afeta a funcionalidade e o desempenho das pesquisas de texto completo executadas pelos seus usuários com o Outlook no modo online ou em dispositivos móveis com Windows.<BR>O <A href="in-place-ediscovery-exchange-2013-help.md">Descoberta Eletrônica In-loco</A> também depende da Pesquisa do Exchange. Se você desabilitar a Pesquisa do Exchange para um banco de dados de caixa de correio ou para um servidor de Caixa de Correio, as pesquisas de Descoberta eletrônica In-loco não retornarão mensagens do banco de dados ou do servidor.



Para conhecer tarefas de gerenciamento adicionais relacionadas à Pesquisa do Exchange, consulte [Procedimentos de pesquisa do Exchange](exchange-search-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 1 minuto

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Você pode habilitar ou desabilitar a Pesquisa do Exchange para servidores ou bancos de dados de caixa de correio, mas não para usuários individuais de caixa de correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## O que você deseja fazer?

## Desabilitar ou habilitar a Pesquisa do Exchange para um banco de dados de caixa de correio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Pesquisa do Exchange\&quot; no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).


> [!NOTE]
> Não é possível usar o EAC para desabilitar ou habilitar a Pesquisa do Exchange para um banco de dados de caixa de correio.



Este comando desabilita a Pesquisa do Exchange para um banco de dados de caixa de correio chamado EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

Este comando habilita a Pesquisa do Exchange para um banco de dados de caixa de correio chamado EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

## Desabilitar ou habilitar a Pesquisa do Exchange para um servidor de caixa de correio

Para desabilitar a Pesquisa do Exchange para um servidor de Caixa de Correio, é necessário desabilitar e interromper o serviço de Pesquisa do Microsoft Exchange. Da mesma maneira, para habilitar a Pesquisa do Exchange para um servidor de Caixa de Correio, você precisa habilitar e iniciar o serviço de Pesquisa do Microsoft Exchange. Para isso, use o console de Serviços ou o Shell.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Gerenciar serviço Pesquisa do Exchange em um servidor de Caixa de Correio\&quot; no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

**Usar o console de Serviços**

1.  Vá até **Iniciar** \> **Ferramentas Administrativas** \> **Serviços**.

2.  No painel de detalhes **Serviços**, clique com o botão direito no serviço **Pesquisa do Microsoft Exchange** e selecione **Propriedades**.

3.  Na guia **Geral**, na lista **Tipo de Inicialização**, selecione **Desabilitado**, para desabilitar o serviço, ou **Automático**, para iniciá-lo automaticamente.
    

    > [!NOTE]
    > O tipo de inicialização afetará o serviço na próxima vez que for feita uma tentativa de inicializá-lo, seja automaticamente, após o servidor ser reiniciado, ou manualmente. Na próxima etapa, o serviço será interrompido ou iniciado manualmente.



4.  Clique em **Parar**, para parar o serviço, ou **Iniciar**, para iniciar o serviço.

5.  Clique em **OK** para salvar as alterações.

**Usar o Shell**

Execute os seguintes comandos para interromper e desabilitar o serviço de Pesquisa do Microsoft Exchange.

```
    Stop-Service MSExchangeFastSearch
```
```
    Set-Service MSExchangeFastSearch -StartupType Disabled
```
Execute os seguintes comandos para configurar o serviço de Pesquisa do Exchange de modo ele seja iniciado automaticamente e depois inicie o serviço.

```
    Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
    Start-Service MSExchangeFastSearch
```
