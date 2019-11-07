# Common Errors and Questions

## S3: 403 error during provisioning

This usually appears if the S3 bucket already exists. Remember, the S3 bucket has a unique global name. Login to your AWS console and create an S3 bucket with the same name you specified in the `bucket` variable to ensure they match.

## Error Applying Plan \(diffs didn't match\)

If you see something similar to the following:

```bash
Error: Error applying plan:

1 error(s) occurred:

* module.stack.aws_autoscaling_group.explorer: aws_autoscaling_group.explorer: diffs didn't match during apply. This is a bug with Terraform and should be reported as a GitHub Issue.

Please include the following information in your report:

    Terraform Version: 0.11.11
    Resource ID: aws_autoscaling_group.explorer
    Mismatch reason: attribute mismatch: availability_zones.1252502072
```

This is due to a bug in Terraform, the fix is to run `ansible-playbook deploy_infra.yml` again, and Terraform will pick up where it left off. This does not always happen, but this is the current workaround if needed.

## Server doesn't start during deployment

Even if the server is configured correctly, sometimes it may not bind the appropriate 4000 port for unknown reasons. If so, simply go to the appropriate nested blockscout folder, kill and rerun the server. For example, you can use the following command: `pkill beam.smp && pkill node && sleep 10 && mix phx.server`.

