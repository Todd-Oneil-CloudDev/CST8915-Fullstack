## Challenges and Learnings

Not really a challenge but I learned a few lessons setting up this lab. When visiting the Store Front on my local machine (localhost:3000) and not the VM. I was still able to reach the Store Front service. I learned that was due to port forwarding from the Remote SSH extension in vscode which allowed me to make that request as if I was local on the VM.

Intalling the individual runtimes was also ver tedious. I can certainly see how mistakes might get made. When installing the runtimes for each service there is the possibility to accidentally install them locally instead of globally. When manually installing runtimes if "sudo" was accidentally omited that runtime wouldn't be installed globally and would cause problems.