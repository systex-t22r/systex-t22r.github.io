# 以AAD加入Systex FinOps & SRE的服務

為了提供Azure用戶最佳的FinOps & SRE服務，需要用戶以AAD（Azure Active Directory）加入我們的Azure Lighthoure，以利進行數據分析。

## 如何加入

加入的方式有三種如下：

1. 使用Powershell加入。
2. 使用Azure CLI加入。
3. 透過Azure 入口網站加入。

這三種方式都需要此目錄下的

1. FinOpsAssessment.json
2. FinOpsAssessment.parameters.json

此二文件都不需任何修改，直接引用即可。

<aside>
💡 確認進行操作的角色須為…

</aside>

## 使用Powershell加入

<aside>
💡 須先登入Azure帳戶才進行以下流程。

</aside>

1. 建立一個資料夾，並下載FinOpsAssessment.json與FinOpsAssessment.parameters.json至其中。
2. 在該資料夾底下開啟Powershell。
3. 輸入以下指令：
    
    ```powershell
    # Deploy Azure Resource Manager template using template and parameter file locally
    New-AzSubscriptionDeployment -Name <deploymentName> `
                     -Location <AzureRegion> `
                     -TemplateFile <pathToTemplateFile> `
                     -TemplateParameterFile <pathToParameterFile> `
                     -Verbose
    ```
    
4. 確認是否加入成功：
    
    ```powershell
    # Confirm successful onboarding for Azure Lighthouse
    
    Get-AzManagedServicesDefinition
    Get-AzManagedServicesAssignment
    ```
    
