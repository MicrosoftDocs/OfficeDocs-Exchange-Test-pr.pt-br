---
title: 'Servidores de Transporte de Borda: Exchange 2013 Help'
TOCTitle: Servidores de Transporte de Borda
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61203511
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servidores de Transporte de Borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-09-29_

Servidores de transporte de borda minimizam a superfície de ataque manipulando todos os fluxo de email na Internet, que fornece serviços de host inteligente para sua organização Exchange e retransmissão de SMTP (Simple Mail Transfer Protocol). Os agentes em execução no servidor de transporte de borda fornecem camadas adicionais de segurança e proteção de mensagem. Esses agentes oferecem proteção contra spam e aplicam regras de transporte para controlar o fluxo de emails.

Como o servidor de Transporte de Borda está instalado na rede de perímetro, ele nunca é membro da floresta interna do Active Directory de sua organização e não tem acesso às informações do Active Directory. No entanto, o servidor de Transporte de Borda exige os dados localizados no Active Directory, por exemplo, informações sobre o conector para fluxo de mensagens e informações sobre o destinatário para tarefas de pesquisa de destinatário antispam. Esses dados são sincronizados com o servidor de Transporte de Borda pelo serviço Microsoft Exchange EdgeSync (EdgeSync). O EdgeSync é uma coleção de processos em execução em um servidor de Caixa de Correio do Exchange 2013 com o objetivo de estabelecer a replicação unidirecional de informações sobre o destinatário e sobre a configuração do Active Directory para a instância do AD LDS (Active Directory Lightweight Directory Services) no servidor de Transporte de Borda. O EdgeSync copia apenas as informações que o servidor de Transporte de Borda precisa para executar tarefas de configuração antispam e para permitir o fluxo de mensagens completo. O EdgeSync executa atualizações agendadas para que as informações no AD LDS permaneçam atuais.

Você pode instalar mais de um servidor de Transporte de Borda na rede de perímetro. Implantar mais de um servidor de Transporte de Borda oferece recursos de redundância e failover para o seu fluxo de mensagens de entrada. Você pode fazer o balanceamento de carga do tráfego SMTP para sua organização entre os servidores de Transporte de Borda definindo mais de um registro MX com o mesmo valor de prioridade para seu domínio de email. Você pode obter consistência na configuração entre vários servidores de Transporte de Borda usando scripts de configuração clonada.

A função de servidor de Transporte de Borda permite que você gerencie os seguintes cenários de processamento de mensagens.

## Fluxo de mensagens da Internet

Os servidores de Transporte de Borda aceitam mensagens que chegam à organização do Exchange a partir da Internet. Após o processamento das mensagens pelo servidor de Transporte de Borda, o próximo roteamento dependerá da configuração de seus servidores internos do Exchange:

  - Se o servidor de Acesso para Cliente e o servidor de Caixa de Correio estiverem instalados em computadores separados, as mensagens serão roteadas para o serviço de Transporte no servidor de Caixa de Correio. O servidor de Acesso para Cliente será ignorado para o fluxo de mensagens SMTP de entrada.

  - Se o servidor de Acesso para Cliente e o servidor de Caixa de Correio estiverem instalados no mesmo computador, as mensagens serão roteadas ao serviço de Transporte front-end no servidor de Acesso para Cliente e, em seguida, para o serviço de Transporte no servidor de Caixa de Correio.

Todas as mensagens enviadas à Internet de dentro da organização são roteadas para servidores de Transporte de Borda depois que as mensagens são processadas pelo serviço de Transporte no servidor de Caixa de Correio. Você pode configurar o servidor de Transporte de Borda para usar o DNS para determinar os registros de recurso MX para domínios SMTP externos ou você pode configurar o servidor de Transporte de Borda para encaminhar mensagens para um host inteligente para resolução de DNS.

## Proteção antispam

Em Exchange 2013, recursos antispam fornecem serviços para bloquear emails comerciais não solicitadas (spam) no perímetro da rede.

Os spammers usam diversas técnicas para enviar spam para a sua organização. Os servidores de Transporte de Borda ajudam a evitar que os usuários recebam spam fornecendo uma coleção de agentes que trabalham juntos para oferecer diferentes camadas de filtragem e proteção contra spam. O estabelecimento de intervalos de tarpitting em conectores torna as tentativas de colheita de emails ineficazes.

## Regras de Transporte de Borda

As regras de Transporte de Borda são usadas para controlar o fluxo de mensagens enviadas ou recebidas da Internet. As regras de Transporte de Borda são configuradas em cada servidor de Transporte de Borda a fim de ajudar a proteger os recursos e os dados da rede corporativa, aplicando uma ação às mensagens que atendem às condições especificadas. As condições da regra de Transporte de Borda são baseadas em dados, como palavras ou padrões de texto específicos no assunto, corpo, cabeçalho ou endereço do remetente da mensagem, no SCL (nível de confiança de spam) ou no tipo de anexo. As ações determinam como a mensagem é processada quando uma condição especificada for verdadeira. As possíveis ações incluem quarentena de uma mensagem, eliminação ou rejeição de uma mensagem, anexo de destinatários adicionais ou log de um evento. Exceções opcionais isentam mensagens específicas da aplicação de uma ação.

## Reconfiguração de endereço

A reconfiguração de endereço apresenta uma aparência de endereço de email consistente aos destinatários externos. Defina a reconfiguração de endereço nos servidores de Transporte de Borda para modificar os endereços SMTP em mensagens de entrada e saída. A reconfiguração de endereço é especialmente útil para organizações que acabaram de realizar uma fusão e desejam apresentar uma aparência de endereço de email consistente.

Para obter mais informações sobre a reconfiguração de endereço, consulte [Reconfiguração nos servidores de transporte de borda de endereço](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

