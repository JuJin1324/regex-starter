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
> Source: -@-+++--"+"--+++-@-  
> Regex: `.*`  
> First match: `-@-+++--"+"--+++-@-`  
> All matches: `-@-+++--"+"--+++-@-`  
>
> 응용 2) - 사이에 A 가 0개 이상 등장하면 매칭     
> Source: -@-+++--"+"--+++-@-  
> Regex: `-A*-`  
> First match: -@-+++`--`"+"--+++-@-  
> All matches: -@-+++`--`"+"`--`+++-@-  
>
> 응용 3) - 또는 @ 가 0개 이상 등장하면 매칭       
> Source: -@-+++--"+"--+++-@-  
> Regex: `[-@]*`  
> First match: `-@-`+++--"+"--+++-@-  
> All matches: `-@-`+++`--`"+"`--`+++`-@-`  
> 
> `x+`: + 앞에 x 가 1개 이상 등장하면 매칭
> 
> 예시)  
> Source: aabc abc bc  
> Regex: `a+b`  
> First match: `aab`c abc bc  
> All matches: `aab`c `ab`c bc  
>
> 응용 1) 문자 + 가 1개 이상 매칭     
> Source: -@-+ ++--"+"--+ ++-@-  
> Regex: `\++`  
> First match: -@-`+` ++--"*"--+ ++-@-  
> All matches: -@-`+` `++`--"`+`"--`+` `++`-@-
>
> 응용 2) - 사이 문자 @가 1개 이상 매칭     
> Source: -@@@-+ ++--"+"--+++-@@@-  
> Regex: `-@+-`  
> First match: `-@@@-`+ ++--"+"--+++-@@@-  
> All matches: `-@@@-`+ ++--"+"--+++`-@@@-`  
>
> 응용 3) 공백이 아닌 것이 1개 이상 매칭       
> Source: -@@@-+ ++--"+"--+++-@@@-  
> Regex: `[^ ]+`  
> First match: `-@@@-` + ++ - - "+" -- + ++ -@@@-  
> All matches: `-@@@-` `+` `++` `-` `-` `"+"` `--` `+` `++` `-@@@-`  
> 
> `x?`: ? 앞에 x 가 0개 이거나 1개인 경우 매칭  
>
> 예시)  
> Source: aabc abc bc  
> Regex: `a?b`  
> First match: a`ab`c abc bc  
> All matches: a`ab`c `ab`c `b`c  
>
> 응용 1) - 뒤에 X 가 0개 이거나 1개, 그 다음엔 X 가 오고, 다음 X 가 0개 이거나 1개, 그 다음엔 X 가 와야 매칭  
> 즉, -XX, -XXX, -XXXX 매칭  
> Source: --XX-@-XX-@@-XX-@@@-XX-@@@@-  
> Regex: `-X?XX?X`  
> First match: -`-XX`-@-XX-@@-XX-@@@-XX-@@@@-  
> All matches: -`-XX`-@`-XX`-@@`-XX`-@@@`-XX`-@@@@-  
>
> 응용 2) - 뒤에 @ 가 0개 이거나 1개, 그 다음 @ 가 0개 이거나 1개, 그 다음 @ 가 0개 이거나 1개, 그 다음에 - 가 와야 매칭  
> 즉, --, -@-, -@@-, -@@@- 매칭  
> Source: --XX-@-XX-@@-XX-@@@-XX-@@@@-  
> Regex: `-@?@?@?-`  
> First match: `--`XX-@-XX-@@-XX-@@@-XX-@@@@-  
> All matches: `--`XX`-@-`XX`-@@-`XX`-@@@-`XX-@@@@-  

