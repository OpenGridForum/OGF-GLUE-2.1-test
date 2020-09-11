# Appendix A. Place-holder values for unknown data

Whilst people endeavor to provide accurate information, there MAY be situations where specific GLUE attributes MAY be assigned place-holder \(or dummy\) values. These place-holder values carry some additional semantic meaning; specifically, that the correct value is currently unknown and the presented value should be ignored. This appendix describes a set of such place-holder values.

Some attributes within the GLUE schema are required whilst others are optional. If the attribute is optional and the corresponding information is unavailable, the information provider MUST either publish a place-holder or not to publish the attribute. If the attribute is required, then the information MUST either publish a place-holder value or refrain from publishing the GLUE object.

If a place-holder value is published, it MUST conform to the scheme described in this appendix. This is to increase the likelihood that software will understand the nature of the information it receives.

This appendix describes place-holder values that have be chosen so they are obvious "wrong" to humans, unlikely to occur under normal operation and valid within the attribute type. This also allows for detection of failing information provider components.

### A.1. Use cases

There are two principle use-cases for place-holder values, although others MAY exist.

Scenario 1. a static value has no good default value and has not been configured for a particular site.

Some provisions for GLUE Schema provide templates. These templates MAY contain attributes that have no good default value; for example, supplying the correct value MAY require site-specific knowledge. Whilst it is expected that these attributes be configured, it is possible that this does not happen, so exposing the attributes' default values.

Scenario 2. information provider is unable to obtain a dynamic value.

A dynamic value is provided by an information provider by querying the underlying grid resources. This query will use a number of ancillary resources \(e.g., DNS, network hardware\) that might fail; the grid services might also fail. If an attribute is required and the current value is unobtainable, a place-holder value MUST be used.

### A.2. Place-holder values

This section describes a number of values that MAY be represented within a given address space \(e.g., Strings/UTF-8, Integers, FQDNs, IPv4 address space\). Each of the different types are introduced along with the place-holder value and a brief discussion on usage, rational and any other considerations.

### A.3. Extended booleans

The reserved value “undefined” SHOULD be used. The way to express that no value is published MUST be defined in the documents defining the realization to concrete data models \(e.g., \[GLUE-REAL\]\).

### A.4. Simple strings

 \(ASCII/UTF-8\) should use "UNDEFINEDVALUE" or should start "UNDEFINEDVALUE:"

Upper-case letters make it easier to spot and a single word avoids any white-space issues.

A short error message MAY be incorporated into the message by appending the message after the colon.

 Examples:

 UNDEFINEDVALUE

 UNDEFINEDVALUE: unable to contact torque daemon.

Using UNDEFINEDVALUE is a default option for strings that have no widely-known structure. If a value is of a more restrictive sub-type \(e.g., FQDNs, FQANs, URIs\) described below, then the rules for more restrictive form MUST be used.

### A.5. Fully qualified domain names

They MUST use a hostname ending either "example.org" for scenario 1, or "invalid" for scenario 2.

RFC 2606 defines two second-level domains: "example.org" and "example.com". These domains have the advantage of ending with a recognisable TLD, so are recognisable as a DNS name. Default configuration \(scenario 1, above\) MUST use DNS names that end "example.org"

RFC 2606 also reserves the "invalid" Top-Level-Domain \(TLD\) as always invalid and clearly so. For dynamic information gathering, a value ending "invalid" MUST be used.

In both cases, additional information MAY be included by specifying a prefix to "example.org" or "invalid". This MAY be used to specify the class of machine that should be present. For dynamic

infomation, if the class of machine is not published then the FQDN "unknown.invalid" MUST be used.

Examples:

www.example.org

your-CE.example.org

unknown.invalid

site-local-BDII.invalid

### A.6. IPv4 address

It MUST use 192.0.2.250

There are several portions of IPv4 addresses that should not appear on a network, but none that are reserved for documentation or to specify a non-existent address. Using any address leads to the risk of side-effects, should this value be used.

The best option is an IP address from the 192.0.2.0/24 subnet. This subnet is defined in RFC 3330 as "TEST-NET" for use in documentation and example code. For consistency, the value 192.0.2.250 MUST be used.

### A.7. IPv6 addr

It MUST use 2001:DB8::FFFF

There is no documented undefined IPv6 address. RFC 3849 reserves the address prefix 2001:DB8::/32 for documentation. For consistency, the address 2001:DB8::FFFF MUST be used.

### A.8. Integers

It MUST use "all nines"

 For uint32/int32 this is 999,999,999

 For uint64/int64 this is 999,999,999,999,999,999

For integers, all numbers expressible within the encoding \(int32/uint32/etc.\) are valid so there is no safe choice.

If an unsigned integer is encoded as a signed integer, it is possible to use negative numbers safely. However, these numbers will be unrepresentable if the number is stored as an unsigned

integer. For this reason a negative number place-holder MUST not be used.

The number was chosen for three reasons. First, attribute scales are often chosen to reduce the likelihood of overflow: numbers towards MAXINT \(the large number representable in an integer domain\) are less likely to appear. Second, repeated numbers stand out more clearly to humans. Finally, the statistical frequency of measured values often follows Benford's law, which indicates that numbers starting with "1" occur far more frequently than those starting with "9" \(about six times more likely\). For these reasons, information providers MUST use all-nines to indicate a place-holder.

### A.9. File path

It MUST start either "/UNDEFINEDPATH" or "\UNDEFINEDPATH".

As with the simple string, a single upper-case word is recommended. The initial slash indicates that the value is a path. Implementations MUST use whichever slash is most appropriate for the underlying system \(Unix-like systems use a forward-slash\). Software should accept either value as an unknown-value place-holder.

