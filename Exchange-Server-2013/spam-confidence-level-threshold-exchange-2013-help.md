---
title: 'Limite do Nível de Confiança de Spam: Exchange 2013 Help'
TOCTitle: Limite do Nível de Confiança de Spam
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50484847
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limite do Nível de Confiança de Spam

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-11-17_


> [!TIP]
> Em 1 de novembro de 2016, o Microsoft interrompeu a produção de atualizações de definição de spam para os Filtros SmartScreen, no Exchange e no Outlook. As definições de spam existentes para SmartScreen permanecerão inalteradas, mas a respectiva eficácia provavelmente diminuirá ao longo do tempo. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Substituição do suporte para SmartScreen no Outlook e no Exchange</A>.



No Microsoft Exchange Server 2013, você pode definir ações específicas de acordo com os limites do nível de confiança do spam. Por exemplo, você pode definir limites diferentes para rejeitar, excluir ou colocar uma mensagem em quarentena em um servidor Exchange com o agente de Filtro de Conteúdo.

A combinação dessa configuração de limite de SCL no agente de Filtro de Conteúdo e a configuração da pasta Lixo Eletrônico de SCL na caixa de correio do usuário ajuda você a implementar uma estratégia antispam mais abrangente e precisa. Essa funcionalidade de ajuste de limite de SCL mais detalhada e precisa no Exchange 2013 pode ajudar você a reduzir o custo geral de implantação e manutenção da solução antispam em toda a organização do Exchange.

O agente do Filtro de Conteúdo atribui uma classificação SCL no final do ciclo antispam, depois que outros agentes antispam processarem as mensagens de entrada. Muitos dos outros agentes anti-spam que processam mensagens de entrada antes que elas sejam processadas pelo agente do Filtro de conteúdo são determinantes em como eles atuam em uma mensagem. Por exemplo, em um servidor de Transporte de Borda, o agente do Filtro de Conexão rejeita todas as mensagens enviadas de um endereço IP que está na lista de bloqueio em tempo real. O agente do Filtro de Remetente e o agente do Filtro de Destinatário processam mensagens de uma forma determinística similar.

No Exchange 2013, esses agentes anti-spam determinísticos processam as mensagens primeiro e assim reduzem muito o número de mensagens que devem ser processadas pelo agente de Filtro de Conteúdo. Para obter mais informações sobre a ordem na qual os agentes anti-spam processam as mensagens, consulte [Proteção contra spam](anti-spam-protection-exchange-2013-help.md).

Como o filtro de conteúdo não é um processo determinístico e exato, a capacidade de ajustar a ação que o agente de Filtro de Conteúdo executa em diferentes valores de SCL é importante. Ao ajustar com cuidado a configuração do limite de SCL, você pode minimizar o seguinte:

  - O tamanho do repositório de quarentena de spam

  - Número de emails legítimos em quarentena por engano

  - Número de emails legítimos que chegam à pasta de Lixo Eletrônico do usuário do Microsoft Outlook

  - Número de mensagens de spam ofensivas que chegam à Caixa de Entrada ou à pasta Lixo Eletrônico do usuário do Outlook

  - Número de emails de spam que chegam à Caixa de Entrada do usuário do Outlook

## Ações de limite SCL

Ajustando as ações de limite de SCL, você pode escalar a ação de filtro de conteúdo que é realizada em mensagens em que o risco de spam é maior. Para entender essa nova funcionalidade, é útil entender as diferentes ações de limite de SCL e como elas são implementadas:

  - **Limite de exclusão de SCL**   Quando o valor de SCL para uma mensagem específica é igual ou superior ao limite de exclusão de SCL, o agente Filtro de Conteúdo exclui a mensagem. Não existe comunicação no nível de protocolo que informe ao sistema de envio ou ao remetente que a mensagem foi excluída. Se o valor de SCL para uma mensagem for menor que o valor do limite de exclusão de SCL, o agente do Filtro de Conteúdo não excluirá a mensagem. Em vez disso, o agente Filtro de Conteúdo comparará o valor de SCL com o limite de rejeição de SCL.

  - **Limite de rejeição de SCL**   Quando o valor de SCL para uma mensagem específica é igual ou superior ao limite de rejeição de SCL, o agente Filtro de Conteúdo exclui a mensagem e envia uma resposta de rejeição ao sistema de envio. Você pode personalizar a resposta de rejeição. Em alguns casos, uma notificação de falha na entrega é enviada ao remetente original da mensagem. Se o valor da SCL para uma mensagem for menor que os valores de limite de rejeição e de exclusão de SCL, o agente do Filtro de Conteúdo não excluirá nem rejeitará a mensagem. Em vez disso, o agente Filtro de Conteúdo comparará o valor de SCL ao limite de quarentena de SCL.

  - **Limite de quarentena de SCL**   Quando o valor de SCL para uma mensagem específica é igual ou superior ao limite de quarentena de SCL, o agente Filtro de Conteúdo envia a mensagem para uma caixa de correio de quarentena. Os administradores de email devem revisar periodicamente a caixa de correio de quarentena. Se o valor de SCL para uma mensagem for menor que os valores de limite de exclusão, rejeição e quarentena de SCL, o agente de Filtro de Conteúdo não excluirá, rejeitará ou colocará a mensagem em quarentena. Em vez disso, o agente do Filtro de Conteúdo enviará a mensagem para o servidor de Caixa de Correio apropriado, em que o valor de limite da pasta Lixo Eletrônico de SCL por destinatário da mensagem será avaliado.

  - **Limite da pasta de Lixo Eletrônico de SCL**   Se o valor de SCL para uma mensagem específica exceder o limite da pasta de Lixo Eletrônico de SCL, a mensagem será entrega na pasta de Lixo Eletrônico do usuário. Se o valor de SCL para uma mensagem for menor que os valores de limite de exclusão, rejeição, quarentena e da pasta Lixo Eletrônico, a mensagem será entregue na Caixa de Entrada do usuário.

