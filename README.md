# Deploying Che on OpenShift

Download the following git repo

```
https://github.com/eclipse/che/tree/master/deploy/openshift
```

Create an OpenShift project where you want to run Che. You can use any project name. I am using the name `ide`

```
oc new-project che
```

In order to do a single user deployment of che in this project run the following command. 

**Note** 

* the parameter `p=ide` represents the name of the project into which you are deploying into.
* you'll need PVC of size 1GB for each workspace that you want to create using Eclipse 


```
$ ./deploy_che.sh -p=ide

                10100000               
            0110011001101101           
       01001001001001011011010110      
   1100110101010001000001011101000001  
0111001001111010111011111000111100010001
1110111011010111000001100000111001110  
101010011001001001    10011101000      
1011000101000              0           
100101011                           0110
10100001                        11011111
111101111011                111011110001
10111001000110101      00000111111011111
0110111111011100000001011001010101111111
1101000001101001000010010111101011011011
    00000001111001000001110111100000   
        000110101101000100011110       
            1101011100001001           
                 000101                


[INFO]: Checking if you are currently logged in... 
[INFO]: Active session found. Your current context is: ide/master-opsday-ocpcloud-com:443/veer 
[INFO]: Creating namespace "ide" 
[INFO]: Namespace "ide" successfully created 
[INFO]: Computing routing suffix 
[INFO]: Routing suffix identified as: apps.opsday.ocpcloud.com 
[INFO]: Deploying Eclipse Che with the following params:
Multi-User: false
HTTPS support: false
Namespace: ide
Che version: nightly
Image: eclipse/che-server
Pull policy: Always
Update strategy: Recreate
Environment variables:
CHE_MULTIUSER=false
CHE_OPENSHIFT_PROJECT=ide
CHE_IMAGE_TAG=nightly
CHE_IMAGE_REPO=eclipse/che-server 
--> Deploying template "ide/che" for "/Users/veer/eclipseche/openshift/templates/che-server-template.yaml" to project ide

     che
     ---------
     Che

     * With parameters:
        * Routing suffix of your OpenShift cluster=apps.opsday.ocpcloud.com
        * Eclipse Che version=nightly
        * Eclipse Che server image=eclipse/che-server
        * Che Multi-user flavor=false
        * OpenShift Username=
        * OpenShift Password=
        * OpenShift token=
        * HTTP protocol=http
        * Websocket protocol=ws
        * HTTPS support=false
        * OpenShift namespace to create workspace objects=${NAMESPACE}
        * Default PVC claim=1Gi
        * PVC strategy=unique
        * Admin password update=true
        * Identity provider URL=${PROTOCOL}://keycloak-${NAMESPACE}.${ROUTING_SUFFIX}/auth
        * Alias of the Openshift identity provider in Keycloak=NULL
        * Update Strategy=Recreate
        * Che server image pull policy=Always
        * OpenShift master URL=
        * Pre-create subpaths in PV=false
        * GitHub Client ID=
        * GitHub Client Secret=

--> Creating resources ...
    serviceaccount "che" created
    rolebinding "che" created
    service "che-host" created
    route "che" created
    deploymentconfig "che" created
--> Success
    Access your application via route 'che-ide.apps.opsday.ocpcloud.com' 
    Run 'oc status' to view your app.
persistentvolumeclaim "che-data-volume" created
deploymentconfig "che" updated
[INFO]: Che successfully deployed and will be soon available at http://che-ide.apps.opsday.ocpcloud.com 
```