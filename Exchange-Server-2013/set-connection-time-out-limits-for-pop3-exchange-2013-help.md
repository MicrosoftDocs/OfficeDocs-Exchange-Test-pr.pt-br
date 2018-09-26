---
title: 'Definir limites de tempo limite de conexão para POP3: Exchange 2013 Help'
TOCTitle: Definir limites de tempo limite de conexão para POP3
ms:assetid: 40003115-be4e-4cf1-97b4-f5ca05b314dc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997604(v=EXCHG.150)
ms:contentKeyID: 50556170
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir limites de tempo limite de conexão para POP3

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-28_

Você pode usar o EAC ou o Shell para configurar os limites de tempo para conexões ociosas POP3 autenticadas e não autenticadas.

Para mais informações relacionadas ao POP3, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações POP3" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para definir limites de tempo de conexão para POP3

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Role para baixo e clique em **Mais opções**.

5.  Em **Configurações de tempo limite**, use as seguintes configurações:
    
      - **Tempo limite autenticado (segundos)**    Especifica o tempo para aguardar antes de fechar uma conexão autenticada ociosa. O valor padrão é 1.800. Os valores possíveis são de 30 a 86.400.
    
      - **Tempo limite não autenticado (segundos)**    Especifica o tempo para aguardar antes de fechar uma conexão não autenticada ociosa. O valor padrão é 60. Os valores possíveis são de 30 a 3.600.

6.  Clique em **Aplicar** e clique em **OK** para salvar as alterações.

Após definir o tempo limite de conexões para POP3, é preciso reiniciar os serviços POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Use o shell para definir limites de tempo de conexão para POP3

Este exemplo define o tempo limite de conexão para conexões autenticadas ociosas.

```powershell
Set -PopSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue
```

Este exemplo define o tempo limite de conexão para conexões não autenticadas ociosas.

```powershell
Set -PopSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue
```

Após definir o tempo limite de conexões para POP3, é preciso reiniciar os serviços POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se os limites de conexão foram definidos com êxito, siga um destes procedimentos:

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Role para baixo e clique em **Mais opções**.

5.  Em **Configurações de tempo limite**, verifique se as configurações de conexão estão corretas.

Ou

1.  Execute o seguinte comando no Shell.
    
  ```powershell
  Get-PopSettings | format-list
  ```

2.  Verifique se as configurações de conexão estão corretas.

## Para mais informações

Após definir limites de tempo de conexão para POP3, talvez você deseje também:

[Habilitar POP3 no Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Definir limites de conexão para POP3](set-connection-limits-for-pop3-exchange-2013-help.md)

