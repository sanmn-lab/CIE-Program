# CIE-Session-6

### HandsOn Process

## Upload Dashboard App

## ssh connect
ssh -i C:\Users\Owner\.ssh\max-effort-lab.pem ubuntu@35.72.6.172

## scp file upload
scp -i C:\Users\Owner\.ssh\max-effort-lab.pem  -r C:\CIE-Program\pov-consul ubuntu@35.72.6.172:/home/ubuntu

## Upload Counting App

## ssh connect
ssh -i C:\Users\Owner\.ssh\max-effort-lab.pem ubuntu@35.72.6.172

## scp file upload
scp -i C:\Users\Owner\.ssh\max-effort-lab.pem   `-o "ProxyJump=ubuntu@35.72.6.172"`
.\counting-service_linux_amd64 `
ubuntu@172.31.10.204:/home/ubuntu/

Public Dashboard to Private Counting Architecture:

    Your PC
      │
      │ HTTP :9001
      ▼
    Dashboard EC2
    35.72.6.172:9001
      │
      │ HTTP :9002
      ▼
    Counting EC2
    172.31.10.204:9002

### 1. PowerShell ကနေ Dashboard EC2 ကို SSH ဝင်ပါ

`bash` command သီးသန့် run စရာမလိုပါဘူး။ PowerShell ကနေ SSH နဲ့ Ubuntu EC2 ထဲဝင်တာနဲ့ Linux bash shell ရပါပြီ။

  ```
  ssh-i"C:\Users\Owner\.ssh\max-effort-lab.pem"ubuntu@35.72.6.172
  ```

ဝင်ပြီးရင်—

  ```
  ubuntu@ip-172-31-32-221:~$
  ```

မြင်ရပါမယ်။ ဒါက Dashboard EC2 ရဲ့ Linux shell ပါ။


### 2. Dashboard ကနေ Counting EC2 ကို SSH ဝင်ချင်ရင်

အရင်ကလို agent forwarding မလုပ်ချင်ရင် PowerShell ကနေ **တစ်ကြောင်းတည်း** ProxyJump နဲ့ ဝင်တာပိုလွယ်ပါတယ်။

Dashboard shell မှာရှိနေရင် အရင်—

```
exit
```

PowerShell ပြန်ရောက်ရင်—

```
ssh-i"C:\Users\Owner\.ssh\max-effort-lab.pem" `-Jubuntu@35.72.6.172 `ubuntu@172.31.10.204
```

အောင်မြင်ရင်—

```
ubuntu@ip-172-31-10-204:~$
```

ရောက်ပါမယ်။

### 3. Counting App ကို port 9002 နဲ့ run ပါ

Counting EC2 ထဲမှာ—

  ```
  cd /home/ubuntuchmod+x counting-service_linux_amd64exportPORT=9002
  ./counting-service_linux_amd64
  ```

သင့် binary က folder တခြားတစ်ခုမှာရှိရင် actual path ကိုသုံးပါ။

အောင်မြင်ရင် အကြမ်းဖျင်း—

  ```
  Serving at http://localhost:9002
  (Pass as PORT environment variable)
  ```

ပြပါလိမ့်မယ်။

**ဒီ terminal ကို မပိတ်သေးပါနဲ့။**

### 4. PowerShell အသစ်တစ်ခုဖွင့်ပြီး Dashboard ကို SSH ဝင်ပါ

Windows မှာ PowerShell window အသစ်ဖွင့်ပြီး—

  ```
  ssh-i"C:\Users\Owner\.ssh\max-effort-lab.pem"ubuntu@35.72.6.172
  ```

Dashboard EC2 ရောက်ရင် Counting ကို စမ်းပါ။

  ```
  curl http://172.31.10.204:9002
  ```

ဒါမှမဟုတ် TCP connection ကိုစစ်ရန်—

  ```
  nc-vz172.31.10.2049002
  ```

အောင်မြင်ရင်—

  ```
  Connection to 172.31.10.204 9002 port [tcp/*] succeeded!
  ```

ရပါမယ်။

### 5. Dashboard App ကို 9001 နဲ့ run ပါ

Dashboard EC2 မှာ—

  ```
  cd /home/ubuntu/pov-consul
  ```

ပြီးရင်—

  ```
  exportPORT=9001exportCOUNTING_SERVICE_URL=http://172.31.10.204:9002
  ```

စစ်ကြည့်ပါ။

  ```
  echo$PORTecho$COUNTING_SERVICE_URL
  ```

Output:

  ```
  9001
  http://172.31.10.204:9002
  ```

ပြီးရင် Dashboard run ပါ။

  ```
  ./dashboard-service_linux_amd64
  ```

ဒီလိုထွက်သင့်ပါတယ်။
  
  ```
  Starting server on http://0.0.0.0:9001
  (Pass as PORT environment variable)
  
  Using counting service at http://172.31.10.204:9002
  (Pass as COUNTING_SERVICE_URL environment variable)
  
  Starting websocket server...
  ```

အခု browser မှာ—

  ```
  http://35.72.6.172:9001
  ```

သုံးပြီး Dashboard ကို ဖွင့်နိုင်ပါတယ်။

  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```
  
###Configuration

    Internet
       │
       │ TCP 9001
       ▼
    Dashboard-SG
    Dashboard EC2
    35.72.6.172
       │
       │ TCP 9002
       │ Source = Dashboard-SG
       ▼
    Counting-SG
    Counting EC2
    172.31.10.204

<img width="1477" height="1065" alt="image" src="https://github.com/user-attachments/assets/b6b4ee9f-0112-42ed-b6c0-6209b950670f" />
<img width="1590" height="702" alt="image" src="https://github.com/user-attachments/assets/c002fa7e-12b1-432c-8766-e47907a92ed1" />
<img width="1588" height="706" alt="image" src="https://github.com/user-attachments/assets/e7382116-d36c-4a31-9798-7fbb8bdd1135" />
<img width="1586" height="711" alt="image" src="https://github.com/user-attachments/assets/f3b60131-0a2a-450b-81c6-e792381f3c10" />
<img width="1579" height="603" alt="image" src="https://github.com/user-attachments/assets/4773612c-8ece-4c59-8015-58a8df7d4721" />
<img width="1586" height="573" alt="image" src="https://github.com/user-attachments/assets/f332004c-aa49-445e-bb2c-7914fd69d297" />
<img width="1579" height="690" alt="image" src="https://github.com/user-attachments/assets/be4c6d9d-2761-4693-a34e-38252129ee8f" />
<img width="1579" height="695" alt="image" src="https://github.com/user-attachments/assets/021d9599-6cbf-4a23-9c34-455caac624fd" />
<img width="1593" height="803" alt="image" src="https://github.com/user-attachments/assets/9ceabdc8-716e-45b9-80cb-085c73880cc6" />
<img width="1962" height="1100" alt="image" src="https://github.com/user-attachments/assets/a9b521ac-a0d5-4b29-aec3-ccd4b61f85b6" />
<img width="1962" height="1264" alt="image" src="https://github.com/user-attachments/assets/a72f4025-36cf-4521-933d-4e9e5c86eaf1" />

  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```  ```
