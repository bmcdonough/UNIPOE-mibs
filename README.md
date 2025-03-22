# UNIPOE-mibs
Guangdong UNIPOE IoT Technology Co Ltd 1.3.6.1.4.1.52208
## discovery
```bash
# Initialize
last_oid=".1.3.6.1.4.1.52208"
> discovered_oids.txt

# Loop without counter
while true; do
  result=$(snmpgetnext -v 2c -c public -On 192.168.1.3 $last_oid)
  echo $result >> discovered_oids.txt
  last_oid=$(echo $result | cut -d ' ' -f1)
  # Break if we leave the subtree we're interested in
  if [[ ! $last_oid =~ ^\.1\.3\.6\.1\.4\.1\.52208 ]]; then
    echo "Finished walking OID tree" >> discovered_oids.txt
    break
  fi
done
```
