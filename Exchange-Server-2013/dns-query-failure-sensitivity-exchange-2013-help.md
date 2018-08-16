---
title: 'Sensibilidade de falha de consulta DNS: Exchange 2013 Help'
TOCTitle: Sensibilidade de falha de consulta DNS
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52058864
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sensibilidade de falha de consulta DNS

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-12-02_

No Microsoft Exchange Server 2013, você pode ajustar a sensibilidade de consulta DNS para entrega de mensagem ligeiramente mais rápida quando erros DNS são encontrados para o domínio de destino. No entanto, dependendo de erros DNS, esse ajuste pode causar falhas de entrega em determinadas circunstâncias.

## Consultas DNS e entrega de mensagens remotos

O servidor Exchange responsável para entrega de mensagens para destinatários externos deve ser capaz de localizar um servidor de mensagens de destino que aceite correio para os destinatários externos. Dependendo do destino, as mensagens são colocadas em uma ou mais filas de entrega remota enquanto aguardam entrega aos destinatários remotos. Para obter mais informações sobre as filas de entrega, consulte [Filas](queues-exchange-2013-help.md).

O Exchange server consulta os servidores DNS configurados para localizar os registros DNS necessários para entregar a mensagem. Os servidores DNS serão consultados na ordem em que estão listadas. Se um dos servidores DNS não estiver disponível, a consulta vai para o próximo servidor DNS na lista. Os servidores DNS são consultados para as seguintes informações:

  - **Registros do exchange (MX) de email para a parte de domínio do destinatário externo**   O registro MX contém o nome de domínio totalmente qualificado (FQDN) do servidor de mensagens é responsável por aceitar mensagens para o domínio e um valor de preferência para esse servidor de mensagens. Um valor mais baixo de preferência indica um servidor de mensagens preferencial. O valor de preferência é importante se o domínio possuir mais de um registro MX. Para otimizar a tolerância a falhas, a maioria das organizações usa vários servidores de mensagens e vários registros MX que possuem valores de preferência diferentes.

  - **Registros de endereço (A) para os servidores de mensagens de destino**   Cada servidor de mensagens é usado em um registro MX deve ter um registro correspondente. O registro é usado para localizar o endereço IP do servidor de mensagens de destino. O servidor de transporte de borda inscrito usa o endereço IP para abrir uma conexão SMTP com o servidor de mensagens de destino. Embora seja tecnicamente possível usar o FQDN de um nome canônico (CNAME) registro em um registro MX, essa prática viola RFC 974, RFC 1034, RFC 1912 e RFC 2181 e, portanto, não é suportada pelos servidores mais mensagens.
    
    A combinação necessária de consultas DNS interativas e consultas DNS recursivas que começam com um servidor DNS raiz é usada para resolver o FQDN do servidor de mensagens que for encontrado no registro MX em um endereço IP.

Exchange 2013, há um limite de consulta DNS não é configurável de 5 segundos para cada servidor DNS e um limite de um minuto para toda a consulta DNS.

## Possíveis problemas DNS

Mesmo quando as configurações de DNS no servidor do Exchange estão configuradas corretamente, problemas com os registros DNS para um domínio específico ou com qualquer um dos servidores DNS que são usados para localizar o servidor DNS autoritativo para um domínio específico ainda pode ocorrer. Em geral, esses problemas são além de seu controle e precisam ser resolvidos por ambas as partes que possuem esses servidores DNS. Esses erros relacionados ao DNS podem ser causados por uma ou mais das seguintes condições:

  - Registros DNS inválidos para o domínio de destino

  - Problemas com a utilização do servidor DNS

  - Problemas com a replicação do servidor DNS

Em Exchange 2013, quando uma consulta DNS resulta em erros, a consulta continua o próximo servidor DNS se o servidor DNS não tiver já retornado um erro quando a consulta atual.

Você pode controlar a sensibilidade de falha de consulta DNS, modificando o arquivo de configuração de aplicativo XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config` . Esse arquivo está associado ao serviço de transporte do Microsoft Exchange. Você pode salvar esse arquivo de alterações são aplicadas depois que você reiniciar o serviço de transporte do Microsoft Exchange. Quando você reiniciar esse serviço, o fluxo de emails no servidor é interrompido temporariamente. A sensibilidade de falha de consulta DNS é controlada pela chave *DnsFaultTolerance* no arquivo EdgeTransport.exe.config. Essa chave usa os seguintes valores:

  - **Branda**   Quando a consulta DNS encontra uma combinação de registros de MX válidos e os registros MX inválidos, a consulta DNS continua até que o valor de tempo limite de consulta DNS de um minuto for atingido. Os registros MX inválidos são descartados e o registro MX válido que tem o valor mais baixo de preferência é usado para enviar uma mensagem para o servidor de mensagens de destino. Este é o valor padrão.

  - **Normal**   Quando a consulta DNS primeiro encontra um registro MX inválido, qualquer resolvido registros MX que têm um valor de preferência for maior que ou igual aos registros MX inválidos imediatamente são descartadas. O registro MX restante que tem o valor mais baixo de preferência é usado para enviar uma mensagem para o servidor de mensagens de destino sem esperar por toda a consulta DNS para o tempo limite. Embora esse comportamento pode resultar em entrega de mensagens mais rápida, provável obstáculo desse comportamento é que a consulta DNS não pode ter nenhum registro MX válida se as seguintes condições forem verdadeiras:
    
      - O registro MX inválido é o primeiro registro MX para o domínio de destino.
    
      - Os registros MX válidos têm o mesmo valor de precedência como os registros MX inválidos.

No modo de `Normal` e `Lenient` modo, nunca em cache os resultados da consulta DNS para um registro MX inválido. Na próxima vez que uma consulta DNS é executada, ele tentará resolver os registros MX para o domínio de destino.


> [!NOTE]
> Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.


