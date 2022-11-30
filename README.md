# admincli

export SSL_CERT_FILE=/opt/sas/viya/config/etc/SASSecurityCertificateFramework/cacerts/trustedcerts.pem

cd /tmp
tar -xvf <sas-admin>
cd bin

tar -xvf <invfile>
tar -xvf <casfile>

./sas-admin plugins install --file ./<invfile> inventory
./sas-admin plugins install --file ./<casfile> cas

./sas-admin profile init
./sas-admin auth login



mkdir assessment
./sas-admin inventory scan services --customer-id "NAME" --deployment-label "viya" --output-location ./assessment
./sas-admin inventory scan filesystem --customer-id "NAME" --deployment-label "viya" --output-location ./assessment
./sas-admin inventory scan cas --customer-id "NAME" --deployment-label "viya" --output-location ./assessment
./sas-admin inventory scan infrastructure --customer-id "NAME" --deployment-label "viya" --output-location ./assessment
mkdir publish
./sas-admin inventory publish --source-location ./assessment --output-location ./publish
