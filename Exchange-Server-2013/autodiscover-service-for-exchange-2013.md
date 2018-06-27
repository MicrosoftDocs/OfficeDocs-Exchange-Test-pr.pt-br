---
title: 'Serviço de descoberta automática: Exchange 2013 Help'
TOCTitle: Serviço de descoberta automática
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50556262
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serviço de descoberta automática

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Saiba mais sobre o serviço de Descoberta Automática do Exchange para o Microsoft Exchange 2013. Você verá o que o serviço de Descoberta Automática do Exchange faz e como ele funciona, bem como quais são as opções de implantação.

Microsoft O Exchange 2013 contém um serviço chamado Descoberta Automática. Este tópico fornece uma visão geral do serviço e explica como ele funciona, configura clientes do Outlook e quais opções estão disponíveis para implantar o serviço de Descoberta Automática em seu ambiente de mensagens.

O serviço de Descoberta Automática:

  - Configura automaticamente as definições de perfil do usuário para clientes que executam o Microsoft, o Office Outlook 2007, o Outlook 2010 ou o Outlook 2013, bem como celulares com suporte. Telefones que executam o Windows Mobile 6.1 ou posterior têm suporte. Se você não possui um celular Windows, verifique a documentação do seu celular para saber se ele tem suporte.

  - Fornece acesso a recursos do Exchange para clientes Outlook 2007, Outlook 2010 ou Outlook 2013 conectados ao seu ambiente de mensagens do Exchange.

  - Usa um endereço de email e uma senha do usuário para fornecer as configurações de perfil para clientes do Outlook 2007, do Outlook 2010 ou do Outlook 2013 e celulares com suporte. Se o cliente do Outlook ingressar no domínio, a conta de domínio do usuário será usada.

**Sumário**

Visão geral do serviço de Descoberta Automática

Como funciona o serviço Descoberta Automática

Opções de implantação do serviço de Descoberta Automática

Configurar a Descoberta Automática para movimentações entre florestas

## Visão geral do serviço de Descoberta Automática

O serviço de Descoberta Automática facilita a configuração do Outlook 2007, do Outlook 2010 ou do Outlook 2013 e alguns telefones celulares. Você não pode usar o serviço de Descoberta Automática com versões do Outlook anteriores à Office Outlook 2007. Em versões anteriores do Microsoft Exchange (Exchange 2003 SP2 ou anterior) e Outlook  (Outlook 2003 ou anterior), era necessário configurar todos os perfis de usuários manualmente para acessar o Exchange. Era necessário um esforço extra para gerenciar esses perfis caso ocorressem mudanças no ambiente do sistema de mensagens. Caso contrário, os clientes do Outlook parariam de funcionar corretamente.

Usando a Descoberta Automática, o Outlook encontra um novo ponto de conexão criado pela GUID da caixa de correio do usuário + @ + a parte de domínio do endereço SMTP principal do usuário. O serviço de Descoberta Automática retorna as seguintes informações para o cliente:

  - O nome de exibição do usuário

  - Configurações de conexões separadas para conectividade interna e externa

  - A localização do servidor da Caixa de Correio do usuário.

  - As URLs de diversos recursos do Outlook que controlam funcionalidades como informações de disponibilidade, Unificação de Mensagens e catálogo de endereços offline

  - Configurações do servidor do Outlook em Qualquer Lugar

Quando as informações do Exchange de um usuário são alteradas, o Outlook reconfigura automaticamente o perfil do usuário por meio do serviço de Descoberta Automática. Por exemplo, se a caixa de correio de um usuário for movida ou se o cliente não conseguir se conectar à caixa de correio do usuário ou aos recursos do Exchange disponíveis, o Outlook entrará em contato com o serviço de Descoberta Automática e atualizará automaticamente o perfil do usuário, para incluir as informações necessárias para a conexão com a caixa de correio e com os recursos do Exchange.

Voltar ao início

## Como funciona o serviço Descoberta Automática

Ao instalar um servidor de Acesso para Cliente no Exchange 2013, um diretório virtual padrão chamado Descoberta Automática é criado no site padrão, no IIS (Serviços de Informações da Internet). Esse diretório virtual trata das solicitações do serviço de Descoberta Automática de clientes do Outlook 2007, Outlook 2010 e Outlook 2013, e telefones celulares aceitos nas seguintes circunstâncias:

  - Quando uma conta de usuário é configurada ou atualizada

  - Quando um cliente Outlook verifica periodicamente as alterações nas URLs dos Serviços Web do Exchange

  - Quando ocorrem alterações de conexão da rede subjacente em seu ambiente de sistema de mensagens do Exchange

Além disso, é criado um novo objeto do Active Directory, chamado ponto de conexão de serviço (SCP), no servidor onde a função de servidor Acesso para Cliente foi instalada.

