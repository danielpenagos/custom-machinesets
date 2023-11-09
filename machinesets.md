AZR_CLUSTER=aro-dpenagos
SUFFIX=p8vzw
AZR_RESOURCE_LOCATION=eastus
VNET_RESOURCE_GROUP=dpenagos-blob
AZR_ARO_VNET=aro-dpenagos-aro-vnet-eastus
AZR_CLUSTER_RESOURCE_GROUP=aro-blob-rg
AZR_ARO_SUBNET_WORKER=aro-dpenagos-aro-machine-subnet-eastus

echo $AZR_CLUSTER
echo $SUFFIX
echo $AZR_RESOURCE_LOCATION
echo $VNET_RESOURCE_GROUP
echo $AZR_ARO_VNET
echo $AZR_CLUSTER_RESOURCE_GROUP
echo $AZR_ARO_SUBNET_WORKER

oc get machineset -n openshift-machine-api

cat <<EOF | oc create -f -
apiVersion: machine.openshift.io/v1beta1
kind: MachineSet
metadata:
  annotations:
    machine.openshift.io/GPU: '0'
    machine.openshift.io/memoryMb: '8192'
    machine.openshift.io/vCPU: '4'
  name: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}1
  generation: 1
  namespace: openshift-machine-api
  labels:
    machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
    machine.openshift.io/cluster-api-machine-role: worker
    machine.openshift.io/cluster-api-machine-type: worker
spec:
  replicas: 1
  selector:
    matchLabels:
      machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
      machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}1
  template:
    metadata:
      labels:
        machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
        machine.openshift.io/cluster-api-machine-role: worker
        machine.openshift.io/cluster-api-machine-type: worker
        machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}1
    spec:
      lifecycleHooks: {}
      metadata: {}
      providerSpec:
        value:
          osDisk:
            diskSettings: {}
            diskSizeGB: 256
            managedDisk:
              storageAccountType: Premium_LRS
            osType: Linux
          networkResourceGroup: ${VNET_RESOURCE_GROUP}
          publicLoadBalancer: ${AZR_CLUSTER}-${SUFFIX}
          userDataSecret:
            name: worker-user-data
          vnet: ${AZR_ARO_VNET}
          credentialsSecret:
            name: azure-cloud-credentials
            namespace: openshift-machine-api
          diagnostics: {}
          zone: '1'
          metadata:
            creationTimestamp: null
          publicIP: false
          resourceGroup: ${AZR_CLUSTER_RESOURCE_GROUP}
          kind: AzureMachineProviderSpec
          location: ${AZR_RESOURCE_LOCATION}
          vmSize: Standard_F4s_v2
          image:
            offer: aro4
            publisher: azureopenshift
            resourceID: ''
            sku: aro_412
            version: 412.86.20230503
          acceleratedNetworking: true
          subnet: ${AZR_ARO_SUBNET_WORKER}
          apiVersion: machine.openshift.io/v1beta1

---

apiVersion: machine.openshift.io/v1beta1
kind: MachineSet
metadata:
  annotations:
    machine.openshift.io/GPU: '0'
    machine.openshift.io/memoryMb: '8192'
    machine.openshift.io/vCPU: '4'
  name: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}2
  generation: 1
  namespace: openshift-machine-api
  labels:
    machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
    machine.openshift.io/cluster-api-machine-role: worker
    machine.openshift.io/cluster-api-machine-type: worker
spec:
  replicas: 1
  selector:
    matchLabels:
      machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
      machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}2
  template:
    metadata:
      labels:
        machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
        machine.openshift.io/cluster-api-machine-role: worker
        machine.openshift.io/cluster-api-machine-type: worker
        machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}2
    spec:
      lifecycleHooks: {}
      metadata: {}
      providerSpec:
        value:
          osDisk:
            diskSettings: {}
            diskSizeGB: 256
            managedDisk:
              storageAccountType: Premium_LRS
            osType: Linux
          networkResourceGroup: ${VNET_RESOURCE_GROUP}
          publicLoadBalancer: ${AZR_CLUSTER}-${SUFFIX}
          userDataSecret:
            name: worker-user-data
          vnet: ${AZR_ARO_VNET}
          credentialsSecret:
            name: azure-cloud-credentials
            namespace: openshift-machine-api
          diagnostics: {}
          zone: '2'
          metadata:
            creationTimestamp: null
          publicIP: false
          resourceGroup: ${AZR_CLUSTER_RESOURCE_GROUP}
          kind: AzureMachineProviderSpec
          location: ${AZR_RESOURCE_LOCATION}
          vmSize: Standard_F4s_v2
          image:
            offer: aro4
            publisher: azureopenshift
            resourceID: ''
            sku: aro_412
            version: 412.86.20230503
          acceleratedNetworking: true
          subnet: ${AZR_ARO_SUBNET_WORKER}
          apiVersion: machine.openshift.io/v1beta1

