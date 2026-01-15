## EC2 instance terminate unexpectedly.How will you troubleshoot?

# Resolution
To identify the cause of the instance termination, 
1. review your AWS CloudTrail events for the TerminateInstances API call. In the event details, note the value of userAgent for the AWS Identity and Access Management (IAM) user or role that invoked the API. Also note the values for SourceIPaddress, eventTime, errorCode, and errorMessage.

Based on the cause of the instance termination issues, take the following troubleshooting actions.

- Review metrics for health check issues
Check the CPUUtilization and StatusCheckFailed_Instance of your Amazon CloudWatch metrics for the terminated instance. Anomalies might show performance issues or hardware faults. For more information, see Status checks for Amazon EC2 instances. If you activated CloudWatch Container Insights, then also check the Container Insights metrics.

- Check the instance logs to understand if your instance has network connection, Out Of Memory, or other underlying issues. High resource usage can cause instance termination issues. Resize your container instance type based on your workload requirements.

- Check Auto Scaling history for issues
Check your Amazon EC2 Auto Scaling group activity history to check whether a scheduled EC2 Auto Scaling event terminated the instance. If you had an unexpected Auto Scaling action, then check your Auto Scaling configuration, scaling policies, and thresholds.

To avoid unexpected instance termination, use managed termination protection to retain Amazon ECS container instances that contain running tasks.

- You can also activate termination protection for your instances to prevent accidental termination. If you activated termination protection and still encounter issues, then see How do I resolve the managed termination protection setting for the capacity provider error in Amazon ECS?

- Check for Spot Instance interruptions
If you use Spot Instances for your cluster, then check why your Spot Instance was terminated or interrupted. Determine whether Amazon EC2 terminated the Spot Instance. If Amazon EC2 interrupts your Spot Instance, then you receive a notice 2 minutes before the interruption.

It's a best practice to use On-Demand Instances for applications with critical workloads that can't be interrupted.

- Set up monitors for your instance
Create CloudWatch alarms to monitor when your instances automatically stop, terminate, reboot, or recover to proactively identify issues. Also, create a CloudWatch alarm for important metrics such as CPUUtilization, DiskReadOps, DiskWriteOps, NetworkIn or NetworkOut.

- Use Amazon Simple Notification Service (Amazon SNS) and Amazon EventBridge to receive alerts for instance state changes, such as stops, terminations, and health check failures. You can also create an alarm that sends an email when an instance changes state.

- To collect metrics at the cluster, instance, service, and task level, set up Container Insights.

- Set up high availability
Use task placement strategies, such as spread and binpack tasks, so that you don't concentrate too many tasks on one instance.

Also, spread your container instances across multiple Availability Zones to reduce the effect of accidental instance termination. For more information, see Amazon ECS availability best practices.