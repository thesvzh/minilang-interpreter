
# MiniLang: An Interpreter Written in C++

This interpreter and REPL software were developed as part of a programming assignment for [CPS2000: Compiler Theory and Practice](https://www.um.edu.mt/courses/studyunit/CPS2000), a course forming part of my B.Sc. in Mathematics and Computer Science.

![REPL Example](images/repl.gif) 

The following code showcases some valid MiniLang syntax. 

    def square(x : real) : real {
        return x*x;
    }

    def repeat_string(s : string, n : int) : string {
      /* Repeats string s, n times */
      var s_rep : string = "";
      while(n > 0){
         set s_rep = s_rep + s;
         set n = n - 1;
      }
      return s_rep;
    }
    
    def fac(n : int) : int {
       /* Recursive factorial */
       if (n == 0) { return 1; }
       else { return n * fac(n-1); }
    }
       
    print fac(5) - square(5.);             // 95
    print repeat_string("Hello", 10);  
    print square(fac(5)+0.);               // 14400

    def f(x : int) : int {
      def g(x : int) : int {
         // the x outside is temporarily hidden
         set x = 2*x;
         return x + 3;
      }
      return g(x) + 7;
    }

    print f(5);                           // 20

    

### MiniLang Production Rules in Extended BNF
The following extended BNF production rules describe the entire grammar of MiniLang.

    ‹program›           = { ‹statement› } 

    ‹block›             = "{" { ‹statement› } "}"

    ‹statement›         = ‹variable-decl› ";"
                        | ‹assignment› ";"
                        | ‹print-statement› ";"
                        | ‹if-statement›
                        | ‹while-statement›
                        | ‹return-statement› ";"
                        | ‹function-decl›
                        | ‹block›

    ‹function-decl›     = "def" ‹identifier› "(" [‹formal-params›] ")" ":" ‹type› ‹block›

    ‹formal-params›     = ‹formal-param› { "," ‹formal-param› }

    ‹formal-param›      = ‹identifier› ":" ‹type›

    ‹while-statement›   = "while" "(" ‹expression› ")" ‹block›

    ‹if-statement›      = "if" "(" ‹expression› ")" ‹block› ["else" ‹block›]

    ‹return-statement›  = "return" ‹expression›

    ‹print-statement›   = "print" ‹expression›

    ‹variable-decl›     = "var" ‹identifier› ":" ‹type› "=" ‹expression›

    ‹assignment›        = "set" ‹identifier› "=" ‹expression›

    ‹expression›        = ‹simple-expression› { ‹relational-op› ‹simple-expression› }

    ‹simple-expression› = ‹term› { ‹additive-op› ‹term› }

    ‹term›              = ‹factor› { ‹multiplicative-op› ‹factor› }

    ‹factor›            = ‹literal›
                        | ‹identifier›
                        | ‹function-call›
                        | ‹sub-expression›
                        | ‹unary›
                        
    ‹unary›             = ( "+" | "-" | "not" ) { ‹expression› }

    ‹sub-expression›    = "(" ‹expression› ")"

    ‹function-call›     = ‹identifier› "(" [‹actual-params›] ")"

    ‹actual-params›     = ‹expression› { "," ‹expression› }

    ‹relational-op›     = "<" | ">" | "==" | "!=" | "<=" | ">="

    ‹additive-op›       = "+" | "-" | "or"

    ‹multiplicative-op› = "*" | "/" | "and"

    ‹identifier›        = ( "_" | ‹letter› ) { "_" | ‹letter› | ‹digit› }

    ‹literal›           = ‹int-literal›
                        | ‹real-literal›
                        | ‹bool-literal›
                        | ‹string-literal›

    ‹int-literal›       = ‹digit› { ‹digit› }

    ‹real-literal›      = ‹digit› { ‹digit› } "." { ‹digit› }
                        | "." ‹digit› { ‹digit› }

    ‹bool-literal›      = "true" | "false"

    ‹string-literal›    = "“" { ‹printable› } "”"

    ‹printable›         = ‹digit› | ‹letter› | " " | "!" | """ | "#" | "$" | "%" | "&" | "'" | "(" | ")" | "*" | "+" | "," | "-" | "." | "/" | ":" | ";" | "<" | "=" | ">" | "?" | "@" | "[" | "\" | "]" | "^" | "_" | "`" | "{" | "|" | "}" | "~"

    ‹letter›            = "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" | "y" | "z" 

     ‹digit›            = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"





