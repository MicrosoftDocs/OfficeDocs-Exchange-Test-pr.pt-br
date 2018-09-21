---
title: 'Regras de fluxo de emails ou de transporte: Exchange 2013 Help'
TOCTitle: Regras de fluxo de email (regras de transporte)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50486597
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regras de fluxo de emails ou de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-04-28_

Você pode usar regras de fluxo de emails (também conhecidas como regras de transporte) para identificar e agir com base nas mensagens que fluem pela organização do Exchange 2013. As regras de fluxo de emails são semelhantes às regras de Caixas de Entrada disponíveis no Outlook e no Outlook Web App. A principal diferença das regras de fluxo de emails é que elas atuam em mensagens que estão em trânsito, não depois que a mensagem foi entregue à caixa de correio. As regras de fluxo de emails contêm conjuntos mais amplos de condições, exceções e ações com os quais é possível desfrutar da flexibilidade necessária para implementar muitos tipos de políticas de mensagem.

Este artigo explica os componentes das regras de fluxo de emails e como eles funcionam.

Para obter informações sobre regras de fluxo de email no Exchange Online, consulte [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)). Para obter informações sobre regras de fluxo de email no Proteção do Exchange Online, consulte [Regras de fluxo de emails (regras de transporte) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/dn271424\(v=exchg.150\))

