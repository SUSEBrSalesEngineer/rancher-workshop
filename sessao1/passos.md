## Sessão 1 - Criando o cluster Kubernetes e Rancher
Para seguir o passo a passo correto, escolher a opção do provider que deseja utilizar.
A SUSE entrega três opções de provisionadores de cluster Kubernetes e você pode escolher a que melhor lhe atende: [K3S](https://rancher.com/docs/k3s/latest/en/) | [RKE](https://rancher.com/docs/rke/latest/en/) | [RKE2](https://rancher.com/docs/rancher/v2.5/en/installation/resources/k8s-tutorials/ha-rke2/). 

> *Para entender sobre a diferença de cada um deles, e escolher qual melhor lhe atende, consulte a equipe de pré-vendas da SUSE.* <br/>
----
Nessa sessão, utilizaremos o RKE pra provisionar o nosso cluster:

### Preparacão
Para iniciar o processo, a máquina deve estar com algumas definicões checadas.
Siga o procedimento abaixo antes de seguir para a próxima sessão:
> OBS: Não use o root para executar os comandos

1. Certificar que o swap está desativado e remover respectiva linha do fstab:
```
sudo swapoff -a
sudo vim /etc/fstab
```
2. Adicionar os módulos presentes em [modulos.conf](https://github.com/SUSEBrSalesEngineer/rancher-workshop/blob/main/sessao1/modules.conf) no seguinte arquivo:
```
vim /etc/modules-load.d/modules.conf
```

3. Adicionar o seu usuário ao sudoers da máquina
```
echo "$USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
```

4. Como usuário normal, criar keygen para todos os nós, apertando ENTER para selecionar as opções default
```
ssh-keygen -t rsa -b 4096
eval `ssh-agent`
ssh-add
```

5. Na mesma máquina, copiar a chave recém-criada no passo anterior
```
ssh-copy-id
```

6. Adicionar a seguinte linha no arquivo de sysctl
```
vim /etc/sysctl.conf
net.bridge.bridge-nf-call-iptables=1
```

7. Reiniciar a máquina!<br/> Após reinicializacão, verificar se os módulos foram carregados e aplicar configuracão do sysctl (passos 2 e 6)
```
sysctl -p 

for module in br_netfilter ip6_udp_tunnel ip_set ip_set_hash_ip ip_set_hash_net iptable_filter iptable_nat iptable_mangle iptable_raw nf_conntrack_netlink nf_conntrack nf_conntrack_ipv4   nf_defrag_ipv4 nf_nat nf_nat_ipv4 nf_nat_masquerade_ipv4 nfnetlink udp_tunnel veth vxlan x_tables xt_addrtype xt_conntrack xt_comment xt_mark xt_multiport xt_nat xt_recent xt_set  xt_statistic xt_tcpudp;
     do
       if ! lsmod | grep -q $module; then
         echo "module $module is not present";
       fi;
     done
```

8. Permitir o TCP Forwarding no arquivo de SSH, removendo o comentário da linha "AllowTcpForwarding yes"
```
vim /etc/ssh/sshd_config
AllowTcpForwarding yes
```

9. Caso a máquina esteja dentro de uma regra do firewall, certificar de que o procedimento de abertura de portas foi realizada.

> Para mais detalhes do processo de preparacão das máquinas, acessar a [página do RKE](https://rancher.com/docs/rke/latest/en/os/) no site da Rancher: 


### Criar o cluster e preparar o Rancher
Após procedimento de preparacão da máquina, estamos prontos para criar o nosso cluster.
Esse procedimento está descrito no seguinte [link](https://rancher.com/docs/rke/latest/en/installation/), e pode ser usado para maiores detalhes.
