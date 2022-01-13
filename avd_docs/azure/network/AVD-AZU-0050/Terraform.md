
Block port 22 access from the internet

```hcl
resource "azurerm_network_security_rule" "good_example" {
  name                        = "good_example_security_rule"
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "TCP"
  source_port_range           = "*"
  destination_port_range      = ["22"]
  source_address_prefix       = "82.102.23.23"
  destination_address_prefix  = "*"
}

resource "azurerm_network_security_group" "example" {
  name                = "tf-appsecuritygroup"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
  
  security_rule {
    source_port_range           = "any"
    destination_port_range      = ["22"]
    source_address_prefix       = "82.102.23.23"
    destination_address_prefix  = "*"
  }
}
```

#### Remediation Links
 - https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/network_security_group#security_rule
 - https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_rule#source_port_ranges
        