Você pode usar o Centro de administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange para gerenciar as regras de fluxo de emails. Confira as instruções sobre como gerenciar regras de transporte em [Gerenciar regras de fluxo de emails](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

Você pode impor e testar cada regra ou testar e notificar o remetente. Para saber mais sobre as políticas de teste, consulte [Testar uma regra de fluxo de email](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules) e [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips).

Para implementar políticas de mensagens específicas usando regras do fluxo de emails, confira estes tópicos:

  - [Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Cenários comuns de bloqueio de anexo](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Usar regras de fluxo de email para que mensagens poderá ignorar desorganização](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [Cenários comuns de aprovação de mensagem](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios)

## Componentes de regra de fluxo de email

Uma regra de fluxo de email é composta por condições, exceções, ações e propriedades:

  - **Condições** Identificam as mensagens nas quais você gostaria de aplicar uma ação. Algumas condições examinam campos de cabeçalhos de mensagens (por exemplo, os campos Para, De ou Cc). Outras condições examinam propriedades de mensagens (por exemplo, assunto, corpo, anexos, tamanho e classificação da mensagem). A maioria das condições exige que você especifique um operador de comparação (por exemplo, igual a, diferente de ou contém) e um valor a ser correspondido. Se não houver condições ou exceções, a regra será aplicada a todas as mensagens.
    
    Para obter mais informações sobre condições de regra de fluxo de email no Exchange 2013, consulte [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

  - **Exceções** Opcionalmente, identificam as mensagens às quais as ações não devem se aplicar. Os mesmos identificadores de mensagens disponíveis nas condições também estão disponíveis nas exceções. As exceções substituem as condições e impedem que as ações da regra sejam aplicadas a uma mensagem, mesmo que a mensagem atenda a todas as condições configuradas.

  - **Ações** Especificam o que fazer com as mensagens que atendem a todas as condições na regra, mas não se encaixam em nenhuma das exceções. Há muitas ações disponíveis, como rejeitar, excluir ou redirecionar mensagens, incluir destinatários adicionais, incluir prefixos no assunto da mensagem ou inserir avisos de isenção legal no corpo da mensagem.
    
    Para obter mais informações sobre ações de regra de fluxo de email no Exchange 2013, consulte [Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

  - **Propriedades** Especificam outras configurações de regras que não sejam condições, exceções ou ações. Por exemplo, quando a regra deve ser aplicada, se devemos impor ou testar a regra e o período em que a regra é ativa.
    
    Para obter mais informações, consulte a seção de Propriedades de regra de fluxo de email neste tópico.

## Várias condições, exceções e ações

A seguinte tabela mostra como várias condições, valores de condição, exceções e ações são tratadas em uma regra.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Lógica</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Várias condições</p></td>
<td><p>E</p></td>
<td><p>Uma mensagem deve atender a todas as condições da regra. Se você precisar combinar uma condição ou outra, use regras separadas para cada condição. Por exemplo, se quiser adicionar o mesmo aviso de isenção legal a mensagens com anexos e mensagens com texto específico, crie uma regra para cada condição. No EAC, você pode facilmente copiar uma regra.</p></td>
</tr>
<tr class="even">
<td><p>Uma condição com vários valores</p></td>
<td><p>OU</p></td>
<td><p>Algumas condições permitem especificar mais de um valor. A mensagem deve corresponder a qualquer um dos valores especificados (não todos). Por exemplo, se o assunto de uma mensagem de email for <strong>Informações sobre o mercado de ações</strong> e a condição <strong>O assunto inclui qualquer uma destas palavras</strong> estiver configurada para corresponder às palavras <strong>Contoso</strong> ou <strong>ações</strong>, a condição será atendida, pois o assunto contém pelo menos um dos valores especificados.</p></td>
</tr>
<tr class="odd">
<td><p>Várias exceções</p></td>
<td><p>OU</p></td>
<td><p>Se uma mensagem corresponder a qualquer uma das exceções, as ações não são aplicadas na mensagem. A mensagem não precisa coincidir com todas as exceções.</p></td>
</tr>
<tr class="even">
<td><p>Várias ações</p></td>
<td><p>E</p></td>
<td><p>As mensagens que atendem às condições de uma regra recebem todas as ações que estão especificadas na regra. Por exemplo, se as ações <strong>Preceder o assunto da mensagem com</strong> e <strong>Adicionar destinatários à caixa Cco</strong> estiverem selecionadas, ambas as ações serão aplicadas à mensagem.</p>
<p>Lembre-se que algumas ações, como <strong>Excluir a mensagem sem notificar ninguém</strong>, impedem que regras subsequentes sejam aplicadas à mensagem. Outras ações como <strong>Encaminhar a mensagem</strong> não permitem ações adicionais.</p>
<p>Também é possível configurar uma ação em uma regra de tal forma que, quando ela for aplicada, as regras seguintes não sejam aplicadas à mensagem.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Propriedades de regras de fluxo de email

A tabela a seguir descreve as propriedades das regras que estão disponíveis nas regras de fluxo de emails.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da propriedade no EAC</th>
<th>Nome do parâmetro no PowerShell</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Prioridade</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>Indica a ordem que as regras são aplicadas às mensagens. A prioridade padrão se baseia no momento em que a regra é criada (regras mais antigas têm uma prioridade mais alta que as regras mais recentes e as regras de prioridade mais alta são processadas antes das regras de prioridade mais baixa).</p>
<p>Altere a prioridade da regra no EAC movendo a regra para cima ou para baixo na lista de regras. No PowerShell, defina o número de prioridade (0 é a prioridade mais alta).</p>
<p>Por exemplo, se tiver uma regra para rejeitar mensagens que incluam um número de cartão de crédito e outra exigindo aprovação, você desejará que a regra de rejeição ocorra primeiro e pare a aplicação das outras regras.</p>
<p>Para saber mais, veja <a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules">Set the priority of a mail flow rule</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modo</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>Você pode especificar se deseja que a regra comece a processar as mensagens imediatamente, ou se deseja testar as regras sem afetar a entrega da mensagem (com ou sem Prevenção contra Perda de Dados ou Dicas de Política DLP).</p>
<p>As dicas de política apresentam uma anotação breve no Outlook ou no Outlook na Web que fornecem informações sobre possíveis violações de política para a pessoa que está criando a mensagem. Para saber mais, veja <a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips">Dicas de política</a>.</p>
<p>Para saber mais sobre os modos, confira <a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules">Testar uma regra de fluxo de email</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ativar esta regra na seguinte data</strong></p>
<p><strong>Desativar esta regra na seguinte data</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>Especifica o intervalo de datas quando a regra está ativa.</p></td>
</tr>
<tr class="even">
<td><p><strong>Na</strong> caixa de seleção selecionada ou não selecionada</p></td>
<td><p>Novas regras: parâmetro <em>Enabled</em> no cmdlet <strong>New-TransportRule</strong>.</p>
<p>Regras existentes: Use os cmdlets <strong>Enable-TransportRule</strong> ou <strong>Disable-TransportRule</strong>.</p>
<p>O valor é exibido na propriedade <strong>State</strong> da regra.</p></td>
<td><p>Você pode criar uma regra desabilitada e ativá-la quando estiver pronto para testá-la. Ou, você pode desativar uma regra sem excluí-la para preservar as configurações.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Adiar a mensagem se o processamento de regra não for concluído</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>Você pode especificar como a mensagem deveria ser tratada se o processamento de regra não puder ser concluído. Por padrão, a regra será ignorada, mas você pode optar por reenviar a mensagem para processamento.</p></td>
</tr>
<tr class="even">
<td><p><strong>Corresponder endereço do remetente da mensagem</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Se a regra usa condições ou exceções que examinam o endereço de email do remetente, você pode procurar o valor no cabeçalho da mensagem, no envelope da mensagem ou em ambos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Parar o processamento de mais regras</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Essa é uma ação para a regra, mas se parece com uma propriedade no EAC. Você pode optar por evitar a aplicação de regras adicionais a uma mensagem após uma regra processar uma mensagem.</p></td>
</tr>
<tr class="even">
<td><p><strong>Comentários</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>Você pode inserir comentários descritivos sobre a regra.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Como as regras de fluxo de correio são aplicadas a mensagens

Todas as mensagens que fluem por sua organização são avaliadas pelas regras de fluxo de emails habilitadas para a sua organização. As regras são processadas na ordem listada na página **Fluxo de emails** \> **Regras** ou baseadas no valor do parâmetro *Priority* correspondente no PowerShell.

Cada regra também oferece a opção de parar o processamento de outras quando é encontrada correspondência com a regra. Esta configuração é importante para as mensagens que atendem às condições em várias regras de fluxo de emails (qual regra você deseja aplicar à mensagem? Todas? Apenas uma?).

## Diferenças no processamento com base no tipo de mensagem

Existem vários tipos de mensagens que transitam por uma organização. A tabela a seguir mostra quais tipos de mensagens podem ser processados por regras de fluxo de emails.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de mensagem</th>
<th>Uma regra pode ser aplicada?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Mensagens normais</strong>   Mensagens que contêm um único corpo com formato rich text (RTF), HTML ou texto sem formatação, ou um conjunto de corpos de mensagem em várias partes ou alternativo.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Criptografia de Mensagem do Office 365</strong>    As mensagens criptografadas por Criptografia de Mensagem do Office 365 em Office 365. Para saber mais, veja <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Criptografia de Mensagens do Office 365</a>.</p></td>
<td><p>As regras sempre podem acessar os cabeçalhos de envelope e processar as mensagens com base nas condições que inspecionam cabeçalhos.</p>
<p>Para uma regra inspecionar ou modificar o conteúdo de uma mensagem criptografada, é preciso verificar se a descriptografia de transporte está habilitada (Obrigatória ou Opcional; o padrão é Opcional). Para saber mais, veja <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Habilitar ou desabilitar a descriptografia de transporte</a>.</p>
<p>Você também pode criar uma regra que descriptografa automaticamente mensagens criptografadas. Para saber mais, veja <a href="https://go.microsoft.com/fwlink/p/?linkid=402846">Definir regras para criptografar ou descriptografar mensagens de email</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensagens criptografadas em S/MIME</strong></p></td>
<td><p>As regras podem apenas acessar os cabeçalhos de envelope e processar as mensagens com base nas condições que inspecionam cabeçalhos.</p>
<p>As regras com condições que exigem a inspeção do conteúdo da mensagem ou ações que modificam o conteúdo da mensagem não podem ser processadas.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mensagens protegidas por RMS</strong> Mensagens que tinham um Active Directory Rights Management Services (AD RMS) ou uma Azure Rights Management (RMS) política aplicada.</p></td>
<td><p>As regras sempre podem acessar os cabeçalhos de envelope e processar as mensagens com base nas condições que inspecionam cabeçalhos.</p>
<p>Para uma regra inspecionar ou modificar o conteúdo de uma mensagem protegida por RMS, é preciso verificar se a descriptografia de transporte está habilitada (Obrigatória ou opcional; o padrão é opcional). Para saber mais, veja <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Habilitar ou desabilitar a descriptografia de transporte</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensagem com assinatura não criptografada</strong>   Mensagens que foram assinadas, mas não foram criptografadas.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Mensagens da UM</strong>   Mensagens criadas ou processadas pelo serviço de Unificação de Mensagens, como uma mensagem de voz, fax, notificações de chamadas não atendidas e mensagens criadas ou encaminhadas usando o Microsoft Outlook Voice Access.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensagens anônimas</strong>   Mensagens enviadas por remetentes anônimos.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Notificações de leitura</strong>   Relatórios gerados em resposta às solicitações de confirmação de leitura pelos remetentes. Notificações de leitura têm a classe de mensagem <code>IPM.Note*.MdnRead</code> ou <code>IPM.Note*.MdnNotRead</code>.</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


## Regras de Transporte e associação a grupos

Quando você define uma regra de transporte usando uma condição que expande a associação de um grupo de distribuição, a lista resultante de destinatários é armazenada em cache pelo serviço Transporte no servidor de caixas de correio que aplica a regra. Isso é conhecido como *Cache de Grupos Expandidos* e também é usado pelo agente de Registro em Diário para avaliar a associação a grupos para regras de diário. Por padrão, o Cache de Grupos Expandidos armazena a associação do grupo por quatro horas. Destinatários retornados pelo filtro de destinatários do grupo de distribuição dinâmica também são armazenados. O Cache de Grupos Expandidos faz visitas repetidas ao Active Directory e o tráfego de rede resultante da resolução de associações de grupos desnecessária.

No Exchange 2013, esse intervalo e outros parâmetros relacionados ao Cache de Grupos Expandidos são configuráveis. Você pode diminuir o intervalo de expiração do cache, ou desabilitar totalmente o cache, para garantir que as associações de grupo sejam atualizadas com mais frequência. Você deve se planejar para o aumento na carga correspondente em seus controladores de domínio do Active Directory, para pesquisas de expansão do grupo de distribuição. Você também pode limpar o cache em um servidor de Caixa de Correio reiniciando o serviço de Transporte do Microsoft Exchange naquele servidor. Faça isso em cada servidor de Caixa de Correio onde deseja limpar o cache. Ao criar, testar e solucionar problemas de regras de transporte que usam condições baseadas na associação a grupos de distribuição, considere também o impacto do Cache de Grupos Expandidos.

## Armazenamento e replicação de regra

Regras de fluxo de email que você criar e configurar em servidores de caixa de correio são armazenadas em Active Directory, e são lidos e aplicados pelo serviço de transporte em todos os servidores de caixa de correio na organização. Quando você cria, modificar ou remove uma regra de fluxo de email, a alteração seja replicada entre os controladores de domínio em sua organização. Isso permite Exchange fornecer regras de fluxo de um conjunto consistente de email em toda a organização.

**Observações**:

  - Replicação entre os controladores de domínio depende de fatores que não são controlados pela Exchange (por exemplo, o número de sites de Active Directory ) e a velocidade dos links de rede. Portanto, você precisa considerar os atrasos de replicação quando você implementa as regras de fluxo de correio em sua organização. Para obter mais informações sobre a replicação Active Directory, consulte [Introdução ao gerenciamento de topologia usando o Windows PowerShell e de replicação do Active Directory](https://go.microsoft.com/fwlink/p/?linkid=274904).

  - Grupos de distribuição expandido para evitar repetidas Active Directory consultas para determinar a associação de um grupo de caches de cada servidor de caixa de correio. Por padrão, as entradas no cache de grupos expandida expiração cada quatro horas. Portanto, as alterações à associação do grupo não são detectadas pelas regras de fluxo de email até que o cache de grupos expandida é atualizado. Para forçar uma atualização imediata do cache em um servidor de caixa de correio, reinicie o Microsoft Exchange serviço de transporte. Você precisará reiniciar o serviço em cada servidor de caixa de correio onde deseja obrigatoriamente atualizar o cache.

Regras de fluxo de email que você criar e configurar em servidores de transporte de borda são armazenadas na instância local do AD LDS no servidor. Nenhuma replicação automatizada de regras de fluxo de email ocorre em servidores de transporte de borda. Regras no servidor de transporte de borda se aplicam apenas a mensagens que fluem através do servidor local. Se você precisa aplicar o mesmo conjunto de regras de fluxo de correio em vários servidores de transporte de borda, você pode clonar a configuração do servidor de transporte de borda, ou exportar e importar as regras de fluxo de email. Para obter mais informações, consulte [Configuração clonada do servidor de transporte de borda](edge-transport-server-cloned-configuration-exchange-2013-help.md) e [importação ou exportação coleções de regras de fluxo de email](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

Sempre que o serviço de transporte em um servidor de caixa de correio ou servidor de transporte de borda detecta uma regra de fluxo de email modificadas, um evento é registrado no log do aplicativo no Visualizador de eventos (evento ID 4002 nos servidores de caixa de correio e a identificação de evento 16028 nos servidores de transporte de borda).

## Armazenamento e replicação de regra em ambientes mistos

Há dois cenários de ambiente misto que são comuns em Exchange 2013:

  - **Implantações híbridas em que a parte da sua organização reside no UNRESOLVED\_TOKEN\_VAL(Office365)**
    
    Em um ambiente híbrido, não há nenhuma replicação das regras entre sua organização local do Exchange e UNRESOLVED\_TOKEN\_VAL(Office365). Portanto, quando você cria uma regra em Exchange, você precisa criar uma regra correspondente no UNRESOLVED\_TOKEN\_VAL(Office365). Regras criadas no UNRESOLVED\_TOKEN\_VAL(Office365) são armazenados na nuvem, enquanto as regras que você criar em sua organização local são armazenados localmente em Active Directory. Quando você gerencia regras em um ambiente híbrido, você precisa manter os dois conjuntos de regras sincronizados pela fazendo a alteração em ambos os lugares, ou fazer a alteração em um ambiente e, então, exportar as regras e importá-las em outro ambiente.
    

    > [!IMPORTANT]
    > Embora haja uma sobreposição substancial entre as condições e ações que estão disponíveis no UNRESOLVED_TOKEN_VAL(Office365) e Exchange Server, há algumas diferenças. Se você planeja criar a regra de mesma em ambos os locais, certifique-se de que todas as condições e ações que você planeja usar estão disponíveis. Para ver a lista de condições disponíveis e ações que estão disponíveis no UNRESOLVED_TOKEN_VAL(Office365), consulte os seguintes tópicos:<BR><A href="https://technet.microsoft.com/pt-br/library/jj919235(v=exchg.150)">Exceções (predicados) e condições de regra de fluxo de email no Exchange Online</A><BR><A href="https://technet.microsoft.com/pt-br/library/jj919237(v=exchg.150)">Email ações de regra de fluxo no Exchange Online</A>



  - **Coexistência com o Exchange 2010 ou Exchange 2007**
    
    Quando você coexistir com Exchange 2010 ou Exchange 2007, todas as regras de fluxo de email são armazenadas em Active Directory e replicadas em sua organização, independentemente da versão de Exchange Server que você usou para criar as regras. No entanto, todas as regras de fluxo de email associados com a versão do servidor de Exchange Server que foi usada para criá-los e é armazenada em um contêiner específico da versão no Active Directory. Quando você implanta Exchange 2013 em sua organização, todas as regras existentes são importadas para Exchange 2013 como parte do processo de instalação. No entanto, qualquer alteração posteriormente seria precisam ser feitas com as duas versões. Por exemplo, se você alterar uma regra existente no Exchange 2013 (Shell de Gerenciamento do Exchange ou o EAC), você precisará fazer a mesma alteração no Exchange 2010 (Shell de Gerenciamento do Exchange ou o UNRESOLVED\_TOKEN\_VAL(exEMC) ). Ou, você pode exportar as regras de Exchange 2013 e importá-los para Exchange 2010.
    
    Exchange 2010 não conseguirá processar regras que tenham o valor de **versão** ou **RuleVersion** 15. *n*. *n*. *n*. Para garantir que todas as suas regras podem ser processados, use apenas as regras que têm o valor 14. *n*. *n*. *n*.

## Para saber mais

[Gerenciar regras de fluxo de emails](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)

[Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Agentes de transporte](transport-agents-exchange-2013-help.md)

