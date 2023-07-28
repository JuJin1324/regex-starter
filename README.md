# regex-starter
> 정규표현식

## 패턴
### 기본 패턴
> 정규표현식의 기본 패턴은 문자를 그대로 사용하는 것이다.  
> 정규표현식은 기본적으로 대소문자를 구분한다.  
> Source: Hello, world! Hello!   
> Regex: Hello   
> First match: `Hello`, world! Hello!    
> All matches: `Hello`, world! `Hello`!    
>
> Source: Hello, world! Hello! 
> Regex: hello  
> First match: Hello, world! Hello!    
> All matches: Hello, world! Hello!

### 위치
> `^x` 는 시작 문자가 x 인 경우만 찾는다.
> Source: who is who  
> Regex: ^who  
> First match: `who` is who  
> All matches: `who` is who  
> 
> Source: hello who  
> Regex: ^who  
> First match: hello who    
> All matches: hello who    
> 
> `x$` 는 x 로 끝나는 경우만 찾는다.  
> Source: who is who  
> Regex: who$  
> First match: who is `who`  
> All matches: who is `who`  
 
### 이스케이핑
> `^` 이나 `$` 와 같이 정규표현식에서 사용되는 문자가 찾으려는 텍스트인 경우 앞에 `\`(역슬래쉬)를 붙여서 정규표현식이 아닌 문자라는 것을 표현한다.  
> Source: $12$\-\$25$  
> Regex: ^$  
> First match: $12$\-\$25$  
> All matches: $12$\-\$25$  
>
> Source: $12$\-\$25$  
> Regex: \$   
> First match: `$`12$\-\$25$    
> All matches: `$`12`$`\-\`$`25`$`  
>
> Source: $12$\-\$25$  
> Regex: ^\$  
> First match: `$`12$\-\$25$  
> All matches: `$`12$\-\$25$  
>
> Source: $12$\-\$25$  
> Regex: \$$  
> First match: $12$\-\$25`$`  
> All matches: $12$\-\$25`$`  
>
> Source: $12$\-\$25$  
> Regex: \\  
> First match: $12$`\`-\$25$  
> All matches: $12$`\`-`\`$25$

### 와일드카드
> `.`: 모든 문자에 적용되는 와일드카드  
> Source: Regular expressions are powerful!!!    
> Regex: .  
> First match: `R`egular expressions are powerful!!!  
> All matches: `Regular expressions are powerful!!!`  
>
> Source: Regular expressions are powerful!!!    
> Regex: .....  
> First match: `Regula`r expressions are powerful!!!  
> All matches: `Regula` `r expr` `ession` `s are ` `powerf` ul!!!  
> 마지막 ul!!! 는 6글자 미만(위의 정규표현식은 .이 6개이다)이기 때문에 매칭되지 않음.  
>
> **이스케이핑**  
> Source: O.K.  
> Regex: \.  
> First match: O`.`K.  
> All matches: O`.`K`.`  

### 특정문자
> `[xyz]`: [] 안에 들어가는 문자들 중 1개만 일치해도 매칭시킨다.  
> 
> Source: How do you do?  
> Regex: `[oyu]`  
> First match: H`o`w do you do?  
> All matches: H`o`w d`o` `you` d`o`?   
>
> Source: How do you do?  
> Regex: `[dH].`  
> First match: `Ho`w do you do?  
> All matches: `Ho`w `do` you `do`?   
>
> Source: How do you do?  
> Regex: `[oyu][yow]`  
> First match: H`ow` do you do?  
> All matches: H`ow` do `yo`u do?   
> 
> **범위지정**  
> `[C-K]`: 알파벳 대문자 C 부터 순서대로 K 까지 범위의 문자 매칭  
>
> Source: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> Regex: `[C-K]`  
> First match: AB`C`DEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> All matches: AB`CDEFGHIJK`LMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz   
>
> Source: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> Regex: `[a-d]`  
> First match: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n `a`bcdefghijklmnopqrstuvwxyz  
> All matches: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n `abcd`efghijklmnopqrstuvwxyz   
>
> Source: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> Regex: `[a-dC-K]`  
> First match: AB`C`DEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> All matches: AB`CDEFGHIJK`LMNOPQRSTUVWXYZ \n `abcd`efghijklmnopqrstuvwxyz   
> 
> `[]` 안에서의 ^ 의미: Not 의 의미를 가져서 `[]` 안의 문자에 해당하지 않는 매칭  
>
> Source: ABCDEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> Regex: `[^a-dC-K]`  
> First match: `A`BCDEFGHIJKLMNOPQRSTUVWXYZ \n abcdefghijklmnopqrstuvwxyz  
> All matches: `AB`CDEFGHIJK`LMNOPQRSTUVWXYZ \n `abcd`efghijklmnopqrstuvwxyz`   
 
### 서브 패턴
> `(x|y|z)`: 괄호 안에 지정한 문자들 중 1개만 일치해도 매칭  
> 
> 예시)   
> Source: Monday Tuesday Friday  
> Regex: `(on|ues|rida)`  
> First match: M`on`day Tuesday Friday  
> All matches: M`on`day T`ues`day F`rida`y  
> 
> 응용 1)  
> Source: Monday Tuesday Friday  
> Regex: `(Mon|Tues|Fri)day`  
> First match: `Monday` Tuesday Friday   
> All matches: `Monday Tuesday Friday`    
>
> 응용 2) 와일드카드 2개와 서브패턴 그리고 문자   
> Source: Monday Tuesday Friday  
> Regex: `..(id|esd|nd)ay`  
> First match: `Monday` Tuesday Friday   
> All matches: `Monday Tuesday Friday`    

### 수량자(Quantifier)
> `x*`: * 앞에 x 가 0개 이상 등장하면 매칭  
> 
> 예시)  
> Source: aabc abc bc  
> Regex: `a*b`  
> First match: `aab`c abc bc  
> All matches: `aab`c `ab`c `b`c  
> 
> 응용 1) 모든 문자 매칭  
> Source: -@-***--"*"--***-@-  
> Regex: `.*`  
> First match: `-@-***--"*"--***-@-`  
> All matches: `-@-***--"*"--***-@-`  
>
> 응용 2) - 사이에 A 가 0개 이상 등장하면 매칭     
> Source: -@-***--"*"--***-@-  
> Regex: `-A*-`  
> First match: -@-***`--`"*"--***-@-  
> All matches: -@-***`--`"*"`--`***-@-  
>
> 응용 3) - 또는 @ 가 0개 이상 등장하면 매칭       
> Source: -@-***--"*"--***-@-  
> Regex: `[-@]*`  
> First match: `-@-`***--"*"--***-@-  
> All matches: `-@-`***`--`"*"`--`***`-@-`  
> 
> `x+`: + 앞에 x 가 1개 이상 등장하면 매칭
> 
> 예시)  
> Source: aabc abc bc  
> Regex: `a+b`  
> First match: `aab`c abc bc  
> All matches: `aab`c `ab`c bc  
> 
> `x?`: ? 앞에 x 가 0개 이거나 1개인 경우 매칭  
>
> 예시)  
> Source: aabc abc bc  
> Regex: `a?b`  
> First match: a`ab`c abc bc  
> All matches: a`ab`c `ab`c `b`c  


