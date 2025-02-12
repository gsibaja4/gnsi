# gNSI Telemetry Extension

## `gnsi-*` trees
<details>
<summary>

An overview of the changes defined in all `gnsi-*.yang` files are shown
below.
</summary>

```sh
module: gnsi-authz

  augment /oc-sys:system/oc-sys:aaa/oc-sys:authorization/oc-sys:state:
    +--ro grpc-authz-policy-version?      version
    +--ro grpc-authz-policy-created-on?   created-on
  augment /oc-sys:system/oc-sys-grpc:grpc-servers/oc-sys-grpc:grpc-server:
    +--ro authz-policy-counters
       +--ro rpcs
          +--ro rpc* [name]
             +--ro name     -> ../state/name
             +--ro state
                +--ro name?                 string
                +--ro access-rejects?       oc-yang:counter64
                +--ro last-access-reject?   oc-types:timeticks64
                +--ro access-accepts?       oc-yang:counter64
                +--ro last-access-accept?   oc-types:timeticks64

module: gnsi-certz

  augment /oc-sys:system/oc-sys-grpc:grpc-servers/oc-sys-grpc:grpc-server/oc-sys-grpc:state:
    +--ro certificate-version?                             version
    +--ro certificate-created-on?                          created-on
    +--ro ca-trust-bundle-version?                         version
    +--ro ca-trust-bundle-created-on?                      created-on
    +--ro certificate-revocation-list-bundle-version?      version
    +--ro certificate-revocation-list-bundle-created-on?   created-on
    +--ro counters
       +--ro access-rejects?       oc-yang:counter64
       +--ro last-access-reject?   oc-types:timeticks64
       +--ro access-accepts?       oc-yang:counter64
       +--ro last-access-accept?   oc-types:timeticks64

module: gnsi-credentialz

  augment /oc-sys:system:
    +--rw console
       +--rw config
       +--ro state
          +--ro counters
             +--ro access-rejects?       oc-yang:counter64
             +--ro last-access-reject?   oc-types:timeticks64
             +--ro access-accepts?       oc-yang:counter64
             +--ro last-access-accept?   oc-types:timeticks64
  augment /oc-sys:system/oc-sys:ssh-server/oc-sys:state:
    +--ro active-trusted-user-ca-keys-version?      version
    +--ro active-trusted-user-ca-keys-created-on?   created-on
    +--ro active-host-certificate-version?          version
    +--ro active-host-certificate-created-on?       created-on
    +--ro active-host-key-version?                  version
    +--ro active-host-key-version-created-on?       created-on
    +--ro counters
       +--ro access-rejects?       oc-yang:counter64
       +--ro last-access-reject?   oc-types:timeticks64
       +--ro access-accepts?       oc-yang:counter64
       +--ro last-access-accept?   oc-types:timeticks64
  augment /oc-sys:system/oc-sys:aaa/oc-sys:authentication/oc-sys:users/oc-sys:user/oc-sys:state:
    +--ro password-version?                   version
    +--ro password-created-on?                created-on
    +--ro authorized-users-list-version?      version
    +--ro authorized-users-list-created-on?   created-on
    +--ro authorized-keys-list-version?       version
    +--ro authorized-keys-list-created-on?    created-on

module: gnsi-pathz

  augment /oc-sys:system:
    +--ro gnmi-pathz-policies
       +--ro policies
          +--ro policy* [instance]
             +--ro instance    -> ../state/instance
             +--ro state
                +--ro instance?     enumeration
                +--ro version?      version
                +--ro created-on?   created-on
  augment /oc-sys:system/oc-sys-grpc:grpc-servers/oc-sys-grpc:grpc-server/oc-sys-grpc:state:
    +--ro gnmi-pathz-policy-version?      version
    +--ro gnmi-pathz-policy-created-on?   created-on
  augment /oc-sys:system/oc-sys-grpc:grpc-servers/oc-sys-grpc:grpc-server:
    +--ro gnmi-pathz-policy-counters
       +--ro paths
          +--ro path* [xpath]
             +--ro xpath    -> ../state/xpath
             +--ro state
                +--ro xpath?    string
                +--ro reads
                |  +--ro access-rejects?       oc-yang:counter64
                |  +--ro last-access-reject?   oc-types:timeticks64
                |  +--ro access-accepts?       oc-yang:counter64
                |  +--ro last-access-accept?   oc-types:timeticks64
                +--ro writes
                   +--ro access-rejects?       oc-yang:counter64
                   +--ro last-access-reject?   oc-types:timeticks64
                   +--ro access-accepts?       oc-yang:counter64
                   +--ro last-access-accept?   oc-types:timeticks64
```
</details>

