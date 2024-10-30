create cluster admin users to access the cluster

This is configured to use google idp so requires a mapping to google user id( not user name)

Oauth configuration to map to google idp:

```
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
name: cluster
spec:
identityProviders:
- google:
    clientID: <secret>
    clientSecret:
        name: <secret>
    mappingMethod: lookup //to allow all google emails
    name: googleidp
    type: Google
```


Create user 
` oc create user <username>`
Create identity
`oc create identity <identity>`
Create user identity mapping 
`oc create useridentitymapping <identity> <mapping>`

Add user to cluster admin role
`oc adm policy add-cluster-role-to-user cluster-admin sumiranchugh --rolebinding-name=cluster-admin`