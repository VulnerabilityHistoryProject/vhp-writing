Vulnerabilities with this tag were given a CVSS rating as part of the requirement to be included into the [National Vulnerability Database](https://nvd.nist.gov/). You can learn more about what the individual scores mean in the [CVSS specification document](https://www.first.org/cvss/specification-document). 

Quote from the CVSS specification regarding High Access Complexity:

>   This metric describes the conditions beyond the attacker’s control that must exist in order to exploit the vulnerability. As described below, such conditions may require the collection of more information about the target, or computational exceptions. 
>   Importantly, the assessment of this metric excludes any requirements for user interaction in order to exploit the vulnerability (such conditions are captured in the User Interaction metric). 
>   If a specific configuration is required for an attack to succeed, the Base metrics should be scored assuming the vulnerable component is in that configuration. The Base Score is greatest for the least complex attacks.
> 	A successful attack depends on conditions beyond the attacker's control. That is, a successful attack cannot be accomplished at will, but requires the attacker to invest in some measurable amount of effort in preparation or execution against the  
>    vulnerable component before a successful attack can be expected. For example, a successful attack may depend on an attacker overcoming any of the following conditions:
>   * The attacker must gather knowledge about the environment in which the vulnerable target/component exists. For example, a requirement to collect details on target configuration settings, sequence numbers, or shared secrets.
>   * The attacker must prepare the target environment to improve exploit reliability. For example, repeated exploitation to win a race condition, or overcoming advanced exploit mitigation techniques.
>   * The attacker must inject themselves into the logical network path between the target and the resource requested by the victim in order to read and/or modify network communications (e.g., a man in the middle attack).