## `openconfig-system` tree

The `openconfig-system` subtree after applying augments defined in the
`gnsi-telemetry.yang` file is shown below.

For interactive version click [here](gnsi-telemetry.html).

```txt
module: openconfig-system
  +--rw system
     +--rw config
     |  +--rw hostname?       oc-inet:domain-name
     |  +--rw domain-name?    oc-inet:domain-name
     |  +--rw login-banner?   string
     |  +--rw motd-banner?    string
     +--ro state
     |  +--ro hostname?           oc-inet:domain-name
     |  +--ro domain-name?        oc-inet:domain-name
     |  +--ro login-banner?       string
     |  +--ro motd-banner?        string
     |  +--ro current-datetime?   oc-yang:date-and-time
     |  +--ro boot-time?          oc-types:timeticks64
     +--rw clock
     |  +--rw config
     |  |  +--rw timezone-name?   timezone-name-type
     |  +--ro state
     |     +--ro timezone-name?   timezone-name-type
     +--rw dns
     |  +--rw config
     |  |  +--rw search*   oc-inet:domain-name
     |  +--ro state
     |  |  +--ro search*   oc-inet:domain-name
     |  +--rw servers
     |  |  +--rw server* [address]
     |  |     +--rw address    -> ../config/address
     |  |     +--rw config
     |  |     |  +--rw address?   oc-inet:ip-address
     |  |     |  +--rw port?      oc-inet:port-number
     |  |     +--ro state
     |  |        +--ro address?   oc-inet:ip-address
     |  |        +--ro port?      oc-inet:port-number
     |  +--rw host-entries
     |     +--rw host-entry* [hostname]
     |        +--rw hostname    -> ../config/hostname
     |        +--rw config
     |        |  +--rw hostname?       string
     |        |  +--rw alias*          string
     |        |  +--rw ipv4-address*   oc-inet:ipv4-address
     |        |  +--rw ipv6-address*   oc-inet:ipv6-address
     |        +--ro state
     |           +--ro hostname?       string
     |           +--ro alias*          string
     |           +--ro ipv4-address*   oc-inet:ipv4-address
     |           +--ro ipv6-address*   oc-inet:ipv6-address
     +--rw ntp
     |  +--rw config
     |  |  +--rw enabled?              boolean
     |  |  +--rw ntp-source-address?   oc-inet:ip-address
     |  |  +--rw enable-ntp-auth?      boolean
     |  +--ro state
     |  |  +--ro enabled?              boolean
     |  |  +--ro ntp-source-address?   oc-inet:ip-address
     |  |  +--ro enable-ntp-auth?      boolean
     |  |  +--ro auth-mismatch?        oc-yang:counter64
     |  +--rw ntp-keys
     |  |  +--rw ntp-key* [key-id]
     |  |     +--rw key-id    -> ../config/key-id
     |  |     +--rw config
     |  |     |  +--rw key-id?      uint16
     |  |     |  +--rw key-type?    identityref
     |  |     |  +--rw key-value?   string
     |  |     +--ro state
     |  |        +--ro key-id?      uint16
     |  |        +--ro key-type?    identityref
     |  |        +--ro key-value?   string
     |  +--rw servers
     |     +--rw server* [address]
     |        +--rw address    -> ../config/address
     |        +--rw config
     |        |  +--rw address?            oc-inet:host
     |        |  +--rw port?               oc-inet:port-number
     |        |  +--rw version?            uint8
     |        |  +--rw association-type?   enumeration
     |        |  +--rw iburst?             boolean
     |        |  +--rw prefer?             boolean
     |        +--ro state
     |           +--ro address?            oc-inet:host
     |           +--ro port?               oc-inet:port-number
     |           +--ro version?            uint8
     |           +--ro association-type?   enumeration
     |           +--ro iburst?             boolean
     |           +--ro prefer?             boolean
     |           +--ro stratum?            uint8
     |           +--ro root-delay?         uint32
     |           +--ro root-dispersion?    uint64
     |           +--ro offset?             uint64
     |           +--ro poll-interval?      uint32
     +--rw ssh-server
     |  +--rw config
     |  |  +--rw enable?             boolean
     |  |  +--rw protocol-version?   enumeration
     |  |  +--rw timeout?            uint16
     |  |  +--rw rate-limit?         uint16
     |  |  +--rw session-limit?      uint16
     |  +--ro state
     |     +--ro enable?                                              boolean
     |     +--ro protocol-version?                                    enumeration
     |     +--ro timeout?                                             uint16
     |     +--ro rate-limit?                                          uint16
     |     +--ro session-limit?                                       uint16
     |     +--ro gnsi-credz:active-trusted-user-ca-keys-version?      version
     |     +--ro gnsi-credz:active-trusted-user-ca-keys-created-on?   created-on
     |     +--ro gnsi-credz:active-host-certificate-version?          version
     |     +--ro gnsi-credz:active-host-certificate-created-on?       created-on
     |     +--ro gnsi-credz:active-host-key-version?                  version
     |     +--ro gnsi-credz:active-host-key-version-created-on?       created-on
     |     +--ro gnsi-credz:counters
     |        +--ro gnsi-credz:access-rejects?       oc-yang:counter64
     |        +--ro gnsi-credz:last-access-reject?   oc-types:timeticks64
     |        +--ro gnsi-credz:access-accepts?       oc-yang:counter64
     |        +--ro gnsi-credz:last-access-accept?   oc-types:timeticks64
     +--rw telnet-server
     |  +--rw config
     |  |  +--rw enable?          boolean
     |  |  +--rw timeout?         uint16
     |  |  +--rw rate-limit?      uint16
     |  |  +--rw session-limit?   uint16
     |  +--ro state
     |     +--ro enable?          boolean
     |     +--ro timeout?         uint16
     |     +--ro rate-limit?      uint16
     |     +--ro session-limit?   uint16
     +--rw logging
     |  +--rw console
     |  |  +--rw config
     |  |  +--ro state
     |  |  +--rw selectors
     |  |     +--rw selector* [facility severity]
     |  |        +--rw facility    -> ../config/facility
     |  |        +--rw severity    -> ../config/severity
     |  |        +--rw config
     |  |        |  +--rw facility?   identityref
     |  |        |  +--rw severity?   syslog-severity
     |  |        +--ro state
     |  |           +--ro facility?   identityref
     |  |           +--ro severity?   syslog-severity
     |  +--rw remote-servers
     |     +--rw remote-server* [host]
     |        +--rw host         -> ../config/host
     |        +--rw config
     |        |  +--rw host?             oc-inet:host
     |        |  +--rw source-address?   oc-inet:ip-address
     |        |  +--rw remote-port?      oc-inet:port-number
     |        +--ro state
     |        |  +--ro host?             oc-inet:host
     |        |  +--ro source-address?   oc-inet:ip-address
     |        |  +--ro remote-port?      oc-inet:port-number
     |        +--rw selectors
     |           +--rw selector* [facility severity]
     |              +--rw facility    -> ../config/facility
     |              +--rw severity    -> ../config/severity
     |              +--rw config
     |              |  +--rw facility?   identityref
     |              |  +--rw severity?   syslog-severity
     |              +--ro state
     |                 +--ro facility?   identityref
     |                 +--ro severity?   syslog-severity
     +--rw aaa
     |  +--rw config
     |  +--ro state
     |  +--rw authentication
     |  |  +--rw config
     |  |  |  +--rw authentication-method*   union
     |  |  +--ro state
     |  |  |  +--ro authentication-method*   union
     |  |  +--rw admin-user
     |  |  |  +--rw config
     |  |  |  |  +--rw admin-password?          string
     |  |  |  |  +--rw admin-password-hashed?   oc-aaa-types:crypt-password-type
     |  |  |  +--ro state
     |  |  |     +--ro admin-password?          string
     |  |  |     +--ro admin-password-hashed?   oc-aaa-types:crypt-password-type
     |  |  |     +--ro admin-username?          string
     |  |  +--rw users
     |  |     +--rw user* [username]
     |  |        +--rw username    -> ../config/username
     |  |        +--rw config
     |  |        |  +--rw username?   string
     |  |        |  +--rw role?       union
     |  |        +--ro state
     |  |           +--ro username?                                      string
     |  |           +--ro password?                                      string
     |  |           +--ro password-hashed?                               oc-aaa-types:crypt-password-type
     |  |           +--ro role?                                          union
     |  |           +--ro gnsi-credz:password-version?                   version
     |  |           +--ro gnsi-credz:password-created-on?                created-on
     |  |           +--ro gnsi-credz:authorized-users-list-version?      version
     |  |           +--ro gnsi-credz:authorized-users-list-created-on?   created-on
     |  |           +--ro gnsi-credz:authorized-keys-list-version?       version
     |  |           +--ro gnsi-credz:authorized-keys-list-created-on?    created-on
     |  +--rw authorization
     |  |  +--rw config
     |  |  |  +--rw authorization-method*   union
     |  |  +--ro state
     |  |  |  +--ro authorization-method*                      union
     |  |  |  +--ro gnsi-authz:grpc-authz-policy-version?      version
     |  |  |  +--ro gnsi-authz:grpc-authz-policy-created-on?   created-on
     |  |  +--rw events
     |  |     +--rw event* [event-type]
     |  |        +--rw event-type    -> ../config/event-type
     |  |        +--rw config
     |  |        |  +--rw event-type?   identityref
     |  |        +--ro state
     |  |           +--ro event-type?   identityref
     |  +--rw accounting
     |  |  +--rw config
     |  |  |  +--rw accounting-method*   union
     |  |  +--ro state
     |  |  |  +--ro accounting-method*   union
     |  |  +--rw events
     |  |     +--rw event* [event-type]
     |  |        +--rw event-type    -> ../config/event-type
     |  |        +--rw config
     |  |        |  +--rw event-type?   identityref
     |  |        |  +--rw record?       enumeration
     |  |        +--ro state
     |  |           +--ro event-type?   identityref
     |  |           +--ro record?       enumeration
     |  +--rw server-groups
     |     +--rw server-group* [name]
     |        +--rw name       -> ../config/name
     |        +--rw config
     |        |  +--rw name?   string
     |        |  +--rw type?   identityref
     |        +--ro state
     |        |  +--ro name?   string
     |        |  +--ro type?   identityref
     |        +--rw servers
     |           +--rw server* [address]
     |              +--rw address    -> ../config/address
     |              +--rw config
     |              |  +--rw name?      string
     |              |  +--rw address?   oc-inet:ip-address
     |              |  +--rw timeout?   uint16
     |              +--ro state
     |              |  +--ro name?                  string
     |              |  +--ro address?               oc-inet:ip-address
     |              |  +--ro timeout?               uint16
     |              |  +--ro connection-opens?      oc-yang:counter64
     |              |  +--ro connection-closes?     oc-yang:counter64
     |              |  +--ro connection-aborts?     oc-yang:counter64
     |              |  +--ro connection-failures?   oc-yang:counter64
     |              |  +--ro connection-timeouts?   oc-yang:counter64
     |              |  +--ro messages-sent?         oc-yang:counter64
     |              |  +--ro messages-received?     oc-yang:counter64
     |              |  +--ro errors-received?       oc-yang:counter64
     |              +--rw tacacs
     |              |  +--rw config
     |              |  |  +--rw port?                oc-inet:port-number
     |              |  |  +--rw secret-key?          oc-types:routing-password
     |              |  |  +--rw secret-key-hashed?   oc-aaa-types:crypt-password-type
     |              |  |  +--rw source-address?      oc-inet:ip-address
     |              |  +--ro state
     |              |     +--ro port?                oc-inet:port-number
     |              |     +--ro secret-key?          oc-types:routing-password
     |              |     +--ro secret-key-hashed?   oc-aaa-types:crypt-password-type
     |              |     +--ro source-address?      oc-inet:ip-address
     |              +--rw radius
     |                 +--rw config
     |                 |  +--rw auth-port?             oc-inet:port-number
     |                 |  +--rw acct-port?             oc-inet:port-number
     |                 |  +--rw secret-key?            oc-types:routing-password
     |                 |  +--rw secret-key-hashed?     oc-aaa-types:crypt-password-type
     |                 |  +--rw source-address?        oc-inet:ip-address
     |                 |  +--rw retransmit-attempts?   uint8
     |                 +--ro state
     |                    +--ro auth-port?             oc-inet:port-number
     |                    +--ro acct-port?             oc-inet:port-number
     |                    +--ro secret-key?            oc-types:routing-password
     |                    +--ro secret-key-hashed?     oc-aaa-types:crypt-password-type
     |                    +--ro source-address?        oc-inet:ip-address
     |                    +--ro retransmit-attempts?   uint8
     |                    +--ro counters
     |                       +--ro retried-access-requests?   oc-yang:counter64
     |                       +--ro access-accepts?            oc-yang:counter64
     |                       +--ro access-rejects?            oc-yang:counter64
     |                       +--ro timeout-access-requests?   oc-yang:counter64
     +--rw memory
     |  +--rw config
     |  +--ro state
     |     +--ro physical?   uint64
     |     +--ro reserved?   uint64
     +--ro cpus
     |  +--ro cpu* [index]
     |     +--ro index    -> ../state/index
     |     +--ro state
     |        +--ro index?                union
     |        +--ro total
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro user
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro kernel
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro nice
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro idle
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro wait
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro hardware-interrupt
     |        |  +--ro instant?    oc-types:percentage
     |        |  +--ro avg?        oc-types:percentage
     |        |  +--ro min?        oc-types:percentage
     |        |  +--ro max?        oc-types:percentage
     |        |  +--ro interval?   oc-types:stat-interval
     |        |  +--ro min-time?   oc-types:timeticks64
     |        |  +--ro max-time?   oc-types:timeticks64
     |        +--ro software-interrupt
     |           +--ro instant?    oc-types:percentage
     |           +--ro avg?        oc-types:percentage
     |           +--ro min?        oc-types:percentage
     |           +--ro max?        oc-types:percentage
     |           +--ro interval?   oc-types:stat-interval
     |           +--ro min-time?   oc-types:timeticks64
     |           +--ro max-time?   oc-types:timeticks64
     +--rw processes
     |  +--ro process* [pid]
     |     +--ro pid      -> ../state/pid
     |     +--ro state
     |        +--ro pid?                  uint64
     |        +--ro name?                 string
     |        +--ro args*                 string
     |        +--ro start-time?           oc-types:timeticks64
     |        +--ro cpu-usage-user?       oc-yang:counter64
     |        +--ro cpu-usage-system?     oc-yang:counter64
     |        +--ro cpu-utilization?      oc-types:percentage
     |        +--ro memory-usage?         uint64
     |        +--ro memory-utilization?   oc-types:percentage
     +--ro alarms
     |  +--ro alarm* [id]
     |     +--ro id        -> ../state/id
     |     +--ro config
     |     +--ro state
     |        +--ro id?             string
     |        +--ro resource?       string
     |        +--ro text?           string
     |        +--ro time-created?   oc-types:timeticks64
     |        +--ro severity?       identityref
     |        +--ro type-id?        union
     +--rw messages
     |  +--rw config
     |  |  +--rw severity?   oc-log:syslog-severity
     |  +--ro state
     |  |  +--ro severity?   oc-log:syslog-severity
     |  |  +--ro message
     |  |     +--ro msg?        string
     |  |     +--ro priority?   uint8
     |  |     +--ro app-name?   string
     |  |     +--ro procid?     string
     |  |     +--ro msgid?      string
     |  +--rw debug-entries
     |     +--rw debug-service* [service]
     |        +--rw service    -> ../config/service
     |        +--rw config
     |        |  +--rw service?   identityref
     |        |  +--rw enabled?   boolean
     |        +--ro state
     |           +--ro service?   identityref
     |           +--ro enabled?   boolean
     +--rw license
     |  +--rw licenses
     |     +--rw license* [license-id]
     |        +--rw license-id    -> ../config/license-id
     |        +--rw config
     |        |  +--rw license-id?     string
     |        |  +--rw license-data?   union
     |        |  +--rw active?         boolean
     |        +--ro state
     |           +--ro license-id?        string
     |           +--ro license-data?      union
     |           +--ro active?            boolean
     |           +--ro description?       string
     |           +--ro issue-date?        uint64
     |           +--ro expiration-date?   uint64
     |           +--ro in-use?            boolean
     |           +--ro expired?           boolean
     |           +--ro valid?             boolean
     +--rw oc-sys-grpc:grpc-servers
     |  +--rw oc-sys-grpc:grpc-server* [name]
     |     +--rw oc-sys-grpc:name                         -> ../config/name
     |     +--rw oc-sys-grpc:config
     |     |  +--rw oc-sys-grpc:name?                      string
     |     |  +--rw oc-sys-grpc:services*                  identityref
     |     |  +--rw oc-sys-grpc:enable?                    boolean
     |     |  +--rw oc-sys-grpc:port?                      oc-inet:port-number
     |     |  +--rw oc-sys-grpc:transport-security?        boolean
     |     |  +--rw oc-sys-grpc:certificate-id?            string
     |     |  +--rw oc-sys-grpc:metadata-authentication?   boolean
     |     |  +--rw oc-sys-grpc:listen-addresses*          union
     |     |  +--rw oc-sys-grpc:network-instance?          oc-ni:network-instance-ref
     |     +--ro oc-sys-grpc:state
     |     |  +--ro oc-sys-grpc:name?                                           string
     |     |  +--ro oc-sys-grpc:services*                                       identityref
     |     |  +--ro oc-sys-grpc:enable?                                         boolean
     |     |  +--ro oc-sys-grpc:port?                                           oc-inet:port-number
     |     |  +--ro oc-sys-grpc:transport-security?                             boolean
     |     |  +--ro oc-sys-grpc:certificate-id?                                 string
     |     |  +--ro oc-sys-grpc:metadata-authentication?                        boolean
     |     |  +--ro oc-sys-grpc:listen-addresses*                               union
     |     |  +--ro oc-sys-grpc:network-instance?                               oc-ni:network-instance-ref
     |     |  +--ro gnsi-certz:certificate-version?                             version
     |     |  +--ro gnsi-certz:certificate-created-on?                          created-on
     |     |  +--ro gnsi-certz:ca-trust-bundle-version?                         version
     |     |  +--ro gnsi-certz:ca-trust-bundle-created-on?                      created-on
     |     |  +--ro gnsi-certz:certificate-revocation-list-bundle-version?      version
     |     |  +--ro gnsi-certz:certificate-revocation-list-bundle-created-on?   created-on
     |     |  +--ro gnsi-certz:counters
     |     |  |  +--ro gnsi-certz:access-rejects?       oc-yang:counter64
     |     |  |  +--ro gnsi-certz:last-access-reject?   oc-types:timeticks64
     |     |  |  +--ro gnsi-certz:access-accepts?       oc-yang:counter64
     |     |  |  +--ro gnsi-certz:last-access-accept?   oc-types:timeticks64
     |     |  +--ro gnsi-pathz:gnmi-pathz-policy-version?                       version
     |     |  +--ro gnsi-pathz:gnmi-pathz-policy-created-on?                    created-on
     |     +--ro gnsi-authz:authz-policy-counters
     |     |  +--ro gnsi-authz:rpcs
     |     |     +--ro gnsi-authz:rpc* [name]
     |     |        +--ro gnsi-authz:name     -> ../state/name
     |     |        +--ro gnsi-authz:state
     |     |           +--ro gnsi-authz:name?                 string
     |     |           +--ro gnsi-authz:access-rejects?       oc-yang:counter64
     |     |           +--ro gnsi-authz:last-access-reject?   oc-types:timeticks64
     |     |           +--ro gnsi-authz:access-accepts?       oc-yang:counter64
     |     |           +--ro gnsi-authz:last-access-accept?   oc-types:timeticks64
     |     +--ro gnsi-pathz:gnmi-pathz-policy-counters
     |        +--ro gnsi-pathz:paths
     |           +--ro gnsi-pathz:path* [xpath]
     |              +--ro gnsi-pathz:xpath    -> ../state/xpath
     |              +--ro gnsi-pathz:state
     |                 +--ro gnsi-pathz:xpath?    string
     |                 +--ro gnsi-pathz:reads
     |                 |  +--ro gnsi-pathz:access-rejects?       oc-yang:counter64
     |                 |  +--ro gnsi-pathz:last-access-reject?   oc-types:timeticks64
     |                 |  +--ro gnsi-pathz:access-accepts?       oc-yang:counter64
     |                 |  +--ro gnsi-pathz:last-access-accept?   oc-types:timeticks64
     |                 +--ro gnsi-pathz:writes
     |                    +--ro gnsi-pathz:access-rejects?       oc-yang:counter64
     |                    +--ro gnsi-pathz:last-access-reject?   oc-types:timeticks64
     |                    +--ro gnsi-pathz:access-accepts?       oc-yang:counter64
     |                    +--ro gnsi-pathz:last-access-accept?   oc-types:timeticks64
     +--rw gnsi-credz:console
     |  +--rw gnsi-credz:config
     |  +--ro gnsi-credz:state
     |     +--ro gnsi-credz:counters
     |        +--ro gnsi-credz:access-rejects?       oc-yang:counter64
     |        +--ro gnsi-credz:last-access-reject?   oc-types:timeticks64
     |        +--ro gnsi-credz:access-accepts?       oc-yang:counter64
     |        +--ro gnsi-credz:last-access-accept?   oc-types:timeticks64
     +--ro gnsi-pathz:gnmi-pathz-policies
        +--ro gnsi-pathz:policies
           +--ro gnsi-pathz:policy* [instance]
              +--ro gnsi-pathz:instance    -> ../state/instance
              +--ro gnsi-pathz:state
                 +--ro gnsi-pathz:instance?     enumeration
                 +--ro gnsi-pathz:version?      version
                 +--ro gnsi-pathz:created-on?   created-on

```
