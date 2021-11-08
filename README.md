# Rancher Workshop

<p>
  <img src="https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/img/rancher-logo-horiz-color.png" width="150" title="Rancher Logo">
  <img src="https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/img/SUSE_Logo-hor_L_Green-pos_sRGB-720x240-9ebdc54a-3ee7-4747-87fa-edef424f9b36.png" width="130" title="SUSE Logo">
</p>

## Descrição
O seguinte documento descreve os pré-requisitos mínimos para a construção de um ambiente de teste envolvendo a solução Rancher Management. As recomendações mínimas aqui contidas cobrem um cenário apenas de teste e validação da ferramenta, não sendo recomendadas para um ambiente de produção.

## Pré-requisito
### Máquinas
Será necessário um cluster inicial de Rancher e um segundo equipamento para instalação do cluster cliente. <br/> Para tal, será requerido as seguintes configurações para o Cluster SUSE Rancher e o Cluster cliente:

Quantidade | Item | Características
| :---: | :---: | :---
2 | IP elásticos na Amazon | Acesso ao Rancher, em caso do Racher ser instalado em cloud 
1 | IP válido para uso do LoadBalancer (MetalLB) | Separação de um range de 3 IPs para deploy de aplicação teste 
1 | Máquina | *On-prem ou na nuvem* <br/> - 64 bits <br/> - RAM: 8 GB <br/> - Processadore(s) ou Core(s): 2 <br/> - Disco: 40 GB <br/> - Rede IPv4 – 1 IP com conectividade ao cliente para a PoC.   <br/>  - **Ou t3-medium na aws**
1 | Máquina para deployment | *On-prem ou na nuvem*. <br/> Pode ser utilizada a máquina pessoal do administrador <br/> - 64 bits <br/> - RAM: 4 GB <br/> - Processadore(s) ou Core(s): 2 <br/> - Disco: 30 GB <br/> - Rede IPv4 – 1 IP com conectividade ao cliente para a PoC.   <br/>  - **Ou t3-medium na aws**
1 | Máquina para cluster adicional | *On-prem ou na nuvem*. - 64 bits <br/> - RAM: 16 GB <br/> - Processadore(s) ou Core(s): 4 <br/> - Disco: 100 GB <br/> - Rede IPv4 – 1 IP com conectividade ao cliente para a PoC.   <br/>  - **Ou t3-medium na aws**

### Conectividade de rede e acessos:
Caso o ambiente a ser testado esteja dentro do perímetro do firewall, serão necessárias as seguintes regras de liberação de portas no Firewall para comunicação do SUSE Rancher Cluster cliente e serviços externos de instalação: [Rancher Requirements Ports](https://rancher.com/docs/rancher/v2.x/en/installation/requirements/ports/)

<p align="center">
<img src="https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/img/rancher-ports.PNG" width="650" title="Rancher Ports">
</p>

## Exemplo
- Exemplo de estrutura de comunicação do SUSE Rancher
<p align="center">
<img src="https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/img/rancher-structure.PNG" width="350" title="Rancher Ports">
</p>

## Agenda
**Sessão 1**: [Criação do cluster Kubernetes e Rancher](sessao1/passos.md)<br/>
**Sessão 2**: [Adicionar um cluster secundário no Rancher](sessao2/passos.md)<br/>
**Sessão 3**: [Deploy de aplicações](sessao3/passos.md)<br/>
