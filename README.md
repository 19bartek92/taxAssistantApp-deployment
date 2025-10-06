# 🚀 TaxAssistantApp - Simplified Deployment

Deploy the TaxAssistantApp to your Azure subscription with a simple one-click process. This deployment creates only the necessary infrastructure (App Service + Key Vault) without complex integrations.

## ✨ What gets deployed

- **Azure App Service** - Hosts your web application
- **Azure Key Vault** - Securely stores your API keys
- **Managed Identity** - Allows the app to access Key Vault securely

## 📋 Prerequisites

Before deploying, you'll need:

1. **Azure Subscription** - With permissions to create resources
2. **NSA Search API Key** - For tax interpretation search functionality
3. **NSA Detail API Key** - For detailed interpretation retrieval

## 🎯 Deployment Process

### Step 1: Click Deploy to Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2F19bartek92%2FtaxAssistantApp-deployment%2Fmain%2Fazuredeploy.json)

*[Screenshot placeholder: Azure deploy button]*

### Step 2: Login to Azure

You'll be redirected to Azure Portal to authenticate with your Azure account.

*[Screenshot placeholder: Azure login screen]*

### Step 3: Configure Deployment Parameters

Fill in the deployment form with your settings:

| Parameter | Description | Example | Required |
|-----------|-------------|---------|----------|
| **Subscription** | Your Azure subscription | `My Company Subscription` | ✅ |
| **Resource Group** | Create new or use existing | `rg-taxassistant` | ✅ |
| **Region** | Azure region for deployment | `Poland Central` | ✅ |
| **App Service Plan Name** | Name for hosting plan | `taxassistant-plan` | ✅ |
| **Web App Name** | Name for your application | `taxassistant-mycompany` | ✅ |
| **SKU** | Hosting plan size | `F1` (Free tier) | ✅ |
| **NSA Search API Key** | Your API key for search | `your-search-key-here` | ✅ |
| **NSA Detail API Key** | Your API key for details | `your-detail-key-here` | ✅ |
| **Key Vault Name** | Name for secure storage | `kv-taxassistant` | ✅ |

*[Screenshot placeholder: Azure deployment form with filled parameters]*

### Step 4: Review and Create

1. Check "I agree to the terms and conditions stated above"
2. Click **"Review + create"**
3. Review your settings
4. Click **"Create"**

*[Screenshot placeholder: Review and create screen]*

### Step 5: Wait for Deployment

The deployment typically takes 3-5 minutes. You'll see a progress screen.

*[Screenshot placeholder: Deployment in progress]*

### Step 6: Deployment Complete

Once finished, you'll see a success message with deployment outputs.

*[Screenshot placeholder: Deployment complete with outputs]*

## 📥 Download Publish Profile

After deployment completes, you need to download the publish profile to send to the developer:

1. Go to **Azure Portal** → **App Services**
2. Find and click on your deployed app (e.g., `taxassistant-abc123`)
3. In the **Overview** section, click **"Download publish profile"**
4. Save the `.pubxml` file

*[Screenshot placeholder: App Service overview with download button highlighted]*

## 📧 Send to Developer

**⚠️ Important: Handle securely!**

The publish profile contains deployment credentials. Please:

1. **Encrypt the file** or use a secure file sharing service
2. **Send via secure method** (encrypted email, password-protected zip, etc.)
3. **Include this information:**
   - Resource Group name
   - Web App name
   - Any special requirements

### Email Template
```
Subject: TaxAssistantApp Deployment - Publish Profile

Hi [Developer],

I've successfully deployed the TaxAssistantApp infrastructure to Azure.

Deployment Details:
- Resource Group: [your-resource-group-name]
- Web App Name: [your-web-app-name]
- App URL: [your-app-url]

Please find the publish profile attached (encrypted/password-protected).
Password: [if applicable]

The infrastructure is ready for application deployment.

Best regards,
[Your name]
```

## 🔧 Developer Instructions

For the developer deploying the application:

1. **Extract** the publish profile file
2. **Build** the application: `dotnet publish -c Release -o ./publish`
3. **Deploy** using Azure CLI:
   ```bash
   az webapp deploy \
     --resource-group [resource-group-name] \
     --name [web-app-name] \
     --src-path ./publish \
     --type zip
   ```

## 🌐 Access Your Application

After the developer deploys the code, your application will be available at:
```
https://[your-web-app-name].azurewebsites.net
```

## ❓ Troubleshooting

### Common Issues

**Q: Deployment fails with "Key Vault name not available"**
A: Key Vault names must be globally unique. Try a different name or let the system generate one.

**Q: Can't download publish profile**
A: F1 (Free) tier has limited publish options. You can still deploy using Visual Studio Code with Azure extension or Azure CLI with deployment center.

**Q: App shows error after deployment**
A: The infrastructure is created, but the application code needs to be deployed by the developer.

**Q: API keys not working**
A: Double-check that you've entered the correct NSA API keys during deployment.

### Getting Help

If you encounter issues:

1. Check the Azure Portal → Resource Group → Deployments for error details
2. Contact your developer with the error message
3. Ensure all required parameters were filled correctly

## 🔒 Security Notes

- API keys are stored securely in Azure Key Vault
- The application uses Managed Identity to access secrets
- All connections use HTTPS
- Publish profile contains temporary deployment credentials

## 💰 Cost Estimation

Estimated monthly cost for F1 plan in Poland Central:
- **App Service Plan (F1)**: FREE (with limitations)
- **Key Vault**: ~€0.50/month (for secret operations)
- **Total**: ~€0.50/month

*F1 limitations: 60 minutes compute time per day, 1GB disk space, no custom domains*

*Note: Costs may vary by region and usage. Check Azure pricing calculator for accurate estimates.*

---

## 📞 Support

For technical support or questions about this deployment process, please contact your development team.

**Happy deploying!** 🎉