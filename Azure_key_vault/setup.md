#to create an Azure key vault and store secrets.
 1. to create the key vault:
 > az keyvault create --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b" --location centralus --name newsecret



2. add the secret

> az keyvault secret set --name SecretPassword --value reindeer_flotilla --vault-name newsecret


3. az appservice plan create --name keyvault-exercise-plan --sku FREE --location centralus --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b"
4. az webapp create --plan keyvault-exercise-plan --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b" --name mytask123
5. az webapp config appsettings set --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b" --name mytask123 --settings 'VaultName=newsecret'
6. az webapp identity assign --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b" --name mytask123
7. az keyvault set-policy --secret-permissions get list --name newsecret --object-id 3a3de973-6783-4c74-bc80-ce7d2e3f027b
8. cd KeyVaultDemoApp/
9. dotnet publish -o pub
zip -j site.zip pub/*

az webapp deploy --src-path site.zip --resource-group "learn-cf81827a-97ad-42d5-859f-18acefe6c74b" --name mytask123

to access :  https://<your-unique-app-name>.azurewebsites.net/api/SecretTest

