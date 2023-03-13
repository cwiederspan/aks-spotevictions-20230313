# AKS Spot Eviction Testing


``` bash

az login -t 16b3c013-d300-468d-ac64-7eda0820b6d3

az aks get-credentials -g cdw-akstesting-20230311 -n cdw-akstesting-20230311

kubectl get nodes

kubectl apply -f busybox.yaml

kubectl describe node aks-spot-29843220-vmss000002

kubectl exec --stdin --tty busybox -n testing -- sh

wget --header 'metadata: true' -qO- http://169.254.169.254/metadata/scheduledevents?api-version=2020-07-01

# Simulate eviction
az rest --method post --url https://management.azure.com/subscriptions/30c417b6-b3c1-4b62-94c9-0d3a80a182e9/resourceGroups/MC_cdw-akstesting-20230311_cdw-akstesting-20230311_southcentralus/providers/Microsoft.Compute/virtualMachineScaleSets/aks-spot-29843220-vmss/virtualMachines/2/simulateEviction?api-version=2022-11-01

# Reboot a node
az rest --method post --url https://management.azure.com/subscriptions/30c417b6-b3c1-4b62-94c9-0d3a80a182e9/resourceGroups/MC_cdw-akstesting-20230311_cdw-akstesting-20230311_southcentralus/providers/Microsoft.Compute/virtualMachineScaleSets/aks-spot-29843220-vmss/virtualMachines/2/simulateEviction?api-version=2022-11-01

```
