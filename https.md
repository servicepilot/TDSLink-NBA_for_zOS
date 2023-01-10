
# Access ServicePilot TDSLink - NBA for zOS using HTTPS

The TDSLink - NBA for zOS agent includes a web interface serving pages using HTTP. To secure this interface with HTTPS it is necessary to implement **AT-TLS** technology.


## AT-TLS information

- [Application Transparent Transport Layer Security (AT-TLS)](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.halx001/transtls.htm)

- [Getting started with AT-TLS](https://www.ibm.com/support/knowledgecenter/SSLTBW_2.1.0/com.ibm.zos.v2r1.halz002/attls_get_started.htm)

- [Using the RACDCERT command to administer certificates](https://www.ibm.com/support/knowledgecenter/SSLTBW_2.1.0/com.ibm.zos.v2r1.icha700/digurdc.htm)


## AT-TLS settings for TDSLink - NBA for zOS

1. Add a *server* certificate for TDSLink - NBA for zOS (See `RACDCERT` command)
2. Add the *server* certificate *private key*
3. Add the *server* certificate chain
4. Associate the server certificate information with **AT-TLS** with `RACF` rules.

   For reference, here are `RACF` rules and keyring:

   Digital ring information for user NWNBA: 
Ring: 

       >HTTPSRING< 
       Certificate Label Name Cert Owner USAGE DEFAULT
       -------------------------------- ------------ -------- -------
       XXXX-MPOLICY-G2-CA CERTAUTH CERTAUTH NO 
       XXXX-PRODMASSL4-G2-CA CERTAUTH CERTAUTH NO 
       XXXX-PRODSSL6-G2-CA CERTAUTH CERTAUTH NO 
       XXXX-Root-G2-CA CERTAUTH CERTAUTH NO 
       MAINFRAME B000 CERT G2 2018 SITE PERSONAL NO
       *** 
       PERMIT IRR.DIGTCERT.GENCERT CLASS(FACILITY) ID(NWNBA) ACCESS(CONTROL) 
       PERMIT IRR.DIGTCERT.LISTRING CLASS(FACILITY) ID(NWNBA) ACCESS(READ) 
       PERMIT IRR.DIGTCERT.LISTRING CLASS(FACILITY) ID(NWNBA) ACCESS(UPDATE)

5. Configure **AT-TLS** to let all IP addresses connect to all mainframe addresses. Set ciphers and TLS1.2 only. Set the TDSLink - NBA for zOS port as allowing inbound connections only from the certificate label in the policy.

## Copyright

© Copyright ServicePilot Inc 2023
