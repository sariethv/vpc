---

copyright:
  years:  2023
lastupdated: "2023-10-30"

keywords:

subcollection: vpc

---

{{site.data.keyword.attribute-definition-list}}

# Attaching floating IPs to a virtual network interface
{: #vni-add-fip}

This VPC feature is available only to accounts with special approval to preview this feature.
{: preview}

You can attach floating IPs to a VNI with the UI, CLI, API, or Terraform.

## Attaching a floating IP to a virtual network interface in the UI
{: #vni-add-fip-ui}
{: ui}

To add a floating IP to an existing virtual network interface, follow these steps.

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **VPC Infrastructure > Virtual network interfaces**.
1. Click the name of the virtual network interface that you want to add a floating IP to in the Virtual network interfaces for VPC table.
1. In the Floating IPs section, click **Attach**.
1. In the Attach floating IP panel that appears, you can do one of the following:
    * Reserve a new floating IP by clicking **Reserve new floating IP** and completing the requested information in the panel that appears
    * Select an existing floating IP from the Floating IP addresses menu.
1. Click **Attach** to attach the floating IP to your virtual network interface, or click **Cancel**.

## Attaching a floating IP to a virtual network interface from the CLI
{: #vni-add-fip-cli}
{: cli}

Before you begin, make sure to [set up your CLI environment](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference).

```sh
export IBMCLOUD_IS_FEATURE_VNI_PHASE_II=true
```
{: pre}

Then run the following command:

```sh
ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE_NAME | --nic TARGET_INTERFACE [--in TARGET_INSTANCE | --bm TARGET_BARE_METAL_SERVER | --vni TARGET_VIRTUAL_NETWORK_INTERFACE]) [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```
{: pre}

Where:

`FLOATING_IP_NAME`
:   ID or name of the floating IP.

`--zone`
:   ID or name of the zone.

`--nic TARGET_INTERFACE`
:   The target interface.

`--in TARGET_INSTANCE`
:   The target virtual server instance.

`--bm TARGET_BARE_METAL_SERVER`
:   The target bare metal server.

`--vni TARGET_VIRTUAL_NETWORK_INTERFACE`
:   The target virtual network interface.

`--resource-group-id RESOURCE_GROUP_ID`
:   The ID of the resource group.

`--resource-group-name RESOURCE_GROUP_NAME`
:   The name of the resource group.

`--output`
:   Specify output format, only JSON is supported. One of: `JSON`.

`-q, --quiet`
:   Suppress verbose output.



## Attaching a floating IP to a virtual network interface with the API
{: #vni-api-add-fip}
{: api}

To add a floating IP address to a virtual network interface with the API, follow these steps:

1. Set up your API environment [with the right variables](/docs/vpc?topic=vpc-set-up-environment#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands; for example:

    * `version` (string): The API version, in format `YYYY-MM-DD`.
    * `virtual_network_interface_id` (string): The virtual network interface identifier.
    * `floating_ip_id` (string): The floating IP identifier.

1. When all variables are initiated, add the floating IP address to the virtual network interface:

    ```sh
    curl -X PUT \
    "$vpc_api_endpoint/v1/virtual_network_interfaces/$virtual_network_interface_id/floating_ips/$floating_ip_id?version=$version&generation=2" \
    -H "Authorization: Bearer $iam_token"
    ```
    {: codeblock}

## Attaching a floating IP to a virtual network interface with Terraform
{: #vni-terraform-add-fip}
{: terraform}

The following example adds a floating IP address to a virtual network interface by using Terraform:

```terraform
resource "ibm_is_virtual_network_interface_floating_ip" "my_vni_floatingip" {
  virtual_network_interface = ibm_is_virtual_network_interface.my_virtual_network_interface.id
  floating_ip = ibm_is_floating_ip.my_floatingip.id
}
```
{: codeblock}
