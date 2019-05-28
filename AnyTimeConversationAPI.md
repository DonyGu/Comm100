
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
   - http status code

### Enable/Disable a email account
`put api/v2/anytimeConversation/emailAccount/{id}`
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
