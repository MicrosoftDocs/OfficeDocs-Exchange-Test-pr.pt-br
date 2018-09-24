---
title: 'Colocar todas as caixas de correio em espera: Exchange 2013 Help'
TOCTitle: Colocar todas as caixas de correio em espera
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486255
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Colocar todas as caixas de correio em espera

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-01-18_


> [!NOTE]
> Adiamos o prazo de 1 de julho de 2017 para criar novos Bloqueios In-loco no Exchange Online (em planos autônomos do Office 365 e do Exchange Online). No entanto, mais para o fim deste ano ou no início do próximo ano, não será possível criar novos Bloqueios In-loco no Exchange Online. Como alternativa ao uso de Bloqueios In-loco, use <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de descoberta eletrônica</A> ou <A href="https://go.microsoft.com/fwlink/?linkid=827811">políticas de retenção</A> no Centro de Conformidade e Segurança do Office 365. Após encerrarmos os novos Bloqueios In-loco, você ainda conseguirá modificar os existentes, e a criação de novos bloqueios em implantações híbridas no Exchange Server 2013 e no Exchange ainda terão suporte. Além disso, você poderá posicionar caixas de entrada em Retenção de Litígio.



Sua organização pode exigir de todos os dados de correio seja preservado por um período específico. Você pode usar litígio ou bloqueio In-loco para atender a esse requisito. Depois de colocar uma caixa de correio em retenção de litígio ou bloqueio In-loco, itens de caixa de correio que serão modificados ou que são excluídos permanentemente são preservados na pasta itens recuperáveis. Para obter mais informações, consulte [Retenção local e Retenção de litígio](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-and-litigation-holds).

Antes de colocar todas as caixas de correio de uma organização em Retenção de litígio ou Bloqueio In-loco, considere o seguinte:

  - Quando você realiza as caixas de correio em espera, o conteúdo no correio de arquivo morto do usuário (se ele estiver habilitado) também é colocado em espera.

  - Colocar todas as caixas de correio em uma organização em espera pode afetar significativamente o tamanho das caixas postais. Em uma implantação de Exchange Server 2013, planeje armazenamento adequado atender aos requisitos de preservação da sua organização. Em Exchange Online, [limites de armazenamento de caixa de correio](https://go.microsoft.com/fwlink/?linkid=403645) para seus usuários dependem da licença de inscrição do usuário.

  - Preservando dados de caixa de correio por um longo período resultará em crescimento da pasta itens recuperáveis na caixa de correio principal do usuário e a caixa de correio de arquivo morto. A pasta itens recuperáveis tem seu próprio limite de armazenamento, portanto não são considerados itens na pasta rumo ao limite de armazenamento de caixa de correio. Em Exchange Server 2013 e Exchange Online, o limite de armazenamento padrão da pasta itens recuperáveis é 30 GB.
    
      - Em Exchange Online, a cota da pasta itens recuperáveis automaticamente é aumentada para 100 GB quando você realiza uma caixa de correio em espera.
    
      - Exchange Server 2013, recomendamos que você deseja monitorar periodicamente o tamanho dessa pasta para garantir que ele não atinge o limite. Para mais informações, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

## Escolhendo entre o bloqueio de litígio e bloqueio In-loco

Aqui estão alguns fatores a serem considerados ao decidir o recurso de espera, você deve usar para colocar todas as caixas de correio em sua organização em espera.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Você deseja...</th>
<th>Usar Retenção de Litígio</th>
<th>Usar Bloqueio In-loco</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usar o EAC</p></td>
<td><p>Sim</p>
<p>Para a definição de litígio, EAT é mais adequado para a rápida ações únicas em algumas caixas de correio. É recomendável usar o Shell para configuração de litígio para todos os usuários em sua organização.</p></td>
<td><p>Sim</p>
<p>No entanto, não é possível selecionar mais de 500 caixas de correio de origem no EAC.</p></td>
</tr>
<tr class="even">
<td><p>Usar o Shell</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Colocar mais de 10.000 caixas de correio em espera</p></td>
<td><p>Sim</p>
<p>Litígio é uma propriedade de correio. Você pode colocar todas as caixas de correio em uma organização em espera usando o cmdlet <strong>Set-Mailbox</strong> .</p></td>
<td><p>Sim; Use vários In-Place Holds</p>
<p>Você pode usar grupos de distribuição para especificar um máximo de 10.000 caixas de correio em um único In-Place Hold. Para colocar mais caixas de correio em espera, você deve criar In-Place Holds adicionais. Isso resultará em sobrecarga de gerenciamento adicionais. Usando a retenção de litígio colocação grandes números de caixas de correio em espera é mais simples.</p></td>
</tr>
<tr class="even">
<td><p>Colocar várias caixas de correio diferentes em espera por diferentes períodos.</p></td>
<td><p>Sim</p>
<p>A Retenção de Litígio é uma propriedade de caixa de correio. Você pode colocar cada caixa de correio (ou conjuntos de caixas de correio) em espera por um período diferente.</p>
<p>Consulte a seção informações adicionais para exemplos de como usar propriedades de destinatário em um filtro, assim é possível colocar um litígio em um subconjunto de caixas de correio.</p></td>
<td><p>Sim</p>
<p>Se estiver colocando retenções individuais em milhares de caixas de correio, recomendamos o uso da Retenção de Litígio. Se estiver criando retenções para eventos especificos que envolvem vários usuários, use um único Bloqueio In-loco para o grupo de usuários.</p>
<p>Ele não tem recomendado para criar retenções de locais separados para cada caixa de correio, pois isso criará muitas consultas de bloqueio In-loco que serão mais difíceis de gerenciar que retém litígios. Um grande número de objetos de bloqueio In-loco também pode resultar em desempenho lento no EAC durante a atualização, criando ou modificando objetos de espera.</p></td>
</tr>
<tr class="odd">
<td><p>Colocar automaticamente novas caixas de correio em espera</p></td>
<td><p>Não</p>
<p>Você precisa colocar uma nova caixa de correio em retenção de litígio, após sua criação. Você pode agendar o comando ou script para executar a mesma frequência necessários para alcançar o mesmo efeito.</p></td>
<td><p>Não</p>
<p>Você precisa adicionar uma nova caixa de correio para um bloqueio In-loco, mesmo se você especificou um grupo de distribuição quando você criou o bloqueio In-loco. Você também pode agendar o comando ou script para executar a mesma frequência necessários para alcançar o mesmo efeito. É recomendável verificar se a verificação de script se um bloqueio In-loco existente já tiver atingido o limite de 10.000 caixas de correio e crie um novo In-Place Hold se necessário.</p></td>
</tr>
<tr class="even">
<td><p>Colocar todas as pastas públicas em espera</p></td>
<td><p>Não</p>
<p>Exchange Online, colocar um litígio em caixas de correio de pasta pública não é suportado. Você tem que usar In-Place Hold.</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


## Colocar todas as caixas de correio em Retenção de Litígio

É possível rapidez e facilidade colocar todas as caixas em espera indefinidamente ou por um período especificado usando o Shell. Esse comando coloca todas as caixas de correio em espera por 2555 dias (aproximadamente sete anos).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

O exemplo usa o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) e um filtro de destinatário para recuperar todas as caixas de correio do usuário na organização e, em seguida canaliza toda a lista de caixas de correio para o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) para habilitar a retenção de litígio e especificar uma duração de espera. Para mais informações, consulte [Colocar uma caixa de correio em Retenção de Litígio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md).