O agente do Filtro do Conteúdo e a pasta Lixo Eletrônico processam o valor de limite de SCL de maneira diferente. O agente do Filtro do Conteúdo atua sobre o valor limite de SCL que você configura. A pasta de Lixo Eletrônico age de acordo com o valor do limite SCL que você configurar mais 1. Por exemplo, se você configurar a ação Excluir para um SCL de 8 no agente de Filtro de Conteúdo, todas as mensagens com um SCL de 8 ou mais serão excluídas. No entanto, se você configurar a pasta Lixo Eletrônico com um limite de SCL de 4, todas as mensagens com um SCL de 5 ou maior serão movidas para a pasta Lixo Eletrônico.

Por exemplo, se você definir o limite de exclusão de SCL como 8, o limite de rejeição de SCL como 7, o limite de quarentena de SCL como 6 e o limite da pasta Lixo Eletrônico de SCL como 4, todos os emails com SCL 5 ou menor serão entregues à caixa de correio do usuário. Os emails com um valor SCL de 5 serão colocados na pasta Lixo Eletrônico do usuário. Emails com um valor SCL de 4 ou menos irão para a Caixa de Entrada do usuário.

Você pode configurar exclusão, rejeição, quarentena e a pasta Lixo Eletrônicos nos seguintes locais:

  - **Na configuração do agente do Filtro de Conteúdo (de acordo com a configuração do SCL do servidor)**   Use o cmdlet **Set-ContentFilterConfig** para habilitar ou desabilitar e definir os limites de exclusão, rejeição e quarentena no servidor Exchange em que você executa o agente do Filtro de Conteúdo. Com o tempo, à medida que você analisa a funcionalidade e a métrica de spam fornecidas pelos recursos de relatório e log antispam, você pode fazer ajustes adicionais nessas configurações de limite de SCL conforme necessário.
    
    Os parâmetros SCL disponíveis no cmdlet **Set-ContentFilterConfig** são descritos na tabela a seguir.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Descrição</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>Esse parâmetro habilita ou desabilita a exclusão de uma mensagem sem uma notificação de falha de entrega (NDR) quando o valor SCL da mensagem for maior ou igual ao valor especificado pelo parâmetro <em>SCLDeleteThreshold</em>. As entradas válidas para este parâmetro são <code>$true</code> ou <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>A entrada válida para esse parâmetro é um inteiro entre 0 e 9, inclusive. O valor desse parâmetro deve ser maior do que os outros parâmetros de limites de SCL. Esse parâmetro somente é significativo se o valor do parâmetro <em>SCLDeleteEnabled</em> é <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>Esse parâmetro habilita ou desabilita a rejeição de uma mensagem sem uma NDR quando o valor SCL da mensagem for maior ou igual ao valor especificado pelo parâmetro <em>SCLRejectThreshold</em>. As entradas válidas para este parâmetro são <code>$true</code> ou <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>A entrada válida para esse parâmetro é um inteiro entre 0 e 9, inclusive. O valor desse parâmetro deve ser menor do que o do parâmetro <em>SCLDeleteThreshold</em>, mas maior do que o dos outros parâmetros de limite de SCL. Esse parâmetro só tem significado se o valor do parâmetro <em>SCLRejectEnabled</em> for <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>Esse parâmetro habilita ou desabilita o envio de uma mensagem para a caixa de correio de quarentena de spam quando o valor SCL da mensagem for maior ou igual ao valor especificado pelo parâmetro <em>SCLQuarantineThreshold</em>. As entradas válidas para este parâmetro são <code>$true</code> ou <code>$false</code>.</p>
    <p>Para obter mais informações sobre a caixa de correio de quarentena de spam, consulte <a href="spam-quarantine-exchange-2013-help.md">Quarentena de spam</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>A entrada válida para esse parâmetro é um inteiro entre 0 e 9, inclusive. O valor desse parâmetro deve ser menor do que o do parâmetro <em>SCLRejectThreshold</em>, mas maior do que o parâmetro <em>SCLJunkThreshold</em> nos cmdlets <strong>Set-OrganizationConfig</strong> ou <strong>Set-Mailbox</strong>. Esse parâmetro somente é significativo se o valor do parâmetro <em>SCLQuarantineThreshold</em> é <code>$true</code>.</p></td>
    </tr>
    </tbody>
    </table>


  - **Nas configurações da organização (configuração SCL em toda a organização)**   Use o cmdlet **Set-OrganizationConfig** para definir o limite da pasta Lixo Eletrônico do SCL para todas as caixas de correio na organização.
    
    O parâmetro SCL disponível no cmdlet **Set-OrganizationConfig** é descrito na tabela a seguir. Para um exemplo de uso do SCLJunkThreshold, consulte [Definir Configurações Anti-Spam em Caixas de Correio](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Descrição</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>Esse parâmetro especifica o valor SCL que uma mensagem deve exceder para ela ser movida para para pasta de Lixo Eletrônico da caixa de correio do destinatário. A entrada válida para esse parâmetro é um inteiro entre 0 e 9, inclusive. O valor desse parâmetro deve ser menor do que os outros parâmetros de limites de SCL. Por exemplo, se você especificar o valor 4, as mensagens com um valor SCL de 5 ou mais serão movidas para a pasta de Lixo Eletrônico do usuário.</p></td>
    </tr>
    </tbody>
    </table>


  - **Nas caixas de correio dos usuários (configuração de SCL por destinatário)**   Use o cmdlet **Set-Mailbox** para habilitar ou desabilitar e definir os limites de exclusão, rejeição, quarentena e limites da pasta Lixo Eletrônico nas caixas de correio individuais. Você pode usar somente o cmdlet **Set-Mailbox** para habilitar ou desabilitar o limite da pasta Lixo Eletrônico de SCL em caixas de correio individuais. Os limites de exclusão, rejeição e quarentena de SCL por destinatário são armazenados no Active Directory e são replicados para os servidores de Transporte de Borda pelo serviço EdgeSync do Microsoft Exchange. As configurações de limite de SCL por destinatário são usadas pelo agente do Filtro de conteúdo mesmo se você já tiver definido as configurações de SCL de servidor por transporte. Por isso, se você tiver definido limites de SCL por destinatário, o agente do Filtro de conteúdo usará os limites de SCL por destinatário para usuários específicos, no lugar da configuração de SCL no agente do Filtro de conteúdo. Para exemplos, consulte [Definir Configurações Anti-Spam em Caixas de Correio](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    

    > [!TIP]
    > Os limites de SCL por destinatário não são impostos em mensagens recebidas por meio dos grupos de distribuição.

    
    Os mesmos parâmetros de SCL estão disponíveis no cmdlet **Set-Mailbox** estão disponíveis nos cmdlets **Set-ContentFilterConfig** e **Set-OrganizationConfig**:
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    Entretanto, todos os parâmetros SCL no cmdlet **Set-Mailbox** também aceitam o valor `$null`. Se uma configuração de SCL em uma caixa de correio estiver em branco (`$null`), a configuração do agente de Filtro de Conteúdo correspondente ou a configuração da organização será aplicada à caixa de correio. Se uma configuração de SCL em uma caixa de correio tiver o valor de `$true` ou `$false`, a configuração na caixa de correio ignora a configuração correspondente por toda a organização, no agente do Filtro de Conteúdo ou na configuração da organização.
    
    O parâmetro SCL que está disponível somente no cmdlet **Set-Mailbox** é descrito na tabela a seguir.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Descrição</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>Esse parâmetro habilita ou desabilita a entrega de uma mensagem para a pasta de Lixo Eletrônico quando o valor SCL da mensagem for maior ou igual ao valor especificado pelo parâmetro <em>SCLQuarantineThreshold</em>. As entradas válidas para esse parâmetro são <code>$true</code>, <code>$false</code> ou <code>$null</code>.</p>
    <p>Observe que a filtragem de lixo eletrônico é habilitada por padrão, para todas as caixas de correio de usuário na organização. Por padrão, o parâmetro <em>Enabled</em> é definido para o valor <code>$true</code> no cmdlet <strong>Set-MailboxJunkEmailConfiguration</strong> para todas as caixas de correio de usuário.</p></td>
    </tr>
    </tbody>
    </table>
    
    Para mais informações sobre como configurar limites de SCL para uma caixa de correio, consulte [Definir Configurações Anti-Spam em Caixas de Correio](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).

## Monitorar limites de SCL

Você pode usar vários scripts internos localizados na pasta `%ExchangeInstallPath%Scripts`, como **get-AntispamSCLHistogram.ps1**, para reunir os dados de resultados da filtragem. Se os dados indicarem que você deve fazer ajustes imediatos, reconfigure os limites de SCL. Caso contrário, colete dados e analise o relatório de spam para determinar se os ajustes são necessários.

