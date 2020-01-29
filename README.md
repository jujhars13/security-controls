# Security Controls

## About

Information security controls frameworks are a bit of a mess, with multiple hard-to-parse formats and inconsistent structures describing similar goals.  This project aspires to help users:

1. Easily obtain clean, consistent controls information from one place
1. Easily search, manipulate, and use controls information
1. Map controls across frameworks
1. Easily share controls information with other tools and platforms

... and more.

### Risk-Focused

This project is designed to support a thoughtful risk management strategy where security moves beyond mere "compliance" (or "maturity") and into _risk mitigation_.  Controls decisions and priorities should consider the full risk equation and avoid "box-checking."

> ```text
> risk = impact x likelihood
> risk = (functional_impact + information_impact) x (threat x vulnerability)
> risk = ((functional_impact + information_impact) - (controls_mitigation)) x (threat x (vulnerability - controls_mitigation))
> ```

## Controls (_a.k.a._, actions, requirements, outcomes)

### Frameworks

ID |Framework | URL | Version |  Notes
-- | -- | -- | -- | --
`nist_csf_v1.1` | National Institute for Standards and Technology (NIST) Framework for Improving Critical Infrastructure Cybersecurity | [NIST CSF](https://www.nist.gov/cyberframework) | 1.1 |
`cis_csc_7.1` | Center for Internet Security (CIS) Controls | [CIS CSC](http://www.cisecurity.org/controls/) | 7.1 | _a.k.a._, CIS Critical Security Controls, Top 20
`800_53_v4` | NIST Security and Privacy Controls for Federal Information Systems and Organizations | [NIST 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-4/final) | 4 |
`800_171_v1` | Protecting Controlled Unclassified Information in Nonfederal Systems and Organizations | [NIST 800-171](https://csrc.nist.gov/publications/detail/sp/800-171/rev-1/final) | 1 |
`owasp_10_v3` | Open Web Application Security Project (OWASP) Top Ten Proactive Controls 2018 | [OWASP Top 10](https://owasp.org/www-project-proactive-controls/) | 3 | Distinct from [OWASP Top 10 Security Risks](https://owasp.org/www-project-top-ten/)
`asvs_v4.0.1` | OWASP Application Security Verification Standard| [ASVS](https://owasp.org/www-project-application-security-verification-standard/) | 4.0.1 |

### Format

All controls are standardized to capture the following fields:

Field | Description | Example
-- | -- | --
`source` | framework from which the item was drawn, using the ID listed above| `nist_csf_v1.1`
`id_raw` | identifier for the item drawn from the source (may not be globally unique), in its original format | `RS.MI`
`id` | globally unique (namespaced) identifier created by combining `source` with lowercase, no-spaces `id_raw` | `nist_csf_v1.1:rs.mi`
`tier_raw` | tier (group) for the item drawn from the source (may not be globally unique or consistent), in its original format | `Category`
`tier` | 0-based level in the hierarchy of the original framework (_i.e._, the number of ancestors for this item) | `1`
`title` | short description of the item (optional), in its original format | `Mitigation`
`description` | long description of the item (optional), in its original format | `Activities are performed ...`

## Relationships (_e.g._, equivalence, hierarchy, association)

TODO

## Labels (_a.k.a._, tags, metadata)

TODO

## Notes

* Hierarchical groups of controls are captured as higher-tier controls, even when not explicitly described that way in the source (_e.g._, CIS CSC implementation groups).  When a set of controls is defined by some cross-cutting aspect of the controls (_e.g._, 800-171 basic vs. derived requirements, or CIS CSC asset types) rather than a hierarchy, this is captured using labels.
* This project maintains format from the source document(s) in order to comply with licenses and avoid becoming a copy-editing nightmare.  This means data retains capitalization artifacts, style inconsistencies, and typographical errors, among other issues.  Proposed fixes should first determine if the issue is present in the underlying source (in which case, it will likely remain by design, and to comply with license terms).
* This approach clearly leaves out useful information from each framework, but benefits from simplicity and consistency.  This project emphasizes these values over comprehensiveness.
* Items deeper than tier-2 are wrapped into their nearest tier 2 ancestor (_e.g._, `800_53_v4` tier-3 items `AC-2h.1.`, `AC-2h.2.`, `AC-2h.3.` are included in tier-2 item `AC-2h.`).
* "Withdrawn" controls in `800_53_v4` do not appear in the consolidated data.
* Leading and trailing spaces were removed in consolidated data.
* **DISCLAIMER:** Much of the initial consolidation was done by hand with the assistance of good old Excel.  There are likely transcription errors.  Please create an issue or pull request if you identify a problem.

## Use Cases

The data and tools in this project can support:

1. Efficiency and cost savings by avoiding duplication of effort across multiple departments (_e.g._, security operations and product development)
1. Transitions from one regime to another (_e.g._, due to an acquisition or initiative)
1. Integrating controls information into task tracking, ticketing, planning, and [GRC](https://en.wikipedia.org/wiki/Governance,_risk_management,_and_compliance) tools (e.g., Archer, SAP, github/gitlab, JIRA, Zendesk)
1. Integrating controls information into operations tools like log aggregators, SIEMs, visualization tools, and orchestration platforms (_e.g._, Elastic Stack, Splunk, Demisto, Phantom)
1. Visualizing coverage and progress towards goals
1. Prioritizing controls based on the **threat** component of risk (_e.g._, in concert with threat intelligence and adversary activity taxonomies like [MITRE ATT&CK](https://attack.mitre.org/) or [CAPEC](https://capec.mitre.org/))
1. Prioritizing controls based on business, mission, regulatory, and legal **impact** components of risk (_e.g._, using lists of critical assets, information, and accounts)
1. Prioritizing controls based on the **vulnerability** component of risk
1. Prioritizing controls based on the confidentiality, integrity, and availability requirements of assets and information

## Frequently Asked Questions (FAQ)

* **Why do you mix application security and organizational/corporate information security frameworks?** Our master list strives to include all reputable information security controls, across a wide variety of domains.  We support the use of [labels](#labels) to add metadata to controls, and if that distinction is important to your team, we encourage you to capture it within the mode.  More broadly: different organizations assign security responsibilities differently, and for many firms their applications _are_ their entire organization.  There's often no meaningful distinction in the world of small business, DevSecOps, or integrated IT/security teams - the same people are responsible for most of it!
* **How did you choose the relationships (mappings)?** We created initial mappings based on the source documents themselves (_i.e._, they say X maps to Y), as well as a good-faith effort to apply the principles in ISO 25964-2, "Information and documentation — Thesauri and interoperability with other vocabularies - Part 2: Interoperability with other vocabularies."  In so many cases it's a matter of judgment and usability - if you think X should be mapped to Y, please open an issue or pull request and we can discuss it!  Because relationships have metadata, you can also create and use your own without breaking anything.

## References and Prior Art

* [Open Control](https://github.com/opencontrol)
* See [NOTICE](NOTICE) for additional source material and references

## Roadmap

* [x] Publish clean, consistent controls framework data
* [ ] Determine mapping approach using ISO 25964-2 and source documents
* [ ] Capture mappings for NIST CSF to 800-53 (from CSF source xml)
* [ ] Capture mappings for NIST CSF to CIS CSC (from NIST CSF source document)* [ ] Capture mappings for CIS CSC to NIST CSF (from CIS CSC source document)
* [ ] Complete initial mapping for NIST CSF, CIS CSC, and 800-53
* [ ] POC for visualization capabilities
* [ ] Consider including and mapping adversary activity taxonomies (_e.g._, [ATT&CK](https://attack.mitre.org/), [OWASP Top 10 Security Risks](https://owasp.org/www-project-top-ten/), [CAPEC](https://capec.mitre.org/))
* [ ] Consider including SOC 2
* [ ] Consider including PCI/DSS
* [ ] Consider including ISO 2700X
* [ ] Consider including COBIT
* [ ] Consider including ITIL
* [ ] Consider including HIPAA/HITRUST
* [ ] Consider including FedRAMP

## License and Notice

**Controls information is copyright its respective creator and used according its respective license.** See the [NOTICE](NOTICE) file for details on each source.  These licenses include:

* [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International Public License](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode) (_e.g._, for items marked `cis_csc_v7.1`)
* [Creative Commons Attribution ShareAlike 3.0](https://creativecommons.org/licenses/by-sa/3.0/legalcode) (e.g., for items marked `asvs_`)
* [Public domain and not subject to copyright in the United States](https://www.nist.gov/nist-research-library/library-faqs) (_e.g._, for items marked `nist_`)
* [Creative Commons Attribution-ShareAlike 4.0 International Public License](https://creativecommons.org/licenses/by-sa/4.0/legalcode) (_e.g._, for items marked `owasp_10_`)

Original assets are Copyright 2020 Counteractive Security and licensed under the Apache License, Version 2.0 (the "License"); you may not use this work except in compliance with the License. You should have received a [copy of the license](LICENSE) along with this work, and you may obtain a copy of the License [here](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

## Changelog

Version | Release Date | Notes
-- | -- | --
N/A  | N/A | Pre-release
