# SemanticDT_TD

## RAW CONTEXT

<https://raw.githubusercontent.com/Salva5297/SemanticDT_TD/main/context/sdt.td.context.json-ld>

---

## Dimensions

- [x] Physical Entities (Sensors/Actuators/Devices)
	- [x] Components
- [x] Virtual Entities
	- [x] Models
	- [x] Schemas
- [x] Digital Twin Data
	- [x] Internal
	- [x] External
- [x] Digital Twin Services (THIS IS ALREADY SATISFIED BY TRADITIONAL THING DESCRIPTIONS)
	- [x] Internal --> Described in the DT as a normal TD
	- [x] External --> Described in other DT TDs --> This can be seen by the connection part
- [x] Digital Twin Connections
	- [x] Internal
	- [x] External --> External DTs --> In this case, it is a definition of a DTA not a DTI

- [ ] Add formats to context
---
## Physical Entities
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Physical Entity". |
| `@id` | required | IRI / URN | An identifier for the Physical Entity. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `components` | required | set of [Components](#components) | A set of components that are described in the Physical Entities. |
### Components
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Component", "Sensor" or "Actuator". |
| `@id` | optional | IRI | An identifier for the Component. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the model is allocated. |
### Example

```json
"pe" : [
	{
		"@id" : "data:SDT-TD-1/pe/1",
		"@type" : "Physical Entity",
		"name" : "Physical Entity 1",
		"description" : "Physical Entity 1 description.",
		"comment" : "Just a Comment.",
		"components" : [
			{
				"@id" : "sensor_td_id",
				"@type" : "Sensor",
				"name" : "Name of the Sensor Thing Description.",
				"description" : "Description of the Sensor Thing Description.",
				"href" : ["https://.../td/sensor_td_id"]
			},
			{
				"@id" : "actuator_td_id",
				"@type" : "Actuator",
				"name" : "Name of the Actuator Thing Description.",
				"description" : "Description of the Actuator Thing Description.",
				"href" : ["https://.../td/actuator_td_id"]
			}
		]
	},
	{}
]
```

---
### Virtual Entities
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Virtual Entity". |
| `@id` | required | IRI / URN | An identifier for the Virtual Entity. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `models` | required | set of [Models](#models) | A set of models that define the contents of this Virtual Entity. |
### Models
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Model" (Models described in the ontology). |
| `@id` | optional | IRI | An identifier for the Model. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the model is allocated. |
| `extends` | optional | set of [Models](#model) | A set of models that this models refers/extends. |
| `formats` | optional | set of [Formats](#formats) | A set of formats used to describe the model. |
### Formats
#### Simple_Format
| Format | Description |
| ---- | ---- |
| `json` | JSON file format |
| `ifc` | IFC file format |
| `ttl` | Turtle file format |
| `json-ld` | JSON-LD file format |
| `rdf` | RDF file format |
| `xml` | XML file format |
| `html` | HTML file format |
| `csv` | CSV file format |
| `html` | HTML file format |
| `boolean` | a *boolean* value |
| `date` | a date in ISO 8601 format, per [RFC 3339](https://tools.ietf.org/html/rfc3339) |
| `dateTime` | a date and time in ISO 8601 format, per [RFC 3339](https://tools.ietf.org/html/rfc3339) |
| `double` | a finite numeric value that is expressible in IEEE 754 double-precision floating point format, conformant with *xsd:double* |
| `duration` | a duration in ISO 8601 format |
| `float` | a finite numeric value that is expressible in IEEE 754 single-precision floating point format, conformant with *xsd:float* |
| `integer` | a signed integral numeric value that is expressible in 4 bytes |
| `long` | a signed integral numeric value that is expressible in 8 bytes |
| `string` | a UTF8 string |
| `time` | a time in ISO 8601 format, per [RFC 3339](https://tools.ietf.org/html/rfc3339) |
| `http` | a request-response protocol |
| `mqtt` | a publish-subscribe protocol |
| ... | ... |
#### Complex Format
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Format". |
| `@id` | optional | IRI | An identifier for the Format. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the model is allocated. |
| `format` | required | a [Simple Format](#simple_format) | A simple format to describe the model. |
### Example

```json
"ve" : [
	{
		"@id" : "data:SDT-TD-1/ve/1",
		"@type" : "Virtual Entity",
		"name" : "Virtual Entity 1",
		"description" : "Virtual Entity 1 description.",
		"comment" : "Just a Comment.",
		"models" : [
			{
				"@id" : "sdt:1:onto;1",
				"@type" : "Ontology_Model",
				"name" : "Ontology",
				"description" : "Description of the Ontology",
				"extends" : ["https://.../def/onto#"],
				"formats" : [
					{
						"@id" : "sdt:1:format:ttl",
						"@type" : "Format",
						"name" : "Turtle",
						"comment" : "",
						"description" : "Contains Ontology X Extension in Turtle Format.",
						"href" : "https://.../*.ttl",
						"format" : "ttl"
					},
					{
						"@id" : "sdt:1:format:json-ld",
						"@type" : "Format",
						"name" : "JSON-LD",
						"comment" : "",
						"description" : "Contains Ontology X Extension in JSON-LD Format.",
						"href" : "https://.../*.json",
						"format" : "json-ld"
					},
					{
						"@id" : "sdt:1:format:xml",
						"@type" : "Format",
						"name" : "XML",
						"comment" : "",
						"description" : "Contains Ontology X Extension in XML format.",
						"href" : "https://.../*.xml",
						"format" : "xml"
					}
				]
			},
			{
				"@id" : "sdt:1:shacl;1",
				"@type" : "SHACL_Shapes_Model",
				"name" : "SHACL Shapes",
				"description" : "SHACL Shapes used to validate the Knowledge Graph information of the DT",
				"extends" : ["https://.../original.ttl"],
				"formats" : [
					{
						"@id" : "sdt:1:format:ttl",
						"@type" : "Format",
						"name" : "Turtle",
						"comment" : "",
						"description" : "Contains SHACL Shapes Extension in Turtle Format.",
						"href" : "https://.../*.ttl",
						"format" : "ttl"
					}
				]
			}
		]
	},
	{}
]
```

---
## Digital Twin Data
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Digital Twin Data". |
| `@id` | required | IRI / URN | An identifier for the Digital Twin Data. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `storages` | required | set of [Storages](#storages) | A set of models that define the storages of this Digital Twin Data. |
### Storages
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Triplestore", "FileStorage" or "File". |
| `@id` | required | IRI / URN | An identifier for the Storage. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `endpoint` | required | IRI | A link where the storage can be queried to obtain the information. |
| `default-graph` | optional | IRI | A link of the default graph that contains the information needed at a "Triplestore". |
| `format` | required | a [Simple Format](#simple_format) | A simple format to describe the datatype of the data stored. |
| `internal` | required | *boolean* | A *boolean* value that informs if the data is inside the SDT or is outside of it. |
### Example

```json
"dd" : [
	{
		"@id" : "data:SDT-TD-1/dd/1",
		"@type" : "Digital Twin Data",
		"name" : "Digital Twin Data 1",
		"description" : "Digital Twin Data 1 description.",
		"comment" : "Just a comment.",
		"storages" : [
			{
				"@id" : "sdt:1:triplestore",
				"@type" : "Triplestore",
				"name" : "Ontotext GraphDB Triplestore",
				"description" : "Ontotext GraphDB Triplestore used to store knowledge graphs.",
				"comment" : "Just a comment.",
				"endpoint" : "https://triplestore.../sparql",
				"default-graph" : "https://triplestore.../statements/default-graph",
				"format" : "rdf",
				"internal" : "true"
			},
			{
				"@id" : "sdt:1:ifc_file:12345",
				"@type" : "File",
				"name" : "IFC File 1234",
				"description" : "IFC File with identifier '1234', that contains the construction information of SDT1.",
				"comment" : "Just a comment.",
				"endpoint" : "https://dtp.../files/x.ifc",
				"format" : "ifc",
				"internal" : "false"
			}
		]
	},
	{}
]
```

---
## Digital Twin Connections
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Digital Twin Connection", "DD-SS", "DD-DD" or "SS-SS". |
| `@id` | required | IRI / URN | An identifier for the Digital Twin Connection. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `connections` | required | set of [Connections](#connections) | A set of connections that define the Digital Twin Connections. |
| `dt_connections` | optional | set of [DTConnections](#dt_connections) | A set of connections with external Semantic Digital Twins. |
### Connections
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Digital_Twin_Data" or "Digital_Twin_Service". |
| `@id` | required | IRI / URN | An identifier for the Connection. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `internal` | required | *boolean* | A *boolean* value that informs if the element of the connection is in the SDT or is outside of it. |
| `href` | required | IRI | A link where one of the points of the connection is used by the others in order to create the connection. |
| `function` | required | *string* | A function that is made. This must be "client" or "server". |
### DT_Connections
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "SDT". |
| `@id` | required | IRI / URN | An identifier for the SDT. |
| `name` | optional | *string* | A localizable name for display. |
| `comment` | optional | *string* | A comment for model authors. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the SDT Thing Description is allocated. |
### Example

```json
"cn" : [
	{
		"@id" : "data:SDT-TD-1/cn/1",
		"@type" : "Digital Twin Connection",
		"name" : "Digital Twin Connection 1",
		"description" : "Digital Twin Connection 1 description.",
		"comment" : "Just a comment.",
		"connections" : [
			{
				"@id" : "sdt:1:service:1",
				"@type" : "Digital_Twin_Service",
				"name" : "Service 1",
				"description" : "Service 1 of the SDT",
				"comment" : "Just a comment.",
				"href" : "https://service1.../execute_job",
				"function" : "client",
				"internal" : "true"
			},
			{
				"@id" : "sdt:1:ifc_file:12345",
				"@type" : "Digital_Twin_Data",
				"name" : "IFC File 1234",
				"description" : "IFC File with identifier '1234', that contains the construction information of SDT1.",
				"comment" : "Just a comment.",
				"href" : "https://dtp.../files/x.ifc",
				"function" : "server",
				"internal" : "false"
			}
		],
		"dt_connections" : [
			{
				"@id" : "sdt:2",
				"@type" : "SDT",
				"name" : "Semantic Digital Twin 2",
				"description" : "Semantic Digital Twin 2 that makes function X",
				"comment" : "Just a comment.",
				"href" : "https://.../td/sdt_td_2"
			},
			{}
		]
	},
	{}
]
```
