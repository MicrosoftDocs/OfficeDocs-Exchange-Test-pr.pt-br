---
title: 'Definir limites de conexão para POP3: Exchange 2013 Help'
TOCTitle: Definir limites de conexão para POP3
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50556189
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir limites de conexão para POP3

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-28_

Você pode usar o EAC ou o Shell para gerenciar limites de conexão de POP3 para sua organização.

Quando especificar os limites de conexão para POP3, você poderá selecionar os limites de conexão para o servidor, um endereço IP ou um usuário específico.

Para mais informações relacionadas a POP3, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações POP3" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EMC para definir limites de conexão POP3 para um servidor, endereço IP ou usuário

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Role para baixo e clique em **Mais opções**.

5.  Em **Limites de Conexão**, use as seguintes configurações:
    
      - **Máximo de Conexões**   Especifica o número total de conexões que o servidor especificado aceitará. Isso inclui conexões autenticadas e não autenticadas. O valor padrão é 2.147.483.647. Os valores possíveis vão de 1 a 2.147.483.647.
    
      - **Número máximo de conexões de um único endereço IP**   Especifica o número de conexões que o servidor aceitará de um único endereço IP. O valor padrão é 2.147.483.647. Os valores possíveis vão de 1 a 2.147.483.647.
    
      - **Número máximo de conexões de um único usuário**   Especifica o número máximo de conexões que o servidor aceitará de um usuário particular. O valor padrão é 16. Os valores possíveis vão de 1 a 2.147.483.647.
    
      - **Tamanho máximo de comando (bytes)**   Especifica o tamanho máximo de um único comando. O tamanho padrão é 512. Os valores possíveis são de 40 a 1.024.

6.  Clique em **Aplicar** e clique em **OK** para salvar as alterações.

Depois de definir limites de conexão, você deve reiniciar os serviços POP3. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Usar o Shell para definir limites de conexão POP3 para um servidor, endereço IP ou usuário

Este exemplo define o limite de conexão para um servidor.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnections Value
```

Este exemplo define o limite de conexão para um endereço IP.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

Este exemplo define o limite de conexão para um usuário.

    Set-PopSettings -MaxConnectionsPerUser Value 

Este exemplo define o tamanho máximo de comando.

```powershell
Set-PopSettings -MaxCommandSize Value
```

Depois de definir limites de conexão, você deve reiniciar os serviços POP3. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você definiu os limites de conexão com êxito, siga um destes procedimentos:

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Role para baixo e clique em **Mais opções**.

5.  Em **Limites de conexão**, verifique se as configurações de conexão estão corretas.

Ou

1.  Execute o seguinte comando no Shell.
    
    ```powershell
Get-PopSettings | format-list
```

2.  Verifique se configurações de conexão estão corretas.

## Para mais informações

Após definir limites de conexão POP3 para um servidor, um endereço IP ou usuário, você poderá também:

[Habilitar POP3 no Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Definir limites de tempo limite de conexão para POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

