# Troubleshooting

## GitHub actions

### Verifying Connectivity

Checking DNS
```powershell
$DNSDOMAIN=""
$DNSRG=""
$RECORDNAME=""
az network dns record-set list -g $DNSRG -z $DNSDOMAIN --query "[?name=='$RECORDNAME'][{type:type,fqdn:fqdn,aRecords:aRecords,txtRecords:txtRecords}]"


$RG=""
$AKSNAME=""
az aks list -o table
az aks get-credentials -n $AKSNAME -g $RG --admin --overwrite-existing
kubectl get ing
```

### Errors

Workflow | Step | Error | What it means | Action to take
---|---|---|---|---
ByoVnet | Create Root Cert references in AppGw | ERROR: (Canceled) Operation was canceled. | The Az commands for Application Gateway seem to do this frequently | Re-run
ByoVnet | Create Root Cert references in AppGw | ERROR: (ApplicationGatewayCertificateDataOrKeyVaultSecretIdMustBeSpecified) Either Data or KeyVaultSecretId must be specified for Certificate /cert-default-tls-secret in Application Gateway. | Seen when existing apps using certs are present and running in the cluster |
ByoVnet | Create FrontEnd Cert references in AppGw | ERROR: (ApplicationGatewayCertificateDataOrKeyVaultSecretIdMustBeSpecified) Either Data or KeyVaultSecretId must be specified for Certificate /cert-default-tls-secret' in Application Gateway. | Seen when existing apps using certs are present and running in the cluster |
ByoVnet | Verify Java App is reachable | Process completed with exit code 28. (ERR_CONNECTION_TIMED_OUT) | Seen for subsequent deployments, investigating if there's an NSG issue through DINE policy | 
