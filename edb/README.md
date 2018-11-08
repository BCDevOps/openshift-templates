# Install
```
# Set the current project
oc project devops-sso-sandbox

#Create Secrets
oc process -f edbas-secrets.yaml -p 'NAME=edb' -l app=sso-pg | oc apply -f -

#Create PVCs
oc process -f edbas-pvc.yaml -p 'PERSISTENT_VOLUME_CLAIM=sso-pg-sandbox' -p 'BACKUP_VOLUME_CLAIM=sso-pg-backup-sandbox' -l app=sso-pg | oc apply -f -


#Create DC/SVC/Route/Etc.
oc process -f edbas-persistent.yaml -p 'DATABASE_NAME=edb' -p 'PERSISTENT_VOLUME_CLAIM=sso-pg-sandbox' -p 'BACKUP_VOLUME_CLAIM=sso-pg-backup-sandbox' -l app=sso-pg  | oc apply -f -

```

# Uninstall
```
oc delete all -l app=sso-pg
oc delete secret,pvc,configmap,RoleBinding -l app=sso-pg
```
