---
title: 'Funções de servidor em implantações híbridas do Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Funções de servidor em implantações híbridas do Exchange 2013/Exchange 2007
ms:assetid: d7104efe-6d2a-4260-bc4e-f05da477e30b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn151302(v=EXCHG.150)
ms:contentKeyID: 54652005
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Funções de servidor em implantações híbridas do Exchange 2013/Exchange 2007

Este tópico está em andamento.  

_**Aplica-se a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Quando você configurar uma implantação híbrida em uma organização do Exchange 2007, deve instalar pelo menos um servidor do Exchange 2013 com as funções de servidor de Caixa de Correio e de Acesso para Cliente em sua organização existente do Exchange 2007. Seus servidores de Acesso para Cliente e de Caixa de Correio do Exchange 2013 coordenam as comunicações entre sua organização local existente do Exchange 2007 e a organização do Exchange Online. Essa comunicação inclui o transporte de mensagens e os recursos de mensagens entre a organização local e a organização do Exchange Online.

É altamente recomendada a instalação de mais de um servidor do Exchange 2013 em sua organização no local para ajudar a aumentar a confiabilidade e a disponibilidade dos recursos de implantação híbrida.

## Funções de servidor em uma implantação híbrida

Eis uma rápida visão geral das funções de servidor do Exchange 2013 em uma implantação híbrida:

  - **Função de servidor de Acesso do Cliente**   A função de servidor de Acesso para Cliente do Exchange 2013 continua a oferecer muitas das mesmas funções normalmente fornecidas por servidores de Acesso para Cliente do Exchange 2007 em sua organização com algumas adições necessárias para suportar uma implantação híbrida e coexistência com o Exchange 2007. O servidor de Acesso para Cliente também lida com mensagens de email seguras enviadas da organização do Exchange Online para a organização no local, assim como lida com as regras de transporte, políticas de registro no diário e entrega de mensagens para os servidores de Caixa de Correio em uma implantação híbrida. Um conector de Recebimento dedicado é configurado por padrão no servidor de Acesso para Cliente para suportar o transporte de email híbrido seguro. Toda a conectividade do cliente, incluindo o acesso para cliente do Outlook, o Outlook Web App e o Outlook em Qualquer Lugar, passa pela função de servidor Acesso para Cliente. Os recursos de relacionamento da organização entre as organizações locais e as organizações do Exchange Online, como compartilhamento de disponibilidade, também são tratados pela função de servidor de Acesso para Cliente.
    
    Saiba mais em [Servidor de Acesso para Cliente](https://technet.microsoft.com/pt-br/library/dd298114\(v=exchg.150\)).

  - **Função de servidor de caixa de correio**   A função de servidor de Caixa de Correio do Exchange 2013 lida com mensagens de email seguras enviadas para a organização do Exchange Online a partir da organização local. Embora não seja comum, ela também pode hospedar caixas de correio locais do destinatário e se comunicar com a organização do Exchange Online por proxy pelo servidor de Acesso de Cliente no local. Por padrão, um conector de Envio dedicado é configurado na função servidor de Caixa de Correio para suportar o transporte de email híbrido seguro.
    
    Saiba mais em [Servidor de Caixa de Correio](https://technet.microsoft.com/pt-br/library/jj150491\(v=exchg.150\)).

Dependendo da configuração de implantação híbrida que deseja, um servidor do Exchange 2013 exige uma ou ambas as funções de servidor para serem instaladas nele:

  - **Servidor do Exchange único**   Se você escolher instalar um único servidor do Exchange em sua organização local, você precisará instalar as funções de servidor de Acesso para Cliente e de Caixa de Correio no servidor único.

  - **Mais de um servidor do Exchange**   Se você escolher instalar mais de um servidor do Exchange em sua organização local, você pode instalar as funções de servidor em servidores separados em sua organização local. Por exemplo, você pode instalar um servidor do Exchange 2013 que possui as funções de Caixa de Correio e de Acesso para Cliente instaladas e também instalar outro servidor do Exchange que possui apenas a função de servidor de Acesso para Cliente instalada. No entanto, a prática recomendada e a configuração de servidor recomendada é instalar os servidores de Acesso para Cliente e de Caixa d Correio em *cada* servidor do Exchange 2013 implantado em sua organização local.

Saiba mais sobre o planejamento de capacidade do Exchange em [Noções Básicas Sobre Várias Configurações de Função de Servidor no Planejamento da Capacidade](http://go.microsoft.com/fwlink/?linkid=266576).

## Funcionalidade do Exchange Server em implantações híbridas

Servidores Exchange oferecem várias funções importantes para a sua organização local em uma implantação híbrida:

  - **Federação** Os servidores do Exchange 2013 permitem criar uma confiança de federação para sua organização local com o Microsoft Federation Gateway. O Microsoft Federation Gateway é um serviço gratuito baseado na nuvem oferecido pela Microsoft, atuando como agente de confiança entre a organização local e a organização locatária do Office 365. A federação é requisito para a criação de um relacionamento de organização entre a organização local e a organização do Exchange Online.
    
    Saiba mais em [Federação](https://technet.microsoft.com/pt-br/library/dd335047\(v=exchg.150\)).

  - **Relacionamentos de organização**   Os servidores do Exchange 2013 com a função de servidor de Acesso para Cliente permitem a criação dos relacionamentos da organização entre as organizações local e do Exchange Online. Os relacionamentos de organização são necessários para muitos outros serviços em uma implantação híbrida, incluindo compartilhamento de informações de disponibilidade de calendário, acompanhamento de mensagens e movimentações de caixa de correio entre a organização local e a organização do Exchange Online.
    
    Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

  - **Transporte de mensagem**   Os servidores do Exchange 2013 com funções de servidor de Acesso para Cliente e Caixa de Correio são responsáveis pelo transporte de mensagens em uma implantação híbrida. Usando conectores de Envio e Recebimento, eles servem como ponto de extremidade de conexão para mensagens externas de entrada e também oferecem a entrega de mensagens de saída para a Internet e a organização do Exchange Online.
    
    Saiba mais em [Opções de transporte em implantações híbridas do Exchange 2013/Exchange 2007](transport-options-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

  - **Segurança de transporte de mensagens**   Os servidores do Exchange 2013 com a função de servidor de Acesso para Cliente e de Caixa de Correio ajudam a proteger a comunicação de mensagens entre a organização local e a organização do Exchange Online usando a funcionalidade de Segurança de Domínio no Exchange 2013. A segurança pode ser aumentada usando autenticação de segurança de camada de transporte mútua e criptografia para comunicações de mensagens.
    
    Saiba mais em [Noções básicas sobre segurança de domínio](http://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook Web App**   Servidores do Exchange 2013 com a função de servidor de Acesso para Cliente suportam a configuração de um único ponto de extremidade de URL para conexões externas para caixas de correio local e do Exchange Online. Para caixas de correio locais, os servidores de Acesso para Cliente são configurados para solicitações do Outlook Web App de serviço. Para caixas de correio da organização do Exchange Online, os servidores de Acesso para Cliente são configurados para exibir automaticamente um link para o ponto de extremidade do Outlook Web App na organização do Exchange Online.
    
    Saiba mais em [Outlook Web App](https://technet.microsoft.com/pt-br/library/jj657718\(v=exchg.150\)).

## Topologia do servidor do Exchange

Se você adicionar servidores adicionais do Exchange 2013 para suportar sua implantação híbrida, o servidor do Exchange será implantado de maneira muito semelhante que qualquer outro servidor do Exchange seria implantado em sua organização existente do Exchange 2007. Configurar sua organização do Exchange 2007 local existente para uma implantação híbrida não exige nenhuma topologia especial do servidor do Exchange. No entanto, você deve instalar o Exchange 2007 Service Pack 3 (SP3) com pacote cumulativo de atualizações 10 em seus servidores do Exchange 2007 e, também, instalar o Exchange 2013 com atualização cumulativa 1 (CU1) ou superior para permitir a compatibilidade e a funcionalidade híbrida completas com o Office 365.

A tabela a seguir descreve brevemente as alterações nos serviços após a implantação híbrida.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Serviço</th>
<th>Antes da implantação híbrida</th>
<th>Após a implantação híbrida</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transporte de mensagens (entrada e saída)</p></td>
<td><p>Servidor de Acesso para Cliente do Exchange 2007</p></td>
<td><p>Servidor de Acesso para Cliente Exchange 2013 ou Exchange Online Protection (EOP) incluído com o Office 365</p></td>
<td><p>O registro MX (servidor de mensagens) para o domínio pode permanecer inalterado ou ser atualizado para apontar para o EOP.</p></td>
</tr>
<tr class="even">
<td><p>URL pública do Outlook Web App</p></td>
<td><p>Servidor de Acesso para Cliente do Exchange 2007</p></td>
<td><p>Servidor de Acesso para Cliente Exchange 2013</p></td>
<td><p>O proxy de servidores de Acesso para Cliente do Exchange 2013 Outlook Web App solicita caixas de correio no local aos servidores do Acesso para Cliente do Exchange 2007. As solicitações do Outlook Web App para caixas de correio hospedadas no Exchange Online são fornecidas com um link para a URL do Outlook Web App do Exchange.</p></td>
</tr>
</tbody>
</table>


## Software de servidor do Exchange

A CU1 ou superior do Exchange 2013 habilita a funcionalidade de implantação híbrida com o assistente de Configuração Híbrida. É possível usar qualquer mídia da CU1 ou superior do Exchange 2013 instalando os servidores do Exchange 2013 adicionais.

Para obter informações sobre como baixar a versão mais recente do Exchange 2013, consulte [Atualizações para Exchange 2013](http://technet.microsoft.com/library/jj907309).


> [!IMPORTANT]
> Você deve licenciar o servidor híbrido quando configurar uma implantação híbrida com o Exchange 2013 ou o 2010 e com o Office 365. Para obter uma chave do produto (Product Key) gratuita do Exchange Server para usar na configuração de uma implantação híbrida, use a <A href="https://aka.ms/hybridkey">ferramenta Chave do Produto para Edição Híbrida</A>.


