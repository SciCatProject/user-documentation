# Central Configuration of Backend: ```.env```

The configuration file ```.env``` allows the systems administrator to configure connected services, like authentication services and message queues, and also switching on/off almost all available features and is read by the backend at runtime.

There are currently many configurable additions to SciCat which makes it very flexible these are:

* OIDC for identification
* LDAP for authentication
* Elastic Search
* SMTP for sending emails to notify users of SciCat jobs
* AMQP to provide a message queue for the jobs

## Environment Variables
All environment variables can be used in the ```.env``` filee. The current source code contains an example .env file, named _.env.example_, listing all (79) environment variables available to configure the backend. They can be found [here](https://github.com/SciCatProject/scicat-backend-next/blob/master/.env.example) and define

* How SciCat handles access rights and connects to other services e.g. to identity providers - such as LDAP or OIDC for authentication.
* How to configure [DOIs](#how-to-configure-doi-minting).
* How to configure elasitc search (ES)
* How to configure jobs

The list is compiled according to the configuration class defined in [_src/config/configuration.ts_](https://github.com/SciCatProject/scicat-backend-next/blob/master/src/config/configuration.ts).

- ADMIN\_GROUPS:  
  list of groups that have admin priviliges  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed.  

- DELETE\_GROUPS:  
  list of groups that are allowed to delete content  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed.  

- CREATE\_DATASET\_GROUPS:  
  list of non admin groups that are allowed to create datasets without pid. The pid is assigned by the system. If set to "#all", all users can create a dataset belonging to any of the groups they belong to.    
  _default_: "#all"  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed.  

- CREATE\_DATASET\_WITH\_PID\_GROUPS:  
  list of non admin groups that are allowed to create datasets with explicit pid. If set to "#all", all users can create a dataset belonging to any of the groups they belong to and with esplicit pid.  
  If the pid verification is enabled, pid will be validated agains the specification passed.  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed.  

- CREATE\_DATASET\_PRIVILEGED\_GROUPS:  
  list of non admin groups that are allowed to create datasets for groups they do not belong to. If set to "#all", all users can create a dataset belonging to any group with explicit pid.  
  If the pid verification is enabled, pid will be validated agains the specification passed.  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed.  

- PROPOSAL\_GROUPS:  
  list of non admin groups that are allowed to create and update proposals for groups they do not belong to. If set to "#all", all users can create a dataset belonging to any group with explicit pid.  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed  

- SAMPLE\_GROUPS:  
  list of non admin groups that are allowed to create and update samples for the groups they belong to. If set to "#all", all users can create a dataset belonging to their group.  
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed  

- SAMPLE\_PRIVILEGED\_GROUPS:  
  list of non admin groups that are allowed to create samples for any groups, but can only update samples belonging to groups they belong to.
  _default_: ""  
  _format_: comma separated list of strings. Leading and trailing spaces are trimmed  


- ACCESS\_GROUPS\_STATIC\_VALUES:  
  List of groups assigned by default to all users. Used in the vanilla implementation for easy configuration.  
  If you do not want or need to assign any default group, it should be set to empty string "".  
  Default value: ""  
  _format_: Comman separated list of strings. Leading and trailing spaces are trimmed  
  _example_: "group1,group2,group3,..."  

- ACCESS\_GROUP\_SERVICE\_TOKEN:
  Access token needed to access the API specified in ACCESS\_GROUP\_SERVICE\_API\_URL, used to retrieve access groups from a third party system.  
  _format*: string 

- ACCESS\_GROUP\_SERVICE\_API\_URL:  
  Well formed url of the service API used to provide access groups. Only one value is allowed.  
  _format_: string  
  _example_: "https://my.access.group/service/api/url"
  
- DOI_PREFIX:  
  The facility DOI prefix, with trailing slash.  
  _default_: ""  
  _format_: string  

- EXPRESS\_SESSION\_SECRET:  
  Secret used to set up express session.  
  _default_: ""  
  _format_: string  

- LOGOUT\_URL:  
  URL specified upon successful logout. It is returned in the json object for the frontend, or third party UI, to be used locally.  
  _default_: ""  
  _format_: string  

- HTTP\_MAX\_REDIRECTS:  
  Max number of redirects for http requests.  
  _default_: 5  
  _format_: integer  

- HTTP\_TIMEOUT:  
  Timeout from http requests in ms.  
  _default_: 5000  
  _format_: integer
  
- JWT_SECRET:  
  The secret used to create any JWT token, used for authorization.  
  _default_: ""  
  _format_: string  

- JWT\_EXPIRES\_IN:  
  Expiration time of any JWT token in seconds.  
  _default_: 3600 (s)  
  _format_: integer  

- JWT\_NEVER\_EXPIRES:  
  Length of time that the never expiring jwt token will last.  
  _default_: 100y  
  _format_: string as in number of years  

- LDAP\_URL:  
  Full URI (including port) of your local LDAP server, if this is your selected authentication method.  
  _default_: No default  
  _example_: ldaps://ldap.server.com:636/   
  _format_: string  

- LDAP\_BIND\_DN:  
  Bind DN to access information on your LDAP server.  
  _default_: No default  
  _format_: string  

- LDAP\_BIND\_CREDENTIALS:  
  Credentials associated with your bind DN to acccess your LDAP server.  
  _default_: No default  
  _format_: string  

- LDAP\_SEARCH\_BASE:  
  Search base for your LDAP server.  
  _default_: No default   
  _format_: string  

- LDAP\_SEARCH\_FILTER:  
  Search filter for you LDAP server.  
  _default_: No default  
  _format_: string   
  _example_: "(LDAPUsername={{username}})"  

- LDAP\_MODE:  
  type of ldap server we are communicating with  
  **_NEEDS TO BE UPDATED. Not sure which other values are accepted_**  
  _default_: ad  
  _format_: string  
  _acceptable values_: ad  
  
- LDAP\_EXTERNAL\_ID:  
  LDAP matching field that provides the external id  
  _default_: sAMAccountName  
  _format_: string  

- LDAP\_USERNAME:  
  LDAP field providing the username  
  _default_: displayName  
  _format_: string  

- OIDC\_ISSUER:  
  Full URL of your OIDC identity provider  
  _default_: No default  
  _format_: string  
  _example_: "https://identity.your.facility/your/realm"  

- OIDC\_CLIENT\_ID:  
  Client id used to convert OIDC code to OIDC token. This is assigned in the OIDC service when the token is generated  
  _default_: No default  
  _format_: string  
  _example_: "scicat"  

- OIDC\_CLIENT\_SECRET:   
  Token used to convert OIDC code to OIDC token. This is assigned in the OIDC service when the token is generated  
  _example_: "90f1268..."  

- OIDC\_CALLBACK\_URL:  
  URL of the endpoint that is called when the authentication has been executed with the OIDC service.   
  _default_: No default   
  _format_: string    
  _example_: "http://localhost:3000/api/v3/oidc/callback"  

- OIDC\_SCOPE:  
  Information returned by the OIDC service together with token  
  _default_: No default  
  _format_: string   
  _example_: "openid profile email"  

- OIDC\_SUCCESS\_URL:  
  Frontend URL that the user is directed to after a successful authentication. It must be a valid frontend URL.  
  _default_: No default  
  _format_: string  
  _example_: "http://localhost:3000/Datasets"  

- OIDC\_ACCESS\_GROUPS:  
  field used to retrieve access groups from the OIDC service. It is not used in the vanilla implementation.  
  _default_: No default  
  _format_: string  
  _example_: "access_groups"  

- OIDC\_ACCESS\_GROUPS\_PROPERTY:  
  name of the OIDC property used to retrieve the users groups from OIDC.  
  _default_: none  
  _format_: string  

- OIDC\_AUTO\_LOGOUT:  
  if enabled, when login out from SciCat, we logout from OIDC also.  
  _default_: false  
  _format_: boolean  

- OIDC\_RETURN\_URL:  
  URL the user is redirected after a successful logout  
  _default_: none  
  _format_: string  

- LOGBOOK\_ENABLED:  
  Flag to enable/disable the Logbook endpoints.  
  accept values: "yes", "no"  
  _default_: no   
  _format_: string  

- LOGBOOK\_BASE\_URL:  
  The base URL to the SciChat wrapper API. Only required if Logbook is enabled.  
  _default_: "http://localhost:3030/scichatapi"  
  _format_: string  

- LOGBOOK\_USERNAME:  
  The username used to authenticate to the SciChat wrapper API. Only required if Logbook is enabled.  
  _default_: No default  
  _format_: string  

- LOGBOOK\_PASSWORD:  
  The password used to authenticate to the SciChat wrapper API. Only required if Logbook is enabled.  
  _default_: No default  
  _format_: string  

- METADATA\_KEYS\_RETURN\_LIMIT:  
  The maximum number of keys returned by the `/Datasets/metadataKeys` endpoint.  
  _default_: No default  
  _format_: integer  

- METADATA\_PARENT\_INSTANCES\_RETURN\_LIMIT:  
  The maximum number of Datasets used to extract metadata keys in the `/Datasets/metadataKeys` endpoint.  
  _default_: No default  
  _format_: integer  

- MONGODB\_URI:  
  The URI for your MongoDB instance.  
  _default_: No default  
  _format_: string "mongodb://<USERNAME>:<PASSWORD>@<HOST>:27017/<DB_NAME>"  
  
- OAI\_PROVIDER\_ROUTE:  
  URI to OAI provider, which is used in the `/publisheddata/:id/resync` endpoint.  
  _default_: no default  
  _format_: string  

- PID\_PREFIX:  
  The facility PID prefix, with trailing slash.  
  _default_: no default  
  _format_: string  

- PUBLIC\_URL\_PREFIX:  
  The base URL to the facility Landing Page.  
  _default_: No default  
  _format_: string  
  _example_: "https://doi.ess.eu/detail/"  

- PORT:  
  The port on which the backend listen on.  
  _default_: 3000  
  _format_: integer  

- RABBITMQ\_ENABLED:  
  Flag to enable/disable RabbitMQ consumer.  
  accepted values: "yes", "no"  
  _deprecated_. Will be removed in future releases.  
  _default_: no  
  _format_: string  
  
- RABBITMQ\_HOSTNAME:  
  The hostname of the RabbitMQ message broker. Only required if RabbitMQ is enabled.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _default_: string  

- RABBITMQ\_USERNAME:  
  The username used to authenticate to the RabbitMQ message broker. Only required if RabbitMQ is enabled.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string  

- RABBITMQ\_PASSWORD:  
  The password used to authenticate to the RabbitMQ message broker. Only required if RabbitMQ is
  enabled.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string  

- REGISTER\_DOI\_URI:  
  URI to the organization that registers the facilities DOIs.  
  _default_: no default  
  _format_: string  
  _example_: "https://mds.test.datacite.org/doi"  

- REGISTER\_METADATA\_URI:  
  URI to the organization that registers the facilities published data metadata.  
  _default_: no default  
  _format_: string  
  _example_: ="https://mds.test.datacite.org/metadata"  

- DOI\_USERNAME:
  Username used to authenticate on the DOI site  
  _default_: no default  
  _format_: string  

- DOI\_PASSWORD:  
  Password used to authenticate on the DOI site  
  _default_: no default  
  _format_: string  

- SITE:  
  The name of your site.  
  _default_: no default  
  _format_: string  

- SMTP\_HOST:  
  Host of SMTP server.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string  

- SMTP\_MESSAGE\_FROM:  
  Email address that emails should be sent from.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string, email  

- SMTP\_PORT:  
  Port of SMTP server.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string  

- SMTP\_SECURE:  
  Secure of SMTP server.  
  _deprecated_. Will be removed in future releases.  
  _default_: no default  
  _format_: string  

- POLICY\_PUBLICATION\_SHIFT:  
  Number of years that needs to elapse before the dataset is made publicly acceessible  
  _default_: 3  
  _format_: integer  

- POLICY\_RETENTION\_SHIFT:  
  Number of years that the datasets are kept online before are archived or deleted. A negative value means that they are never archived/deleted  
  _default_: -1  
  _format_: integer  

- ELASTICSEARCH\_ENABLED:  
  Flag to enable/disable the ElasticSearch service  
  accept values: "yes", "no"  
  _default_: no default  
  _format_: string  

- ES\_HOST:  
  The base URL to the Elasticsearch cluster. Use `http` if xpack.security is disabled  
  _default_: no default  
  _format_: string   
  _example_: "https://localhost:9200" or "http://localhost:9200"  

- MONGODB\_COLLECTION:  
  Collection name to be mapped into specified Elasticsearch index  
  _default_: no default  
  _format_: string  
 
- ES\_MAX\_RESULT:   
  Maximum records can be indexed into Elasticsearch.  
  _default_: 10000  
  _format_: number  

- ES\_FIELDS\_LIMIT:   
  The total number of fields in an index.  
  _default_: 1000  
  _format_: number  

- ES\_INDEX:  
  The total number of fields in an index.  
  _default_: no default  
  _format_: string  

- ES\_REFRESH:  
  The total number of fields in an index.  
  accept values: true, false, "wait_for"  
  _default_: false  
  _format_: boolean or string  

- ES\_USERNAME:  
  Elasticsearch cluster username.  
  _default_: no default, optional.  
  _format_: string  

- ELASTIC\_PASSWORD:   
  Elasticsearch cluster password.  
  _default_: no default.  
  _format_: string  

## Environment Variables as now
```
ACCESS_GROUP_SERVICE_API_URL=""
ACCESS_GROUP_SERVICE_TOKEN=""
DOI_PREFIX="<DOI_PREFIX>"
EXPRESS_SESSION_SECRET="<EXPRESS_SESSION_SECRET>"
HTTP_MAX_REDIRECTS=5
HTTP_TIMEOUT=5000
JWT_SECRET=<JWT_SECRET>
JWT_EXPIRES_IN=3600
LDAP_URL="ldaps://ldap.server.com:636/"
LDAP_BIND_DN="<USERNAME>@server.com"
LDAP_BIND_CREDENTIALS=<PASSWORD>
LDAP_SEARCH_BASE=<SEARCH_BASE>
LDAP_SEARCH_FILTER="(LDAPUsername={{username}})"
LOGBOOK_ENABLED="no"
LOGBOOK_BASE_URL="http://localhost:3030/scichatapi"

METADATA_KEYS_RETURN_LIMIT=100
METADATA_PARENT_INSTANCES_RETURN_LIMIT=100
MONGODB_URI="mongodb://<USERNAME>:<PASSWORD>@<HOST>:27017/<DB_NAME>"
OAI_PROVIDER_ROUTE="<OAI_PROVIDER_ROUTE>"
PID_PREFIX="<PID_PREFIX>"
PUBLIC_URL_PREFIX="https://doi.esss.se/detail/"
PORT=3000
RABBITMQ_ENABLED=<"yes"|"no">
RABBITMQ_HOSTNAME="localhost"
RABBITMQ_USERNAME="rabbitmq"
RABBITMQ_PASSWORD="rabbitmq"
REGISTER_DOI_URI="https://mds.test.datacite.org/doi"
REGISTER_METADATA_URI="https://mds.test.datacite.org/metadata"
DOI_USERNAME="username"
DOI_PASSWORD="password"
SITE=<SITE>
EMAIL_TYPE=<"smtp"|"ms365">
EMAIL_FROM=<MESSAGE_FROM>
SMTP_HOST=<SMTP_HOST>
SMTP_PORT=<SMTP_PORT>
SMTP_SECURE=<"yes"|"no">
MS365_TENANT_ID=<tenantId>
MS365_CLIENT_ID=<clientId>
MS365_CLIENT_SECRET=<clientSecret>

DATASET_CREATION_VALIDATION_ENABLED=true
DATASET_CREATION_VALIDATION_REGEX="^[0-9A-F]{8}-[0-9A-F]{4}-4[0-9A-F]{3}-[89AB][0-9A-F]{3}-[0-9A-F]{12}$"

ADMIN_GROUPS=""
DELETE_GROUPS=""
CREATE_DATASET_GROUPS="all"
CREATE_DATASET_WITH_PID_GROUPS=""
CREATE_DATASET_PRIVILEGED_GROUPS=""
CREATE_JOB_GROUPS=""
UPDATE_JOB_GROUPS=""
SAMPLE_PRIVILEGED_GROUPS="sampleingestor"
SAMPLE_GROUPS="group1"
PROPOSAL_GROUPS=""

ACCESS_GROUPS_GRAPHQL_ENABLED=true
ACCESS_GROUP_SERVICE_TOKEN=""
ACCESS_GROUP_SERVICE_API_URL=""
ACCESS_GROUP_SERVICE_HANDLER=""
ACCESS_GROUPS_STATIC_ENABLED=true
ACCESS_GROUPS_OIDCPAYLOAD_ENABLED=true

OIDC_USERINFO_MAPPING_FIELD_USERNAME="iss, sub"
OIDC_USERINFO_MAPPING_FIELD_DISPLAYNAME="preferred_username"
OIDC_USERINFO_MAPPING_FIELD_EMAIL="email"
OIDC_USERINFO_MAPPING_FIELD_GROUP="groups"
OIDC_USERQUERY_OPERATOR=<"or"|"and">
OIDC_USERQUERY_FILTER="username:username, email:email"

ELASTICSEARCH_ENABLED=<"yes"|"no">
STACK_VERSION="8.8.2"
CLUSTER_NAME="es-cluster"
MEM_LIMIT="4G"
MONGODB_COLLECTION="Dataset"
ES_MAX_RESULT=100000
ES_FIELDS_LIMIT=400000
ES_INDEX="dataset"
ES_PORT=9200
ES_HOST="https://localhost:9200"
ES_USERNAME="elastic"
ES_PASSWORD="duo-password"
ES_REFRESH=<"wait_for"|"false">

LOGGERS_CONFIG_FILE="loggers.json"
DATASET_TYPES_FILE="datasetTypes.json"
PROPOSAL_TYPES_FILE="proposalTypes.json"
```
### How to configure to connect the backend to other services
In [scicatlive](https://www.scicatproject.org/scicatlive/latest/services/backend/) you find documentation on how to integrate your SciCat system with services providing identities, (e.g. KeyCloak) and authentication (OpenLDAP).

### How to configure DOI minting 
In SciCat one can publish selected datasets that triggers a DOI minting process. Find [here](../datasets/Publishing.md) a short introduction and instructions how to set up such a service. SciCat also has the option to make datasets publicly via APIs available, to get a better idea of that follow [this Link](dois.md)


## More advanced options
If you are compiling the application from source, you can edit the file _src/config/configuration.ts_ with the correct values for your infrastructure. **This option is still undocumented, although it is our intention to provide a detailed how-to guide as soon as we can.**
