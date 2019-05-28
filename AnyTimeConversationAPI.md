
# Email Accounts
## objects 
### emailAccount
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | the id of Email Server |
| `type`| string | Exchange, IMAP, Email Forwording|
| `businessEmail` | string | your business email address |
| `displayName` | string | the display name your recipients will see |
| `serverInfo` | dynamic | `exchangeServer`, `IMAPServer`, `emailForwordingServer` |
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
### List Email Accounts
`get api/v2/anytimeConversation/emailAccounts` 
+ Parameters
    - no parameters
+ Response 
    - emailAccounts: [emailAccount](#emailAccount) list

### Get a email account 
`get api/v2/anytimeConversation/emailAccounts/{id} ` 
+ Parameters 
    - id: uniqueIdentifier, email account id  
+ Response 
    - emailAccount: [emailAccount](#emailAccount) 

### Submit a new email account
`post api/v2/anytimeConversation/emailAccounts`
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
`put api/v2/anytimeConversation/emailAccount/{id}`
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
`put api/v2/anytimeConversation/emailAccount/{id}/test`
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
`put api/v2/anytimeConversation/emailAccount/{id}/enable`
+ Parameters
    - id: uniqueIdentifier, email account id
    - enable: boolean, if enable email account
+ Response
    - http status code

### Delete a email account
`delete api/v2/anytimeConversation/emailAccount/{id}`
+ Parameters
    - id: uniqueIdentifier, email account id
+ Response
    - http status code

# Routing rules
+ adjust from social

# Auto Allocation
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
`get api/v2/anytimeConversation/autoAllocation`
+ Parameters
    - no parameters
+ Response
    - autoAllocationSetting: [autoAllocationSetting](#autoAllocationSetting)

### Enable/Disable auto allocation
`put api/v2/anytimeConversation/autoAllocation/enable `
+ Parameters
    - enable: boolean, if enable Auto Allocation
+ Response
    - http status code

### Update auto allocation settings
`put api/v2/anytimeConversation/autoAllocation `
+ Parameters
    - enable: boolean, if enable Auto Allocation
    - allocationRuleSettings: [allocationRuleSetting](#allocationRuleSetting)[]
    - setMaxNumberForEachAgent: boolean, if set max conversation for each agent
    - maxNumberForAllAgents: integer, max conversation number for all agents
    - departmentFilters: [departmentFilter](#departmentFilter)[]
    - allocationAgentPreferences: [allocationAgentPreference](#allocationAgentPreference)[]
    - excludePendingExternal: boolean, if exclude `Pending Extenal` status while validating if an agent has reached the max number
    - excludeOnHold: boolean, if exclude `On Hold` status while validating if an agent has reached the max number
+ Response
    - autoAllocationSetting: [autoAllocationSetting](#autoAllocationSetting)

 