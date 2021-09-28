build: clean ../main.yaml

../main.yaml: main.yaml
	kustomize build >$@

main.yaml: clean/main.yaml
	kustomize build clean >$@

clean/main.yaml: clean/values.yaml
	-helm repo add hashicorp https://helm.releases.hashicorp.com
	helm repo update
	helm template vault hashicorp/vault \
		--version 0.16.0 --namespace=vault --values=clean/values.yaml --include-crds --kube-version 1.21 >$@

.PHONY: clean
clean:
	rm -f ../main.yaml main.yaml clean/main.yaml
