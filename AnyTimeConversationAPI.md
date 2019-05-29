
# EmailAccounts
## objects 
### emailAccount
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | the id of email account |
| `type`| string | Exchange, IMAP, Email Forwording|
| `businessEmail` | string | your business email address |
| `displayName` | string | the display name your recipients will see |
| `serverInfo` | dynamic | `exchangeServer`, `IMAPServer`, `emailForwardingServer` |
| `assigneedDepartment` | integer | default assigneed department |
| `assigneedAgent` | integer | default assigneed agent |
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

### emailForwordingServer
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

### Submit a new email account
`post api/v3/anytimeConversation/emailAccounts`
+ Parameters
    - type: string, exchange, IMAP, emailForwording
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assigneedDepartment: integer, default assigneed department
    - assigneedAgent: integer, default assigneed agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwordingServer`
+ Response
    - emailAccounts: [emailAccount](#emailAccount) list

### Update a email account
`put api/v3/anytimeConversation/emailAccount/{id}`
+ Parameters
    - id: uniqueIdentifier, email account id
    - type: string, exchange, IMAP, emailForwording
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assigneedDepartment: integer, default assigneed department
    - assigneedAgent: integer, default assigneed agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwordingServer`
+ Response
   - emailAccount: [emailAccount](#emailAccount) 

### Test a email account
`put api/v3/anytimeConversation/emailAccount/{id}/test`
+ Parameters
    - id: uniqueIdentifier, email account id
    - type: string, exchange, IMAP, emailForwording
    - businessEmail: string, your business email address
    - displayName: string, the display name your recipients will see
    - assigneedDepartment: integer, default assigneed department
    - assigneedAgent: integer, default assigneed agent
    - serverInfo: dynamic, `exchangeServer`, `IMAPServer`, `emailForwordingServer`
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
+ adjust from social

# AutoAllocation
## object
### autoAllocationSetting
| Name | Type | Description | 
| - | - | - | 
| `enable` | boolean | if enable Auto Allocation |
| `isEnabledDepartment` | boolean | if the department is enabled |
| `allocationRuleSettings`| [allocationRuleSetting](#allocationRuleSetting)[] | array of allocation rule settings |
| `setMaxNumberForEachAgent` | boolean | if set max conversation for each agent |
| `maxNumberForAllAgents` | integer | max conversation number for all agents |
| `departmentFilters` | [departmentFilter](#departmentFilter)[] | departments |
| `allocationAgentPreferences` | [allocationAgentPreference](#allocationAgentPreference)[] | agent preference for allocation |
| `excludePendingExternal` | boolean | if exclude `Pending Extenal` status while validating if an agent has reached the max number |
| `excludeOnHold` | boolean | if exclude `On Hold` status while validating if an agent has reached the max number |

### allocationRuleSetting
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | uniqueIdentifer | department id |
| `allocationTo` | string | allocated object |
| `allocationRule`| string | `loadBalancing`, `roundRobin` |
| `preferLastAssignee` | boolean | prefer to allocate to the last assignee |

### departmentFilter
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | uniqueIdentifer | department id |
| `department` | string | department name |
| `agentIds`| string | the ids of the agents in the department |

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
    - departmentFilters: [departmentFilter](#departmentFilter)[]
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
| `event` | string | `When a conversation is created`, `When a conversation reply is received`, `When agent replied`, `When the assignee of a conversation is changed`, `When the status of a conversation is changed`, `When a conversation stays at a status for a specified period of time` |
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

### conditoin
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | id of the condition |
| `type` | string | `query`, `rule`, `sla`, `routingRule` |
| `fieldId` | integer | field id | 
| `matchType` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
| `value` | string | condition value | 

### autoUpdate
| Name | Type | Description | 
| - | - | - | 
| `id` | uniqueIdentifier | id of the condition |
| `type` | string | `query`, `rule`, `sla`, `routingRule` |
| `fieldId` | integer | field id | 
| `matchType` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
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
    - todo:
+ Response
    - todo:

 ### Update a trigger
`put api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - todo:
+ Response
    - todo:

### Upgrade/Downgrade a triggers
`put api/v3/anytimeConversation/triggers/{id}`
+ Parameters
    - todo:
+ Response
    - todo:

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

## endpoints


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
| `id` | integer | field id | 
| `type` | string | `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`, `operator`, <br/>`radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department` | 
| `name` | integer | field name | 
| `isSystemField` | boolean | if is system field | 
| `isRequired` | boolean | value if is required | 
| `defaultValue` | string | field default value | 
| `helpText` | string | field help text | 
| `length` | integer | field value max length | 
| `options` | [field option](#fieldoption)[] | value option | 

### fieldOption 
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | option id | 
| `name` | string | option name | 
| `value` | string | field value | 
| `order` | integer | option order | 

## endpoints 
### List all fields and their options 
`get api/v3/ticket/fields` 
+ Parameters
    - no parameters
+ Response 
    - fields: [field](#field) list 
