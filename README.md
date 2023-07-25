![Simulation Controller GitHub](https://github.com/citysciencelab/cut-masterportal-simulation-controller/assets/61881523/bdc5bd48-873e-4f63-ba8e-955286d23228)

# Simulation Controller Masterportal Add-On 
The Simulation Controller is an inofficial Masterportal Add-On developed in the [Connected Urban Twins](https://www.connectedurbantwins.de/en/) project to connect the Masterportal to the [Urban Model Platform](https://github.com/citysciencelab/urban-model-platform) architecture. In order to understand the architecture of the Urban Model Platform, we refer to [its repository](https://github.com/citysciencelab/urban-model-platform).

## Configuration
The frontend can be configured to provide a selected list of simulation models (= processes) provided by the backend api. All necessary configuration is done in the [config.js](/portal/simulation/config.js), the [config.json](/portal/simulation/config.json) and the [services-internet.json](/portal/simulation/resources/services-internet.json) file.

### config.js
It is necessary to enable the addon in the portal configuration by listing it in the addons array ```addons: ["simulationTool"]```. Further, it is necessary to specify the url of the OGC API Processes conformant Urban Model Platform by setting the ```simulationApiUrl: "https://urban-model-platform.de/api" ``` attribute. Note that is should be the url to the landing page of the API processes, not the /processes page.  


### config.json
In the config.json, the simulation layers are configured as any other layers in the Masterporal by linking to the specific ID in the [services-internet.json](/portal/simulation/resources/services-internet.json).

### services-internet.json
There are various parameters that one needs to set in order to configure one layer as a simulation layer.
- ```id``` should correspond to the ID configured in the config.json file
- ```isSimulationLayer``` needs to be set on true
- ```simModelId``` refers to the model/process ID of the Urban Model Platform in the style of ```provider:modelId````. The list of available process IDs is provided by the backend endpoint <base url>/api/processes.
- ```filterOnClient```can be set to true if all the features from the simulation layer should be loaded in the client to be filtered there. Otherwise, the features are filtered on the Urban Model Platform. This is a choice to make depending on how many features will be the simulation results. If there are only few, it's best to filter on the client. If there are many, it is best to filter on the server side. 
- ```url``` should point to the Geoserver workspace that stores the results of the different simulation platforms, such as ```https://your-geoserver-instance.com/geoserver/workspace/ows```

## Setup
Please refer to the [Masterportal](#masterportal) to have a complete overview of the setup. In short, clone this repo, make sure that node is installed on your machine, run ```npm i```and then ```npm start``` and a development portal instance including the Simulation controller AddOn should be running. 

## Masterportal
The Masterportal is a tool-kit to create geo web applications based on [OpenLayers](https://openlayers.org), [Vue.js](https://vuejs.org/) and [Backbone.js](https://backbonejs.org). The Masterportal is Open Source Software published under the [MIT License](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/dev/License.txt).

The Masterportal is a project by [Geowerkstatt Hamburg](https://www.hamburg.de/geowerkstatt/).