## Colocar todas as caixas de correio em Bloqueio In-loco

Você pode usar o EAC para selecionar até 500 caixas de correio e colocá-las em espera. Para obter detalhes, consulte [Criar ou remover um bloqueio In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/create-or-remove-in-place-holds).


> [!TIP]
> Para colocar mais de 500 usuários em bloqueio In-loco, use o Shell. Consulte <A href="https://technet.microsoft.com/pt-br/library/dd298064(v=exchg.150)">New-MailboxSearch</A>.



## Mais informações

  - Quando você coloca todas as caixas de correio em sua organização em espera, somente as caixas de correio existentes ao tempo que você executar o comando são colocadas em retenção. Se você criar novas caixas de correio mais tarde, executadas o comando novamente para colocá-los em espera. Se você cria frequentemente novas caixas de correio, você pode executar o comando como uma tarefa agendada frequentemente conforme necessário.

  - Colocação de caixas de correio em espera preserva os dados, evitando a exclusão antes que o período especificado e salvando a versão original de uma mensagem antes que ele seja modificado. Ele não excluir mensagens automaticamente após o período especificado. Combine litígio ou bloqueio In-loco com uma política de retenção, que pode excluir mensagens automaticamente após o período especificado, para atender aos requisitos de retenção de email da sua organização. Consulte [Marcas e políticas de retenção](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies) para obter detalhes.

  - O comando PowerShell usado neste tópico para colocar um litígio em todas as caixas de correio utiliza um filtro de destinatário que retorna todas as caixas de correio do usuário. Você pode usar outras propriedades de destinatário para retornar uma lista de caixas de correio específicas que você pode direcionar ao cmdlet **Set-Mailbox** para colocar um litígio nessas caixas de correio.
    
    Eis alguns exemplos de usar os cmdlets **Get-Mailbox** e **Get-Recipient** para obter um subconjunto de caixas de correio com base em propriedades de usuário ou de caixa de correio comuns. Esses exemplos supõem que as propriedades de caixa de correio relevantes (como *CustomAttributeN* ou *Department*) foram preenchidas.
    
```
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
```
```    
    ```powershell
Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
```
```   
``` 
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
```
```    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
```
```    
    ```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
```
```

Você pode usar outras propriedades de caixa de correio em um filtro para incluir ou excluir caixas de correio. Para saber mais, confira [Propriedades filtráveis para o parâmetro -Filter](https://technet.microsoft.com/pt-br/library/bb738155\(v=exchg.150\)).

