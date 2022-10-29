# GCP ACM / ASM Config Controller + Policy Controller setup

## Demo setup

### Initial setup of environment variables

Create a config shell script to create all environmnet variables

Note:
* To determine ip address: `curl -4 ifconfig.co`.

### 1) Stand up config controller instance

### X) Replace environment variables with actualy values

Navigate to new demo directory

```
cd ./to/new/demo/dir
```

Change variables


```
sed -i 's\${GKE_NAME}\'"$GKE_NAME"'\g' **/**/*.yaml
sed -i 's\${GKE_SA}\'"$GKE_SA"'\g' **/**/*.yaml
sed -i 's\${GKE_LOCATION}\'"$GKE_LOCATION"'\g' **/**/*.yaml
sed -i 's\${GKE_PLATFORM_REPO_URL}\'"$GKE_PLATFORM_REPO_URL"'\g' **/**/*.yaml
sed -i 's\${GKE_CONFIGS_REPO_URL}\'"$GKE_CONFIGS_REPO_URL"'\g' **/**/*.yaml
sed -i 's\${HOST_PROJECT_ID}\'"$HOST_PROJECT_ID"'\g' **/**/*.yaml
sed -i 's\${TENANT_PROJECT_ID}\'"$TENANT_PROJECT_ID"'\g' **/**/*.yaml
sed -i 's\${TENANT_PROJECT_NUMBER}\'"$TENANT_PROJECT_NUMBER"'\g' **/**/*.yaml
sed -i 's\${TENANT_PROJECT_SA_EMAIL}\'"$TENANT_PROJECT_SA_EMAIL"'\g' **/**/*.yaml
```