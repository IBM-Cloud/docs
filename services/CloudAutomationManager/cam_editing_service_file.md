---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-22"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Editing a service file
<!-- for example, Uploading your data -->
{: #cam_editing_service_file}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Use the correct syntax when importing or editing a service file. 
{:shortdesc}

A service file has the following structure:

```
{
	"service_metadata": {
	...
	},
	"service_parameters": [{
	...
	}],
	"service_conditions": [],
	"service_templates": [{
	...
	}],
	"service_process": {}
}
```

For information about the sections that are contained in the service file, see the following sections:

- [service_metadata](#cam_service_metadata)
- [service_parameters](#cam_service_parameters)
- [service_conditions](#cam_service_conditions)
- [service_templates](#cam_service_templates)
- [service_process](#cam_service_process)

For an example of a service file, see [Service file example](#cam_service_file_example).

## service_metadata
{: #cam_service_metadata}
```
"service_metadata": {
	"name": "The name of the service",		
	"description": "A short description of the service",
	"longDescription": "A long of description of the service",
	"providerDisplayName": "The provider of the service. For example: IBM",
	"image": "The name of the icon file. For example: serviceicon_1.svg",
	"version": "The version number. For example: 1",
	"author": "The author of the service",
	"tag": "The category to which the service is assigned",
	"bullets": [{
		"title": "The name of the first feature",
		"description": "A description for the first feature"
	},
	{
		"title": "The name of a the second feature",
		"description": "A description for the second feature"
	},
	...
	]
}
```

The information in the `service_metadata` section is the information that you provided in the **Overview** tab when you create the service. This information is overwritten if you import a service file in the **Edit Source Code** tab.

The `image` attribute value is the file name of the icon associated to the service. The file name must be `serviceicon_<n>.svg` where `<n>` is a number from 1 to 10. If you specify another file name, the `image` attribute value is changed by default to `serviceicon_1.svg`.

The `bullets` attribute contains the list of the service features. 

## service_parameters
{: #cam_service_parameters}
```
"service_parameters": [{
		"name": "The name of the service parameter",
		"label": "The label to be displayed in the user interface for this parameter",
		"description": "A description for this service parameter",
		"type": "The type of parameter. For example: text",
		"default": "The default value of the parameter",
		"hidden": "Specify if the parameter is not displayed in the user interface. The value must be true or false",
		"immutable": "Specify if the parameter is read only. The value must be true or false",
		"required": "Specify if the parameter is required. The value must be true or false",
		"secured": "Specify if the parameter value is shown as ********. The value must be true or false",
		"validation": "A valdation pattern for the value specified by the user",
		"dependent": "Specify if the parameter is dependent from another attribute. The value must be true or false",
		"dependent_attribute": "The name of the attribute on which the current attribute depends",
		"return_type": "The type of the parameter that is returned"
	},
	...
]
```

The `type` attribute can have `text` or `list` value. If the `type` value is `list`, in the `default` attribute specify the list of the values that can be assigned to the parameter in the format `["<First value>","<Second value>",...,"<Last value>"]`. For example, `["IBM Cloud","Amazon EC2"]`.

## service_conditions
{: #cam_service_conditions}
```
"service_conditions": []
```
This section is not used in the current beta release.

## service_templates
{: #cam_service_templates}

```
"service_templates": [{
	"template_name": "The name of the template", 
	"instance_name": "The name of the instance associated to this template when deployed",
	"cloud_connection_name": "The name of the cloud connection to be used to deploy the template",
	"template_params": [
		{
			"name": "The name of the template parameter",
			"label": "The label to be displayed in the user interface for this parameter",
			"description": "A description for this template parameter",
			"type": "The type of parameter. For example: text",
			"default": "The default value of the parameter",
			"hidden": "Specify if the parameter is not displayed in the user interface. The value must be true or false",
			"immutable": "Specify if the parameter is read only. The value must be true or false",
			"required": "Specify if the parameter is required. The value must be true or false",
			"secured": "Specify if the parameter value is shown as ********. The value must be true or false",
			"validation": "A valdation pattern for the value specified by the user"
		},
		{
		...
		}	
	]
}]
```

**Note:** In this beta release, you can specify only one template in the service file. 

The `type` attribute can have `text` or `list` value. If the `type` value is `list`, in the `default` attribute specify the list of the values that can be assigned to the parameter in the format `["<First value>","<Second value>",...,"<Last value>"]`. For example, `["IBM Cloud","Amazon EC2"]`.

If you want to set a template parameter to the value of a service parameter, specify the `default` attribute value like:
```
"default": "${service_parameters.<service_parameter_name>}
```

For example, if you have the following service parameter:
```
"service_parameters": [{
		"name": "datacenter",
		"label": "datacenter",
		"description": "Target vSphere datacenter for VM creationr",
		"type": "list",
		"default": ["vSphere datacenter 1","vSphere datacenter 2"],
		"hidden": "false",
		"immutable": "false",
		"required": "true",
		"secured": "false",
		"validation": "",
		"dependent": "",
		"dependent_attribute": "",
		"return_type": "text"	
	},
```
you can define the following template parameter to set its value to the related service parameter value that you select when ordering the service:
```
"template_params": [
		{
		"name": "datacenter",
		"label": "datacenter",
		"description": "Target vSphere datacenter for VM creation",
		"type": "text",
		"default": "${service_parameters.datacenter},
		"hidden": "true",
		"immutable": "false",
		"required": "true",
		"secured": "false",
		"validation": "",
		},
```
In the previous example, note that the `hidden` attribute value in the template parameter must be set to `true` to allow the template parameter value to be replaced with the service parameter value when ordering the service.

## service_process
{: #cam_service_process}
```
"service_process": {}
```
This section is not used in the current beta release.

## Service file example
{: #cam_service_file_example}

```
{
	"service_metadata": {
		"name": "Deploy Virtual Server with SSH Key on IBM SoftLayer",
		"description": "Virtual Server deployment on IBM SL as a service.",
		"longDescription": "Use this cloud resource template to quickly provision a Debian 7 64-bit virtual server with SSH key in a datacenter of your choice.",
		"providerDisplayName": "IBM",
		"image": "serviceicon_1.svg",
		"version": "1",
		"author": "Sandy",
		"tag": "Test category",
		"bullets": [{
			"title": "Clouds",
			"description": "IBM Cloud/SoftLayer"
		},
		{
			"title": "Template version",
			"description": "V1.0"
		},
		{
			"title": "Operating systems supported",
			"description": "IBM Cloud: Debian 7"
		},
		{
			"title": "Topology",
			"description": "IBM Cloud: 1 virtual machine"
		}]
	},
	"service_parameters": [{
			"name": "env",
			"label": "Environment",
			"description": "Which environment current template should be deployed in",
			"type": "list",
			"default": ["IBM Cloud"],
			"hidden": "false",
			"immutable": "false",
			"required": "true",
			"secured": "false",
			"validation": "",
			"dependent": "",
			"dependent_attribute": "",
			"return_type": "text"

	}],
	"service_conditions": [],
	"service_templates": [{
		"template_name": "1 Virtual Server with SSH Key",
		"instance_name": "SandyInstance1",
		"cloud_connection_name": "SandySL",
		"template_params": [
		    {
				"name": "public_ssh_key",
				"label": "Public SSH Key",
				"description": "Public SSH key used to conenct to virtual server",
				"type": "text",
				"default": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDXzmzQuIb/uHIATU2Nup01D6/V5CrL4vfpiOWXOnbUsM4fFZ48/WI23duUhHshUV9LuFWLtsuemAM1Af0nNZX06WUZGzfAs7GSKLwczF+k7k8od8EctNaTzWaHM+HBX5H8w8AilZHfWlADud+3JKPZzFh6TrpAeyym5Bgw3lbQz5rjrfQ17EBTMIhUE+VT+/OWUOF0cI5srAX5wj5BOuvVwNz8gmRCVQi2IJ0Zc40qX64Kih1V+6Dz+kOn86+jhmJoCCospNVq3WuJEhDkRZmq1rGxo2nDuT3GygM6jO/xJT25P6e0g2gQQQBwG2ktTUF/gp5gcmSxtZfJvPeLCUlX root@ico-135-1",
				"hidden": "false",
				"immutable": "false",
				"required": "true",
				"secured": "false",
				"validation": ""
			},{
				"name": "datacenter",
				"label": "SoftLayer Data Center",
				"description": "SoftLayer datacenter where infrastructure resources will be deployed",
				"type": "text",
				"default": "dal09",
				"hidden": "false",
				"immutable": "false",
				"required": "true",
				"secured": "false",
				"validation": ""
			},{
				"name": "hostname",
				"label": "Host Name",
				"description": "Host name of the virtual instance (small flavor) to be deployed",
				"type": "text",
				"default": "debian-host",
				"hidden": "false",
				"immutable": "false",
				"required": "true",
				"secured": "false",
				"validation": ""
			}
		]
	}],
	"service_process": {}
}
```
