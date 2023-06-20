# advance-smart-contract-development-on-celo
Advanced smart contract development for Celo developers: Working with Yul and inline assembly - part 1

## Yul's Syntax

- Comments
   > Yul parses comments, identifiers, and literals in ways similar to Solidity.
   Use `//` and `/* */` to denote comments.

- Code block
   - declaring a variable,
        ```js
           let y := 5,  
           let x := add(y, 3) 
           let x  - initial value will be set to zero (0)
       ```

   - literals (string or hex or integer literals. 
       > E.g `0x1234`, `47` or `"abc"` (strings up to 32 characters)

   - Calling builtin functions: 
        ```js
            add(1, mload(0))
            sub(6, mload(0))
            sub(6,  add(1, mload(0)))
        ```

   - identifiers (variables)
       ```js
           add(5, y)
           sub(4, x)
           mul(7, z)
       ```

    - assignments,
       ```js
          x := add(y, 6)
          y := 5
          x := div(z, 2)
       ```
     - Local block scope i.e. where local variables are scoped
        ```js
         { 
             let initValue := 3 
             { 
                let result := add(initValue, 10) 
             } 
         }
        ```

    - if statements
      ```js
         if lt(x, y) { 
              sstore(0, 1) 
         }
      ```
    
    - Switch statements

        ```js
        {
            function power(_b, _exp) -> result
            {
                switch _exp
                case 0 { result := 1 }
                case 1 { result := _b }
                default
                {
                    result := power(mul(_b, _b), div(_exp, 2))
                    switch mod(_exp, 2)
                        case 1 { result := mul(_b, result) }
                }
            }
        }
        ```
   - for loops
      ```js
         for { let i := 0} lt(i, 10) { i := add(i, 1) } { 
           mstore(i, 7) 
         }
      ```
   - Defining functions
      ```js
          function doSomething(a, b) -> c { 
              c := add(a, b) 
         }
      ```
