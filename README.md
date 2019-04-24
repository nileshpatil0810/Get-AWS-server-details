# Get-AWS-server-details
How to get AWS server status details in Script ?

putenv('AWS_DEFAULT_REGION=us-west-2'); //Add your region
putenv("AWS_ACCESS_KEY_ID=REPLACE_WITH_AWS_ACCESS_KEY"); //Add Access key
putenv("AWS_SECRET_ACCESS_KEY=REPLACE_WITH_AWS_ACCESS_KEY"); //Add Secret Key

$instance_details = shell_exec("aws ec2 describe-instance-status --instance-id i-XXXXXXXX"); //Add here instance details
$aws_server_decode = json_decode($instance_details);
$server_InstanceStatuses = $aws_server_decode->InstanceStatuses[0]->InstanceState->Name;
$server_SystemStatus = $aws_server_decode->InstanceStatuses[0]->SystemStatus->Status;

//RDS
$rds_details = shell_exec("aws rds describe-db-instances");
$rds_details = json_decode($rds_details);

$rds_status = $rds_details->DBInstances[0]->DBInstanceStatus;
