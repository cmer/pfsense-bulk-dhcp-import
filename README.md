# Bulk DHCP entries import for pfSense

This script takes a CSV file and converts its entries to an XML file containing entries compatible with pfSense.

## Installation

1. Make sure Ruby 2.7.0 is installed. Not familiar with Ruby? See [RVM](https://rvm.io).
2. Clone the repo locally.
2. Run `gem install bundler && bundle` in the repo directory.

## Data Conversion & Import

1. Create a CSV file with the data you want to import.

    - See `example.csv`. Note that your CSV file **requires** a header line with the proper field names.
    - `ipaddr` and `mac` are required fields.
    - Optional fields are: `CID HOSTNAME DESCR FILENAME ROOTPATH DEFAULTLEASETIME MAXLEASETIME GATEWAY DOMAIN DOMAINSEARCHLIST DDNSDOMAIN DDNSDOMAINPRIMARY DDNSDOMAINKEYNAME DDNSDOMAINKEY TFTP LDAP`

2. Create an XML backup of your pfSense installation.

    - **IMPORTANT:** only select "DHCP Server" as your Backup Area.

3. Run the script against your CSV file.

    - `./convert /path/to/dhcp.csv`
    - or `./convert /path/to/dhcp.csv /path/to/output.xml`

4. Add the generated entries to your pfSense backup file.

    - With your favorite text editor, open BOTH the generated XML file and the pfSense backup XML file.
    - Copy all the `staticmap` entries from the generated XML file and replace the old `staticmap` entries in your pfSense XML backup file.
    - If your pfSense XML file does not contain `staticmap` entries, simply paste the generated content below `dhcpleaseinlocaltime`.

5. In pfSense, import the modified backup file.

    - **IMPORTANT:** only select "DHCP Server" as your Import Area.

