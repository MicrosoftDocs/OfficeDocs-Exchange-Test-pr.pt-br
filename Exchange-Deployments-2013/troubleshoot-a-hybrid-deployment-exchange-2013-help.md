---
title: 'Solucionar problemas em uma implantação híbrida: Exchange 2013 Help'
TOCTitle: Solucionar problemas em uma implantação híbrida
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50487118
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solucionar problemas em uma implantação híbrida

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-04-29_

Configurar uma implantação híbrida no Exchange com o assistente de Configuração Híbrida minimiza consideravelmente os possíveis problemas que a implantação híbrida pode enfrentar. No entanto, há algumas áreas típicas fora do escopo do assistente de Configuração Híbrida que, se configuradas incorretamente, podem apresentar problemas em uma implantação híbrida. Este tópico descreve as seguintes áreas comuns nas quais podem surgir problemas, e descreve as etapas básicas para verificar ou corrigi-los:

  - Servidores Exchange locais

  - Certificados

  - Erros específicos do assistente de Configuração Híbrida


> [!TIP]
> Neste tópico, "servidores Exchange" referem-se ao seguinte: 
> <UL>
> <LI>
> <P><STRONG>Servidores de Acesso para Cliente</STRONG> Exchange 2013 e anterior</P>
> <LI>
> <P><STRONG>Servidores de Caixa de Correio</STRONG> Exchange 2016 e posterior</P></LI></UL>



