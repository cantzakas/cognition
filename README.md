# cognition
pivotal-cognition-use-case-and-poc

## Info on Syslog Message Format

The syslog message has the following ABNF [RFC5234] definition:

      SYSLOG-MSG      = HEADER SP STRUCTURED-DATA [SP MSG]

      HEADER          = PRI VERSION SP TIMESTAMP SP HOSTNAME
                        SP APP-NAME SP PROCID SP MSGID
      PRI             = "<" PRIVAL ">"
      PRIVAL          = 1*3DIGIT ; range 0 .. 191
      VERSION         = NONZERO-DIGIT 0*2DIGIT
      HOSTNAME        = NILVALUE / 1*255PRINTUSASCII

      APP-NAME        = NILVALUE / 1*48PRINTUSASCII
      PROCID          = NILVALUE / 1*128PRINTUSASCII
      MSGID           = NILVALUE / 1*32PRINTUSASCII

      TIMESTAMP       = NILVALUE / FULL-DATE "T" FULL-TIME
      FULL-DATE       = DATE-FULLYEAR "-" DATE-MONTH "-" DATE-MDAY
      DATE-FULLYEAR   = 4DIGIT
      DATE-MONTH      = 2DIGIT  ; 01-12
      DATE-MDAY       = 2DIGIT  ; 01-28, 01-29, 01-30, 01-31 based on
                                ; month/year
      FULL-TIME       = PARTIAL-TIME TIME-OFFSET
      PARTIAL-TIME    = TIME-HOUR ":" TIME-MINUTE ":" TIME-SECOND
                        [TIME-SECFRAC]
      TIME-HOUR       = 2DIGIT  ; 00-23
      TIME-MINUTE     = 2DIGIT  ; 00-59
      TIME-SECOND     = 2DIGIT  ; 00-59
      TIME-SECFRAC    = "." 1*6DIGIT
      TIME-OFFSET     = "Z" / TIME-NUMOFFSET
      TIME-NUMOFFSET  = ("+" / "-") TIME-HOUR ":" TIME-MINUTE


      STRUCTURED-DATA = NILVALUE / 1*SD-ELEMENT
      SD-ELEMENT      = "[" SD-ID *(SP SD-PARAM) "]"
      SD-PARAM        = PARAM-NAME "=" %d34 PARAM-VALUE %d34
      SD-ID           = SD-NAME
      PARAM-NAME      = SD-NAME
      PARAM-VALUE     = UTF-8-STRING ; characters '"', '\' and
                                     ; ']' MUST be escaped.
      SD-NAME         = 1*32PRINTUSASCII
                        ; except '=', SP, ']', %d34 (")

      MSG             = MSG-ANY / MSG-UTF8
      MSG-ANY         = *OCTET ; not starting with BOM
      MSG-UTF8        = BOM UTF-8-STRING
      BOM             = %xEF.BB.BF
