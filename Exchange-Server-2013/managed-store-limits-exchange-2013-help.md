---
title: 'Gerenciados os limites de armazenamento: Exchange 2013 Help'
TOCTitle: Gerenciados os limites de armazenamento
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226020
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciados os limites de armazenamento

 

_**Tópico modificado em:**2016-09-15_

**Resumo:** limites de conexão sobre o repositório gerenciado e como configurá-los.

No MicrosoftExchange Server 2013, conexão e limites de uso tiverem sido colocados no repositório de Managed Exchange para impedir que um único aplicativo ou um único usuário use todas as conexões disponíveis para o repositório gerenciado. Se um único usuário ou aplicativo tem permissão para usar todas as conexões, outros usuários ou aplicativos não podem ser capazes de acessar o repositório gerenciado, que pode resultar na inatividade do sistema.


> [!TIP]
> Para todas as conexões feitas por contas que possuem privilégios administrativos, os limites máximos de sessão aumentaram para 64.000.



## Terminologia

Conhecimento dos termos a seguir ajudarão você a compreender os tipos de conexões referenciados neste tópico.

  - Sessões  
    Sessões representam as conexões usadas pelos serviços e aplicativos de cliente, como o Microsoft Outlook, para conexão com o repositório gerenciado. Serviços e clientes podem ter várias sessões em um momento específico. Os termos de *conexões* e *sessões* podem ser usados forma intercambiável.

<!-- end list -->

  - Threads  
    Representam de threads em execução simultânea solicitações para o repositório gerenciado. Por exemplo, se um usuário abre uma pasta no Outlook, Outlook executa uma solicitação para o repositório gerenciado em nome do usuário. Que a execução da solicitação é um único segmento.
    
    No Exchange Server 2013, não existem mais limites de threads com base no tipo de cliente. Em vez disso, para todos os clientes, o número máximo de threads **por banco de dados de caixa de correio** é de 50. A exceção é o serviço de disponibilidade, que tem um limite máximo de 16 por usuário.

Voltar ao início

## Limites de sessão

A tabela a seguir lista os tipos de conexões de cliente para o repositório gerenciado e os limites com base em dessas conexões. Se você deseja modificar os limites de sessão, consulte "Configurar limites de sessão" imediatamente a tabela a seguir.

Versões anteriores do Exchange definir limites no número de conexões para o repositório de gerenciadas com base no número de conexões por servidor. No Exchange 2013, limites de sessão são baseados em conexões por banco de dados de caixa de correio.

Os tipos de limites de conexão no Exchange 2013 são:

  - **Sessões máxima por processo**   Especifica o número máximo de sessões que um serviço Exchange pode ter abrir ao mesmo tempo em um banco de dados de caixa de correio.

  - **Sessões de usuário máxima por processo**   Especifica o número máximo de sessões para um determinado protocolo de um único usuário.

A seção a seguir, "Configurar limites de sessão", descreve como modificar esses limites.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de cliente</th>
<th> </th>
<th>Sessões máxima por banco de dados de caixa de correio</th>
<th>Número de sessões por banco de dados de caixa de correio de usuário padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Serviço de Disponibilidade</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Indexação de conteúdo</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Serviços Web do Exchange</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>MAPI na camada intermediária (MoMT)</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants: eventos</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants: atingiu o tempo</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Chamada de procedimento remoto do MSExchange</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft OfficeOutlook Web App</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 e IMAP4</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Transporte</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Unificação de Mensagens</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Outras pessoas</p></td>
<td> </td>
<td><p>Não aplicável</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## Configurar limites de sessão

Você pode modificar os limites de sessão padrão.


> [!TIP]
> Se você deseja modificar os limites de sessão, você precisará modificá-los em todos os servidores de caixa de correio em quaisquer grupos de disponibilidade de banco de dados (DAGs). Se você não fizer as mesmas alterações em todos os servidores, os resultados serão inconsistentes. Para aumentar o limite de sessão no servidor de acesso para cliente, o valor de <CODE>RCAMaxConcurrency</CODE> deve ser aumentado na diretiva de limitação. Para obter mais informações, consulte <A href="https://technet.microsoft.com/pt-br/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</A>.




> [!WARNING]
> A edição incorreta do Registro pode causar problemas graves que podem exigir a reinstalação do sistema operacional. Talvez não seja possível resolver os problemas resultantes da edição incorreta do Registro. Antes de editar o Registro, faça backup de todos os dados importantes.



