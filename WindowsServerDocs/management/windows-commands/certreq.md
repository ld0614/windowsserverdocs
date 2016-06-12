---
title: certreq
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
---
# certreq
Certreq can be used to request certificates from a certification authority \(CA\), to retrieve a response to a previous request from a CA, to create a new request from an .inf file, to accept and install a response to a request, to construct a cross\-certification or qualified subordination request from an existing CA certificate or request, and to sign a cross\-certification or qualified subordination request.  
  
> [!WARNING]  
> Earlier versions of certreq may not provide all of the options that are described in this document. You can see all the options that a specific version of certreq provides by running the commands shown in the Syntax notations section.  
  
## <a name="BKMK_Contents"></a>Contents  
The major sections in this article are as follows:  
  
1.  [verbs](certreq.md#BKMK_verbs)  
  
2.  [Syntax notations](certreq.md#BKMK_notation)  
  
3.  [Options](certreq.md#BKMK_Options)  
  
4.  [formats](certreq.md#BKMK_formats)  
  
5.  [additional certreq examples](certreq.md#BKMK_Examples)  
  
## <a name="BKMK_verbs"></a>verbs  
There following table describes the verbs that can be used with the certreq command  
  
|Switch|Description|  
|----------|---------------|  
|\-Submit|Submits a request to a CA. for more information, see [Certreq \-submit](certreq.md#BKMK_Submit).|  
|\-retrieve *RequestID*|Retrieves a response to a previous request from a CA. for more information, see [Certreq \-retrieve](certreq.md#BKMK_Retrieve).|  
|\-New|creates a new request from an .inf file. for more information, see [Certreq \-new](certreq.md#BKMK_New).|  
|\-Accept|Accepts and installs a response to a certificate request. for more information, see [Certreq \-accept](certreq.md#BKMK_accept).|  
|\-Policy|Sets the policy for a request. for more information, see [Certreq \-policy](certreq.md#BKMK_policy).|  
|\-Sign|Signs a cross\-certification or qualified subordination request. for more information, see [Certreq \-sign](certreq.md#BKMK_sign).|  
|\-Enroll|Enrolls for or renews a certificate. for more information, see [Certreq \-enroll](certreq.md#BKMK_enroll).|  
|\-?|Displays a list of certreq syntax, options, and descriptions.|  
|*<verb>* \-?|Displays help for the verb specified.|  
|\-v \-?|Displays a verbose list of the certreq syntax, options, and descriptions.|  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_notation"></a>Syntax notations  
  
-   for basic command line syntax, run `certreq -?`  
  
-   for the syntax on using certutil with a specific verb, run **certreq** *<verb>* **\-?**  
  
-   To send all of the certutil syntax into a text file, run the following commands:  
  
    -   `certreq -v -? > certreqhelp.txt`  
  
    -   `notepad certreqhelp.txt`  
  
The following table describes the notation used to indicate command\-line syntax.  
  
|Notation|Description|  
|------------|---------------|  
|Text without brackets or braces|Items you must type as shown|  
|<Text inside angle brackets>|Placeholder for which you must supply a value|  
|\[Text inside square brackets\]|Optional items|  
|{Text inside braces}|Set of required items; choose one|  
|vertical bar \(&#124;\)|Separator for mutually exclusive items; choose one|  
|Ellipsis \(…\)|Items that can be repeated|  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_Submit"></a>Certreq \-submit  
This is the default certreq.exe parameter, if no option is specified explicitly at the command\-line prompt, certreq.exe attempts to submit a certificate request to a CA.  
  
```  
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]  
```  
  
You must specify a certificate request file when using the –submit option. if this parameter is omitted, a common File Open window is displayed where you can select the appropriate certificate request file.  
  
You can use these examples as a starting point to build your certificate submit request:  
  
To submit a simple certificate request use the example below:  
  
```  
certreq –submit certRequest.req certnew.cer certnew.pfx  
```  
  
To request a certificate by specifying the san attribute, see the detailed steps in Microsoft Knowledge Base article 931351 [How to add a Subject Alternative Name to a secure LDAP certificate](http://support.microsoft.com/kb/931351) in the "How to use the Certreq.exe utility to create and submit a certificate request that includes a san" section.  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_Retrieve"></a>Certreq \-retrieve  
  
```  
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]  
```  
  
-   if you don’t specify the CAcomputerName or CAName in \-config CAcomputerName\\CANamea dialog box appears and displays a list of all CAs that are available.  
  
-   if you use \-config \- instead of \-config CAcomputerName\\CAName, the operation is processed using the default CA.  
  
-   You can use certreq \-retrieve *RequestID* to retrieve the certificate after the CA has actually issued it. The *RequestID*PKC can be a decimal or hex with 0x prefix and it can be a certificate serial number with no 0x prefix. You can also use it to retrieve any certificate that has ever been issued by the CA, including revoked or expired certificates, without regard to whether the certificate's request was ever in the pending state.  
  
-   if you submit a request to the CA, the policy module of the CA might leave the request in a pending state and return the *RequestID* to the Certreq caller for display. Eventually, the CA's administrator will issue the certificate or deny the request.  
  
The command below retrieves the certificate id 20 and creates the certificate file \(.cer\):  
  
```  
certreq -retrieve 20 MyCertificate.cer  
  
```  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_New"></a>Certreq \-new  
  
```  
certreq -new [Options] [PolicyFileIn [RequestFileOut]]  
```  
  
Since the INF file allows for a rich set of parameters and options to be specified, it is difficult to define a default template that administrators should use for all purposes. Therefore, this section describes all the options to enable you to create an INF file tailored to your specific needs. The following key words are used to describe the INF file structure.  
  
1.  A *section* is an area in the INF file that covers a logical group of keys. A section always appears in brackets in the INF file.  
  
2.  A *key* is the parameter that is to the left of the equal sign.  
  
3.  A *value* is the parameter that is to the right of the equal sign.  
  
for example, a minimal INF file would look similar to the following:  
  
```  
[NewRequest]   
; at least one value must be set in this section   
Subject = "CN=W2K8-BO-DC.contoso2.com"  
```  
  
The following are some of the possible sections that may be added to the INF file:  
  
**\[NewRequest\]**  
  
This section is mandatory for an INF file that acts as a template for a new certificate request. This section requires at least one key with a value.  
  
|Key|Definition|Value|Example|  
|-------|--------------|---------|-----------|  
|Subject|Several applications rely on the subject information in a certificate. Thus, it is recommended that a value for this key be specified. if the subject is not set here, it is recommended that a subject name be included as part of the subject alternative name certificate extension.|Relative Distinguished Name string values|Subject \= "CN\=computer1.contoso.com" Subject\="CN\=John Smith,CN\=Users,DC\=Contoso,DC\=com"|  
|Exportable|if this attribute is set to TRUE, the private key can be exported with the certificate. To ensure a high level of security, private keys should not be exportable; however, in some cases, it might be required to make the private key exportable if several computers or users must share the same private key.|true, false|ExportableEncrypted \= TRUE. CNG keys can distinguish between this and plaintext exportable. CAPI1 keys cannot.|  
|ExportableEncrypted|Specifies whether the private key should be set to be exportable.|true, false|Exportable \= true **Tip:** Not all public key sizes and algorithms will work with all hash algorithms. Tamehe specified CSP must also support the specified hash algorithm. To see the list of supported hash algorithms, you can run the command `certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo`|  
|HashAlgorithm|Hash Algorithm to be used for this request.|Sha256, sha384, sha512, sha1, md5, md4, md2|HashAlgorithm \= sha1. To see the list of supported hash algorithms use: certutil \-oid 1 &#124; findstr pwszCNGAIgid &#124; findstr \/v CryptOIDInfo|  
|KeyAlgorithm|The algorithm that will be used by the service provider to generate a public and private key pair.|RSA, DH, DSA, EcdH\_P256, EcdH\_P521, EcdSA\_P256, EcdSA\_P384, EcdSA\_P521|KeyAlgorithm \= RSA|  
|KeyContainer|It is not recommended to set this parameter for new requests where new key material is generated. The key container is automatically generated and maintained by the system. for requests where the existing key material should be used, this value can be set to the key\-container name of the existing key. Use the certutil –key command to display the list of available key containers for the machine context. Use the certutil –key –user command for the current user’s context.|Random string value **Tip:** You should use double quotes around any INF key value that has blanks or special characters to avoid potential INF parsing issues.|KeyContainer \= {C347BD28\-7F69\-4090\-AA16\-BC58CF4D749C}|  
|KeyLength|Defines the length of the public and private key. The key length has an impact on the security level of the certificate. Greater key length usually provides a higher security level; however, some applications may have limitations regarding the key length.|Any valid key length that is supported by the cryptographic service provider.|KeyLength \= 2048|  
|KeySpec|Determines if the key can be used for signatures, for Exchange \(encryption\), or for both.|at\_NONE, at\_SIGNatURE, at\_KEYEXchange|KeySpec \= at\_KEYEXchange|  
|KeyUsage|Defines what the certificate key should be used for.|CERT\_DIGITAL\_SIGNatURE\_KEY\_USAGE \-\- 80 \(128\) **Tip:** The values shown are hexadecimal \(decimal\) values for each bit definition. Older syntax can also be used: a single hexadecimal value with multiple bits set, instead of the symbolic representation. for example, KeyUsage \= 0xa0.<br /><br />CERT\_NON\_REPUDIatION\_KEY\_USAGE \-\- 40 \(64\)<br /><br />CERT\_KEY\_ENcipherMENT\_KEY\_USAGE \-\- 20 \(32\)<br /><br />CERT\_DatA\_ENcipherMENT\_KEY\_USAGE \-\- 10 \(16\)<br /><br />CERT\_KEY\_AGREEMENT\_KEY\_USAGE \-\- 8<br /><br />CERT\_KEY\_CERT\_SIGN\_KEY\_USAGE \-\- 4<br /><br />CERT\_offline\_CRL\_SIGN\_KEY\_USAGE \-\- 2<br /><br />CERT\_CRL\_SIGN\_KEY\_USAGE \-\- 2<br /><br />CERT\_ENcipher\_ONLY\_KEY\_USAGE \-\- 1<br /><br />CERT\_DEcipher\_ONLY\_KEY\_USAGE \-\- 8000 \(32768\)|KeyUsage \= "CERT\_DIGITAL\_SIGNatURE\_KEY\_USAGE &#124; CERT\_KEY\_ENcipherMENT\_KEY\_USAGE" **Tip:** Multiple values use a pipe \(&#124;\) symbol separator. Ensure that you use double\-quotes when using multiple values to avoid INF parsing issues.|  
|KeyUsageProperty|Retrieves a value that identifies the specific purpose for which a private key can be used.|NCRYPT\_ALLOW\_DECRYPT\_FLAG \-\- 1<br /><br />NCRYPT\_ALLOW\_SIGNING\_FLAG \-\- 2<br /><br />NCRYPT\_ALLOW\_KEY\_AGREEMENT\_FLAG \-\- 4<br /><br />NCRYPT\_ALLOW\_ALL\_USAGES \-\- ffffff \(16777215\)|KeyUsageProperty \= "NCRYPT\_ALLOW\_DECRYPT\_FLAG &#124; NCRYPT\_ALLOW\_SIGNING\_FLAG"|  
|MachineKeySet|This key is important when you need to create certificates that are owned by the machine and not a user. The key material that is generated is maintained in the security context of the security principal \(user or computer account\) that has created the request. When an administrator creates a certificate request on behalf of a computer, the key material must be created in the machine’s security context and not the administrator’s security context. Otherwise, the machine could not access its private key since it would be in the administrator’s security context.|true, false|MachineKeySet \= true **Tip:** The default is false.|  
|NotBefore|Specifies a date or date and time before which the request cannot be issued. NotBefore can be used with Validityperiod and ValidityperiodUnits.|date or date and time|NotBefore \= "7\/24\/2012 10:31 AM" **Tip:** NotBefore and NotAfter are for Requesttype\=cert only.date parsing attempts to be locale\-sensitive.Using month names will disambiguate and should work in every locale.|  
|NotAfter|Specifies a date or date and time after which the request cannot be issued. NotAfter cannot be used with Validityperiod or ValidityperiodUnits.|date or date and time|NotAfter \= "9\/23\/2014 10:31 AM" **Tip:** NotBefore and NotAfter are for Requesttype\=cert only.date parsing attempts to be locale\-sensitive.Using month names will disambiguate and should work in every locale.|  
|PrivateKeyArchive|The PrivateKeyArchive setting works only if the corresponding Requesttype is set to "CMC" because only the Certificate management Messages over CMS \(CMC\) request format allows for securely transferring the requester’s private key to the CA for key archival.|true, false|PrivateKeyArchive \= True|  
|EncryptionAlgorithm|The encryption algorithm to use.|Possible options vary, depending on the operating system version and the set of installed cryptographic providers.To see the list of available algorithms, run the command`certutil -oid 2 &#124; findstr pwszCNGAlgid`The specified CSP used must also support the specified symmetric encryption algorithm and length.|EncryptionAlgorithm \= 3des|  
|EncryptionLength|Length of encryption algorithm to use.|Any length allowed by the specified EncryptionAlgorithm.|EncryptionLength \= 128|  
|ProviderName|The provider name is the display name of the CSP..|if you do not know the provider name of the CSP you are using, run certutil –csplist from a command line. The command will display the names of all CSPs that are available on the local system|ProviderName \= "Microsoft RSA SChannel Cryptographic Provider"|  
|Providertype|The provider type is used to select specific providers based on specific algorithm capability such as "RSA Full".|if you do not know the provider type of the CSP you are using, run certutil –csplist from a command\-line prompt. The command will display the provider type of all CSPs that are available on the local system.|Providertype \= 1|  
|renewalCert|if you need to renew a certificate that exists on the system where the certificate request is generated, you must specify its certificate hash as the value for this key.|The certificate hash of any certificate that is available at the computer where the certificate request is created. if you do not know the certificate hash, use the Certificates mmc Snap\-In and look at the certificate that should be renewed. Open the certificate properties and see the "Thumbprint" attribute of the certificate. Certificate renewal requires either a PKCS\#7 or a CMC request format.|renewalCert \= 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D|  
|RequesterName **Note:** This makes the request to enroll on behalf of another user request.The request must also be signed with an Enrollment Agent certificate, or the CA will reject the request. Use the \-cert option to specify the enrollment agent certificate.|The requester name can be specified for certificate requests if the Requesttype is set to PKCS\#7 or CMC. if the Requesttype is set to PKCS\#10, this key will be ignored. The Requestername can only be set as part of the request. You cannot manipulate the Requestername in a pending request.|Domain\\User|Requestername \= "Contoso\\BSmith"|  
|Requesttype|Determines the standard that is used to generate and send the certificate request.|PKCS10 \-\- 1<br /><br />PKCS7 \-\- 2<br /><br />CMC \-\- 3<br /><br />Cert \-\- 4 **Tip:** This option indicates a self\-signed or self\-issued certificate. It does not generate a request, but rather a new certificate and then installs the certificate.Self\-signed is the default.Specify a signing cert by using the –cert option to create a self\-issued certificate that is not self\-signed.|Requesttype \= CMC|  
|SecurityDescriptor **Tip:** This is relevant only for machine context non\-smart card keys.|Contain the security information associated with securable objects. for most securable objects, you can specify an object's security descriptor in the function call that creates the object.|Strings based on [security descriptor definition language](http://msdn.microsoft.com/library/aa379567(v=vs.85).aspx).|SecurityDescriptor \= "D:P\(A;;GA;;;SY\)\(A;;GA;;;BA\)"|  
|AlternateSignatureAlgorithm|Specifies and retrieves a Boolean value that indicates whether the signature algorithm object identifier \(OID\) for a PKCS\#10 request or certificate signature is discrete or combined.|true, false|AlternateSignatureAlgorithm \= false **Tip:** for an RSA signature, false indicates a Pkcs1 v1.5. True indicates a v2.1 signature.|  
|Silent|By default, this option allows the CSP access to the interactive user desktop and request information such as a smart card PIN from the user. if this key is set to TRUE, the CSP must not interact with the desktop and will be blocked from displaying any user interface to the user.|true, false|Silent \= true|  
|SMIME|if this parameter is set to TRUE, an extension with the object identifier value 1.2.840.113549.1.9.15 is added to the request. The number of object identifiers depends on the on the operating system version installed and CSP capability, which refer to symmetric encryption algorithms that may be used by Secure Multipurpose Internet Mail Extensions \(S\/MIME\) applications such as Outlook.|true, false|SMIME \= true|  
|UseExistingKeySet|This parameter is used to specify that an existing key pair should be used in building a certificate request. if this key is set to TRUE, you must also specify a value for the renewalCert key or the KeyContainer name. You must not set the Exportable key because you cannot change the properties of an existing key. In this case, no key material is generated when the certificate request is built.|true, false|UseExistingKeySet \= true|  
|KeyProtection|Specifies a value that indicates how a private key is protected before use.|XCN\_NCRYPT\_UI\_NO\_PROTCTION\_FLAG \-\- 0<br /><br />XCN\_NCRYPT\_UI\_PROTECT\_KEY\_FLAG \-\- 1<br /><br />XCN\_NCRYPT\_UI\_forCE\_HIGH\_PROTECTION\_FLAG \-\- 2|KeyProtection \= NCRYPT\_UI\_forCE\_HIGH\_PROTECTION\_FLAG|  
|SuppressDefaults|Specifies a Boolean value that indicates whether the default extensions and attributes are included in the request. The defaults are represented by their object identifiers \(OIDs\).|true, false|SuppressDefaults \= true|  
|FriendlyName|A friendly name for the new certificate.|Text|FriendlyName \= "Server1"|  
|ValidityperiodUnits **Note:** This is used only when the request type\=cert.|Specifies a number of units that is to be used with Validityperiod.|Numeric|ValidityperiodUnits \= 3|  
|Validityperiod **Note:** This is used only when the request type\=cert.|VValidityperiod must be an US English plural time period.|Years, Months, Weeks, Days, Hours, Minutes, Seconds|Validityperiod \= Years|  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
**\[Extensions\]**  
  
This section is optional.  
  
|Extension OID|Definition|Value|Example|  
|-----------------|--------------|---------|-----------|  
|2.5.29.17|||2.5.29.17 \= "{text}"|  
|\_continue\_|||\_continue\_ \= "UPN\=User@Domain.com&"|  
|\_continue\_|||\_continue\_ \= "EMail\=User@Domain.com&"|  
|\_continue\_|||\_continue\_ \= "DNS\=host.domain.com&"|  
|\_continue\_|||\_continue\_ \= "directoryName\=CN\=Name,DC\=Domain,DC\=com&"|  
|\_continue\_|||\_continue\_ \= "URL\=http:\/\/host.domain.com\/default.html&"|  
|\_continue\_|||\_continue\_ \= "IPaddress\=10.0.0.1&"|  
|\_continue\_|||\_continue\_ \= "registeredId\=1.2.3.4.5&"|  
|\_continue\_|||\_continue\_ \= "1.2.3.4.6.1\={utf8}String&"|  
|\_continue\_|||\_continue\_ \= "1.2.3.4.6.2\={octet}AAECAwQFBgc\=&"|  
|\_continue\_|||\_continue\_ \= "1.2.3.4.6.2\={octet}{hex}00 01 02 03 04 05 06 07&"|  
|\_continue\_|||\_continue\_ \= "1.2.3.4.6.3\={asn}BAgAAQIDBAUGBw\=\=&"|  
|\_continue\_|||\_continue\_ \= "1.2.3.4.6.3\={hex}04 08 00 01 02 03 04 05 06 07"|  
|2.5.29.37|||2.5.29.37\="{text}"|  
|\_continue\_|||\_continue\_ \= "1.3.6.1.5.5.7.|  
|\_continue\_|||\_continue\_ \= "1.3.6.1.5.5.7.3.1"|  
|2.5.29.19|||"{text}ca\=0pathlength\=3"|  
|Critical|||Critical\=2.5.29.19|  
|KeySpec|||at\_NONE \-\- 0<br /><br />at\_SIGNatURE \-\- 2<br /><br />at\_KEYEXchange \-\- 1|  
|Requesttype|||PKCS10 \-\- 1<br /><br />PKCS7 \-\- 2<br /><br />CMC \-\- 3<br /><br />Cert \-\- 4|  
|KeyUsage|||CERT\_DIGITAL\_SIGNatURE\_KEY\_USAGE \-\- 80 \(128\)<br /><br />CERT\_NON\_REPUDIatION\_KEY\_USAGE \-\- 40 \(64\)<br /><br />CERT\_KEY\_ENcipherMENT\_KEY\_USAGE \-\- 20 \(32\)<br /><br />CERT\_DatA\_ENcipherMENT\_KEY\_USAGE \-\- 10 \(16\)<br /><br />CERT\_KEY\_AGREEMENT\_KEY\_USAGE \-\- 8<br /><br />CERT\_KEY\_CERT\_SIGN\_KEY\_USAGE \-\- 4<br /><br />CERT\_offline\_CRL\_SIGN\_KEY\_USAGE \-\- 2<br /><br />CERT\_CRL\_SIGN\_KEY\_USAGE \-\- 2<br /><br />CERT\_ENcipher\_ONLY\_KEY\_USAGE \-\- 1<br /><br />CERT\_DEcipher\_ONLY\_KEY\_USAGE \-\- 8000 \(32768\)|  
|KeyUsageProperty|||NCRYPT\_ALLOW\_DECRYPT\_FLAG \-\- 1<br /><br />NCRYPT\_ALLOW\_SIGNING\_FLAG \-\- 2<br /><br />NCRYPT\_ALLOW\_KEY\_AGREEMENT\_FLAG \-\- 4<br /><br />NCRYPT\_ALLOW\_ALL\_USAGES \-\- ffffff \(16777215\)|  
|KeyProtection|||NCRYPT\_UI\_NO\_PROTECTION\_FLAG \-\- 0<br /><br />NCRYPT\_UI\_PROTECT\_KEY\_FLAG \-\- 1<br /><br />NCRYPT\_UI\_forCE\_HIGH\_PROTECTION\_FLAG \-\- 2|  
|SubjectNameFlags|template||CT\_FLAG\_SUBJECT\_REQUIRE\_COMMON\_NAME \-\- 40000000 \(1073741824\)<br /><br />CT\_FLAG\_SUBJECT\_REQUIRE\_dirECTORY\_path \-\- 80000000 \(2147483648\)<br /><br />CT\_FLAG\_SUBJECT\_REQUIRE\_DNS\_AS\_CN \-\- 10000000 \(268435456\)<br /><br />CT\_FLAG\_SUBJECT\_REQUIRE\_EMAIL \-\- 20000000 \(536870912\)<br /><br />CT\_FLAG\_OLD\_CERT\_SUPPLIES\_SUBJECT\_AND\_ALT\_NAME \-\- 8<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_dirECTORY\_GUID \-\- 1000000 \(16777216\)<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_DNS \-\- 8000000 \(134217728\)<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_DOMAIN\_DNS \-\- 400000 \(4194304\)<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_EMAIL \-\- 4000000 \(67108864\)<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_SPN \-\- 800000 \(8388608\)<br /><br />CT\_FLAG\_SUBJECT\_ALT\_REQUIRE\_UPN \-\- 2000000 \(33554432\)|  
|X500NameFlags|||CERT\_NAME\_STR\_NONE \-\- 0<br /><br />CERT\_OID\_NAME\_STR \-\- 2<br /><br />CERT\_X500\_NAME\_STR \-\- 3<br /><br />CERT\_NAME\_STR\_SEMICOLON\_FLAG \-\- 40000000 \(1073741824\)<br /><br />CERT\_NAME\_STR\_NO\_PLUS\_FLAG \-\- 20000000 \(536870912\)<br /><br />CERT\_NAME\_STR\_NO\_QUOTING\_FLAG \-\- 10000000 \(268435456\)<br /><br />CERT\_NAME\_STR\_CRLF\_FLAG \-\- 8000000 \(134217728\)<br /><br />CERT\_NAME\_STR\_COMMA\_FLAG \-\- 4000000 \(67108864\)<br /><br />CERT\_NAME\_STR\_REverSE\_FLAG \-\- 2000000 \(33554432\)<br /><br />CERT\_NAME\_STR\_forWArd\_FLAG \-\- 1000000 \(16777216\)<br /><br />CERT\_NAME\_STR\_DISABLE\_IE4\_UTF8\_FLAG \-\- 10000 \(65536\)<br /><br />CERT\_NAME\_STR\_ENABLE\_T61\_UNICODE\_FLAG \-\- 20000 \(131072\)<br /><br />CERT\_NAME\_STR\_ENABLE\_UTF8\_UNICODE\_FLAG \-\- 40000 \(262144\)<br /><br />CERT\_NAME\_STR\_forCE\_UTF8\_dir\_STR\_FLAG \-\- 80000 \(524288\)<br /><br />CERT\_NAME\_STR\_DISABLE\_UTF8\_dir\_STR\_FLAG \-\- 100000 \(1048576\)<br /><br />CERT\_NAME\_STR\_ENABLE\_PUNYCODE\_FLAG \-\- 200000 \(2097152\)|  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
> [!NOTE]  
> SubjectNameFlags allows the INF file to specify which Subject and SubjectAltName extension fields should be auto\-populated by certreq based on the current user or current machine properties: DNS name, UPN, and so on. Using the literal “template” means the template name flags are used instead. This allows a single INF file to be used in multiple contexts to generate requests with context\-specific subject information.  
>   
> X500NameFlags specifies the flags to be passed directly to CertStrToName API when the Subject INF keys value is converted to an ASN.1 encoded Distinguished Name.  
  
To request a certificate based using certreq \-new use the steps from the example below:  
  
> [!WARNING]  
> The content for this topic is based on the default settings for Windows Server 2008 AD CS; for example, setting the key length to 2048, selecting Microsoft Software Key Storage Provider as the CSP, and using Secure Hash Algorithm 1 \(SHA1\). Evaluate these selections against the requirements of your company’s security policy.  
  
To create a Policy File \(.inf\) copy and save the example below in Notepad and save as RequestConfig.inf:  
  
```  
[NewRequest]   
Subject = "CN=<FQDN of computer you are creating the certificate>"   
Exportable = TRUE   
KeyLength = 2048   
KeySpec = 1   
KeyUsage = 0xf0   
MachineKeySet = TRUE   
[Requestattributes]  
CertificateTemplate=”WebServer”  
[Extensions]   
OID = 1.3.6.1.5.5.7.3.1   
OID = 1.3.6.1.5.5.7.3.2  
  
```  
  
On the computer for which you are requesting a certificate type the command below:  
  
```  
CertReq –New RequestConfig.inf CertRequest.req  
  
```  
  
The following example demonstrates implementing the \[Strings\] section syntax for OIDs and other difficult to interpret data. The new {text} syntax example for EKU extension, which uses a comma separated list of OIDs:  
  
```  
[version]  
Signature="$Windows NT$  
  
[Strings]  
szOID_ENHANCED_KEY_USAGE = "2.5.29.37"  
szOID_PKIX_KP_SERver_AUTH = "1.3.6.1.5.5.7.3.1"  
szOID_PKIX_KP_CLIENT_AUTH = "1.3.6.1.5.5.7.3.2"  
  
[NewRequest]  
Subject = "CN=TestSelfSignedCert"  
Requesttype = Cert  
  
[Extensions]  
%szOID_ENHANCED_KEY_USAGE%="{text}%szOID_PKIX_KP_SERver_AUTH%,"  
_continue_ = "%szOID_PKIX_KP_CLIENT_AUTH%"  
```  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_accept"></a>Certreq \-accept  
  
```  
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]  
```  
  
The –accept parameter links the previously generated private key with the issued certificate and removes the pending certificate request from the system where the certificate is requested \(if there is a matching request\).  
  
You can use this example for manually accepting a certificate:  
  
```  
certreq -accept certnew.cer  
  
```  
  
> [!WARNING]  
> The \-accept verb, the \-user and –machine options indicate whether the cert being installed should be installed in user or machine context. if there’s an outstanding request in either context that matches the public key being installed, then these options are not needed. if there is no outstanding request, then one of these must be specified.  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_policy"></a>Certreq \-policy  
  
```  
certreq -policy [-attrib attributestring] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]  
```  
  
-   The configuration file that defines the constraints that are applied to a CA certificate when qualified subordination is defined is called Policy.inf..  
  
-   You can find an example of the Policy.inf file in the [appendix A of planning and Implementing Cross\-Certification and Qualified Subordination](http://technet.microsoft.com/library/cc738878(WS.10).aspx) white paper.  
  
-   if you type the certreq \-policy without any additional parameter it will open a dialog window so you can select the requested fie \(req, cmc, txt, der, cer or crt\). Once you select the requested file and click Open button, another dialog window will open in order to select the INF file.  
  
You can use this example to build a cross certificate request:  
  
```  
certreq -policy Certsrv.req Policy.inf newcertsrv.req  
  
```  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_sign"></a>Certreq \-sign  
  
```  
certreq -sign [Options] [RequestFileIn [RequestFileOut]]  
```  
  
-   if you type the certreq \-sign without any additional parameter it will open a dialog window so you can select the requested file \(req, cmc, txt, der, cer or crt\).  
  
-   Signing the qualified subordination request may require Enterprise Administrator credentials. This is a best practice for issuing signing certificates for qualified subordination.  
  
-   The certificate used to sign the qualified subordination request is created using the qualified subordination template. Enterprise Admins will have to sign the request or grant user permissions for the individuals that will sign the certificate.  
  
-   When you sign the CMC request, you may need to have multiple personnel sign this request, depending on the assurance level that is associated with the qualified subordination.  
  
-   if the parent CA of the qualified subordinate CA you are installing is offline, you must obtain the CA certificate for the qualified subordinate CA from the offline parent. if the parent CA is online, specify the CA certificate for the qualified subordinate CA during the Certificate Services Installation Wizard.  
  
The sequence of commands below will show how to create a new certificate request, sign it and submit it:  
  
```  
certreq -new policyfile.inf MyRequest.req  
certreq -sign MyRequest.req MyRequest_Sign.req  
certreq -submit MyRequest_Sign.req MyRequest_cert.cer  
  
```  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_enroll"></a>Certreq \-enroll  
To enroll to a certificate  
  
```  
certreq –enroll [Options] TemplateName  
```  
  
To renew an existing certificate  
  
```  
certreq –enroll –cert CertId [Options] renew [ReuseKeys]  
```  
  
You can only renew certificates that are time valid. Expired certificates cannot be renewed and must be replaced with a new certificate.  
  
Here an example of renewing a certificate using its serial number:  
  
```  
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" renew  
```  
  
Here an example of enrolling to a certificate template called WebServer by using asterisk \(\*\) to select the policy server via U\/I:  
  
```  
certreq -enroll –machine –policyserver * "WebServer"  
```  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_Options"></a>Options  
  
|Options|Description|  
|-----------|---------------|  
|\-any|force ICertRequest::Submit to determine encoding type.|  
|\-attrib <attributestring>|Specifies the Name and Value string pairs, separated by a colon.<br /><br />Separate Name and Value string pairs with \\n \(for example, Name1:Value1\\nName2:Value2\).|  
|\-binary|formats output files as binary instead of base64\-encoded.|  
|\-PolicyServer *<PolicyServer>*|"ldap: *<path>*"<br /><br />Insert the URI or unique ID for a computer running the Certificate Enrollment Policy Web Service.<br /><br />To specify that you would like to use a request file by browsing, just use a minus \(\-\) sign for *<policyserver>*.|  
|\-config <ConfigString>|Processes the operation by using the CA specified in the configuration string, which is CAhostname\\CAName. for an https connection, specify the enrollment server URI. for the local machine store CA, use a minus \(\-\) sign.|  
|\-Anonymous|Use anonymous credentials for Certificate Enrollment Web Services.|  
|\-Kerberos|Use Kerberos \(domain\) credentials for Certificate Enrollment Web Services.|  
|\-ClientCertificate *<ClientCertId>*|You can replace the *<ClientCertID>* with a certificate thumbprint, CN, EKU, template, email, UPN, and the new name\=value syntax.|  
|\-UserName *<UserName>*|Used with Certificate Enrollment Web Services. You can substitute *<UserName>* with the SAM name or domain\\user. This option is for use with the \-p option.|  
|\-p *<Password>*|Used with Certificate Enrollment Web Services. substitute *<Password>* with the actual user's password. This option is for use with the \-UserName option.|  
|\-user|Configures the \-user context for a new certificate request or specifies the context for an a certificate acceptance. This is the default context, if none is specified in the INF or template.|  
|\-machine|Configures a new certificate request or specifies the context for an a certificate acceptance for the machine context. for new requests it must be consistent with the MachineKeyset INF key and the template context. if this option is not specified and the template does not set a context, then the default is the user context.|  
|\-crl|Includes certificate revocation lists \(CRLs\) in the output to the base64\-encoded PKCS \#7 file specified by CertChainFileOut or to the base64\-encoded file specified by RequestFileOut.|  
|\-rpc|Instructs active directory Certificate Services \(AD CS\) to use a remote procedure call \(RPC\) server connection instead of Distributed COM.|  
|\-AdminforceMachine|Use the Key Service or impersonation to submit the request from Local System context. Requires that the user invoking this option be a member of Local Administrators.|  
|\-renewOnBehalfOf|Submit a renewal on behalf of the subject identified in the signing certificate. This sets CR\_IN\_ROBO when calling [ICertRequest::Submit](http://technet.microsoft.com/subscriptions/aa385040.aspx)|  
|\-f|force existing files to be overwritten. This also bypasses caching templates and policy.|  
|\-q|Use silent mode; suppress all interactive prompts.|  
|\-Unicode|Writes Unicode output when standard output is redirected or piped to another command, which helps when invoked from Windows powershell® scripts\).|  
|\-UnicodeText|Sends Unicode output when writing base64 text encoded data blobs to files.|  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
## <a name="BKMK_formats"></a>formats  
  
|formats|Description|  
|-----------|---------------|  
|RequestFileIn|Base64\-encoded or binary input file name: PKCS \#10 certificate request, CMS certificate request, PKCS \#7 certificate renewal request, X.509 certificate to be cross\-certified, or KeyGen tag format certificate request.|  
|RequestFileOut|Base64\-encoded output file name|  
|CertFileOut|Base64\-encoded X\-509 file name.|  
|PKCS10FileOut|for use with the [Certreq \-policy](certreq.md#BKMK_policy) verb only. Base64\-encoded PKCS10 output file name.|  
|CertChainFileOut|Base64\-encoded PKCS \#7 file name.|  
|FullResponseFileOut|Base64\-encoded full response file name.|  
|PolicyFileIn|for use with the [Certreq \-policy](certreq.md#BKMK_policy) verb only. INF file containing a textual representation of extensions used to qualify a request.|  
  
## <a name="BKMK_Examples"></a>additional certreq examples  
The following articles contain examples of certreq usage:  
  
-   [How to Request a Certificate With a Custom Subject Alternative Name](http://technet.microsoft.com/library/ff625722.aspx)  
  
-   [Test Lab Guide: deploying an AD CS Two\-Tier PKI Hierarchy](http://technet.microsoft.com/library/hh831348.aspx)  
  
-   [appendix 3: Certreq.exe Syntax](http://technet.microsoft.com/library/cc736326.aspx)  
  
-   [How to create a web server SSL certificate manually](http://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)  
  
-   [Request an AMT Provisioning Certificate Using a Windows Server 2008 CA](http://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)  
  
-   [Certificate Enrollment for System Center Operations manager Agent](http://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)  
  
-   [AD CS Step by Step Guide: Two Tier PKI Hierarchy deployment](http://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)  
  
-   [How to enable LDAP over SSL with a third\-party certification authority](http://support.microsoft.com/kb/321051)  
  
Return to [Contents](certreq.md#BKMK_Contents)  
  
