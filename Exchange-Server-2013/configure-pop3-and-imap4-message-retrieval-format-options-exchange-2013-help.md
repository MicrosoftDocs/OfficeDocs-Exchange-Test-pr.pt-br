---
title: 'Configurar formato de recuperação de mensagem POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar opções de formato de recuperação mensagem POP3 e IMAP4
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50556193
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar opções de formato de recuperação mensagem POP3 e IMAP4

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode configurar o formato de recuperação de mensagens para usuários que se conectam ao seu email usando POP3 e IMAP4. As opções de recuperação de mensagens podem ser configuradas no nível de servidor usando o EAC ou o Shell e podem ser configuradas no nível de usuário usando o Shell.

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "configurações de POP3" e "configurações de IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Definir o formato de recuperação de mensagem POP3 no nível do servidor

## Use o EAC para definir o formato de recuperação de mensagens POP3 no nível do usuário

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Em **Formato de Mensagem MIME**, escolha entre as seguintes configurações:
    
      - Texto
    
      - HTML
    
      - HTML e texto alternativo
    
      - Enriched text
    
      - Enriched text e texto alternativo
    
      - Melhor formato do corpo
    
      - TNEF

5.  Clique em **Salvar**.

Após definir as configurações de formato de recuperação de mensagem POP3, é preciso reiniciar os serviços POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Use o Shell para definir o formato de recuperação de mensagens POP3 no nível de servidor

Este exemplo define a opção de formato de recuperação de mensagens para texto apenas usuários POP3 no servidor CAS01.

```powershell
Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly
```

Você pode escolher entre estas opções. Você pode especificar o valor para o parâmetro *MessageRetrievalMimeFormat* usando um valor numérico ou cadeia de caracteres de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato de mensagem</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Texto</p></td>
<td><p><code>0</code> ou <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e texto alternativo</p></td>
<td><p><code>2</code> ou <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> ou <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e texto alternativo</p></td>
<td><p><code>4</code> ou <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Melhor formato do corpo</p></td>
<td><p><code>5</code> ou <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Após definir as configurações de formato de recuperação de mensagem POP3, é preciso reiniciar os serviços POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar se você definiu com êxito as configurações de recuperação de mensagens POP3 em um servidor.

1.  Execute o seguinte comando no Shell.
    
    ```powershell
    Get-PopSettings | format-list
    ```

2.  Verifique se a configuração do *MessageRetrievalMimeFormat* está correta.

## Definir o formato de recuperação de mensagem de IMAP4 no nível do servidor

## Use o EAC para definir o formato de recuperação de mensagens IMAP4 no nível de servidor

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **IMAP4**.

4.  Em **Formato de Mensagem MIME**, escolha entre as seguintes configurações:
    
      - Texto
    
      - HTML
    
      - HTML e texto alternativo
    
      - Enriched text
    
      - Enriched text e texto alternativo
    
      - Melhor formato do corpo
    
      - TNEF

5.  Clique em **Salvar**.

Após definir as configurações de formato de recuperação de mensagem para IMAP4, é preciso reiniciar os serviços IMAP4 para que as configurações entrem em vigor. Para informações sobre como reiniciar os serviços IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Use o Shell para definir o formato de recuperação de mensagens IMAP4 no nível de servidor

Este exemplo define a opção de formato de recuperação de mensagens para texto apenas usuários IMAP4 no servidor CAS01.

```powershell
Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly
```

Você pode escolher entre estas opções. Você pode especificar o valor para o parâmetro *MessageRetrievalMimeFormat* usando um valor numérico ou cadeia de caracteres de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato de mensagem</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Texto</p></td>
<td><p><code>0</code> ou <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e texto alternativo</p></td>
<td><p><code>2</code> ou <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> ou <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e texto alternativo</p></td>
<td><p><code>4</code> ou <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Melhor formato do corpo</p></td>
<td><p><code>5</code> ou <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Após definir as configurações de formato de recuperação de mensagem para IMAP4, é preciso reiniciar os serviços IMAP4 para que as configurações entrem em vigor. Para informações sobre como reiniciar os serviços IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar se você definiu com êxito as configurações de recuperação de mensagens IMAP4 em um servidor.

1.  Execute o seguinte comando no Shell.
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  Verifique se a configuração do *MessageRetrievalMimeFormat* está correta.

## Definir o formato de recuperação de mensagem POP3 de um usuário

## Use o Shell para definir o formato de recuperação de mensagens POP3 para um usuário

Este exemplo define o formato de recuperação de mensagens como apenas texto para acessos POP3 para `USER01`.

```powershell
Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly
```

Você pode escolher entre estas opções. Você pode especificar o valor para o parâmetro *PopMessagesRetrievalMimeFormat* usando um valor numérico ou cadeia de caracteres de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato de mensagem</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Texto</p></td>
<td><p><code>0</code> ou <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e texto alternativo</p></td>
<td><p><code>2</code> ou <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> ou <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e texto alternativo</p></td>
<td><p><code>4</code> ou <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Melhor formato do corpo</p></td>
<td><p><code>5</code> ou <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Após definir as configurações de formato de recuperação de mensagem POP3, é preciso reiniciar os serviços POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar se você definiu com êxito as opções de formato da recuperação de mensagens POP3 para um usuário.

1.  Execute o seguinte comando no Shell.
    
    ```powershell
    Get-CAS Mailbox <identity> | format-list
    ```

2.  Verifique se o valor para *PopMessagesRetrievalMimeFormat* está correto.

## Definir o formato de recuperação de mensagem de IMAP4 para um usuário

## Use o Shell para definir o formato de recuperação de mensagens IMAP4 para um usuário

Este exemplo define o formato de recuperação de mensagens como apenas texto para acessos IMAP4 para `USER01`.

```powershell
Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly
```

Você pode especificar o valor para o parâmetro *ImapMessagesRetrievalMimeFormat* usando um valor numérico ou cadeia de caracteres de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato de mensagem</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Texto</p></td>
<td><p><code>0</code> ou <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e texto alternativo</p></td>
<td><p><code>2</code> ou <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> ou <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e texto alternativo</p></td>
<td><p><code>4</code> ou <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Melhor formato do corpo</p></td>
<td><p><code>5</code> ou <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Após definir as configurações de formato de recuperação de mensagem para IMAP4, é preciso reiniciar os serviços IMAP4 para que as configurações entrem em vigor. Para informações sobre como reiniciar os serviços IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar se você definiu com êxito as opções de formato da recuperação de mensagens IMAP4 para um usuário.

1.  Execute o seguinte comando no Shell.
    
    ```powershell
    Get-CAS Mailbox <identity> | format-list
    ```

2.  Verifique se o valor para *ImapMessagesRetrievalMimeFormat* está correto.

## Para mais informações

Após definir o formato de recuperação de mensagens para usuários IMAP4 e POP3, você também poderá:

[Habilitar ou desabilitar o acesso POP3 de um usuário](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Habilitar ou desabilitar o acesso de IMAP4 para um usuário](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[Configurar opções de calendário para o IMAP4](configure-calendar-options-for-imap4-exchange-2013-help.md)

[Configurar opções de calendário para POP3](configure-calendar-options-for-pop3-exchange-2013-help.md)