### 수량자(Quantifier) 2
> `.{숫자}`: 와일드카드 문자가 5개 매칭  
> 
> 예시)  
> Source: One ring to bring them all and in the darkness bind them  
> Regex: `.{5}`    
> First match: `One r`ing to bring them all and in the darkness bind them    
> All matches: `One ring to bring them all and in the darkness bind the`m    
> 
> `[]{숫자1, 숫자2}`: [] 범위의 문자가 숫자1 개 이상 숫자2 개 이하로 등장하면 매칭  
> 
> 예시)    
> Source: One ring to bring them all and in the darkness bind them    
> Regex: `[els]{1,3}`      
> First match: On`e` ring to bring them all and in the darkness bind them      
> All matches: On`e` ring to bring th`e`m a`ll` and in th`e` darkn`ess` bind th`e`m   
> 
> 응용 1) 소문자 알파벳이 3개 이상 등장하면 매칭  
> Source: One ring to bring them all and in the darkness bind them    
> Regex: `[a-z]{3,}`      
> First match: One `ring` to bring them all and in the darkness bind them      
> All matches: One `ring` to `bring` `them` `all` `and` in `the` `darkness` `bind` `them`   
> 
> `x+` 는 `x{1,}` 과 같다.  
> 예시) `AB+A` 는 `AB{1,}A` 와 같다.  
> 
> `x*` 는 `x{0,}` 과 같다.  
> 예시) `AB*A` 는 `AB{0,}A` 와 같다.  
> 
> `x?` 는 `x{0,1}` 과 같다.  
> 예시) `AB?A` 는 `AB{0,1}A` 와 같다.  
> 
> `문자.*`: 해당 문자 뒤 전체를 매칭  
> 
> 예시)   
> Source: One ring to bring them all and in the darkness bind them    
> Regex: `r.*`      
> First match: One r`ing to bring them all and in the darkness bind them`      
> All matches: One r`ing to bring them all and in the darkness bind them`   
> 
> `x*?`: 수량자 뒤에 ? 가 오게되면 해당 수량자의 가장 적은 갯수에 매칭되도록 의미가 변한다.  
> 
> 응용 1) `r.*?`: r 뒤에 와일드카드가 0개와야 매칭, 즉 r 만 매칭       
> Source: One ring to bring them all and in the darkness bind them    
> Regex: `r.*?`      
> First match: One `r`ing to bring them all and in the darkness bind them      
> All matches: One `r`ing to b`r`ing them all and in the da`r`kness bind them   
> 
> 응용 2) `r.+?`: r 뒤에 와일드카드가 1개와야 매칭, 즉 r<문자 1개> 만 매칭  
> Regex: `r.+?`      
> First match: One `ri`ng to bring them all and in the darkness bind them      
> All matches: One `ri`ng to b`ri`ng them all and in the da`rk`ness bind them   
>
> 응용 2) `r.??`: r 뒤에 와일드카드가 0개와야 매칭, 즉 r 만 매칭  
> Regex: `r.??`      
> First match: One `r`ing to bring them all and in the darkness bind them      
> All matches: One `r`ing to b`r`ing them all and in the da`r`kness bind them   

### 경계
> `\w`: `[A-z0-9_]` 와 같다. 즉 대소문자와 숫자 그리고 언더스코어를 포함.(w 는 word 를 의미)  
> `\W`: not word 즉 워드가 아닌 것과 같다.  
> `\d`: `[0-9]` 와 같다.  
> `\D`: not digit 숫자가 아님.  
> `[A-z]`: 대소문자를 모두 포함한 범위.  

### Assertions
> `(?=x)`: x 가 포함된 문자열을 찾지만 x 는 매칭에 포함되지 않는다.  
> 
> 예시)  
> Source: AAAX---aaax---111    
> Regex: `\w+(?=X)`      
> First match: `AAA`X---aaax---111      
> All matches: `AAA`X---aaax---111   
> 
> 응용) word 가 1개 이상인 경우, 뒤 끝의 글자가 word 인 경우 매칭, 하지만 뒤의 글자는 매칭에서 제외     
> Source: AAAX---aaax---111    
> Regex: `\w+(?=\w)`      
> First match: `AAA`X---aaax---111      
> All matches: `AAA`X---`aaa`x---`11`1   
 
 
