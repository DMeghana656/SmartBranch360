```python
import yaml

with open("smartbranch.yaml", "r") as file:
    data = yaml.safe_load(file)

print("\nSMARTBRANCH 360 VALIDATION REPORT")
print("=" * 45)

required_vlans = [10, 20, 30, 40, 99]

configured_vlans = [vlan["id"] for vlan in data["vlans"]]

print("\nVLAN Validation")
print("-" * 45)

for vlan in required_vlans:
    if vlan in configured_vlans:
        print(f"[PASS] VLAN {vlan} exists")
    else:
        print(f"[FAIL] VLAN {vlan} is missing")

print("\nGateway Validation")
print("-" * 45)

for vlan in data["vlans"]:
    vlan_id = vlan["id"]
    subnet = vlan["subnet"]
    gateway = vlan["gateway"]

    network_part = subnet.split(".")[2]
    gateway_part = gateway.split(".")[2]

    if network_part == gateway_part:
        print(f"[PASS] VLAN {vlan_id} gateway is correct")
    else:
        print(f"[FAIL] VLAN {vlan_id} gateway is incorrect")

print("\nValidation Complete")
print("=" * 45)
```
