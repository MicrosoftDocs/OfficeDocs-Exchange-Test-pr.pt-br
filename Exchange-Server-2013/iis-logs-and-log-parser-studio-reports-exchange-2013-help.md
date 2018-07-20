---
title: 'Logs do IIS e relatórios do Log Parser Studio: Exchange 2013 Help'
TOCTitle: Logs do IIS e relatórios do Log Parser Studio
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63907499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Logs do IIS e relatórios do Log Parser Studio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

## Analisando os relatórios do Log Parser Studio

Log Parser Studio é um utilitário que permite que você pesquise e criar relatórios a partir de vários tipos de arquivos de log, incluindo aqueles para serviços de informações da Internet (IIS). Ele baseia-se na parte superior de Log Parser 2.2 e tem uma interface de usuário completa para facilitar a criação e gerenciamento de consultas do SQL relacionados.

[Baixe o Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244) e, em seguida, consulte a postagem no blog [Getting Started with Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524243).

Lembre-se que no Exchange 2013, todo o tráfego atravessar IIS. Isso significa analisar logs do IIS é a melhor maneira de obter uma imagem completa do número de conexões que estão visitando um servidor, de informações específicas de protocolo sobre as conexões e dos usuários que são mais impacto no desempenho. Mais de vinte novos relatórios foram desenvolvidos para Log Parser Studio, para fins de solução de problemas de desempenho do Exchange 2013.

## Log Parser Studio relatórios para o Exchange 2013 problemas de desempenho

Para obter uma compreensão abrangente de carga geral em seu ambiente do Exchange 2013, use os seguintes relatórios e comparar os números em relação a cada servidor.

Um arquivo. zip contendo os relatórios de Log Parser Studio listados aqui e os relatórios relacionados a solução de problemas adicionais, pode ser [baixado a partir daqui](https://go.microsoft.com/fwlink/p/?linkid=524245).

  - **IIS: solicitações por hora**. Feed nos logs do IIS do Site da Web padrão (W3SVC1 diretório) ou o site de back-end (W3SVC2 directory), mas não ambos, ao mesmo tempo.

  - **ACTIVESYNC\_WP: clientes por %**. Calcula todas as solicitações do ActiveSync, classificadas por agente do usuário e a porcentagem de cada cliente para o número total de solicitações.

  - **ACTIVESYNC\_WP: solicitações por hora (CSV)**. Lista as solicitações do ActiveSync por hora e envia os resultados para um arquivo CSV.

  - **ACTIVESYNC\_WP: solicitações por usuário (CSV)**. Lista de solicitações do ActiveSync por usuário e envia os resultados para um arquivo CSV.

  - **ACTIVESYNC\_WP: solicitações por usuário (10K superior)**. Lista solicitações de ActiveSync por usuário para os principais 10.000 usuários.

  - **ACTIVESYNC\_WP: principais dos participantes (CSV)**. Lista os clientes do ActiveSync superior do maior para menor contagem da solicitação e envia o resultado para um arquivo CSV.

  - **EWS\_WP: clientes por %**. Calcula todas as solicitações EWS classificadas por agente do usuário e a porcentagem de cada cliente para o número total de solicitações.

  - **EWS\_WP: solicitações por hora (CSV)**. Lista o número total de solicitações EWS por hora.

  - **EWS\_WP: solicitações por usuário (CSV)**. Lista de solicitações EWS por usuário e envia os resultados para um arquivo CSV.

  - **EWS\_WP: solicitações por usuário (superior 10K)**. Lista solicitações de EWS por usuário para os principais 10.000 usuários.

  - **EWS\_WP: Top dos participantes (CSV)**. Lista os clientes do EWS superior do valor mais alto a contagem de solicitações mais baixa.

  - **OLA\_WP: erros, por usuário, por hora, por dia**. Outlook em qualquer lugar usuários pelo número de solicitações.

  - **OLA\_WP: solicitações por hora**. Lista as solicitações do Outlook em qualquer lugar por hora.

  - **OLA\_WP: solicitações por hora, por usuário**. Lista as solicitações do Outlook em qualquer lugar por hora, por usuário.

  - **OLA\_WP: solicitações por usuário (CSV)**. Lista solicitações de Outlook em qualquer lugar por usuário.

  - **OLA\_WP: solicitações por usuário (10K superior)**. Lista solicitações de Outlook em qualquer lugar por usuário para os usuários da parte superior de 10.000.

  - **OLA\_WP: Top dos participantes**. Lista os principais Outlook em qualquer lugar clientes do valor mais alto para a contagem de solicitações mais baixa.

  - **OWA\_WP: clientes por %**. Calcula todas as solicitações do OWA, classificadas por agente do usuário e a porcentagem de cada cliente para o número total de solicitações.

  - **OWA\_WP: solicitações por hora (CSV)**. Lista as solicitações de OWA por hora e envia os resultados para um arquivo CSV.

  - **OWA\_WP: solicitações por usuário (CSV)**. Lista de solicitações do OWA por usuário e envia os resultados para um arquivo CSV.

  - **OWA\_WP: solicitações por usuário (superior 10K)**. Lista solicitações de OWA por usuário para os principais 10.000 usuários.

  - **OWA\_WP: Top dos participantes (CSV)**. Lista os clientes do OWA superior do maior para menor contagem da solicitação e envia o resultado para um arquivo CSV.

