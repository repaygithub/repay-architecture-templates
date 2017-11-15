# repay-ext-role-sns-publisher
This cloudformation template allows for the creation of an external role that utilizes AWS best security practices for cross account deputization for limited access on specific resources. Specifically, the first party applying this template will give access to a second party to only list and publish to the designated SNS Topic ARNs input at runtime of the template. This is secured with an external-id that is shared between the parties.

Simply run the cloudformation template in AWS and fill in the parameters as prompted. The parameters do have descriptive text to explain what each parameter is. Then take the output from the cloudformation creation and send it to REPAY so they have the corresponding values to assume the role.

# role assumption would be done by REPAY with a command similar to:
```bash
aws --profile= sts assume-role \
--role-arn=arn:aws:iam::DestinationAccountNumber:role/RoleName \
--external-id=RepaysExternalID \
--duration-seconds=3600 \
--role-session-name=foo
```
* This will generate and output a session token that will last for "duration-seconds". Those session tokens can then be used as credentials to publish through the role to the SNS Topics provided to the template.

# Documentation
* Solving the Confused Deputy Problem with External ID
  * https://aws.amazon.com/blogs/security/how-to-use-external-id-when-granting-access-to-your-aws-resources/
* Assuming External Role
  * http://docs.aws.amazon.com/cli/latest/reference/sts/assume-role.html