Additional information MAY be encoded as data beyond the initial UNDEFINEDPATH, separated by the same slash as started the value. Additional comments should not use any of the following characters: \ \[ \] ; = " : \| , \* .

Examples:

 /UNDEFINEDPATH

 \UNDEFINEDPATH

 /UNDEFINEDPATH/Path to storage area

 /UNDEFINEDPATH/Broker unavailable

### A.10. Email addresses

It MUST use an undefined FQDN for the domain.

RFC 2822 defines emails addresses to have the form: &lt;local-part&gt; '@' &lt;domain&gt;

The &lt;domain&gt; MUST be an undefined FQDN; see above for a complete description. For email addresses, information providers should use "example.org" for scenario 1. and "unknown.invalid" for scenario 2.

The &lt;local-part&gt; MAY be used to encode a small amount of additional information; for example, it MAY indicate the class of user to whom the email address should be delivered. If no such information is to be encoded the value "user" MUST be used.

Examples:

 user@example.org

 user@unknown.invalid

 site-local-contact@example.org

 local-admin@example.org

### A.11. Uniform Resource Identifier \(URI\)

It is schema-specific

RFC 3986 defines URIs as a "federated and extensible naming system." All URIs start with a schema-name part \(e.g., "http"\) and no schema-name has been reserved for undefined or documenting example values.

For any given URI schema \("http", for example\), it MAY be possible to define a place-holder value within that name-space. If a GLUE value has only one valid schema, the undefined value MUST be taken from that schema. If several schemata are possible, one MUST be chosen from the available options. This should be the most commonly used.

Take care with the URI encoding. All place-holder URI values MUST be valid URIs. If additional information is included, it MUST be encoded so the resulting URI is valid.

For schemata that MAY include a FQDN \(e.g., a reference to an Internet host\), an undefined URI MUST use an undefined FQDN; see above for details on undefined FQDNs.

URI schemata that reference a remote data object \(e.g., "http", "ftp", "https"\), additional information MAY be included as the path. The FQDN indicates that the value is a place-holder, indicating an place-holder value, so information providers should not specify "UNDEFINEDPATH".

For "file" URIs, the path part MUST identify the value as unknown and MUST use the forward-slash variant; see above for details on undefined paths.

For "mailto" URIs \(http://www.ietf.org/rfc/rfc2368.txt\) encapsulates valid email addresses with additional information \(such as email headers and message body\). Place-holder mailto URIs MUST use an unknown email address \(see above\). Any additional information MUST be included in the email body.

There MAY be other schemata in use that are not explicitly covered in this section. A place-holder value should be agreed upon within whichever domain such schemata are used. This place-holder value should be in the spirit of the place-holder values described so far.

Examples:

 http://www.example.org/

 httpg://your-CE.example.org/path/to/end-point

 httpg://unknown.invalid/User%20certificate%20has%20expired

 mailto:site-admin@example.org

 mailto:user@maildomain.invalid?body=Problem%20connecting%20to%20WLMS

 file:///UNDEFINEDPATH

 file:///UNDEFINEDPATH/path%20to%20some%20directory

### A.12. X.509 Distinguished Names

It MUST start O=Grid,CN=UNDEFINEDUSER

X.509 uses a X.500 namespace, represented as several Relative Domain-Names \(RDNs\) concatenated by commas \(we refer to syntax defined in IETF RFC 4514\). The final RDN is usually a single common name \(CN\), although multiple CNs are allowed.

Unknown DN values MUST have at least two entries: an initial O=Grid followed immediately by CN=UNDEFINEDUSER.

Additional information MAY be encoded using extra CN entries. These MUST come after CN=UNDEFINEDUSER.

Examples:

 O=Grid,CN=UNDEFINEDUSER

 O=Grid,CN=UNDEFINEDUSER/CN=Your Grid certificate DN here

 O=Grid,CN=UNDEFINEDUSER/CN=Cannot access SE

### A.13. Fully Qualified Attribute Name \(FQAN\)

It MUST use a VO of "vo.example.org" \(for scenario 1.\) or "unknown.invalid" \(for scenario 2\).

The "VOMS Credential Format" document,

http://edg-wp2.web.cern.ch/edg-wp2/security/voms/edg-voms-credential.pdf

states that FQANs MUST have the form:

/VO\[/group\[/subgroup\(s\)\]\]\[/Role=role\]\[/Capability=cap\]

Where VO is a well-formed FQDN. Unlike FQDNs, VO names MUST be lower-case. The place-holder value for FQAN is derived from the place-holder FQDN \(see Section A.5\). It MUST have no subgroup\(s\) or Capability specified.

Any additional information MUST be encoded within a single Role name. Care should be taken that only valid characters \(A-Z, a-z, 0-9 and dash\) are included.

Examples:

 /vo.example.org

 /vo.example.org/Role=Replace-this-example-with-your-FQAN

 /unknown.invalid

 /unknown.invalid/Role=Unable-to-contact-CE-Error-42

### A.14. Geographic locations

It MUST use longitude 0 degrees, latitude 0 degrees.

Meridians of longitude are taken from \(-180,180\] degrees, whilst parallels of latitude are taken from \[-90,90\] degrees. For a place-holder value to be a valid location, it MUST also be taken from these ranges.

By a happy coincidence, the \(0,0\) location is within the Atlantic Ocean, some 380 miles \(611 kilometers\) south of the nearest country \(Ghana\). Since this location is unlikely to be used and repeated numbers are easier for humans to spot, \(0,0\) MUST be used to specify an place-holder location.

## 

