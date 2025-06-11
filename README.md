# BloodHound Query Library 
![Syntax test](https://github.com/SpecterOps/BloodHoundQueryLibrary/actions/workflows/syntax.yml/badge.svg)

The BloodHound Query Library is a community-driven collection of [Cypher queries](https://support.bloodhoundenterprise.io/hc/en-us/articles/16721164740251) designed to help [BloodHound Community Edition](https://github.com/SpecterOps/BloodHound) and [BloodHound Enterprise](https://specterops.io/bloodhound-overview/) users to unlock the full potential of the flexible BloodHound platform by creating an open query ecosystem.

The library is a free tool for the community maintained in a human-readable format (YAML) through this repository and the sleek and searchable front-end is found at https://queries.specterops.io/

The library contains queries that demonstrate BloodHound's versatility beyond traditional attack path analysis. This includes:
- All existing pre-built queries from BloodHound
- Cherry-picked community queries
- SpecterOps-created queries BloodHound Enterprise customers found valuable
- Novel queries to further showcase BloodHound's security assessment capabilities, see [security-assessment-mapping.md](/docs/security-assessment-mapping.md)

Individual query files are stored in stored in [/Queries](/Queries/) as `.yml` and are automatically combined into a single  [Queries.json](/Queries.json) file that powers the front-end.

The query files use the YAML structure found in [query-structure.yml](/docs/query-structure.yml), for example:

```yaml
name: Entra ID SSO accounts not rolling Kerberos decryption key
guid: 1867abf8-08e3-4ea8-8f65-8366079d35c4
prebuilt: false
platform: 
- Active Directory
- Azure
category: Configuration Weakness
description: Microsoft highly recommends that you roll over the Entra ID SSO Kerberos decryption key at least every 30 days.
query: |-
  MATCH (n:Computer)
  WHERE n.name STARTS WITH "AZUREADSSOACC."
  AND n.pwdlastset < (datetime().epochseconds - (30 * 86400))
  RETURN n
note: 
revision: 1
resources: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso-faq#how-can-i-roll-over-the-kerberos-decryption-key-of-the--azureadsso--computer-account-
acknowledgements: Martin Sohn Christensen, @martinsohndk
```

## Learning Cypher
One of BloodHound’s key features is its flexibility through Cypher queries – a query language to search the BloodHound graph database.

Queries can answer anything from simple questions (e.g., “*Which users haven’t reset their passwords in 180 days?*”), to complex identity attack path problems (e.g., “*Which low-privileged users can compromise computers hosting a gMSA with unconstrained delegation?*”).

The library gives you practical examples for learning Cypher and can be combined with the following resources:
- [BloodHound documentation: Searching with Cypher](https://support.bloodhoundenterprise.io/hc/en-us/articles/16721164740251)
- [openCypher resources](https://opencypher.org/resources/)
- [Neo4j Cypher Cheat Sheet](https://opencypher.org/resources/)

You can also learn with the communty by joining the #cypher_queries channel in the [BloodHound community Slack](https://support.bloodhoundenterprise.io/hc/en-us/articles/16730536907547).

## Contributing

The BloodHound Query Library's success depends on community participation. BloodHound users who have developed useful queries are encouraged to contribute them to the library.

Before comitting, please ensure that:
- The query follows the [YAML query structure](docs/query-structure.yml).
- The query is compatible with the [latest BloodHound CE version](https://github.com/SpecterOps/BloodHound)
- The query passess all automated CI/CD tests