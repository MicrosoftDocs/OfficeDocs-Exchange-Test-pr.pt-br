---
title: 'Gerenciar regras de fluxo de emails: Exchange Online Help'
TOCTitle: Gerenciar regras de fluxo de emails
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50486873
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gerenciar regras de fluxo de emails

 

_**Aplica-se a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Você pode usar as regras de fluxo de emails, também conhecidas como regras de transporte, para procurar condições específicas em mensagens que passem pela sua organização e tomar as devidas providências. Este tópico mostra como criar, copiar, ajustar a ordem, habilitar ou desabilitar, excluir, ou importar ou exportar regras, e como monitorar o uso de regras.


> [!TIP]
> Para garantir que suas regras funcionem da maneira esperada, teste completamente cada regra e as interações entre as regras.



Interessado em cenários onde estes procedimentos são usados? Veja os tópicos a seguir:

  - [Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Cenários comuns de bloqueio de anexo](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Cenários comuns de aprovação de mensagem](common-message-approval-scenarios-exchange-2013-help.md)

  - [Usar regras de fluxo de email para que mensagens poderá ignorar desorganização](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Práticas recomendadas para configuração das regras de fluxo de email](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\))

  - [Usar regras de transporte para configurar a filtragem de email em massa](https://technet.microsoft.com/pt-br/library/dn720438\(v=exchg.150\))

  - [Definir regras para criptografar ou descriptografar mensagens](https://go.microsoft.com/fwlink/p/?linkid=402846).

  - [Criar listas de remetentes bloqueados ou remetente seguro em toda a organização no Office 365](https://technet.microsoft.com/pt-br/library/dn198251\(v=exchg.150\))

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Regras de transporte" em [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) (Exchange Server), ou em [Permissões de recursos no Exchange Online](https://technet.microsoft.com/pt-br/library/jj200673\(v=exchg.150\)).

  - Quando uma regra é listada como **versão 14**, isso significa que ela se baseia em um formato de regra de fluxo de emails do Exchange Server 2010. Todas as opções estão disponíveis para essas regras.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma regra de fluxo de emails

Você pode criar uma regra de fluxo de emails configurando uma política de Prevenção de Perda de Dados (DLP), criando uma nova regra ou copiando uma regra. Você pode usar o Centro de administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange.


> [!TIP]
> Após criar ou alterar uma regra de fluxo de emails, pode levar até 30 minutos para a regra nova ou atualizada ser aplicada ao email.



## Usar uma política de DLP para criar regras de fluxo de emails

Cada política de DLP é uma coleção de regras de fluxo de emails. Após criar a política de DLP, você pode ajustar as regras usando os procedimentos a seguir.

1.  Criar uma política de DLP Para obter instruções, veja:
    
      - [Procedimentos de DLP do Exchange Server 2013](dlp-procedures-exchange-2013-help.md)
    
      - [Procedimentos de DLP do Exchange Online](dlp-procedures-exchange-2013-help.md)

2.  Modifique as regras de fluxo de emails criadas pela política de DLP. Confira Exibir ou modificar uma regra de fluxo de emails.

## Usar o EAC para criar uma regra de fluxo de emails

O EAC permite que você crie regras de fluxo de emails usando um modelo, copiando uma regra existente ou começando do zero.

1.  Acesse **Fluxo de emails** \> **Regras**.

2.  Crie a regra usando uma das seguintes opções:
    
      - Para criar uma regra a partir de um modelo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione um modelo.
    
      - Para copiar uma regra, selecione a regra e, em seguida, selecione **Copiar**![Ícone Copiar](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Ícone Copiar").
    
      - Para criar uma nova regra a partir do zero, selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e, em seguida, **Criar uma nova regra**.

3.  Na caixa de diálogo **Nova regra**, nomeie a regra e depois selecione as condições e ações para ela:
    
    1.  Em **Aplicar esta regra se…**, selecione a condição desejada na lista de condições disponíveis.
        
          - Algumas condições exigem que você especifique valores. Por exemplo, se você selecionar a condição **O remetente é…**, deverá especificar um endereço de remetente. Se você estiver adicionando uma palavra ou frase, não são permitidos espaços à direita.
        
          - Se a condição desejada não estiver listada ou se você precisar adicionar exceções, selecione **Mais opções**. As condições e exceções adicionais serão listadas.
        
          - Se você não quiser especificar uma condição quiser que essa regra seja aplicada a cada mensagem da sua organização, selecione a condição **\[Aplicar a todas as mensagens\]**.
    
    2.  Em **Faça o seguinte…**, selecione a ação que a regra deverá executar nas mensagens que correspondam aos critérios a partir da lista de ações disponíveis.
        
          - Algumas das ações exigirão que você especifique valores. Por exemplo, se você selecionar a condição **Encaminhar a mensagem para aprovação a…**, precisará selecionar um destinatário na sua organização.
        
          - Se a condição que você deseja não estiver listada, selecione **Mais opções**. As condições adicionais serão listadas.
    
    3.  Especifique como os dados de correspondência da regra serão exibidos nos [relatórios de Prevenção de Perda de Dados (DLP)](https://go.microsoft.com/fwlink/p/?linkid=402768) e nos [relatórios de regras de transporte](https://go.microsoft.com/fwlink/p/?linkid=402769).
        
          - Em **Auditar esta regra com nível de severidade**, selecione um nível para especificar o nível de severidade aplicado a esta regra. Os relatórios de atividades do Office 365 para o grupo de regras de fluxo de emails regulam as correspondências por nível de severidade. O nível de severidade é apenas um filtro para facilitar o uso de relatórios. O nível de severidade não afeta a prioridade em que a regra é processada.
            

            > [!TIP]
            > Se você desmarcar a caixa de seleção <STRONG>Auditar esta regra com nível de severidade</STRONG>, as correspondências de regra não serão exibidas nos relatórios de regras.

    
    4.  Defina o modo para a regra. Você pode usar um dos dois modos de teste para testar a regra sem causar impacto no fluxo de email. Em ambos os modos de teste, quando as condições são atendidas, uma entrada é adicionada ao rastreamento de mensagem.
        
          - **Impor**   Isso ativará a regra e iniciará o processamento de mensagens imediatamente. Todas as ações da regra serão realizadas..
        
          - **Testar com Dicas de Política**   Isso ativará a regra e qualquer ação de Dicas de Política (**Notificar o remetente com uma Dica de Política**) será enviada, mas nenhuma ação relacionada à entrega de mensagens será executada. A Prevenção de Perda de Dados (DLP) é exigida para usar esse modo. Para saber mais, consulte [Dicas de política](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
        
          - **Testar sem Dicas de Política**   Apenas a ação Gerar relatório de incidente será imposta. Nenhuma ação relacionada à entrega de mensagens será realizada.

4.  Se estiver satisfeito com a regra, vá para a etapa 5. Se quiser adicionar mais condições, ações, especificar exceções ou configurar propriedades adicionais, clique em **Mais opções**. Depois de você clicar em **Mais opções**, preencha os seguintes campos para criar sua regra:
    
    1.  Para adicionar condições, clique em **Adicionar Condição**. Se você tiver mais de uma condição, poderá remover qualquer uma delas clicando em **Remover X** ao lado dela. Observe que há uma variedade maior de condições disponíveis quando você clica em **Mais opções**.
    
    2.  Para adicionar mais ações, clique em **Adicionar ação**. Se você tiver mais de uma ação, poderá remover qualquer uma delas clicando em **Remover X** ao lado dela. Observe que há uma variedade maior de ações disponíveis quando você clica em **Mais opções**.
    
    3.  Para especificar exceções, clique em **Adicionar exceção** e selecione as exceções usando a lista suspensa **Exceto se...** Você pode remover todas as exceções da regra clicando em **Remover X** ao lado dela.
    
    4.  Se quiser aplicar essa regra após uma determinada data, clique em **Ativar esta regra na seguinte data:** e especifique uma data. Observe que a regra ainda será habilitada antes dessa data, mas não será processada.
        
        Da mesma forma, o processamento da regra poderá ser interrompido em uma determinada data. Para isso, clique em **Desativar esta regra na seguinte data:** e especifique uma data. Observe que a regra permanecerá habilitada, mas não será processada.
    
    5.  Você pode optar por evitar a aplicação de regras adicionais quando essa regra processar uma mensagem. Para isso, clique em **Parar de processar mais regras**. Se você selecionar esta opção e uma mensagem for processada por essa regra, nenhuma regra subsequente será processada para essa mensagem.
    
    6.  Você pode especificar como a mensagem deveria ser tratada se o processamento de regra não puder ser concluído. Por padrão, a regra será ignorada e a mensagem será processada regularmente, mas você pode escolher reenviar a mensagem para processamento. Para tanto, marque a caixa de seleção **Adiar a mensagem se o processamento de regra não for concluído**.
    
    7.  Se sua regra analisa o endereço do remetente, ela examinará apenas os cabeçalhos da mensagem por padrão. Entretanto, você pode configurar sua regra para também examinar o envelope de mensagem SMTP. Para especificar o que foi examinado, clique em um dos seguintes valores de **Corresponder endereço do remetente na mensagem**:
        
          - **Cabeçalho**   Apenas os cabeçalhos de mensagem serão examinados.
        
          - **Envelope**   Apenas o envelope de mensagem SMTP será examinado.
        
          - **Cabeçalho ou envelope**   Ambos o cabeçalho e o envelope de mensagem SMTP será examinado.
    
    8.  Você pode adicionar comentários para esta regra na caixa **Comentários** .

5.  Clique em **Salvar** para concluir a criação da regra.

## Usar o Shell de Gerenciamento do Exchange para criar uma regra de fluxo de emails

Este exemplo usa o cmdlet [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)) para criar uma nova regra de fluxo de emails que precede "`External message to Sales DG:`" para as mensagens enviadas de fora da organização para o grupo de distribuição do Departamento de Vendas.

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

Os parâmetros e a ação da regra usados no procedimento acima são apenas para fins ilustrativos. Revise todas as condições e ações disponíveis da regra de fluxo de emails para determinar quais atendem a seus requisitos.

## Como saber se funcionou?

Para verificar se uma nova regra de fluxo de emails foi criada com êxito, faça o seguinte:

  - No EAC, verifique se a nova regra de fluxo de emails criada aparece na lista de **Regras**.

  - No Shell de Gerenciamento do Exchange, verifique se você criou a nova regra de fluxo de emails com êxito executando este comando (o exemplo a seguir verifica a regra criada no exemplo de Shell de Gerenciamento do Exchange, acima):
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## Exibir ou modificar uma regra de fluxo de emails


> [!TIP]
> Após criar ou alterar uma regra de fluxo de emails, pode levar até 30 minutos para a regra nova ou atualizada ser aplicada ao email.



## Usar o EAC para exibir ou modificar uma regra de fluxo de emails

1.  No EAC, vá para **Fluxo de emails** \> **Regras**.

2.  Quando você selecionar uma regra na lista, as condições, ações, exceções e propriedades de seleção dessa regra serão exibidas no painel de detalhes. Para exibir todas as propriedades de uma regra específica, clique duas vezes nela. Isso abre a janela do editor de regras, na qual você pode fazer alterações na regra. Para obter mais informações sobre propriedades de regra, consulte a seção Usar o EAC para criar uma regra de fluxo de emails anteriormente neste tópico.

## Usar o Shell de Gerenciamento do Exchange para exibir ou modificar uma regra de fluxo de emails

O seguinte exemplo apresenta uma lista de todas as regras configuradas na sua organização:

    Get-TransportRule

Para exibir as propriedades de uma regra de fluxo de emails específica, forneça o nome da regra ou seu respectivo GUID. Isso normalmente ajuda a canalizar o resultado para o cmdlet **Format-List** para formatar as propriedades. O exemplo a seguir retorna todas as propriedades da regra de fluxo de emails chamada **O remetente é um membro de Marketing**:

    Get-TransportRule "Sender is a member of marketing" | Format-List

Para modificar as propriedades de uma regra existente, use o cmdlet [Set-TransportRule](https://technet.microsoft.com/pt-br/library/bb123534\(v=exchg.150\)). Este cmdlet permite alterar qualquer propriedade, condição, ação ou exceção associada a uma regra. O seguinte exemplo adiciona uma exceção à regra "O remetente é membro do marketing" para que ela não se aplique a mensagens enviadas pelo usuário Kelly Rollin:

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## Como saber se funcionou?

Para verificar se modificou uma regra de fluxo de emails com êxito, faça o seguinte:

  - Na lista de regras no EAC, clique na regra modificada na lista **Regras** e exiba o painel de detalhes.

  - No Shell de Gerenciamento do Exchange, verifique se você modificou a regra de fluxo de emails com sucesso executando este comando para listar as propriedades modificadas juntamente com o nome da regra (o exemplo a seguir verifica a regra modificada no exemplo de Shell de Gerenciamento do Exchange acima):
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## Propriedades de regras de fluxo de email

Você também pode usar o cmdlet Set-TransportRule para modificar as regras de transporte existentes na sua organização. Abaixo temos uma lista de propriedades não disponíveis no EAC que você pode alterar. Para saber mais sobre como usar o cmdlet Set-TransportRule para fazer alterações, confira [Set-TransportRule](https://technet.microsoft.com/pt-br/library/bb123534\(v=exchg.150\))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome de Condição no EAC</th>
<th>Nome da condição no Shell de Gerenciamento do Exchange</th>
<th>Propriedades</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Parar de processar regras</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>Permite a você parar de processar mais regras</p></td>
</tr>
<tr class="even">
<td><p><strong>Correspondência de cabeçalho/envelope</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>Não aplicável</p></td>
<td><p>Permite que você examine o envelope da mensagem SMTP para garantir que o cabeçalho e o envelope são correspondentes</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>Severidade da auditoria</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Permite que você selecione um nível de severidade de auditoria</p></td>
</tr>
<tr class="even">
<td><p><strong>Modos de regra</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Permite que você defina o modo da regra</p></td>
</tr>
</tbody>
</table>


## Definir a prioridade de uma regra de fluxo de emails

A regra no topo da lista é processada primeiro. Essa regra tem uma **Prioridade** de 0.

## Usar o EAC para definir a prioridade de uma regra

1.  No EAC, vá para **Fluxo de emails** \> **Regras**. Isso exibe as regras na ordem em que são processadas.

2.  Selecione a regra e use as setas para mover a regra para baixo ou para cima na lista.

## Usar o Shell de Gerenciamento do Exchange para definir a prioridade de uma regra

O exemplo a seguir define a prioridade de "Remetente é um membro de marketing" como 2:

    Set-TransportRule "Sender is a member of marketing" priority "2"

## Como saber se funcionou?

Para verificar se modificou uma regra de fluxo de emails com êxito, faça o seguinte:

  - Na lista de regras no EAC, examine a ordem das regras.

  - No Shell de Gerenciamento do Exchange, verifique a prioridade das regras (o exemplo a seguir verifica a regra modificada no exemplo de Shell de Gerenciamento do Exchange acima):
    
        Get-TransportRule * | Format-List Name,Priority

## Habilitar ou desabilitar uma regra de fluxo de emails

As regras são habilitadas no momento em que você as cria. É possível desabilitar uma regra de fluxo de emails.

## Usar o EAC para habilitar ou desabilitar uma regra de fluxo de emails

1.  No EAC, vá para **Fluxo de emails** \> **Regras**.

2.  Para desabilitar uma regra, desmarque a caixa de seleção ao lado do nome dela.

3.  Para habilitar uma regra desabilitada, marque a caixa de seleção ao lado do nome dela.

## Usar o Shell de Gerenciamento do Exchange para habilitar ou desabilitar uma regra de fluxo de emails

O exemplo a seguir desabilita a regra de fluxo de emails "O remetente é um membro de marketing":

    Disable-TransportRule "Sender is a member of marketing"

O exemplo a seguir habilita a regra de fluxo de emails "O remetente é um membro de marketing":

    Enable-TransportRule "Sender is a member of marketing"

## Como saber se funcionou?

Para verificar se houve êxito ao habilitar ou desabilitar uma regra de fluxo de emails, faça o seguinte:

  - No EAC, exiba a lista das regras na lista de **Regras** e verifique o status da caixa de seleção na coluna **ATIVADA**.

  - No Shell de Gerenciamento do Exchange, execute o seguinte comando para retornar uma lista de todas as regras de sua organização, incluindo seu status:
    
        Get-TransportRule | Format-Table Name,State

## Remover uma regra de fluxo de emails

## Usar o EAC para remover uma regra de fluxo de emails

1.  No EAC, vá para **Fluxo de emails** \> **Regras**.

2.  Selecione a regra que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Usar o Shell de Gerenciamento do Exchange para remover uma regra de fluxo de emails

O exemplo a seguir remove a regra de fluxo de emails "O remetente é um membro de marketing":

    Remove-TransportRule "Sender is a member of marketing"

## Como saber se funcionou?

Para verificar se houve êxito ao remover uma regra de fluxo de emails, faça o seguinte:

  - No EAC, verifique as regras na lista de **Regras** e confirme se a regra removida não é mais exibida.

  - No Shell de Gerenciamento do Exchange, execute o seguinte comando e verifique se a regra removida não aparece mais:
    
        Get-TransportRule

## Monitorar o uso de regras

Se você estiver usando o Exchange Online ou o Proteção do Exchange Online, você pode verificar o número de vezes que a regra é correspondida usando um relatório de regras. Para ser incluída nos relatórios, uma regra deve ter a caixa de seleção **Auditar esta regra com nível de severidade** marcada. Você pode analisar um relatório online ou baixar uma versão do Excel dos relatórios de proteção de email.


> [!TIP]
> Embora a maioria dos dados esteja no relatório dentro de 24 horas, alguns dados podem demorar até 5 dias para aparecer.



## Use o centro de administração do Office 365 para gerar um relatório de regras

1.  No centro de administração do Office 365, selecione **Relatórios**.

2.  Na seção **Regras**, selecione **Principais correspondências de regra para email** ou **Correspondências de regra para email**.

Para saber mais, consulte [Exibir relatórios de proteção de email](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Baixar uma versão do Excel dos relatórios

1.  Na página Relatórios no centro de administrador do Office 365, selecione **Relatórios de proteção de email (Excel)**.

2.  Se estiver usando os relatórios de proteção de email do Excel pela primeira vez, será aberta uma guia para a página de download.
    
    1.  Selecione **Baixar** para baixar o Plug-in do Excel do Microsoft Office 365 para os Relatórios do Exchange Online.
    
    2.  Abra o download.
    
    3.  Na caixa de diálogo **Instalar Relatórios de Proteção de Email para o Office 365**, selecione **Avançar**, aceite os termos do contrato de licença e selecione **Avançar**.
    
    4.  Selecione o serviço que está sendo utilizado e, em seguida, selecione **Avançar**.
    
    5.  Verifique os pré-requisitos e selecione **Avançar**.
    
    6.  Selecione **Instalar**. Um atalho para os relatórios será criado na sua área de trabalho.

3.  Na área de trabalho, selecione **Relatórios de proteção de email para o Office 365**.

4.  No relatório, selecione a guia **Regras**.

## Importar ou exportar um conjunto de regras de fluxo de emails

Você deve usar o Shell de Gerenciamento do Exchange para importar ou exportar um conjunto de regras de fluxo de emails. Para saber mais sobre como importar um conjunto de regras de fluxo de emails de um arquivo XML, veja [Import-TransportRuleCollection](https://technet.microsoft.com/pt-br/library/bb123582\(v=exchg.150\)). Para saber sobre como exportar um conjunto de regras de fluxo de emails para um arquivo XML, veja [Export-TransportRuleCollection](https://technet.microsoft.com/pt-br/library/bb124410\(v=exchg.150\)).

## Precisa de mais ajuda?

Recursos para o Exchange Online:

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\))

[Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\))

[Email ações de regra de fluxo no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919237\(v=exchg.150\))

[Limites de regras de transporte e caixa de entrada](https://go.microsoft.com/fwlink/p/?linkid=324584)

Recursos para o Proteção do Exchange Online:

[Regras de fluxo de emails (regras de transporte) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/dn271424\(v=exchg.150\))

[Condições de regra de fluxo e email exceções (predicados) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj919234\(v=exchg.150\))

[De email ações de regra de fluxo no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj920117\(v=exchg.150\))

[Limites de regras de transporte e caixa de entrada](https://go.microsoft.com/fwlink/p/?linkid=324584)

Recursos para o Exchange Server 2013:

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

