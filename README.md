# bob-the-bot

## 🚀 Getting Started

### 🔧 Connecting to Your AKS Cluster

```bash
az login
az account set --subscription <SUBSCRIPTION_ID>
az aks get-credentials --resource-group Aks-Skai-RG --name skai-aks-cluster
kubectl config current-context
```

---

## 🛠️ Upload a new image

1. Connecting to the AWS account.

2. Connecting to ECR using command line with this command  
   (we're working on eu-west-2 region):

   ```bash
   aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.eu-west-2.amazonaws.com
   ```

3. Go to `bob-the-bot-v3` repository.

4. Docker pull the latest image with this command:

   ```bash
   docker pull ${ACCOUNT_ID}.dkr.ecr.eu-west-2.amazonaws.com/bob-the-bot-v3:${LATEST_IMAGE_NUM}
   ```

5. Connecting to ACR by the command:

   ```bash
   az acr login --name skaiaksreg
   ```

6. Docker tag the downloaded image by the command:

   ```bash
   docker tag ${ACCOUNT_ID}.dkr.ecr.eu-west-2.amazonaws.com/bob-the-bot-v3:${LATEST_IMAGE_NUM} skaiaksreg.azurecr.io/bob-the-bot:${NEW_IMAGE_NUMBER}
   ```

7. Docker push the image into ACR:

   ```bash
   docker push skaiaksreg.azurecr.io/bob-the-bot:${NEW_IMAGE_NUMBER}
   ```

---

## 🚀 Updating helm chart

After you are changing something in the Helm chart, you have to run this command:

```bash
helm upgrade --install bob ./ -n bob-the-bot
```

This command will upgrade the cluster to the new changes.

---

## 🛠️ Secrets and CM files

We have some secrets and CM files in private.  
The names of the secrets are:

- `google-drive-secrets`
- `litellm-secrets`
- `bob-secrets`

The name of the CM is:

- `litellm-config`