1.  Inicie o Editor do Registro (regedit).

2.  Navegue até a seguinte subchave do registro:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**.

3.  Clique com o botão **ParametersSystem**, aponte para **novo** e, em seguida, clique em **valor DWORD (32 bits).**
    
    O novo valor é criado no painel de resultados.

4.  Renomear a chave como um dos valores a seguir e pressione Enter:
    
      - **Número máximo de sessões permitido por usuário**   Esse limite Especifica o máximo permitido de sessões por usuário.
    
      - **Máximo de serviço permitido de sessões por usuário**   Esse limite Especifica que as sessões de máximo serviço permitidos por usuário.
    
      - **Sessões máxima Exchange permitidos por serviço**   Esse limite Especifica que o máximo permitido de sessões de Exchange por serviço. O valor padrão é 10.000.

5.  Com o botão direito na chave recém-criada e, em seguida, clique em **Modificar**.

6.  Na caixa**dados** do **valor**, digite o número de objetos para o qual você deseja limitar essa entrada e clique em **OK**. Use a tabela anterior para exibir as configurações padrão.

Voltar ao início

## Limites de Item aberto

Limites de abrir item são limites colocados em que o número de itens que podem ser abertos por uma única caixa de correio em uma única sessão. No entanto, um usuário pode ter várias sessões abertas simultaneamente. Por exemplo, se um usuário tiver duas sessões abertas, o usuário pode abrir pastas de 1.000.

Se você deseja modificar esses limites, consulte "Configurar Open limites Item" imediatamente a tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de item</th>
<th>Tipo de objeto do registro</th>
<th>Max abertos por sessão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Modo de exibição ACL</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Modo de exibição do anexo</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Pasta</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Modo de exibição de pasta</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Fluxo de destino de FX</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Fluxo de origem de FX</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Mensagem</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>Modo de exibição de mensagem</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Notificação</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>Modo de exibição de regra</p></td>
<td><p>objtRulesView</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Stream</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## Configurar limites de Item aberto

Você pode limitar o número máximo de recursos que um cliente MAPI pode usar simultaneamente.


> [!TIP]
> Se você deseja modificar os limites de item aberto, será necessário modificá-los em todos os servidores de caixa de correio em qualquer DAGs e matrizes de acesso do cliente. Se você não fizer as mesmas alterações em todos os servidores, os resultados serão inconsistentes.




> [!WARNING]
> A edição incorreta do Registro pode causar problemas graves que podem exigir a reinstalação do sistema operacional. Talvez não seja possível resolver os problemas resultantes da edição incorreta do Registro. Antes de editar o Registro, faça backup de todos os dados importantes.



1.  Inicie o Editor do Registro (regedit).

2.  Navegue até a seguinte subchave do registro:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  Clique com o botão **ParametersSystem**, aponte para **novo** e clique em **chave**.
    
    Uma nova chave é criada na árvore de console.

4.  Renomear a chave **MaxObjsPerMapiSession** e pressione Enter.

5.  Clique com o botão **MaxObjsPerMapiSession**, aponte para **novo** e clique em **valor DWORD (32 bits)**.
    
    O novo valor é criado no painel de resultados.

6.  Renomear a chave para *\<Object\_type\>*, onde *\<Object\_type\>* é o nome do tipo de objeto do registro que você está modificando. Por exemplo, para modificar o número de mensagens que podem ser abertos, use *objtMessage*. Pressione Enter.

7.  Com o botão direito na chave recém-criada e, em seguida, clique em **Modificar**.

8.  Na caixa **dados do valor**, digite o número de objetos que você deseja limitar a essa entrada para e clique em **OK**. Por exemplo, digite **350** para aumentar o valor do objeto.

9.  Reinicie o serviço Microsoft Exchange Information Store.

Voltar ao início

## Limites de tamanho do item

Limites de tamanho do item são os limites colocados em itens dentro da caixa de correio do usuário. Eles são configuráveis usando os parâmetros *MaxSendSize* e *MaxReceiveSize* no cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) .


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de item</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensagem (salva)</p></td>
<td><p>Tamanho máximo de SendLimit, ReceiveLimit</p></td>
</tr>
<tr class="even">
<td><p>Mensagem (enviada)</p></td>
<td><p>Tamanho máximo do SendLimit</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


Voltar ao início

