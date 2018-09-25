---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518122
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**Tópico modificado em:** 2018-01-17_

**Resumo:**  sobre caixas de correio de arbitragem em Exchange 2013 e como recriá-las.

Exchange 2013 vem com cinco caixas de correio de sistema, conhecidas como *caixas de correio de arbitragem*. Caixas de correio de arbitragem são usadas para armazenar os diferentes tipos de dados de sistema e de gerenciamento de fluxo de trabalho aprovação de mensagens. O gráfico abaixo relaciona cada tipo de caixa de correio de arbitragem e as responsabilidades.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Caixa de correio de arbitragem nome</th>
<th>Nome para exibição</th>
<th>Recursos persistentes</th>
<th>Função</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Caixa de correio do Microsoft Exchange federação</p></td>
<td><p>{}</p></td>
<td><p>Esta caixa de correio armazena dados usados para manter a federação entre organizações diferentes do Exchange. Isso inclui Rights Management Services, sondas de monitoramento de fluxo de emails entre locais e respostas, notificações, arquivos on-line, gerenciamento de registros de mensagens e locais cruzados livre/ocupado informações.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Assistente de aprovação do Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Esta caixa de correio é provisionada para uso pela estrutura de aprovação do Exchange para destinatários solicitações de aprovação de grupo de moderação e automático.</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Migração do Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>Armazena dados de serviço de migração do Exchange usar ao mover caixas de correio em lotes.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>Caixa de correio de sistema de descoberta.</p>
<p>Provisionado para uso pelo recurso de descoberta eletrônica, que é usado pelo oficiais de conformidade para localizar mensagens que correspondam aos critérios de seleção especificada. Esta caixa de correio também é usada pela Unificação de mensagens para armazenar o console de Unificação de mensagens que estão participando de arquivos e outras informações.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>Isso é conhecido como uma caixa de correio da organização. Ele é usado para a criação de catálogos de endereços offline (OABs). A geração do OAB do balanceamento de carga em sua organização, incluindo entre locais separados geograficamente sites, você pode criar caixas de correio adicionais da organização.</p></td>
</tr>
</tbody>
</table>


Se você precisar recriar uma ou mais dessas caixas de correio de arbitragem, consulte as instruções que seguem.

## Você deve saber antes de começar

  - Tempo estimado para conclusão: 10 minutos por procedimento.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use Shell de Gerenciamento do Exchange para recriar uma caixa de correio de arbitragem

Use as instruções a seguir para recriar um tipo específico de caixa de correio de arbitragem.


> [!NOTE]
> Todas as etapas nas seções a seguir devem ser executadas no mesmo diretório onde você extraiu da mídia de instalação do Exchange.



## Recriar a caixa de correio de Federação do Microsoft Exchange

Para recriar a caixa de correio de arbitragem FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042:

1.  Se qualquer caixa de correio de arbitragem estiver ausente, execute o seguinte comando:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  Em Shell de Gerenciamento do Exchange, execute o seguinte:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"
    ```

## Recriar a caixa de correio do Microsoft Exchange aprovação Assistant

Para recriar a caixa de correio de arbitragem SystemMailbox {1f05a927-9350-4efe-a823-5529c2d64109}:

1.  Se qualquer caixa de correio de arbitragem estiver ausente, execute o seguinte comando:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  Em Shell de Gerenciamento do Exchange, execute o seguinte:
    
    ```powershell
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration
    ```

## Recriar a caixa de correio de migração do Microsoft Exchange

Para recriar a caixa de correio de arbitragem Migration.8f3e7716-2011-43e4-96b1-aba62d229136:

1.  Se qualquer caixa de correio de arbitragem estiver ausente, execute o seguinte comando:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  Em Shell de Gerenciamento do Exchange, execute o seguinte:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"
    ```

3.  No Shell de Gerenciamento do Exchange, defina as capacidades persistentes (msExchCapabilityIdentifiers) executando o seguinte comando:
    
    ```powershell
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force
    ```

## Recriar a caixa de correio do sistema de descoberta do Microsoft Exchange

Para recriar a caixa de correio de arbitragem SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}:

1.  Execute o comando a seguir:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

## Recriar a caixa de correio de organização do Microsoft Exchange para OABs

Para recriar a caixa de correio de arbitragem SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}:

1.  Se qualquer caixa de correio de arbitragem estiver ausente, execute o seguinte comando:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  Em Shell de Gerenciamento do Exchange, execute o seguinte:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"
    ```

3.  No Shell de Gerenciamento do Exchange, defina as capacidades persistentes (msExchCapabilityIdentifiers) executando o seguinte comando:
    
    ```powershell
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force
    ```

Quando terminar, se você executar o comando `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` , você verá que 46, 47 e 51 estão ausentes. Execute o seguinte comando para adicionar todos os recursos de volta:

```powershell
    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}
```

## Como saber se funcionou?

Para verificar se você criou com êxito novamente a caixa de correio de arbitragem, use o cmdlet **Get-Mailbox** com a opção *Arbitration* para recuperar caixas de correio do sistema.

```powershell
    Get-Mailbox -Arbitration | Format-Table Name, DisplayName
```

Exiba os resultados do comando para verificar que essa caixa de correio do sistema apropriado, seja pelo nome ou o nome de exibição da tabela acima, foi criada novamente.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


