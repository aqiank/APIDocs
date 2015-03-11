{{{
  "title": "GetAllServersByModifiedDates",
  "date": "12-26-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets a deep list of all modified Servers for a given Hardware Group and its sub groups, or all Servers for a given location. To get all servers that have changed since a certain date, only provide a BeginDate and omit the EndDate.

## URL

    REST: https://api.tier3.com/REST/Server/GetAllServersByModifiedDates/<format>
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetAllServersByModifiedDatesResponseMsg

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
      <td>The alias of the account that owns the servers. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to query a particular sub-account.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>The ID of the Hardware Group, or 0 if providing Location.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The data center location.&nbsp; Otherwise leave blank and provide HardwareGroupID or let it default to account's primary data center.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>BeginDate</td>
      <td>DateTime</td>
      <td>Beginning of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value equals today minus one day.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>DateTime</td>
      <td>End of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value is set to the current date time.&nbsp;</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

    "AccountAlias": "ACCT",

    "Location": "WA1",

    "BeginDate": "2013-05-01",

    "EndDate": "2013-06-30"

    }

#### XML

    <GetAllServersRequest>

        <AccountAlias>ACCT</AccountAlias>

        <Location>WA1</Location>

        <BeginDate>2013-05-01</BeginDate>

        <EndDate>2013-06-30</EndDate>

    </GetAllServersRequest>

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
      <td>Servers</td>
      <td>Complex</td>
      <td>A list of&nbsp;[Server Objects](server-object.md)
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
        "Success":true,
        "Message":"Success",
        "StatusCode":0,
        "Servers":[
            {"ID":1001,"HardwareGroupID":1,"Name":"WA1T3NWEB01","Description":"WA1T3NWEB01",
                "DnsName":"WA1T3NWEB01","IsTemplate":false,"Cpu":2,"MemoryGB":4,"DiskCount":3,
                "TotalDiskSpaceGB":116,"Status":"Active","ServerType":"2","ServiceLevel":"1",
                "OperatingSystem":4,"PowerState":"Started","Location":"WA1","IPAddress":"172.0.0.1"
                "IPAddresses:[
                    {"Address":"172.0.01", "AddressType":1}
                ],"CustomFields":[
                    { "CustomFieldID": 100,"Name": "My Field", "Type": "Text", "Value": "A test"},
                    { "CustomFieldID": 101,"Name": "My Field 2","Type": "Option","Value": "2"},
                    { "CustomFieldID": 102,"Name": "My Field 3","Type": "Checkbox","Value": "true"},]},

            {"ID":1002,"HardwareGroupID":1,"Name":"WA1T3NWEB02","Description":"WA1T3NWEB02",
                "DnsName":"WA1T3NWEB02","IsTemplate":false,"Cpu":2,"MemoryGB":4,"DiskCount":3,
                "TotalDiskSpaceGB":116,"Status":"Active","ServerType":"1","ServiceLevel":"2",
                "OperatingSystem":6,"PowerState":"Started","Location":"WA1","IPAddress":"172.0.0.2"
                "IPAddresses:[
                    {"Address":"172.0.02", "AddressType":1}
                ], "CustomFields": [] }
         ]
    }

#### XML

    <GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0">
        <Servers>
            <Server ID="1001" HardwareGroupID="1" Name="WA1T3NWEB01" Description="WA1T3NWEB01"
                    DnsName="WA1T3NWEB01" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3"
                    TotalDiskSpaceGB="116" Status="Active" ServerType="1" ServiceLevel="2"
                    OperatingSystem="2" PowerState="Started" Location="WA1" IPAddress="172.0.0.1">
                <IPAddresses>
                    <IPAddress Address="172.0.0.1" AddressType="RIP" />
                </IPAddresse>
                <CustomFields CustomFieldID="100" Name="My Field" Type="Text" Value="Test Value" />
                <CustomFields CustomFieldID="101" Name="My 2nd Field" Type="Option" Value="Value 3" />
                <CustomFields CustomFieldID="102" Name="My 3rd Field" Type="Checkbox" Value="true" />
            </Server>
            <Server ID="1002" HardwareGroupID="1" Name="WA1T3NWEB02" Description="WA1T3NWEB02"
                    DnsName="WA1T3NWEB02" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3"
                    TotalDiskSpaceGB="116" Status="Active" ServerType="2" ServiceLevel="1"
                    OperatingSystem="6" PowerState="Started" Location="WA1" IPAddress="172.0.0.2"
                <IPAddresses>
                    <IPAddress Address="172.0.0.2" AddressType="RIP"/>
                </IPAddresses>
                <CustomFields />
           </Server>
        </Servers>
    </GetServersResponse>

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
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Group with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>