Para saber mais, confira [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Para outras tarefas de gerenciamento relacionadas a implantações híbridas, confira [Procedimentos de Implantação Híbrida](hybrid-deployment-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir esta tarefa: varia, dependendo dos tipos de problemas de implantação híbrida.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações híbridas", no tópico [Permissões de infraestrutura do Exchange e do Shell](https://technet.microsoft.com/pt-br/library/dd638114\(v=exchg.150\)).

  - As orientações fornecidas neste tópico aplicam-se às implantações híbridas configuradas com o assistente de Configuração Híbrida. Não há suporte para implantações híbridas configuradas manualmente.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](https://technet.microsoft.com/pt-br/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Solucionar problemas com os servidores do Exchange locais

Normalmente, a configuração dos servidores do Exchange locais é a etapa na qual a maioria dos problemas pode ocorrer em uma implantação híbrida. Normalmente, as áreas que precisam de exame são as seguintes:

  - **Disponibilidade**   A publicação correta dos servidores do Exchange locais na Internet é essencial para que os recursos funcionem corretamente em sua implantação híbrida. Para isso, você deve configurar seu firewall local ou outros dispositivos de segurança a fim de permitir o acesso de entrada da Internet para os pontos de extremidade do EWS (Exchange Web Services) e de Descoberta Automática nos servidores do Exchange locais. Além disso, os servidores do Exchange também devem ser configurados para aceitar email SMTP de entrada. Se o serviço do Microsoft EOP (Proteção do Exchange Online) incluído em sua organização do Office 365 não puder acessar os servidores do Exchange locais, o transporte de email seguro da organização do Exchange Online para a organização local não funcionará corretamente.

  - **Certificados**   O certificado digital usado para o transporte seguro de email entre as organizações locais e do Exchange Online deve ser instalado em todos os servidores do Exchange locais voltados para a Internet que se comunicarão com o Exchange Online, deve ser emitido por uma CA (autoridade de certificação) de terceiros, não deve estar expirado e deve ter os serviços IIS e SMTP atribuídos. Se esses requisitos de certificado não forem atendidos, o transporte seguro de email da organização do Exchange Online para a organização local não funcionará corretamente. Encontre mais informações sobre os requisitos de certificado em "Solucionar problemas com certificados" mais adiante neste tópico.

## Como saber se os servidores do Exchange estão configurados corretamente?

Para verificar se você publicou com êxito seus servidores do Exchange locais, use o Analisador de Conectividade Remota da Microsoft para verificar a conectividade de entrada da Internet para seus servidores do Exchange locais. Faça o seguinte:

1.  Vá para a ferramenta [Analisador de Conectividade Remota](https://www.testexchangeconnectivity.com/).

2.  Essa etapa é para um teste geral das tarefas de EWS para confirmar se elas estão funcionando e se o ponto de extremidade de EWS está configurado.
    
    Execute os testes de **Sincronização, Notificação, Disponibilidade e Respostas Automáticas (Ausência Temporária)** na seção **Testes de Conectividade dos Serviços Web do Microsoft Exchange** e verifique se há erros. Se ocorrerem erros, corrija os itens que o teste identificou.

3.  Essa etapa é para um teste geral do serviço Descoberta Automática para confirmar se ele está funcionando e se o ponto de extremidade de Descoberta Automática está configurado.
    
    Execute o teste **Descoberta Automática do Outlook** na seção **Testes de Conectividade do Microsoft Office Outlook** e verifique se há erros. Se ocorrerem erros, corrija os itens que o teste identificou.

4.  Essa etapa é para um teste de conectividade de SMTP geral e confirma se os servidores do Exchange podem receber mensagens de entrada da Internet.
    
    Execute o teste **Email SMTP de Entrada** na seção **Testes de Email da Internet** e verifique se há erros. Se ocorrerem erros, corrija os itens que o teste identificou.

## Solucionar problemas com certificados

A configuração dos certificados instalados nos servidores do Exchange locais pode ser a origem dos problemas que ocorrem em uma implantação híbrida. Na maioria dos casos, os seguintes problemas relacionados a certificados afetam a funcionalidade híbrida:

  - **Tipo de certificado**   O certificado digital usado para transporte híbrido seguro e definido no assistente de Configuração Híbrida deve ser emitido por uma autoridade de certificação de terceiros. Certificados autoassinados não podem ser usados para autenticação de transporte híbrida. Se um certificado autoassinado for selecionado ou atribuído inadvertidamente, o transporte de email seguro entre o Exchange Online e as organizações locais não funcionará corretamente.

  - **Serviços atribuídos**   Os serviços IIS (Serviço de Informações de Internet) e SMTP (Simple Mail Transport Protocol) devem ser atribuídos ao certificado digital usado para transporte híbrido. Se esses serviços não forem atribuídos, o transporte de email seguro entre o Exchange Online e as organizações locais não funcionará corretamente.

  - **Instalação**   O certificado digital usado para transporte de email seguro entre as organizações do Exchange locais e Online deve ser instalado em todos os servidores do Exchange locais. Se você estiver implantando servidores híbridos com os servidores de Transporte de Borda locais, o certificado digital também deverá ser instalado em seus servidores de Transporte de Borda. Se o certificado não estiver instalado nos servidores locais, o transporte de email seguro entre o Exchange Online e as organizações locais não funcionará corretamente.

  - **Expiração**   O certificado digital usado para transporte de email seguro entre as organizações locais e do Exchange Online não deve ter expirado. Se o certificado tiver expirado, o transporte de email seguro entre o Exchange Online e as organizações locais não funcionará corretamente.

## Como saber se seus certificados estão configurados corretamente?

Para verificar se o certificado para transporte de email híbrido está configurado corretamente em seus servidores do Exchange locais, faça o seguinte:

1.  Em um Exchangex servidor local, abra o Shell de Gerenciamento do Exchange.

2.  No Shell de Gerenciamento do Exchange, execute o seguinte comando.
    
        Get-ExchangeCertificate| format-list

3.  Localize as informações do certificado que você definiu no assistente de Configuração Híbrida que será usado para transporte de email seguro.

4.  Verifique se que os seguintes valores de parâmetro estão atribuídos ao certificado:
    
      - **Parâmetro IsSelfSigned**   Esse valor de parâmetro deve ser *False*.
    
      - **Parâmetro RootCAType**   Esse valor de parâmetro deve ser *Third Party*.
    
      - **Parâmetro Services**   Esse valor de parâmetro deve ser *IIS, SMTP*.
    
      - **Parâmetro NotAfter**   Esse valor de parâmetro é a data de expiração do certificado. A data listada aqui não deve ter expirado.

## Solução de problemas de erros específicos do assistente de Configuração Híbrida

Se um erro for exibido quando você executar o assistente de Configuração Híbrida, normalmente será possível resolver o problema executando algumas verificações ou ações simples. Veja as sugestões a seguir para resolver mensagens ou problemas específicos que você poderá encontrar ao executar o assistente de Configuração Híbrida.

  - **Mensagem "O Conector de Recebimento Padrão não pode ser encontrado no servidor \<Nome do Servidor\>"**   Esta mensagem será exibida se o Conector de Recebimento em qualquer servidor Exchange listado no atributo a seguir não estiver ouvindo na porta TCP 25 para os protocolos IPv4 e IPv6: `(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -  
        Para verificar se os conectores de recebimento nos servidores do Exchange listados quando você executa o `(Get-HybridConfiguration).ReceivingTransportServers.` tem as ligações corretas, execute o seguinte comando no Shell de Gerenciamento do Exchange.
        
            Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
        Você verá a seguinte entrada para os servidores do Exchange: `{[::]:25, 0.0.0.0:25}`
        
        Se essa associação não estiver listada, você precisará adicioná-la a seu Conector de Recebimento usando o parâmetro *Bindings* do cmdlet **Set-ReceiveConnector**. Para obter detalhes, consulte [Set-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125140\(v=exchg.150\)).

