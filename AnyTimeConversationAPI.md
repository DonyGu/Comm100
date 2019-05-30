
# EmailAccounts
## objects 
### emailAccount
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | the id of email account |
| `type`| string | Exchange, IMAP, Email Forwarding|
| `businessEmail` | string | your business email address |
| `displayName` | string | the display name your recipients will see |
| `serverInfo` | dynamic | `exchangeServer`, `IMAPServer`, `emailForwardingServer` |
| `assignedDepartment` | integer | default assigned department |
| `assignedAgent` | integer | default assigned agent |
| `status` | boolean | succeeded, failed |
| `lastReceivedTime` | datetime | last received time |
| `enable` | boolean | if enable email account |

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
`get api/v3/anytimeConversation/emailAccounts` 
+ Parameters
    - no parameters
+ Response 
    - emailAccounts: [emailAccount](#emailAccount) list

### Get a email account 
`get api/v3/anytimeConversation/emailAccounts/{id} ` 
+ Parameters 
    - id: uniqueIdentifier, email account id  
+ Response 
    - emailAccount: [emailAccount](#emailAccount) 

### Create a new email account
`post api/v3/anytimeConversation/emailAccounts`
+ Parameters
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: integer, default assigned department
    - assignedAgent: integer, default assigned agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwardingServer`
+ Response
    - emailAccounts: [emailAccount](#emailAccount) list

### Update a email account
`put api/v3/anytimeConversation/emailAccount/{id}`
+ Parameters
    - id: uniqueIdentifier, email account id
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: integer, default assigned department
    - assignedAgent: integer, default assigned agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwardingServer`
+ Response
   - emailAccount: [emailAccount](#emailAccount) 

### Test a email account
`put api/v3/anytimeConversation/emailAccount/{id}/test`
+ Parameters
    - id: uniqueIdentifier, email account id
    - type: string, exchange, IMAP, emailForwarding
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assignedDepartment: integer, default assigned department
    - assignedAgent: integer, default assigned agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwardingServer`
+ Response
   - http status code

### Enable/Disable a email account
`put api/v3/anytimeConversation/emailAccount/{id}/enable`
+ Parameters
    - id: uniqueIdentifier, email account id
    - enable: boolean, if enable email account
+ Response
    - http status code

### Delete a email account
`delete api/v3/anytimeConversation/emailAccount/{id}`
+ Parameters
    - id: uniqueIdentifier, email account id
+ Response
    - http status code

# RoutingRules
## objects
### routingRule
Route Rule is represented as simple flat JSON objects with the following keys: 
| Name | Type | Description |
| - | - | - |
| `isEnable` | boolean |whether the routing rules isenable or not.
| `type` |string | the type of routing, including `simple`and `rules`. |
| `simpleRouteToObject` | string | the rule of route ,including `department` and `agent` |
| `simpleRouteToId` | uniqueIdentifier | id of the route object |
| `simpleRouteToPriority` | int | conversation priorityenum number |
| `rules` | array | an array of [Custom Rule(#custom-rule-json-format) json object. |
| `matchFailedToObject` | string | the rule of fail route  including `department` and `agent` |
| `matchFailedrouteToId` | uniqueIdentifier | id of the routeobject |
| `matchFailedToPriority` | string | conversation priorityenum number |

### customRule
Custom Rule is represented as simple flat JSON objects with the following keys: 
| Name | Type | Description |
| - | - | - |
| `id` | uniqueIdentifier | id of the custom rule |
| `routeId` | uniqueIdentifier | id of the routingRuleId |
| `orderIndex` | integer | order of the custom rule |
| `isEnable` | boolean | whether the custom rule is enable or not. |
| `name` | string | name of the custom rule |
| `conditions` | [Conditions](#conditions-json-format)  | an trigger condition json object. |
| `routeToObject` | string | type of the route, including `agent` and `department`, value `department` is available when config of department is open. 
| `routeToId` | uniqueIdentifier |id of the route object |
| `routeToPriority` | string | conversation priority enum number|

### Conditions
  Conditions is represented as simple flat JSON objects with the following keys:  
  | Name | Type |Description |
  | - | - | - | 
  | `when` | string | when the rule is triggered, including `all`, `any` and `logicalExpression` |
  | `logicExpression` | string | the logical expression of the conditions |
  | `list` | array | an array of [condition](#condition) |

  
### condition
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | id of the condition |
| `type` | string | `view`, `trigger`, `sla`, `routingRule` |
| `fieldId` | uniqueIdentifier | field id | 
| `matchType` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
| `value` | string | condition value | 

## endpoints
### List all routingRules
`get api/v3/anytimeConversation/routingRules`
+ Parameters
    - no parameters
+ Response
    - routingRules: [routingRule](#routingRule) list

### Enable/Disable routingRules
`put api/v3/anytimeConversation/routingRules/enable`
+ Parameters
    - no parameters
+ Response
    - routingRules: [routingRule](#routingRule) list

### Update a routingRule
`put api/v3/anytimeConversation/routingRules/{id}`
+ Parameters
    - id: uniqueIdentifier
    - enable: boolean
    - type: string, simple or custromRules
    - simpleRouteToObject: string, department and agent
    - simpleRouteToId: uniqueIdentifier
    - simpleRoutePriority: string,
    - matchFailedToObject: string, department and agent
    - matchFailedToId: uniqueIdentifier
    - matchFailedToPriority: string
    - orderIndex: int, rules execute and display order
+ Response
    - routingRule: [routingRule](#routingRule)

### Enable/Disable a custom rule
`put api/v3/anytimeConversation/routingRules/customRules/{id}/enable`
+ Parameters
    - id: uniqueIdentifier
    - enable: boolean
+ Response
    - customRule: [customRule](#customRule) 

### Create a custom rule
`post api/v3/anytimeConversation/routingRules/customRules`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - customRule: [customRule](#customRule)

### Get a custom rule
`get api/v3/anytimeConversation/routingRules/customRules/{id}`
+ Parameters
    - id: uniqueIdentifier
+ Response
    - customRule: [customRule](#customRule)

### Update a custom rule
`put api/v3/anytimeConversation/routingRules/customRules/{id}`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - customRule: [customRule](#customRule)


### Delete a custom rule
`put api/v3/anytimeConversation/routingRules/customRules/{id}`
+ Parameters
    - id: uniqueIdentifier
+ Response
    - http status code

### Upgrade/Downgrade a custom rule
`put api/v3/anytimeConversation/routingRules/customRules/{id}/sort`
+ Parameters
    - id: uniqueIdentifier
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
| `allocationAgentPreferences` | [allocationAgentPreference](#allocationAgentPreference)[] | agent preference for allocation |
| `excludePendingExternal` | boolean | if exclude `Pending Extenal` status while validating if an agent has reached the max number |
| `excludeOnHold` | boolean | if exclude `On Hold` status while validating if an agent has reached the max number |

### allocationRule
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | uniqueIdentifer | department id |
| `allocationTo` | string | allocated object |
| `allocationRule`| string | `loadBalancing`, `roundRobin` |
| `preferLastAssignee` | boolean | prefer to allocate to the last assignee |

### allocationAgentPreference
| Name | Type | Description | 
| - | - | - | 
| `agentId` | uniqueIdentifer | agent id |
| `maxConcurrentCount` | integer | the maximum number of the conversations a agent can accept at the same time |
| `ifAcceptAllocation` | boolean | if the agent accept conversations |

## endpoints
### Get auto allocation settings
`get api/v3/anytimeConversation/autoAllocation`
+ Parameters
    - no parameters
+ Response
    - autoAllocationSetting: [autoAllocationSetting](#autoAllocationSetting)

### Enable/Disable auto allocation
`put api/v3/anytimeConversation/autoAllocation/enable `
+ Parameters
    - enable: boolean, if enable auto allocation
+ Response
    - http status code

### Update auto allocation settings
`put api/v3/anytimeConversation/autoAllocation `
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
| `id` | uniqueIdentifier | id of the trigger |
| `description` | string | description of the trigger |
| `enable` | boolean | if enable the trigger |
| `event` | string | `conversationCreated`, `conversationReplyReceived`, `agentReplied`, `conversationAssigneeChanged`, `conversationStatusChanged`, ` conversation Stays at a status for a specified period of time` |
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
| `id` | uniqueIdentifier | id of the autoUpdate |
| `triggerId` | uniqueIdentifier | trigger id |
| `fieldId` | uniqueIdentifier | field id | 
| `value` | string | condition value | 

## endpoints
### List all triggers
`get api/v3/anytimeConversation/triggers`
+ Parameters 
    - no parameters
+ Response
    - triggers: [trigger](#trigger) list

### Get a trigger
`get api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - id: uniqueIdentifier, trigger id
+ Response
    - trigger: [trigger](#trigger)

### Submit a trigger
`post api/v3/anytimeConversation/triggers`
+ Parameters
    - description, string, description of the trigger
    - enable, boolean, if enable the trigger
    - event, string 
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
`put api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - id, uniqueIdentifier, id of the trigger
    - description, string, description of the trigger
    - enable, boolean, if enable the trigger
    - event, string 
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
`put api/v3/anytimeConversation/triggers/{id}/sort`
+ Parameters
    - id: uniqueIdentifier, trigger id
    - type: string, `up`, `down`
+ Response
    - triggers: [trigger](#trigger) list

### Enable/Disable a triggers
`put api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - id: uniqueIdentifier, trigger id
    - enable: boolean, if enable the trigger
+ Response
    - http status code

 ### Delete a trigger
`delete api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - id: uniqueIdentifier, trigger id
+ Response
    - http status code

# SLAPolicies
## objects
### SLAPolicy
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifer | SLA policy id |
| `enable` | boolean | if enable this SLA policy |
| `firstRespondWithin` | integer | the hours first reply within |
| `nextRespondWithin` | integer | the hours next reply within |
| `resolveRespondWithin` | integer | the hours a conversation should be resolved within |
| `operationalHour`| string | `businessHours`, `calenderHours` |
| `conditions` | [condition](#condition)[] | conditions | 
| `orderIndex` | integer | SLA execute and display order |

## endpoints
### List all SLA policies
`get api/v2/anytimeConversation/SLAPolicies`
+ Parameters
    - no parameters
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy) list

### Get a SLA policy
`get api/v2/anytimeConversation/SLAPolicies/{id}`
+ Parameters
    - id: uniqueIdentifier, SLA policy id
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy)

### Create a SLA policy
`post api/v2/anytimeConversation/SLAPolicies`
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
`put api/v2/anytimeConversation/SLAPolicies/{id}`
+ Parameters
    - id: uniqueIdentifer, SLA policy id 
    - enable: boolean, if enable this SLA policy 
    - firstRespondWithin: integer,  
    - nextRespondWithin: integer, 
    - resolveRespondWithin: integer,  
    - operationalHour: string, `businessHours`, `calenderHours` 
    - conditions: [condition](#condition)[]
+ Response
    - SLAPolicy: [SLAPolicy](#SLApolicy)

### Delete a SLA policy
`delete api/v2/anytimeConversation/SLAPolicies/{id}`
+ Parameters
    - id: uniqueIdentifier, SLA policy id
+ Response
    - http status code

### Upgrade/Downgrade a SLA policy
`put api/v3/anytimeConversation/triggers/{id}/sort`
+ Parameters
    - id: uniqueIdentifier, SLA policy id
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
| `id` | uniqueIdentifier | the id of the holiday |
| `title` | string | the title of the holiday  |
| `date` | datetime | the date of the holiday |

## endpoints
### Get working time setting
`get api/v3/anytimeConversation/workingTime`
+ Parameters
    - no parameters
+ Response
    - workingTimeSetting: [workingTimeSetting](#workingTimeSetting)

### Update working time settings
`put api/v3/anytimeConversation/workingTime`
+ Parameters
    - workingTimeSetting: [workingTimeSetting](#workingTimeSetting)
+ Response
    - http status code

### List all holidays
`get api/v3/anytimeConversation/holidays`
+ Parameters
    - no parameters
+ Response
    - holidays: [holiday](#holiday) list

### Get a holiday
`get api/v3/anytimeConversation/holidays/{id}`
+ Parameters
    - id: uniqueIdentifier
+ Response
    - holiday: [holiday](#holiday)

### Create a holiday
`post api/v3/anytimeConversation/holidays`
+ Parameters
    - id: uniqueIdentifier
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - holiday: [holiday](#holiday)

### Update a holiday
`put api/v3/anytimeConversation/holidays/{id}`
+ Parameters
    - id: uniqueIdentifier
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - holiday: [holiday](#holiday)

### Delete a holiday
`delete api/v3/anytimeConversation/holidays`
+ Parameters
    - id: uniqueIdentifier
+ Response
    - http status code

# BlockedSenders 
## objects 
### blocked sender 
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | the id of blocked sender |
| `email` | string | email or domain | 
| `blockType` | string | `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain` | 

## endpoints 
### List blocked senders 
`get /api/v3/anytimeConversation/blockedSenders` 
+ Parameters 
    - email: string, domain or email address 
+ Response 
    - blockedSenders: [block sender](#blocked-sender) list 

### Get a blocked sender
`get /api/v3/anytimeConversation/blockedSenders/{id}`
+ Parameters
    - id: uniqueIdentifier
+ Response
    - blockedSender: [block sender](#blocked-sender) 

### Add/update a blocked sender 
`put api/v3/anytimeConversation/blockedSenders` 
+ Parameters 
    - `email`, string, domain or email address 
    - `blockType`, string, `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain`
+ Response 
    - blockedSender: [block sender](#blocked-sender) 

### Remove a blocked sender 
`delete api/v3/anytimeConversation/blockedSenders` 
+ Parameters 
   - email: string, domain or email address 
+ Response 
    - http status code


# Fields&Mapping 
## objects 
### field 
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | field id | 
| `type` | string | `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`, `operator`, `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department` |
| `name` | string | field name | 
| `isSystemField` | boolean | if is system field | 
| `isRequired` | boolean | value if is required | 
| `defaultValue` | string | field default value | 
| `helpText` | string | field help text | 
| `length` | integer | field value max length | 
| `options` | [field option](#fieldoption)[] | value option | 
| `chatFieldMapping` | uniqueIdentifier | chat field id |
| `offlineMessageFieldMapping` | uniqueIdentifier | offline message field id |

### fieldOption 
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | option id | 
| `name` | string | option name | 
| `value` | string | field value | 
| `order` | integer | option order | 

### fieldMapping
| Name | Type | Description | 
| - | - | - | 
| `fieldId` | uniqueIdentifier | field id | 
| `chatFieldMapping` | uniqueIdentifier | chat field id |
| `offlineMessageFieldMapping` | uniqueIdentifier | offline message field id |

## endpoints 
### List all fields and their options 
`get api/v3/anytimeConversation/fields` 
+ Parameters
    - isSystemField: boolean, if is system field 
+ Response 
    - fields: [field](#field) list 

### Get a field
`get api/v3/anytimeConversation/fields/{id}`
+ Parameters
    - id: uniqueIdentifier, field id
+ Response
    - fields: [field](#field) 

### Create a field
`post api/v3/anytimeConversation/fields`
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
`put api/v3/anytimeConversation/fields/{id}`
+ Parameters
    - id, uniqueIdentifier, field id 
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
`delete api/v3/anytimeConversation/fields/{id}`
+ Parameters
    - id, uniqueIdentifier, field id 
+ Response
    - http status code

### Mapping fields
`put api/v3/anytimeConversation/fields/mapping`
+ Parameters
    - fieldMappings: [fieldMapping](#fieldMapping) list
+ Response
    - http status code
