# SemanticDT_TD

## Ontology

![SDT Ontology](./ontology/dt_ontology.svg)

## RAW CONTEXT

<https://raw.githubusercontent.com/Salva5297/SemanticDT_TD/main/context/sdt.td.context.jsonld>

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
---
## Physical Entities
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Physical Entity". |
| `@id` | required | IRI / URN | An identifier for the Physical Entity. |
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `components` | required | set of [Components](#components) | A set of components that are described in the Physical Entities. |
### Components
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Component", "Sensor" or "Actuator". |
| `@id` | optional | IRI | An identifier for the Component. |
| `title` | optional | *string* | A localizable title for display. |
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
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `models` | required | set of [Models](#models) | A set of models that define the contents of this Virtual Entity. |
### Models
| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Model" (Models described in the ontology). |
| `@id` | optional | IRI | An identifier for the Model. |
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the model is allocated. |
| `aggregates` | optional | set of [Models](#model) | A set of models that this models refers/extends. |
| `formats` | optional | set of [Formats](#formats) | A set of formats used to describe the model. |
### Formats

| Property | Required | Data type | Description |
| --- | --- | --- | --- |
| `@type` | required | IRI | This must be "Format". |
| `@id` | optional | IRI | An identifier for the Format. |
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the model is allocated. |
| `extension` | required | *string* | An extension in which the model is described. |
### Example

```json
"ve" : [
	{
		"@id" : "data:SDT-TD-1/ve/1",
		"@type" : "Virtual Entity",
		"name" : "Virtual Entity 1",
		"description" : "Virtual Entity 1 description.",
		"models" : [
			{
				"@id" : "sdt:1:onto;1",
				"@type" : "Ontology_Model",
				"name" : "Ontology",
				"description" : "Description of the Ontology",
				"aggregates" : ["https://.../def/onto#"],
				"formats" : [
					{
						"@id" : "sdt:1:format:ttl",
						"@type" : "Format",
						"name" : "Turtle",
						"description" : "Contains Ontology X Extension in Turtle Format.",
						"href" : "https://.../*.ttl",
						"extension" : "ttl"
					},
					{
						"@id" : "sdt:1:format:json-ld",
						"@type" : "Format",
						"name" : "JSON-LD",
						"description" : "Contains Ontology X Extension in JSON-LD Format.",
						"href" : "https://.../*.json",
						"extension" : "json-ld"
					},
					{
						"@id" : "sdt:1:format:xml",
						"@type" : "Format",
						"name" : "XML",
						"description" : "Contains Ontology X Extension in XML format.",
						"href" : "https://.../*.xml",
						"extension" : "xml"
					}
				]
			},
			{
				"@id" : "sdt:1:shacl;1",
				"@type" : "SHACL_Shapes_Model",
				"name" : "SHACL Shapes",
				"description" : "SHACL Shapes used to validate the Knowledge Graph information of the DT",
				"aggregates" : ["https://.../original.ttl"],
				"formats" : [
					{
						"@id" : "sdt:1:format:ttl",
						"@type" : "Format",
						"name" : "Turtle",
						"description" : "Contains SHACL Shapes Extension in Turtle Format.",
						"href" : "https://.../*.ttl",
						"extension" : "ttl"
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
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `data` | required | set of [Data](#data) | A set of models that define the storages of this Digital Twin Data. |
### Data
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Triplestore", "FileStorage" or "File". |
| `@id` | required | IRI / URN | An identifier for the Storage. |
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `href` | required | IRI | A link where the storage can be queried to obtain the information. |
| `default-graph` | optional | IRI | A link of the default graph that contains the information needed at a "Triplestore". |
| `extension` | required | string | An extension in which the data is described. |
| `internal` | required | *boolean* | A *boolean* value that informs if the data is inside the SDT or is outside of it. |
### Example

```json
"dd" : [
	{
		"@id" : "data:SDT-TD-1/dd/1",
		"@type" : "Digital Twin Data",
		"name" : "Digital Twin Data 1",
		"description" : "Digital Twin Data 1 description.",
		"data" : [
			{
				"@id" : "sdt:1:triplestore",
				"@type" : "Triplestore",
				"name" : "Ontotext GraphDB Triplestore",
				"description" : "Ontotext GraphDB Triplestore used to store knowledge graphs.",
				"endpoint" : "https://triplestore.../sparql",
				"default-graph" : "https://triplestore.../statements/default-graph",
				"extension" : "rdf",
				"internal" : "true"
			},
			{
				"@id" : "sdt:1:ifc_file:12345",
				"@type" : "File",
				"name" : "IFC File 1234",
				"description" : "IFC File with identifier '1234', that contains the construction information of SDT1.",
				"endpoint" : "https://dtp.../files/x.ifc",
				"extension" : "ifc",
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
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `connections` | required | set of [Connections](#connections) | A set of connections that define the Digital Twin Connections. |
| `sdt_connections` | optional | set of [DTConnections](#dt_connections) | A set of connections with external Semantic Digital Twins. |
### Connections
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "Digital_Twin_Data" or "Digital_Twin_Service". |
| `@id` | required | IRI / URN | An identifier for the Connection. |
| `title` | optional | *string* | A localizable title for display. |
| `description` | optional | *string* | A localizable description for display. |
| `internal` | required | *boolean* | A *boolean* value that informs if the element of the connection is in the SDT or is outside of it. |
| `href` | required | IRI | A link where one of the points of the connection is used by the others in order to create the connection. |
| `function` | required | *string* | A function that is made. This must be "client" or "server". |
### DT_Connections
| Property | Required | Data type | Description |
| ---- | ---- | ---- | ---- |
| `@type` | required | IRI | This must be "SDT". |
| `@id` | required | IRI / URN | An identifier for the SDT. |
| `title` | optional | *string* | A localizable title for display. |
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
		"connections" : [
			{
				"@id" : "sdt:1:service:1",
				"@type" : "Digital_Twin_Service",
				"name" : "Service 1",
				"description" : "Service 1 of the SDT",
				"href" : "https://service1.../execute_job",
				"function" : "client",
				"internal" : "true"
			},
			{
				"@id" : "sdt:1:ifc_file:12345",
				"@type" : "Digital_Twin_Data",
				"name" : "IFC File 1234",
				"description" : "IFC File with identifier '1234', that contains the construction information of SDT1.",
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
				"href" : "https://.../td/sdt_td_2"
			},
			{}
		]
	},
	{}
]
```
