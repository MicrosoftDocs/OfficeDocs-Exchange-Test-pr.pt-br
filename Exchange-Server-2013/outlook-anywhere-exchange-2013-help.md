---
title: 'Outlook em Qualquer Lugar: Exchange 2013 Help'
TOCTitle: Outlook em Qualquer Lugar
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50486169
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook em Qualquer Lugar

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

No Microsoft Exchange Server 2013, o recurso Outlook em Qualquer Lugar, anteriormente conhecido como RPC sobre HTTP, permite que os clientes que utilizam o MicrosoftOutlook 2013, Outlook 2010 ou Outlook 2007 se conectem aos servidores do Exchange fora da rede corporativa ou pela Internet usando o RPC sobre componente de rede HTTP Windows. Este tópico descreve o recurso Outlook em Qualquer Lugar e lista os benefícios adquiridos com o uso do Outlook em Qualquer Lugar.

**Sumário**

Outlook em Qualquer Lugar e Exchange 2013

Benefícios do uso do Outlook em Qualquer Lugar

Implantando o Outlook em Qualquer Lugar

Gerenciando o Outlook em Qualquer Lugar

Coexistência do Outlook em Qualquer Lugar

Testando a conectividade do Outlook em Qualquer Lugar

## Outlook em Qualquer Lugar e Exchange 2013

O componente de RPC sobre Proxy HTTP do Windows, que os clientes do Outlook em Qualquer Lugar usam para se conectar, envolve as RPCs (chamadas de procedimento remoto) com uma camada HTTP. Isso permite que o tráfego desvie de firewalls de rede sem que as portas RPC estejam abertas. No Exchange 2013, esse recurso está habilitado por padrão porque o Exchange 2013 não permite a conectividade RPC direta.

## Benefícios do uso do Outlook em Qualquer Lugar

O Outlook em Qualquer Lugar oferece os seguintes benefícios para os clientes que usam o Outlook 2013, Outlook 2010 ou Outlook 2007 para acessar a infraestrutura de mensagens do Exchange:

  - Os usuários têm acesso remoto aos servidores do Exchange pela Internet.

  - Você pode usar a mesma URL e o mesmo namespace que usa para o Outlook Web App e o MicrosoftExchange ActiveSync.

  - Você pode usar o mesmo certificado de servidor SSL (Secure Sockets Layer) usado para o Outlook Web App e o Exchange ActiveSync.

  - Solicitações não autenticadas do Outlook não podem acessar servidores do Exchange.

  - Não é necessário usar uma VPN (rede virtual privada) para acessar servidores do Exchange pela Internet.

  - Se você já usa o Outlook Web App com SSL ou o Exchange ActiveSync com SSL, não é necessário abrir portas adicionais na Internet.

  - Você pode testar a conectividade de ponta a ponta de cliente para o Outlook em Qualquer Lugar e para conexões baseadas em TCP usando o cmdlet **Test-OutlookConnectivity**.

## Implantando o Outlook em Qualquer Lugar

No Exchange 2013, o Outlook em Qualquer Lugar está habilitado por padrão, pois toda a conectividade do Outlook acontece pelo Outlook em Qualquer Lugar. A única tarefa pós-implantação que deve ser realizada para utilizar com êxito o Outlook em Qualquer Lugar é instalar um certificado SSL válido no seu servidor de Acesso para Cliente. Os servidores de Caixa de Correio em sua organização exigem apenas o certificado SSL autoassinado padrão.

## Gerenciando o Outlook Anywhere

Você pode gerenciar o Outlook em Qualquer Lugar usando o centro de administração do Exchange ou o Shell de Gerenciamento do Exchange.

## Coexistência do Outlook em Qualquer Lugar

Se você planeja instalar o Exchange 2013 em um cenário de coexistência com versões anteriores do Exchange Server, talvez ainda tenha clientes do Outlook 2003 na sua organização. O cliente do Outlook 2003 não tem suporte no Exchange 2013.

Antes de mover seu namespace para o Exchange 2013, é necessário garantir que todos os clientes do Outlook tenham sido atualizados para as versões mínimas com suporte. O Outlook 2007 ou superior será necessário para uma conexão entre o Outlook em Qualquer Lugar e o Exchange 2013, mesmo se a caixa de correio de destino ainda estiver no Exchange 2007 ou Exchange 2010.

Se você estiver usando Outlook em qualquer lugar no seu Exchange 2007 ou 2010 ambientes, para permitir que o seu servidor de acesso de cliente do Exchange 2013 às conexões de proxy para seus servidores Exchange 2007/2010, você deve habilitar e configurar o Outlook Anywhere em todas as CAS do Exchange 2007/2010 em sua organização. Entretanto, se você não esteja usando o Outlook em qualquer lugar em seu ambiente do Exchange 2007/2010 e você não deseja iniciar a usá-lo, você não precisa habilitar o Outlook em qualquer lugar no ambiente herdado. Para obter instruções sobre como habilitar o Outlook em qualquer lugar para servidores de acesso para cliente executando o Exchange Server 2007, consulte [como habilitar o Outlook em qualquer lugar](https://go.microsoft.com/fwlink/p/?linkid=510497). Para obter instruções sobre como habilitar o Outlook em qualquer lugar para servidores de acesso para cliente executando o Exchange Server 2010, consulte [Habilitar o Outlook em qualquer lugar](https://go.microsoft.com/fwlink/p/?linkid=510502).

Ao habilitar o Outlook em Qualquer Lugar no Servidor de Acesso para Cliente, escolha NTLM para autenticação IIS.

Finalmente, configure o nome de host externo Outlook em qualquer lugar para apontar para o nome de host do Exchange 2013 Outlook Anywhere. Para obter instruções para o Exchange Server 2007, consulte [como configurar um nome de Host externo do Outlook em qualquer lugar](https://go.microsoft.com/fwlink/p/?linkid=510530). Para obter instruções para o Exchange Server 2010, consulte [Configure um nome de Host externo do Outlook em qualquer lugar](https://go.microsoft.com/fwlink/p/?linkid=510531).

## Testar a conectividade do Outlook em Qualquer Lugar

Você pode testar a conectividade de ponta a ponta do Outlook seguindo um destes procedimentos:

  - Executando o cmdlet **Test-OutlookConnectivity**. O cmdlet faz um teste para verificar se há conexões do Outlook em Qualquer Lugar (RPC sobre HTTP). Se o teste do cmdlet falhar, a saída indicará a etapa que falhou. Para obter a sintaxe e os parâmetros detalhados, confira [Test-OutlookConnectivity](https://technet.microsoft.com/pt-br/library/dd638082\(v=exchg.150\)).

  - Execute o teste de conectividade do Outlook em Qualquer Lugar usando o ExRCA (Analisador de Conectividade Remota do Exchange). Ao executar este teste, você obtém um resumo detalhado que mostra onde o teste falhou e quais etapas podem ser seguidas para corrigir os problemas. Para saber mais, confira [Analisador de Conectividade Remota do Exchange](exchange-remote-connectivity-analyzer-exchange-2013-help.md).

Os dois testes tentam entrar pelo Outlook em Qualquer Lugar depois de obter as configurações do servidor do serviço de Descoberta Automática. A verificação de ponta a ponta inclui:

  - Teste de conectividade de Descoberta Automática

  - Validação do DNS

  - Validação de certificados (se o nome do certificado corresponde ao site, se o certificado expirou e se ele é confiável)

  - Verificação da configuração correta do firewall (o ExRCA verifica a configuração geral do firewall. O cmdlet testa a configuração de firewall do Windows).

  - Confirmação da conectividade do cliente que entra na caixa de correio do usuário

