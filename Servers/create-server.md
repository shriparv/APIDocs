{{{
  "title": "Create Server",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}


Creates a new server. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new server from a standard or custom template, or clone an existing server.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP POST.

## URL

### Structure

    https://api.tier3.com/v2/servers/{accountAlias}

### Example

    https://api.tier3.com/v2/servers/ALIAS/

## Request

### URI Parameters

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
      <td>string</td>
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Content Properties

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
      <td>name</td>
      <td>string</td>
      <td>Name of the server to create. Alphanumeric characters and dashes only. Must be between 1-7 characters depending on the length of the account alias.&nbsp;(This name will be appended with a two digit number and prepended with the datacenter code and
        account alias to make up the final server name.)</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>description</td>
      <td>string</td>
      <td>User-defined description of this server</td>
      <td>No</td>
    </tr>
    <tr>
      <td>groupId</td>
      <td>string</td>
      <td>ID of the parent group. Retrieved from query to parent group, or by looking at the URL on the UI pages in the Control Portal.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>sourceServerId</td>
      <td>string</td>
      <td>ID of the server to use a source. May be the ID of a template, or when cloning, an existing server ID. The list of available templates for a given account in a data center can be retrieved from the <a href="https://t3n.zendesk.com/entries/59048754-Get-Data-Center-Deployment-Capabilities">Get Data Center Deployment Capabilities</a>        API operation.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>isManagedOS</td>
      <td>bool</td>
      <td>Whether to create the server as managed or not. Default is false.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>primaryDns</td>
      <td>string</td>
      <td>Primary DNS to set on the server. If not supplied the default value set on the account will be used.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>secondaryDns</td>
      <td>string</td>
      <td>Secondary DNS to set on the server. If not supplied the default value set on the account will be used.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>networkId</td>
      <td>string</td>
      <td>ID of the network to which to deploy the server. If not provided, a network will be chosen automatically. If your account has not yet been assigned a network, leave this blank and&nbsp;one will be assigned automatically.&nbsp;The list of available
        networks for a given account in a data center can be retrieved from the&nbsp;<a href="https://t3n.zendesk.com/entries/59048754-Get-Data-Center-Deployment-Capabilities">Get Data Center Deployment Capabilities</a>&nbsp;API operation.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ipAddress</td>
      <td>string</td>
      <td>IP address to assign to the server. If not provided, one will be assigned automatically.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>password</td>
      <td>string</td>
      <td>Password of administrator or root user on server. If not provided, one will be generated automatically.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>sourceServerPassword</td>
      <td>string</td>
      <td>Password of the source server, used only when creating a clone from an existing server.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>cpu</td>
      <td>int</td>
      <td>Number of processors to configure the server with (1-16)</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>cpuAutoscalePolicyId</td>
      <td>string</td>
      <td>ID of the vertical CPU Autoscale policy to associate the server with. Available IDs can be retrieved from the <strong>Get&nbsp;Autoscale Policies </strong>API operation.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>memoryGB</td>
      <td>int</td>
      <td>Number of GB of memory to configure the server with (1-128)</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Whether to create standard or hyperscale server</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>storageType</td>
      <td>string</td>
      <td>For standard servers, whether to use standard or premium storage. If not provided, will default to premium storage.&nbsp;For hyperscale servers, storage type must be hyperscale.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>antiAffinityPolicyId</td>
      <td>string</td>
      <td>ID of the Anti-Affinity policy to associate the server with. Only valid for hyperscale servers. Available IDs can be retrieved from the&nbsp;<a href="https://t3n.zendesk.com/entries/44657214-Get-Anti-Affinity-Policies">Get&nbsp;Anti-Affinity Policies</a><strong>&nbsp;</strong>API
        operation.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>customFields</td>
      <td>complex</td>
      <td>Collection of custom field ID-value pairs to set for the server.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>additionalDisks</td>
      <td>complex</td>
      <td>Collection of disk parameters</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ttl</td>
      <td>dateTime</td>
      <td>Date/time that the server should be deleted&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>packages</td>
      <td>complex</td>
      <td>Collection of packages to run on the server after it has been built&nbsp;</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### CustomFields Definition

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
      <td>id</td>
      <td>string</td>
      <td>ID of the custom field to set.&nbsp;Available custom field IDs can be retrieved from the&nbsp;<strong>Get Custom Fields</strong>&nbsp;API operation.</td>
    </tr>
    <tr>
      <td>value</td>
      <td>string</td>
      <td>Value to set the custom field to for this server.</td>
    </tr>
  </tbody>
</table>

### AdditionalDisks Definition

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
      <td>path</td>
      <td>string</td>
      <td>File system path for disk (Windows drive letter or Linux mount point). Must not be one of reserved names.</td>
    </tr>
    <tr>
      <td>sizeGB</td>
      <td>int</td>
      <td>Amount in GB to allocate for disk, up to 1024 GB per.</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Whether the disk should be raw or partitioned</td>
    </tr>
  </tbody>
</table>

### Packages Definition

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
      <td>packageId</td>
      <td>string</td>
      <td>ID of the package to run on the server after it builds.&nbsp;Available package IDs can be retrieved from the&nbsp;<strong>Get Packages</strong>&nbsp;API operation.</td>
    </tr>
    <tr>
      <td>parameters</td>
      <td>complex&nbsp;</td>
      <td>Collection of name-value pairs to specify package-specific parameters.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "name": "web",
      "description": "My web server",
      "groupId": "wa1-1002",
      "sourceServerId": "RHEL-6-64-TEMPLATE",
      "isManagedOS": false,
      "primaryDns": "172.17.1.26",
      "secondaryDns": "172.17.1.27",
      "networkId": "101",
      "ipAddress": "10.123.456.12",
      "password": "Password123",
      "cpu": 2,
      "memoryGB": 4,
      "type": "standard",
      "storageType": "standard",
      "customFields":[
        {
          "id": "90b3c5e28162456781d36ee42c5771a3",
          "value": "custom value"
        }
      ],
      "additionalDisks":[
        {
          "path": "data",
          "sizeGB": 10,
          "type": "partitioned"
        }
      ],
      "ttl": "2014-12-17T01:17:17Z"
    }

## Response

### Entity Definition

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
      <td>server</td>
      <td>string</td>
      <td>ID of the server that the operation was performed on.</td>
    </tr>
    <tr>
      <td>isQueued</td>
      <td>boolean</td>
      <td>Boolean indicating whether the operation was successfully added to the queue.</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this server operation.</td>
    </tr>
    <tr>
      <td>errorMessage</td>
      <td>string</td>
      <td>If something goes wrong or the request is not queued, this is the message that contains the details about what happened.</td>
    </tr>
  </tbody>
</table>

### Links Definition

<table>
  <tbody>
    <tr>
      <td><strong>&nbsp;</strong>
      </td>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Value</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>Status Link</td>
      <td>rel</td>
      <td>string</td>
      <td>status</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/operations/[ALIAS]/status/[ID]</td>
      <td>Address of the server creation job in the queue</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[ID]</td>
      <td>The identifier of the job in queue. Can be passed to&nbsp;<a href="/api-docs/v2#queue-get-status">Get Status</a>&nbsp;call to retrieve status of job.</td>
    </tr>
  </tbody>
</table>


<table>
  <tbody>
    <tr>
      <td><strong>&nbsp;</strong>
      </td>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Value</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>Self Link</td>
      <td>rel</td>
      <td>string</td>
      <td>self</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/servers/[ALIAS]/[UUID]?uuid=True</td>
      <td>Address of the server created</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[ID]</td>
      <td>The ID of the server created</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>string</td>
      <td>GET</td>
      <td>Valid HTTP verbs that can act on this resource&nbsp;</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "server":"web",

      "isQueued":true,

      "links":[

        {

          "rel":"status",

          "href":"/v2/operations/alias/status/wa1-12345",

          "id":"wa1-12345"

        },

        {

          "rel":"self",

          "href":"/v2/servers/alias/8134c91a66784c6dada651eba90a5123?uuid=True",

          "id":"8134c91a66784c6dada651eba90a5123",

          "verbs":[

            "GET"

          ]

        }

      ]

    }