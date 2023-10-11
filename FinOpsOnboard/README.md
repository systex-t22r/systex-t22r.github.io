# 精誠FinOps & SRE服務
## 簡介

欲使用精誠FinOps & SRE服務，Azure用戶須以 AAD（Azure Active Directory）透過 Azure Lighthouse 授權精誠 FinOps & SRE 服務帳號存取，方可進行後續的帳單與使用狀況分析。

## 授權方式

1. 使用Powershell授權。
2. 使用Azure CLI授權。
3. 透過Azure入口網站授權。

以上擇一進行即可。

## 前置準備

### 確保操作權限

須以non-guest account進行操作，且須具有Microsoft.Authorization/roleAssignments/write的權限，詳見[Deploy the Azure Resource Manager template](https://learn.microsoft.com/en-us/azure/lighthouse/how-to/onboard-customer#deploy-the-azure-resource-manager-template)。

## 使用Powershell授權
1. 開啟Powershell輸入以下指令（須置換[`<AzureRegion>`](https://learn.microsoft.com/zh-tw/gaming/playfab/api-references/events/data-types/azureregion)）：
   > 須先使用Connect-AzAccount登入Azure帳戶才能進行以下流程。
   ```powershell
   New-AzSubscriptionDeployment -Location <AzureRegion> `
                    -TemplateUri https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.json `
                    -TemplateParameterUri  https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.parameters.json `
                    -Verbose
   ```
2. 確認是否授權成功：
   ```powershell
   Get-AzManagedServicesDefinition
   Get-AzManagedServicesAssignment
   ```

## 使用Azure CLI授權
1. 建立一個資料夾，並下載[FinOpsAssessment.parameters.json](https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.parameters.json)至其中。
2. 在該資料夾位置開啟命令行介面。
3. 輸入以下指令（須置換[`<AzureRegion>`](https://learn.microsoft.com/zh-tw/gaming/playfab/api-references/events/data-types/azureregion)）：
   > 1. 須先登入Azure帳戶（az login）才能進行以下流程。
   > 2. 由於是以反斜槓換行故不可使用Powershell輸入
   ```bash
   # parameters只能使用local file。
   az deployment sub create --location <AzureRegion> \
                            --template-uri https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.json \
                            --parameters FinOpsAssessment.parameters.json \
                            --verbose
   ```
4. 確認是否授權成功：
   ```bash
   az managedservices definition list
   az managedservices assignment list
   ```

## 透過Azure入口網站授權
1. 選取Azure Lighthouse功能
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/1.png?raw=true)
2. 開啟上傳介面  
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/2.png?raw=true)
3. 上傳範本檔案[FinOpsAssessment.json](https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.json)與[FinOpsAssessment.parameters.json](https://systex-t22r.github.io/FinOpsOnboard/FinOpsAssessment.parameters.json)（確保如附圖配置後按上傳）
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/3.png?raw=true)
4. 選擇訂閱帳戶與區域後按「檢閱 + 建立」鈕
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/4.png?raw=true)
5. 確認內容後按「建立」鈕
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/5.png?raw=true)
6. 等待部屬完成如下圖
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/6.png?raw=true)
7. 至Azure Lighthouse，即可看到（可能需要按重新整理）已成功註冊Systex FinOps & SRE Service之服務🎉
   ![](https://github.com/systex-t22r/systex-t22r.github.io/blob/main/FinOpsOnboard/img/lighthouse-onboard-by-portal/7.png?raw=true)


## 參考資料
[Onboard a customer to Azure Lighthouse](https://learn.microsoft.com/en-us/azure/lighthouse/how-to/onboard-customer)

## 備註
1. 無論是使用Powershell或Azure CLI授權，都可以不填`<deploymentName>`，系統會自動產生。
2. Powershell登入Azure所使用的Connect-AzAccount是新模組Az module的功能，相關安裝請參考[Introducing the Azure Az PowerShell module](https://learn.microsoft.com/en-us/powershell/azure/new-azureps-module-az?view=azps-10.3.0)。