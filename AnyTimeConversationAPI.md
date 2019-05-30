
# EmailAccounts
## objects 
### emailAccount
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of email account |
| `type`| string | Exchange, IMAP, Email Forwarding|
| `businessEmail` | string | your business email address |
| `displayName` | string | the display name your recipients will see |
| `serverInfo` | dynamic | [exchangeServer](#exchangeServer), [IMAPServer](#IMAPServer), [emailForwardingServer](#emailForwardingServer) |
| `assignedDepartment` | string | default assigned department |
| `assignedAgent` | string | default assigned agent |
| `status` | boolean | success, failed |
| `lastReceivedTime` | datetime | last received time |
| `enable` | boolean | if enable email account |
| `isDefault` | boolean | if is default email account |

### exchangeServer
| Name | Type | Description | 
| - | - | - | 
| `userName` | string | user name | 
| `serverUrl`| boolean | exchange web server url | 

### IMAPServer
| Name | Type | Description | 
| - | - | - | 
| `userName` | string | user name | 
| `incomingServer`| string | incoming mail server(IMAP) |
| `incomingServerPort` | integer | the port of the incoming mail server |
| `useSSL`| boolean | if use SSL |
| `outgoingServer` | string | outgoing mail server(SMTP) |
| `outgoingServerPort` | integer | the port of the outgoing mail server |
| `encryptedConnectionType`| string | none, SSL, TLS |
| `authentication` | boolean | authentication |

### emailForwardingServer
| Name | Type | Description | 
| - | - | - | 
| `forwardEmailTo` | string | forward email to | 
| `useOwnSMTPServer`| boolean | if use own SMTP server |
| `outgoingServer` | string | outgoing mail server|
| `outgoingServerPort` | integer | the port of the outgoing mail server |
| `encryptedConnectionType`| string | none, SSL, TLS |
| `authentication` | boolean | authentication |
| `userName` | string | user name | 

## endpoints 
### List all email accounts
`get api/v3/anytime/emailAccounts` 
+ Parameters
    - no parameters
+ Response 
    - emailAccounts: [emailAccount](#emailAccount) list

### Get a email account 
`get api/v3/anytime/emailAccounts/{id} ` 
+ Parameters 
    - id: string, email account id  
+ Response 
    - emailAccount: [emailAccount](#emailAccount) 

### Create a new email account
`post api/v3/anytime/emailAccounts`
+ Parameters
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: string, default assigned department
    - assignedAgent: string, default assigned agent
    - serverInfo: dynamic, [exchangeServer](#exchangeServer), [IMAPServer](#IMAPServer), [emailForwardingServer](#emailForwardingServer)
+ Response
    - emailAccounts: [emailAccount](#emailAccount) list

### Update a email account
`put api/v3/anytime/emailAccount/{id}`
+ Parameters
    - id: string, email account id
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: string, default assigned department
    - assignedAgent: string, default assigned agent
    - serverInfo: dynamic, [exchangeServer](#exchangeServer), [IMAPServer](#IMAPServer), [emailForwardingServer](#emailForwardingServer)
+ Response
   - emailAccount: [emailAccount](#emailAccount) 

### Test a email account
`put api/v3/anytime/emailAccount/{id}/test`
+ Parameters
    - id: string, email account id
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: string, default assigned department
    - assignedAgent: string, default assigned agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwardingServer`
+ Response
   - http status code

### Enable/Disable a email account
`put api/v3/anytime/emailAccount/{id}/enable`
+ Parameters
    - id: string, email account id
    - enable: boolean, if enable email account
+ Response
    - http status code

### Delete a email account
`delete api/v3/anytime/emailAccount/{id}`
+ Parameters
    - id: string, email account id
+ Response
    - http status code

### Set default email account
`put api/v3/anytime/emailAccount/{id}`
+ Parameters
    - id: string, email account id
+ Response
    - http status code

# RoutingRules
## objects
### routingRule
| Name | Type | Description |
| - | - | - |
| `isEnable` | boolean |whether the routing rules isenable or not.
| `type` |string | the type of routing, including `simple`and `rules`. |
| `simpleRouteToObject` | string | the rule of route ,including `department` and `agent` |
| `simpleRouteToId` | string | id of the route object |
| `simpleRouteToPriority` | int | conversation priorityenum number |
| `rules` | [customRule](#customRule)[] | an array of [customRule](#customRule) json object. |
| `matchFailedToObject` | string | the rule of fail route  including `department` and `agent` |
| `matchFailedrouteToId` | string | id of the routeobject |
| `matchFailedToPriority` | string | conversation priorityenum number |

### customRule
| Name | Type | Description |
| - | - | - |
| `id` | string | id of the custom rule |
| `routeId` | string | id of the routingRuleId |
| `orderIndex` | integer | order of the custom rule |
| `isEnable` | boolean | whether the custom rule is enable or not. |
| `name` | string | name of the custom rule |
| `conditions` | [conditions](#conditions)  | an trigger condition json object. |
| `routeToObject` | string | type of the route, including `agent` and `department`, value `department` is available when config of department is open. 
| `routeToId` | string |id of the route object |
| `routeToPriority` | string | conversation priority enum number|

### Conditions 
  | Name | Type |Description |
  | - | - | - | 
  | `when` | string | when the rule is triggered, including `all`, `any` and `logicalExpression` |
  | `logicExpression` | string | the logical expression of the conditions |
  | `list` | [condition](#condition)[] | an array of [condition](#condition) |

  
### condition
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the condition |
| `type` | string | `view`, `trigger`, `sla`, `routingRule` |
| `fieldId` | string | field id | 
| `matchType` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
| `value` | string | condition value | 

## endpoints
### List all routingRules
`get api/v3/anytime/routingRules`
+ Parameters
    - no parameters
+ Response
    - routingRules: [routingRule](#routingRule) list

### Enable/Disable routingRules
`put api/v3/anytime/routingRules/enable`
+ Parameters
    - no parameters
+ Response
    - routingRules: [routingRule](#routingRule) list

### Update a routingRule
`put api/v3/anytime/routingRules/{id}`
+ Parameters
    - id: string
    - enable: boolean
    - type: string, simple or custromRules
    - simpleRouteToObject: string, department and agent
    - simpleRouteToId: string
    - simpleRoutePriority: string,
    - matchFailedToObject: string, department and agent
    - matchFailedToId: string
    - matchFailedToPriority: string
    - orderIndex: int, rules execute and display order
+ Response
    - routingRule: [routingRule](#routingRule)

### Enable/Disable a custom rule
`put api/v3/anytime/routingRules/customRules/{id}/enable`
+ Parameters
    - id: string
    - enable: boolean
+ Response
    - customRule: [customRule](#customRule) 

### Create a custom rule
`post api/v3/anytime/routingRules/customRules`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - customRule: [customRule](#customRule)

### Get a custom rule
`get api/v3/anytime/routingRules/customRules/{id}`
+ Parameters
    - id: string
+ Response
    - customRule: [customRule](#customRule)

### Update a custom rule
`put api/v3/anytime/routingRules/customRules/{id}`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - customRule: [customRule](#customRule)


### Delete a custom rule
`put api/v3/anytime/routingRules/customRules/{id}`
+ Parameters
    - id: string
+ Response
    - http status code

### Upgrade/Downgrade a custom rule
`put api/v3/anytime/routingRules/customRules/{id}/sort`
+ Parameters
    - id: string
    - type: string, `up`, `down`
+ Response
    - http status code

# AutoAllocation
## objects
### autoAllocationSetting
| Name | Type | Description | 
| - | - | - | 
| `enable` | boolean | if enable Auto Allocation |
| `isEnabledDepartment` | boolean | if the department is enabled |
| `departmentAllocationRule`| [allocationRule](#allocationRule)[] | array of department allocation rules |
| `defaultAllocationRule`| [allocationRule](#allocationRule) | default allocation rules |
| `setMaxNumberForEachAgent` | boolean | if set max conversation for each agent |
| `maxNumberForAllAgents` | integer | max conversation number for all agents |
| `agentPreferences` | [agentPreference](#agentPreference)[] | agent preference for allocation |
| `excludePendingExternal` | boolean | if exclude `Pending Extenal` status while validating if an agent has reached the max number |
| `excludeOnHold` | boolean | if exclude `On Hold` status while validating if an agent has reached the max number |

### allocationRule
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | string | department id |
| `allocationTo` | string | allocated object |
| `allocationRule`| string | `loadBalancing`, `roundRobin` |
| `preferLastAssignee` | boolean | prefer to allocate to the last assignee |

### agentPreference
| Name | Type | Description | 
| - | - | - | 
| `agentId` | string | agent id |
| `maxConcurrentCount` | integer | the maximum number of the conversations a agent can accept at the same time |
| `ifAcceptAllocation` | boolean | if the agent accept conversations |

## endpoints
### Get auto allocation settings
`get api/v3/anytime/autoAllocation`
+ Parameters
    - no parameters
+ Response
    - autoAllocationSetting: [autoAllocationSetting](#autoAllocationSetting)

### Enable/Disable auto allocation
`put api/v3/anytime/autoAllocation/enable `
+ Parameters
    - enable: boolean, if enable auto allocation
+ Response
    - http status code

### Update auto allocation settings
`put api/v3/anytime/autoAllocation `
+ Parameters
    - enable: boolean, if enable auto allocation
    - allocationRuleSettings: [allocationRuleSetting](#allocationRuleSetting)[]
    - setMaxNumberForEachAgent: boolean, if set max conversation for each agent
    - maxNumberForAllAgents: integer, max conversation number for all agents
    - allocationAgentPreferences: [allocationAgentPreference](#allocationAgentPreference)[]
    - excludePendingExternal: boolean, if exclude `Pending Extenal` status while validating if an agent has reached the max number
    - excludeOnHold: boolean, if exclude `On Hold` status while validating if an agent has reached the max number
+ Response
    - autoAllocationSetting: [autoAllocationSetting](#autoAllocationSetting)

# Triggers
## object
### trigger
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the trigger |
| `description` | string | description of the trigger |
| `enable` | boolean | if enable the trigger |
| `event` | integer | trigger event enum number |
| `conditions` | [condition](#condition)[] | conditions | 
| `setValue` | boolean | if set value |
| `autoUpdate` | [autoUpdate](#autoUpdate)[] | auto update field value |
| `sendEmail` | boolean | if send email |
| `sendToContacts` | boolean | if send email |
| `sendToAgents` | boolean | if send email |
| `toAgents` | integer[] | send  email to agent(s) |
| `subject` | string | subject of the email content |
| `htmlText` | string | html body |
| `plainText` | string | plain text |
| `attachment` | [attachment](#attachment) | attachment |
| `showInConversationCorrespondences` | boolean | if show trigger email in Conversation Correspondence |
| `orderIndex` | integer | trigger execute and display order |

### autoUpdate
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the autoUpdate |
| `triggerId` | string | trigger id |
| `fieldId` | string | field id | 
| `value` | string | condition value | 

## endpoints
### List all triggers
`get api/v3/anytime/triggers`
+ Parameters 
    - no parameters
+ Response
    - triggers: [trigger](#trigger) list

### Get a trigger
`get api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - trigger: [trigger](#trigger)

### Submit a trigger
`post api/v3/anytime/triggers`
+ Parameters
    - description, string, description of the trigger
    - enable, boolean, if enable the trigger
    - event, integer 
    - conditions, [condition](#condition)[], conditions 
    - setValue, boolean, if set value
    - autoUpdate, [autoUpdate](#autoUpdate)[], auto update field value
    - sendEmail, boolean, if send email
    - sendToContacts, boolean, if send email
    - sendToAgents, boolean, if send email
    - toAgents, integer[], send  email to agent(s)
    - subject, string, subject of the email content
    - htmlText, string, html body
    - plainText, string, plain text
    - attachment, [attachment](#attachment), attachment
    - showInConversationCorrespondences, boolean, if show trigger email in Conversation Correspondence
+ Response
    - trigger: [trigger](#trigger)

 ### Update a trigger
`put api/v3/anytime/triggers/{id}`
+ Parameters
    - id, string, id of the trigger
    - description, string, description of the trigger
    - enable, boolean, if enable the trigger
    - event, integer 
    - conditions, [condition](#condition)[], conditions 
    - setValue, boolean, if set value
    - autoUpdate, [autoUpdate](#autoUpdate)[], auto update field value
    - sendEmail, boolean, if send email
    - sendToContacts, boolean, if send email
    - sendToAgents, boolean, if send email
    - toAgents, integer[], send  email to agent(s)
    - subject, string, subject of the email content
    - htmlText, string, html body
    - plainText, string, plain text
    - attachment, [attachment](#attachment), attachment
    - showInConversationCorrespondences, boolean, if show trigger email in Conversation Correspondence
+ Response
    - trigger: [trigger](#trigger)

### Upgrade/Downgrade a triggers
`put api/v3/anytime/triggers/{id}/sort`
+ Parameters
    - id: string, trigger id
    - type: string, `up`, `down`
+ Response
    - triggers: [trigger](#trigger) list

### Enable/Disable a triggers
`put api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
    - enable: boolean, if enable the trigger
+ Response
    - http status code

 ### Delete a trigger
`delete api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - http status code

# SLAPolicies
## objects
### SLAPolicy
| Name | Type | Description | 
| - | - | - | 
| `id` | string | SLA policy id |
| `enable` | boolean | if enable this SLA policy |
| `firstRespondWithin` | integer | the hours first reply within |
| `nextRespondWithin` | integer | the hours next reply within |
| `resolveRespondWithin` | integer | the hours a conversation should be resolved within |
| `operationalHour`| string | `businessHours`, `calenderHours` |
| `conditions` | [condition](#condition)[] | conditions | 
| `orderIndex` | integer | SLA execute and display order |

## endpoints
### List all SLA policies
`get api/v2/anytime/SLAPolicies`
+ Parameters
    - no parameters
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy) list

### Get a SLA policy
`get api/v2/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy)

### Create a SLA policy
`post api/v2/anytime/SLAPolicies`
+ Parameters
    - enable: boolean, if enable this SLA policy 
    - firstRespondWithin: integer, 
    - nextRespondWithin: integer, 
    - resolveRespondWithin: integer, 
    - operationalHour: string, `businessHours`, `calenderHours` 
    - conditions: [condition](#condition)[]
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy)

### Update a SLA policy
`put api/v2/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id 
    - enable: boolean, if enable this SLA policy 
    - firstRespondWithin: integer,  
    - nextRespondWithin: integer, 
    - resolveRespondWithin: integer,  
    - operationalHour: string, `businessHours`, `calenderHours` 
    - conditions: [condition](#condition)[]
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy)

### Delete a SLA policy
`delete api/v2/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - http status code

### Upgrade/Downgrade a SLA policy
`put api/v3/anytime/triggers/{id}/sort`
+ Parameters
    - id: string, SLA policy id
    - type: string, `up`, `down`
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy) list

# WorkingTime&Holiday
## objects
### workingTimeSettings
| Name | Type | Description | 
| - | - | - | 
| `sundayBusinessTime` | [businessTime](#businessTime) | sunday business time |
| `mondayBusinessTime` | [businessTime](#businessTime) | monday business time |
| `tuesdayBusinessTime` | [businessTime](#businessTime) | tuesday business time |
| `wednesdayBusinessTime` | [businessTime](#businessTime) | wednesday business time |
| `thusdayBusinessTime` | [businessTime](#businessTime) | thusday business time |
| `fridayBusinessTime` | [businessTime](#businessTime) | friday business time |
| `saturdayBusinessTime` | [businessTime](#businessTime) | saturday business time |

### businessTime
| Name | Type | Description | 
| - | - | - | 
| `isBusinessDay` | boolean |  |
| `openHour` | integer | business start hour |
| `openMin` | integer | business start min |
| `closeHour` | integer | business close hour |
| `closeMin` | integer | business close min |

### holiday
| Name | Type | Description |
| - | - | - | 
| `id` | string | the id of the holiday |
| `title` | string | the title of the holiday  |
| `date` | datetime | the date of the holiday |

## endpoints
### Get working time setting
`get api/v3/anytime/workingTime`
+ Parameters
    - no parameters
+ Response
    - workingTimeSetting: [workingTimeSetting](#workingTimeSetting)

### Update working time settings
`put api/v3/anytime/workingTime`
+ Parameters
    - workingTimeSetting: [workingTimeSetting](#workingTimeSetting)
+ Response
    - http status code

### List all holidays
`get api/v3/anytime/holidays`
+ Parameters
    - no parameters
+ Response
    - holidays: [holiday](#holiday) list

### Get a holiday
`get api/v3/anytime/holidays/{id}`
+ Parameters
    - id: string
+ Response
    - holiday: [holiday](#holiday)

### Create a holiday
`post api/v3/anytime/holidays`
+ Parameters
    - id: string
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - holiday: [holiday](#holiday)

### Update a holiday
`put api/v3/anytime/holidays/{id}`
+ Parameters
    - id: string
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - holiday: [holiday](#holiday)

### Delete a holiday
`delete api/v3/anytime/holidays`
+ Parameters
    - id: string
+ Response
    - http status code

# BlockedSenders 
## objects 
### blocked sender 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of blocked sender |
| `email` | string | email or domain | 
| `blockType` | string | `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain` | 

## endpoints 
### List blocked senders 
`get /api/v3/anytime/blockedSenders` 
+ Parameters 
    - email: string, domain or email address 
+ Response 
    - blockedSenders: [block sender](#blocked-sender) list 

### Get a blocked sender
`get /api/v3/anytime/blockedSenders/{id}`
+ Parameters
    - id: string
+ Response
    - blockedSender: [block sender](#blocked-sender) 

### Add/update a blocked sender 
`put api/v3/anytime/blockedSenders` 
+ Parameters 
    - `email`, string, domain or email address 
    - `blockType`, string, `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain`
+ Response 
    - blockedSender: [block sender](#blocked-sender) 

### Remove a blocked sender 
`delete api/v3/anytime/blockedSenders` 
+ Parameters 
   - email: string, domain or email address 
+ Response 
    - http status code


# Fields&Mapping 
## objects 
### field 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | field id | 
| `type` | string | `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`, `operator`, `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department` |
| `name` | string | field name | 
| `isSystemField` | boolean | if is system field | 
| `isRequired` | boolean | value if is required | 
| `defaultValue` | string | field default value | 
| `helpText` | string | field help text | 
| `length` | integer | field value max length | 
| `options` | [field option](#fieldoption)[] | value option | 
| `chatFieldMapping` | string | chat field id |
| `offlineMessageFieldMapping` | string | offline message field id |

### fieldOption 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | option id | 
| `name` | string | option name | 
| `value` | string | field value | 
| `order` | integer | option order | 

### fieldMapping
| Name | Type | Description | 
| - | - | - | 
| `fieldId` | string | field id | 
| `chatFieldMapping` | string | chat field id |
| `offlineMessageFieldMapping` | string | offline message field id |

## endpoints 
### List all fields and their options 
`get api/v3/anytime/fields` 
+ Parameters
    - isSystemField: boolean, if is system field 
+ Response 
    - fields: [field](#field) list 

### Get a field
`get api/v3/anytime/fields/{id}`
+ Parameters
    - id: string, field id
+ Response
    - fields: [field](#field) 

### Create a field
`post api/v3/anytime/fields`
+ Parameters
    - type, string, `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`,     `operator`,     `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department`
    - name, string, field name 
    - isSystemField, boolean, if is system field 
    - isRequired, boolean, value if is required 
    - defaultValue, string, field default value 
    - helpText, string, field help text 
    - length, integer, field value max length 
    - options, [field option](#fieldoption)[], value option 
+ Response
    - fields: [field](#field) 

### Update a field
`put api/v3/anytime/fields/{id}`
+ Parameters
    - id, string, field id 
    - type, string, `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`,     `operator`,     `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department`
    - name, string, field name 
    - isSystemField, boolean, if is system field 
    - isRequired, boolean, value if is required 
    - defaultValue, string, field default value 
    - helpText, string, field help text 
    - length, integer, field value max length 
    - options, [field option](#fieldoption)[], value option 
+ Response
    - fields: [field](#field) 

### Delete a field
`delete api/v3/anytime/fields/{id}`
+ Parameters
    - id, string, field id 
+ Response
    - http status code

### Mapping fields
`put api/v3/anytime/fields/mapping`
+ Parameters
    - fieldMappings: [fieldMapping](#fieldMapping) list
+ Response
    - http status code
