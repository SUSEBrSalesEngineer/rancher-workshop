## Sessão 2 - Adicionando outros clusters ao Rancher
Essa sessão visa adicionar um cluster secundário ao nosso Rancher Management.
Caso você já possua o seu cluster secundário criado, pular para a sessão [Adicionando o cluster ao Rancher](https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/sessao2/passos.md#adicionar-cluster-ao-rancher).

### Criar um cluster Kubernetes com K3s
Dessa vez, utilizaremos o K3s para criar o nosso cluster secundário.
Diferente da sessão 1, esse procedimento é realizado através de um único script executável.

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

3. (OPCIONAL) Caso queira adicionar mais um nó ao seu cluster K3s, o procedimento é simples.
```
curl -sfL https://get.k3s.io | K3S_URL=https://<FQDN>:6443 K3S_TOKEN=<TOKEN> sh -
```
A chave está dentro do arquivo /var/lib/rancher/k3s/server/node-token

---
### Adicionar cluster ao Rancher
Com o cluster criado, é fácil adicioná-lo ao Rancher

<p>
  <img src="https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/img/add-cluster.gif" width="130" title="Add cluster">
</p>