O objeto SCP contém a lista autoritativa de URLs do serviço de Descoberta Automática para a floresta. Você pode usar o cmdlet **Set-ClientAccessServer** para atualizar o objeto SCP. Para saber mais, consulte [Set-ClientAccessServer](https://technet.microsoft.com/pt-br/library/bb125157\(v=exchg.150\)).


> [!IMPORTANT]
> Antes de executar o cmdlet <STRONG>Set-ClientAccessServer</STRONG>, certifique-se de que a conta Usuários Autenticados no servidor de Acesso para Cliente tem permissões de Leitura no objeto SCP. Se os usuários não tiverem as permissões corretas, não poderão pesquisar ou ler itens.



Para saber mais sobre os objetos do SCP, consulte [Publicar com pontos de conexão de serviço](https://go.microsoft.com/fwlink/p/?linkid=72744).

Para acesso externo, ou usando DNS, o cliente localiza o serviço de Descoberta Automática na Internet usando o endereço de domínio SMTP primário do endereço de email do usuário.


> [!TIP]
> Você deve fornecer um registro de recurso do serviço de host (SRV) no DNS para clientes do Outlook para descobrir o serviço de Descoberta Automática usando DNS. Para obter mais informações, consulte a documentação do Windows sobre configuração do DNS e <A href="https://go.microsoft.com/fwlink/p/?linkid=85214">White Paper: Serviço de Descoberta Automática do Exchange 2007</A>.



Dependendo de o serviço de Descoberta Automática estar configurado ou não em um site separado, a URL do serviço de Descoberta Automática será https://\<*smtp-address-domain*\>/autodiscover/autodiscover.xml ou https://autodiscover.\<*smtp-address-domain*\>/autodiscover/autodiscover.xml, em que ://\<*smtp-address-domain*\> é o endereço de domínio SMTP principal. Por exemplo, se o endereço de email do usuário for davi@contoso.com, o endereço de domínio SMTP principal é contoso.com. Ao se conectar ao Active Directory, o cliente procura o objeto SCP criado durante a Instalação. Nas implantações que abrangem diversos servidores de Acesso para Cliente, é criado um objeto SCP de Descoberta Automática para cada servidor de Acesso para Cliente. O objeto SCP contém o atributo *ServiceBindingInfo*, que possui o nome de domínio totalmente qualificado (FQDN) do servidor de Acesso para Cliente na forma de https://CAS01/autodiscover/autodiscover.xml, onde CAS01 é o FQDN desse servidor. Usando as credenciais do usuário, o cliente do Outlook 2007, do Outlook 2010 ou do Outlook 2013 é autenticado no Active Directory e procura objetos SCP da Descoberta Automática. Depois de obter e enumerar as instâncias do serviço de Descoberta Automática, o cliente se conecta ao primeiro servidor de Acesso para Cliente na lista enumerada e obtém as informações do perfil na forma de dados XML, necessários para conexão com a caixa de correio do usuário e com os recursos do Exchange disponíveis.

Voltar ao início

## Opções de implantação do serviço de Descoberta Automática

O serviço de Descoberta Automática deve ser implantado e configurado corretamente para que clientes Outlook 2007, Outlook 2010 e Outlook 2013 se conectem automaticamente a recursos do Exchange, como o catálogo de endereços offline, o serviço de Disponibilidade e a UM (Unificação de Mensagens). A implantação do serviço de Descoberta Automática é apenas uma etapa para garantir que seus serviços do Exchange, como o serviço de Disponibilidade, possam ser acessados por clientes do Outlook 2007, do Outlook 2010 ou do Outlook 2013.

## Configurar a Descoberta Automática para movimentações entre florestas

O serviço de Descoberta Automática pode fornecer informações de perfil para conectar clientes Outlook em caixas de correio que foram movidas de uma floresta do Exchange para outra. Para que isso aconteça, você deve configurar um usuário habilitado para email tanto na floresta original onde a caixa de correio do usuário residia quanto na floresta de destino usando o cmdlet **New-MailUser**. Na floresta de origem, você deve usar o parâmetro *ExternalEmailAddress* no cmdlet para especificar o novo endereço de email da caixa de correio na floresta de destino. Para saber mais, consulte [New-MailUser](https://technet.microsoft.com/pt-br/library/aa996335\(v=exchg.150\)).

Ao configurar um usuário habilitado para email, o serviço de Descoberta Automática na floresta de original redirecionará o usuário a ser autenticado para o novo endereço de email na floresta de destino. O cliente Outlook que está se conectando será então redirecionado para o servidor de Acesso para Cliente na floresta de destino para onde a caixa de correio foi movida.

Voltar ao início