---
apiVersion: machine.openshift.io/v1beta1
kind: MachineSet
metadata:
  annotations:
    machine.openshift.io/GPU: '0'
    machine.openshift.io/memoryMb: '8192'
    machine.openshift.io/vCPU: '4'
  name: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}3
  generation: 1
  namespace: openshift-machine-api
  labels:
    machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
    machine.openshift.io/cluster-api-machine-role: worker
    machine.openshift.io/cluster-api-machine-type: worker
spec:
  replicas: 1
  selector:
    matchLabels:
      machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
      machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}3
  template:
    metadata:
      labels:
        machine.openshift.io/cluster-api-cluster: ${AZR_CLUSTER}-${SUFFIX}
        machine.openshift.io/cluster-api-machine-role: worker
        machine.openshift.io/cluster-api-machine-type: worker
        machine.openshift.io/cluster-api-machineset: ${AZR_CLUSTER}-${SUFFIX}-worker-fvm-${AZR_RESOURCE_LOCATION}3
    spec:
      lifecycleHooks: {}
      metadata: {}
      providerSpec:
        value:
          osDisk:
            diskSettings: {}
            diskSizeGB: 256
            managedDisk:
              storageAccountType: Premium_LRS
            osType: Linux
          networkResourceGroup: ${VNET_RESOURCE_GROUP}
          publicLoadBalancer: ${AZR_CLUSTER}-${SUFFIX}
          userDataSecret:
            name: worker-user-data
          vnet: ${AZR_ARO_VNET}
          credentialsSecret:
            name: azure-cloud-credentials
            namespace: openshift-machine-api
          diagnostics: {}
          zone: '3'
          metadata:
            creationTimestamp: null
          publicIP: false
          resourceGroup: ${AZR_CLUSTER_RESOURCE_GROUP}
          kind: AzureMachineProviderSpec
          location: ${AZR_RESOURCE_LOCATION}
          vmSize: Standard_F4s_v2
          image:
            offer: aro4
            publisher: azureopenshift
            resourceID: ''
            sku: aro_412
            version: 412.86.20230503
          acceleratedNetworking: true
          subnet: ${AZR_ARO_SUBNET_WORKER}
          apiVersion: machine.openshift.io/v1beta1

EOF

oc get machineset -n openshift-machine-api

oc get nodes

oc adm cordon aro-dpenagos-p8vzw-worker-eastus2-k9r2l
oc adm cordon aro-dpenagos-p8vzw-worker-eastus3-xglsk 

oc adm drain aro-dpenagos-p8vzw-worker-eastus2-k9r2l aro-dpenagos-p8vzw-worker-eastus3-xglsk --timeout=60s

oc get machine -n openshift-machine-api

oc scale --replicas=0 ${MACHINESET} -n openshift-machine-api

oc scale --replicas=0 aro-dpenagos-p8vzw-worker-eastus1 -n openshift-machine-api
oc scale --replicas=0 aro-dpenagos-p8vzw-worker-eastus2 -n openshift-machine-api
oc scale --replicas=0 aro-dpenagos-p8vzw-worker-eastus3 -n openshift-machine-api


oc delete machineset ${MACHINESET} -n openshift-machine-api

oc delete machineset aro-dpenagos-p8vzw-worker-eastus1 -n openshift-machine-api
oc delete machineset aro-dpenagos-p8vzw-worker-eastus2 -n openshift-machine-api
oc delete machineset aro-dpenagos-p8vzw-worker-eastus3 -n openshift-machine-api
