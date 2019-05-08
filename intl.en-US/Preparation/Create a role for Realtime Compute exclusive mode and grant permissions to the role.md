# Create a role for Realtime Compute exclusive mode and grant permissions to the role {#concept_73035_zh .concept}

This topic describes how to create and authorize a role for Realtime Compute exclusive mode.

## Automatically create a default role and grant permissions to the role {#JoJo_Flink_Sec01 .section}

If you have not created the default role with required permissions for your Realtime Compute account, a popup appears when you create a project or open it for the first time.

**Note:** If the default AliyunStreamDefaultRole role exists, you do not need to create it again.

1.  Click **Go to Authorize**.
2.  Select **AliyunStreamDefaultRole** and click **Confirm Authorization Policy** to grant required permissions to the role.
3.  Refresh the Realtime Compute console and start using Realtime Compute.

**Note:** 

For more information about the **AliyunStreamDefaultRole** role, log on to the RAM console.The following code shows the permissions granted to the AliyunStreamDefaultRole role in Realtime Compute:

``` {#codeblock_xm4_u5m_6nf .language-sql}
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "ots:List*",
        "ots:DescribeTable",
        "ots:Get*",
        "ots:*Row"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "dhs:Create*",
        "dhs:List*",
        "dhs:Get*",
        "dhs:PutRecords",
        "dhs:DeleteTopic"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "log:List*",
        "log:Get*",
        "log:Post*"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "mns:List*",
        "mns:Get*",
        "mns:Send*",
        "mns:Publish*",
        "mns:Subscribe"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "drds:DescribeDrdsInstance",
        "drds:ModifyDrdsIpWhiteList"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "rds:Describe*",
        "rds:ModifySecurityIps*"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "vpc:DescribeVpcs",
        "vpc:DescribeVSwitches"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "ecs:CreateSecurityGroup",
        "ecs:AuthorizeSecurityGroup",
        "ecs:CreateNetworkInterface",
        "ecs:DescribeNetworkInterfaces",
        "ecs:AttachNetworkInterface",
        "ecs:DescribeNetworkInterfacePermissions",
        "ecs:CreateNetworkInterfacePermission"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": "oss:*",
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}           
```

## Add an authorization policy {#section_lg2_w21_wfb .section}

The procedure is as follows:

1.  Log on to the [Alibaba Cloud console](https://home-intl.console.aliyun.com).
2.  Click the user icon in the upper-right corner and select **RAM** from the menu that appears.
3.  On the RAM page that appears, choose Permissions \> Policies from the left-side navigation pane. On the Policies page that appears, click **Create Policy**.
4.  Specify a name for the authorization policy.
5.  Replace the existing policy content with the following code.

    ```language-html
    {
      "Version": "1",
      "Statement": [
        {
          "Action": [
            "vpc:DescribeVpcs",
            "vpc:DescribeVSwitches"
          ],
          "Resource": "*",
          "Effect": "Allow"
        },
        {
          "Action": [
            "ecs:CreateSecurityGroup",
            "ecs:AuthorizeSecurityGroup",
            "ecs:CreateNetworkInterface",
            "ecs:DescribeNetworkInterfaces",
            "ecs:AttachNetworkInterface",
            "ecs:DescribeNetworkInterfacePermissions",
            "ecs:CreateNetworkInterfacePermission"
          ],
          "Resource": "*",
          "Effect": "Allow"
        }
      ]
    }
    					
    ```

    **Note:** After the cluster is created, you can delete the following two permissions from the preceding authorization policy:

    -   ecs:CreateSecurityGroup
    -   ecs:AuthorizeSecurityGroup
6.  Add the custom authorization policy to the AliyunStreamDefaultRole role.
7.  Add the AliyunOSSFullAccess policy to the AliyunStreamDefaultRole role. You can enter OSS in the search box to search for the policy.

