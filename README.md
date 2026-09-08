# CIE-Program 2
Dashboard App and Counting App running in Local IP.

GitHub
[Releases · hashicorp/demo-consul-101](https://github.com/hashicorp/demo-consul-101/releases)

Git Bash
PORT=9999 ./dashboard-service

Powershell Listen
while ($true) { Clear-Host; netstat -ano | findstr :9999; Start-Sleep 1 }

<img width="2713" height="1714" alt="image" src="https://github.com/user-attachments/assets/af9721fa-f856-4287-9ee9-37f7c7cbadfb" />

Multiple Access
<img width="2724" height="1692" alt="image" src="https://github.com/user-attachments/assets/7b8f4a91-f978-424f-9827-2fba21733193" />

Upstring Doewnstring Concept
User　→→　Browser　→→　Application (Dashboard app　→→　Counting app)

          　  　　 →→　Browser：Dashboard app is Upstring.

                   ←←　Application：Browser is Downstring.

Git Bash
PORT=9000 ./counting-service
PORT=9999 COUNTING_SERVICE_URL="http://localhost:9000" ./dashboard-service

Powershell Listen
while ($true) { Clear-Host; netstat -ano | findstr :9000; Start-Sleep 1 }

<img width="1266" height="423" alt="image" src="https://github.com/user-attachments/assets/70299c11-e49d-4dfa-bbc4-bf13369b7587" />

When we changed 9000 to 9001
PORT=9999 COUNTING_SERVICE_URL="http://localhost:9001" ./dashboard-service

<img width="2691" height="1635" alt="image" src="https://github.com/user-attachments/assets/2a154c5e-7b40-47e4-9182-59dea6b13a3e" />
<img width="1269" height="477" alt="image" src="https://github.com/user-attachments/assets/fb2b04f5-68dc-4503-b52f-b4bc3cda1a1b" />

NOTE: 
Application  Scale means Horizional Scaling. (Solve for Single Point of failure)
CPU size extaned means Vertival Scaling. (Solve for Load Problem)
