# SwipeBack Deployment

## Backend for SideSwipe

## Create environment

1. Create .env file (.env.example can be found [here](https://github.com/SlackOverflowHack/swipeback))
2. convert .env file to yml secret:
    ```bash
    kubectl -n sportswipe create secret generic swipeback-env --from-env-file=./.env
    ```
    Your secret is now deployed on k8s and can be used by the swipeback deployment

3. Create a secret for pulling the docker image from the private registry
    ```bash
    kubectl create -n sportswipe secret docker-registry regcred --docker-server=registry.goebel.app --docker-username=_token --docker-password=<your-pword> --docker-email=<your-email>
    ```

## Update a secret
```bash
kubectl -n sportswipe create secret generic swipeback-env \
    --save-config --dry-run=client \
    --from-env-file=./.env \
    -o yaml | 
  kubectl apply -f -
```