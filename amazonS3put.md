#FoyerLive - Sending data feeds via AWS S3

## Feed File Naming Convention
All files are uploaded to a folder dedicated to each FoyerLive Account.

The folder location is: `s3://upload.foyerlive.com/ACOUNT_CODE/` where ACCOUNT_CODE is provided to you by FoyerLive.

Please follow this naming convention for providing files:

`feedSize`-`dataType`-`datetime`.`fileExtension` - i.e. `full-products-2016-05-13-07-15-05.csv`

| Field | Valid Values |Description|
| ----- | ---- | ---- |
|*feedSize*|'full' or 'delta'|A 'full' upload expects all items for the dataType, and will optionally disable missing products. A 'delta' upload will process only the items supplied.|
|*dataType*|'products', 'reviews', 'inventory'|FoyerLive has built in processors for importing Products, Product Reviews & Product Inventory.|
|*dateTime*|YYYY-MM-DD-HH-II-SS|A date and time reference for when the file was generated.|
|*fileExtension*|'csv', 'json', 'xml'|The appropriate extension for the format of the data provided.  When providing CSVs, please include a header row.|

### Valid file names

```
full-products-2016-05-13-07-15-05.csv
delta-products-2016-05-13-07-15-05.json
full-reviews-2016-05-13-07-15-05.csv
delta-reviews-2016-05-13-07-15-05.xml
full-inventory-2016-05-13-07-15-05.csv
delta-inventory-2016-05-13-07-15-05.json
```

## Using an AWS SDK to deliver feeds
If you have the ability to install libraries for your platform language, delivering content via an API may be appropriate.

### Delivery process
- [Install the relevant SDK for your platform.](https://aws.amazon.com/code/)
- Retrieve your 'Access Key ID' & 'Secret Access Key' from FoyerLive.
- Use the SDK to call a `putObject` request and deliver the file.


#### AWS PHP SDK File Sending Example
Below is some example code when using the AWS PHP SDK to deliver a generated file.
```php
$s3Client = new S3Client([
    'version'     => 'latest',
    'region'      => 'us-west-1',
    'credentials' => [
        'key'    => 'foyerlive-provided-access-key-id',
        'secret' => 'foyerlive-provided-secret-access-key',
    ],
]);

// Local file example...
$result = $s3Client->putObject([
    'Bucket' => 'upload.foyerlive.com',
    'Key' => 'FOYERLIVE_ACCOUNT_CODE/REPLACE_WITH_DESTINATION_FILE_NAME', // The destination filename must match a convention listed above.
    'SourceFile' => 'REPLACE_WITH_FILE_SYSTEM_REFERENCE_TO_SOURCE_FILE'
]);
```

#### AWS PHP SDK File Contents Sending Example
Below is some example code when using the AWS PHP SDK to deliver generated output directly for an inventory update for the client 'ACME'
```php
$s3Client = new S3Client([
    'version'     => 'latest',
    'region'      => 'us-west-1',
    'credentials' => [
        'key'    => 'foyerlive-provided-access-key-id',
        'secret' => 'foyerlive-provided-secret-access-key',
    ],
]);

$CSVdata = "SKU,Inventory\n";
$CSVdata .= "3452354,54\n";
$CSVdata .= "3452355,37\n";
$CSVdata .= "3452356,22\n";

// Local file example...
$result = $s3Client->putObject([
    'Bucket' => 'upload.foyerlive.com',
    'Key' => 'acme/delta-inventory-2016-08-01-17-00-00.csv', // The destination filename must match a convention listed above.
    'Body' => $CSVdata,
]);
```

## Using the AWS Command Line Interface (CLI) to deliver feeds
- [Install the AWS CLI.](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)
- Retrieve your 'Access Key ID' & 'Secret Access Key' from FoyerLive.
- [Configure the AWS CLI.](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
- Setup your platform to export files to a folder accessible via a CRON script.
- Clone and modify the [Command-line script](#example-command-line-script) below to deliver files to FoyerLive.

### Example Command-line script
Below is an example BASH script that will look for the latest exported file, and then upload it to FoyerLive.
```
#!/bin/bash
file=$(ls -ltr | tail -1 | awk '{print $NF}')
now=$(date +"%Y-%m-%d-%H-%M-%S")
remote="s3://upload.foyerlive.com/REPLACE_WITH_ACCOUNT_CODE/full-products-$now.csv"
if [ -f $file ] ; then
  echo $file
  echo $remote
  aws s3 cp $file $remote
fi
```
