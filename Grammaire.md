PROGRAM         ::= "program" ID ";" { CONST_DECL | TYPE_DECL | VAR_DECL } PROC_FUNC_PART BLOC "."

CONST_DECL      ::= "const" CONST_ITEM { CONST_ITEM }

CONST_ITEM      ::= ID "=" "(" NUM | REAL ")" ";"

TYPE_DECL       ::= "type" TYPE_ITEM { TYPE_ITEM }

TYPE_ITEM       ::= ID "=" TYPE_EXPR ";"

VAR_DECL        ::= "var" VAR_ITEM { VAR_ITEM }

VAR_ITEM        ::= ID_LIST ":" BASE_TYPE ";"

ID_LIST         ::= ID { "," ID }

BASE_TYPE       ::= "integer" | "real" | "boolean" | ID

PROC_FUNC_PART  ::= { PROC_DECL | FUNC_DECL }

PROC_DECL       ::= "procedure" ID [ PARAM_DECL_LIST ] ";" BLOC ";"

PARAM_DECL_LIST ::= PARAM_GROUP { ";" PARAM_GROUP }

PARAM_GROUP     ::= ID_LIST ":" BASE_TYPE

FUNC_DECL       ::= "function" ID [ PARAM_DECL_LIST ] ":" BASE_TYPE ";" BLOC ";"

BLOC            ::= { CONST_DECL | TYPE_DECL | VAR_DECL } "begin" INSTS "end"

INSTS           ::= INST { ";" INST }

INST            ::= CALL_OR_ASSIGN | IF_INST | WHILE_INST | REPEAT_INST | FOR_INST | CASE_INST | "begin" INSTS "end" | WRITE_INST | READ_INST

CALL_OR_ASSIGN  ::= ID [ "(" ARGUMENTS ")" ] | ID ":=" EXPR

IF_INST         ::= "if" COND "then" INST [ "else" INST ]

WHILE_INST      ::= "while" COND "do" INST

REPEAT_INST     ::= "repeat" INSTS "until" COND

FOR_INST        ::= "for" ID ":=" EXPR  ( "to" | "downto" )  EXPR "do" INST

CASE_INST       ::= "case" EXPR "of" CASE_BRANCHES [ "else" INST ] "end"

CASE_BRANCHES   ::= { NUM ":" INST ";" } | [ "else" INST [";"] ]  

CASE_BRANCH     ::= NUM ":" INST [ ";" ]

WRITE_INST      ::= "write" "(" EXPR { "," EXPR } ")"

READ_INST       ::= "read" "(" ID { "," ID } ")"

COND            ::= EXPR RELOP EXPR

RELOP           ::= "=" | "<>" | "<" | "<=" | ">" | ">="

EXPR            ::= TERM { ("+" | "-") TERM }

TERM            ::= FACT { ("*" | "/") FACT }

FACT            ::= ID [ "(" ARGUMENTS ")" ] | NUM | REAL | "(" EXPR ")"

ARGUMENTS       ::= EXPR { "," EXPR }

ID              ::= LETTER { LETTER | DIGIT }

NUM             ::= DIGIT { DIGIT }

REAL            ::= NUM "." NUM

LETTER          ::= "a" | "b" | ... | "z" | "A" | ... | "Z"

DIGIT           ::= "0" | "1" | ... | "9"