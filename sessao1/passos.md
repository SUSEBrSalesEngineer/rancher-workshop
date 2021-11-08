## Sessão 1 - Criando o cluster Kubernetes e Rancher
Para seguir o passo a passo correto, escolher a opção do provider que deseja utilizar.
A SUSE entrega três opções de provisionadores de cluster Kubernetes e você pode escolher a que melhor lhe atende: [K3S](https://rancher.com/docs/k3s/latest/en/) | [RKE](https://rancher.com/docs/rke/latest/en/) | [RKE2](https://rancher.com/docs/rancher/v2.5/en/installation/resources/k8s-tutorials/ha-rke2/). 

> *Para entender sobre a diferença de cada um deles, e escolher qual melhor lhe atende, consulte a equipe de pré-vendas da SUSE.* <br/>
----
Nessa sessão, utilizaremos o RKE pra provisionar o nosso cluster:

### Preparacão
Para iniciar o processo, a máquina deve estar com algumas definicões checadas.
Siga o procedimento abaixo antes de seguir para a próxima sessão:

1. Certificar que o swap está desativado e remover respectiva linha do fstab:
```
sudo swapoff -a
sudo vim /etc/fstab
```
2. Adicionar os módulos presentes em modulos.conf no seguinte arquivo:
```
vim /etc/modules-load.d/modules.conf
```

1. Instalar k3s via script automatizado
```
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE=0644 sh -
```
Outros parâmetros podem ser passados ao script de instalação como alterar a rede, escolher a versão do Kubernetes.<br/> Veja as demais opções nesse [link](https://rancher.com/docs/k3s/latest/en/installation/install-options/)

2. Aguardar a inicialização de todos os pods do Kubernetes. Esse tempo é necessário para que todos os componentes subam com êxito.<br/>
O processo pode ser acompanhado através do comando: 
```
kubectl get pods -A
```
Caso todos os componentes apareçam como "Running" ou "Completed", você está pronto para ir para o próximo ponto.

3. 
