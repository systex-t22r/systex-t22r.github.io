# 以AAD加入Systex FinOps & SRE的服務

為了提供Azure用戶最佳的FinOps & SRE服務，需要用戶以AAD（Azure Active Directory）加入我們的Azure Lighthoure，以利進行數據分析。

## 如何加入

### 加入方式

1. 使用Powershell加入。
2. 使用Azure CLI加入。
3. 透過Azure 入口網站加入。

以上擇一進行即可。

### 前置準備

這三種方式都需要此目錄下的

1. FinOpsAssessment.json
2. FinOpsAssessment.parameters.json

建議使用Download raw file的方式下載，如下圖，以確保檔名與內容正確。

![](./img/2023-10-06 13.22.58.png)

此二文件都不需任何修改，在後續流程直接引用即可。

> 須以non-guest account進行操作，且須具有Microsoft.Authorization/roleAssignments/write的權限，詳見[Deploy the Azure Resource Manager template](https://learn.microsoft.com/en-us/azure/lighthouse/how-to/onboard-customer#deploy-the-azure-resource-manager-template)。

## 使用Powershell加入

> 須先使用Connect-AzAccount登入Azure帳戶才進行以下流程。

1. 建立一個資料夾，並下載FinOpsAssessment.json與FinOpsAssessment.parameters.json至其中。
2. 在該資料夾底下開啟Powershell。
3. 輸入以下指令（須置換<deploymentName>與<AzureRegion>）：

   ```powershell
   New-AzSubscriptionDeployment -Name <deploymentName> `
                    -Location <AzureRegion> `
                    -TemplateFile FinOpsAssessment.json `
                    -TemplateParameterFile FinOpsAssessment.parameters.json `
                    -Verbose
   ```
4. 確認是否加入成功：

   ```powershell
   # Confirm successful onboarding for Azure Lighthouse

   Get-AzManagedServicesDefinition
   Get-AzManagedServicesAssignment
   ```

## 使用****Azure CLI****加入

> 須先登入Azure帳戶才進行以下流程。

1. 建立一個資料夾，並下載FinOpsAssessment.json與FinOpsAssessment.parameters.json至其中。
2. 在該資料夾位置開啟命令行介面。
3. 輸入以下指令：

   ```bash
   # Deploy Azure Resource Manager template using template and parameter file locally
   az deployment sub create --name <deploymentName> \
                            --location <AzureRegion> \
                            --template-file <pathToTemplateFile> \
                            --verbose
   ```
4. 確認是否加入成功：

   ```bash
   # Confirm successful onboarding for Azure Lighthouse

   az managedservices definition list
   az managedservices assignment list
   ```

## 透過Azure入口網站加入

todo
