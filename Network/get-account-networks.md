{{{
  "title": "GetAccountNetworks",
  "date": "2-6-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

Gets the list of Networks mapped to an account in any Data Center.

## URL

    REST: https://api.tier3.com/REST/Network/GetAccountNetworks/<format>
    SOAP: https://api.tier3.com/SOAP/Network.asmx?op=GetAccountNetworks

## Request

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the network. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to get networks in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The Network's home datacenter alias.&nbsp; If blank, the account home datacenter location is assumed.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "AccountAlias": "UNK",

      "Location": "UN1"

    }

#### XML

    <NetworkRequest>

        <AccountAlias>UNK</AccountAlias>

        <Location>UN1</Location>

    </NetworkRequest>

## Response

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>Networks</td>
      <td>Complex</td>
      <td>
        <p>A list of Network (see below)</p>
      </td>
    </tr>
  </tbody>
</table>

### Network Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
<tbody>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>
        <p>The name of the Network.</p>
        <p>This value should be used on other api methods that require a network reference.</p>
      </td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The friendly name of the network if one has been configured.</td>
    </tr>
    <tr>
      <td>Gateway</td>
      <td>IPAddress</td>
      <td>The default gateway for the network.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "Networks": [

        {

          "Name": "vlan_1114_10.81.14",

          "Description": "vlan_1114_10.81.14",

          "Gateway": "10.81.14.1",

          "Location": "UN1",

          "AccountAlias": "UNK"

        },

        {

          "Name": "vlan_1241_10.81.141",

          "Description": "vlan_1241_10.81.141",

          "Gateway": "10.81.141.1",

          "Location": "UN1",

          "AccountAlias": "UNK"

        }

      ],

      "Success": true,

      "Message": "Networks successfully queried.",

      "StatusCode": 0

    }

#### XML

    <GetNetworksResponse Success="true" Message="Networks successfully queried." StatusCode="0">

        <Networks>

            <Network Name="vlan_1114_10.81.14" Description="vlan_1114_10.81.14" Gateway="10.81.14.1" Location="UN1" AccountAlias="UNK"/>

            <Network Name="vlan_1241_10.81.141" Description="vlan_1241_10.81.141" Gateway="10.81.141.1" Location="UN1" AccountAlias="UNK"/>

        </Networks>

    </GetNetworksResponse>

### Status Codes

<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>