# automation-scripts

Meraki Dashboard API automation/migration scripts in Python
--------------------------------------

Here you can find Meraki Dashboard API scripts written for Python 3.

Check back from time to time, as new scripts are added and existing ones are sometimes polished and improved after initial posting.

Files contained in this repository:

**Installing Python on Windows.txt:** General info for installing Python 3 on Windows

**copymxvlans.py:** This script can be used to export MX VLAN configuration of a source org to a file and import it to a destination org. The script will look for the exact same network names as they were in the source org. Use copynetworks.py and movedevices.py to migrate networks and devices if needed.

**copynetworks.py:** Copies networks and their base attributes from one organization to another. Does not move devices over or copy individual device configuration. Combined networks will be copied as "wireless switch appliance".

**copyswitchcfg.py:** This script can be used to export switchport configuration of a source org to a file and import it to a destination org. The script will look for the exact same network names and device serial numbers, as they were in the source org. Use copynetworks.py and movedevices.py to migrate networks and devices if needed.

**deployappliance.py:** This script claims a single Security Appliance or Teleworker Gateway into an organization, creates a new network for it and binds that network to an existing template.

**deploydevices.py:** This script claims multiple devices and licenses into an organization, creates a new network for them and binds that network to an existing template. Initial config, including hostnames and street address/map markers are set for the devices.

**find_ports.py:** This script finds all MS switchports that match the input search parameter, searching either by clients from a file listing MAC addresses (one per line), a specific tag in Dashboard currently applied to ports, or the specific access policy currently configured.

**googletimezonetest.py:** Example script that gets the time zone that corresponds to a street address by using Google Maps APIs. You can use this code to set network timezones dynamically in your Meraki Dashboard API scripts.

**invlist.py:** Creates a list of all serial numbers and models of devices that are part of a Meraki network for an organization with a given name. Can print to Stdout or file.

**listip.py:** Almost exactly the same as invlist.py, but also prints the "lanIp" of the device. If the device has no "lanIp", it prints "None" for that field instead.

**migratecomware.py:** Proof of concept script that migrates legacy switch infrastructure based on Comware (HPE A-series) to Meraki MS switches. Comware switch configurations can be provided as files, or by entering the IP address and SSH credentials of the source device. A valid initialization configuration file must be provided, where source devices are mapped to target Meraki serial numbers. Please see migration_init_file.txt in this repository for an example of such a file. This version of the script only supports Comware-based switches and a limited set of Layer 2 switchport commands. The script could be expanded to cover more commands and other CLI-based switch families.

**migration_init_file.txt:** Example init config file for migratecomware.py.

**movedevices.py:** This script that can be used to move all devices from one organization to another. The script will only process devices that are part of a network. The networks of the source org need to exist in the destination org too. Use copynetworks.py if needed to create them.

**mx_fwrules_to_csv.py** A simple example showing how to use the Meraki Dashboard API library to GET MX L3 firewall rules from a provided network and output to CSV.

**setlocation.py:** Sets the street address and optionally the map marker of all devices in a network or organization. To be more easily clickable, devices will be placed in a spiral around a seed location. There is an option to preserve marker location for MR access points, to avoid breaking wireless map layout.

**setlocation_legacy.py:** Sets the street address of all devices in a given network to a given value. The intent of this script is to quickly fix address misconfigurations on large networks. The script has been updated from its initial version to use the Google Geocoding API to calculate a reasonable new positions for device map markers. This is a legacy script that is preserved as an example of integrating the Meraki Dashboard API with info extracted from a Google API. Please see setlocation.py for an improved version of the script that does not require a Google API key.

**update_ports.py:** This script finds all MS switchports that match the input search parameter, searching either by clients from a file listing MAC addresses (one per line), a specific tag in Dashboard currently applied to ports, or the specific access policy currently configured. It then changes the configuration of the port by applying the new access policy specified.

**uplink.py:** Iterates through all devices, and exports to two CSV files: one for appliance (MX, Z1, Z3, vMX100) networks to collect WAN uplink information, and the other for all other devices (MR, MS, MC, MV) with local uplink info.
Possible statuses:
- Active: active and working WAN port
- Ready: standby but working WAN port, not the preferred WAN port
- Failed: was working at some point but not anymore
- Not connected: nothing was ever connected, no cable plugged in
- (For load balancing, both WAN links would show active.)

More info about the scripts can be found inline as comments.
