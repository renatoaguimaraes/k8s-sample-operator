## Kubernetes Operator

Download the operator SDK.
https://github.com/operator-framework/operator-sdk/releases

Create the operator skeleton.
operator-sdk-v0.18.0-x86_64-apple-darwin new k8s-sample-operator --type go --repo github.com/renatoaguimaraes/k8s-sample-operator

Add API. 
operator-sdk-v0.18.0-x86_64-apple-darwin add api --kind Sample --api-version sample.novitatus.com/v1alpha1

Add Controller.
operator-sdk-v0.18.0-x86_64-apple-darwin add controller --kind Sample --api-version sample.novitatus.com/v1alpha1

Generate CRDS.
operator-sdk-v0.18.0-x86_64-apple-darwin generate crds

Generate K8s.
operator-sdk-v0.18.0-x86_64-apple-darwin generate k8s 

Apply CRD against the cluster.
kubectl apply -f deploy/crds/sample.novitatus.com_samples_crd.yaml 

Check API on k8s.
curl http://127.0.0.1:8001/apis/sample.novitatus.com
curl http://127.0.0.1:8001/apis/sample.novitatus.com/v1alpha1

Run local operator.
operator-sdk-v0.18.0-x86_64-apple-darwin run --local

kubectl apply -f <(echo "
apiVersion: sample.novitatus.com/v1alpha1
kind: Sample
metadata:
  name: k8s-sample
spec:
  webhook: https://httpbin.org/get  
")

 kubectl get Sample 