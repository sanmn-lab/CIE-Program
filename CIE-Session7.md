Verfication 1(Set up SystemD)

Verfication 2(Create Specific User[jump-host-user,dashboard-user,counting-user])

<img width="648" height="414" alt="image" src="https://github.com/user-attachments/assets/d811121b-1249-4666-b3d8-86a83ee14d87" />


<img width="814" height="272" alt="image" src="https://github.com/user-attachments/assets/6f6c6450-d50b-417d-aa62-dbe583cc40de" />


Set dashboard-user for Dashboard-EC2

<img width="1336" height="625" alt="image" src="https://github.com/user-attachments/assets/ad5bfdb7-5e85-4971-8e44-e062d09bcb34" />


Set counting-user for Counting-EC2

<img width="1503" height="771" alt="image" src="https://github.com/user-attachments/assets/6f7d1334-87fc-47b8-9b23-7f9d3697a5e3" />


Change dashboard-user and counting-user

<img width="1464" height="63" alt="image" src="https://github.com/user-attachments/assets/d73e70ec-4aa6-4e1d-8b79-7099fc248261" />


Verfication 3(ELB : LoadBalancer to Recover Single Point of Failure)

<img width="2352" height="1821" alt="image" src="https://github.com/user-attachments/assets/077620f2-461d-450a-b4c5-328fd19d6706" />


<img width="832" height="684" alt="image" src="https://github.com/user-attachments/assets/4df60458-db7b-4fab-bbc3-a0209da337f9" />



Set Permission

chmod 400 Dashboard-EC2-Key.pem

chmod 400 Counting-EC2-Key.pem

<img width="632" height="290" alt="image" src="https://github.com/user-attachments/assets/ed6e8d32-bc8b-4270-9946-74f4909a5a53" />




Install and unzip App

<img width="1530" height="645" alt="image" src="https://github.com/user-attachments/assets/1ce5d4e2-c4d1-4ead-9c60-92e128c9cef9" />
<img width="690" height="648" alt="image" src="https://github.com/user-attachments/assets/833b79f2-d408-425f-84b7-a5645fe18a33" />
<img width="855" height="621" alt="image" src="https://github.com/user-attachments/assets/2758b396-a322-47ed-8f32-012be63cd5b0" />

Unhealthy ⇒ Healthy
<img width="843" height="621" alt="image" src="https://github.com/user-attachments/assets/7f427a42-6db2-4e4b-9502-fbc15837c460" />

<img width="1588" height="591" alt="image" src="https://github.com/user-attachments/assets/b28e4fcb-176d-42c4-b648-ebb1289eced4" />
<img width="1588" height="504" alt="image" src="https://github.com/user-attachments/assets/042aaa11-d53d-49b5-b4c9-96aef3c8beb7" />

Verfication 4(Load Test)

dashboard-load-test.js
import http from 'k6/http';
import { check } from 'k6';

const BASE_URL =
  __ENV.BASE_URL ||
  'http://Dashboard-LB-2044222564.ap-northeast-1.elb.amazonaws.com';

const RATE = Number(__ENV.RATE || 1000);
const DURATION = __ENV.DURATION || '60s';

export const options = {
  discardResponseBodies: true,

  scenarios: {
    dashboard_traffic: {
      executor: 'constant-arrival-rate',
      rate: RATE,
      timeUnit: '1s',
      duration: DURATION,
      preAllocatedVUs: 300,
      maxVUs: 1000,
      gracefulStop: '10s',
    },
  },

  thresholds: {
    http_req_failed: ['rate<0.01'],
    http_req_duration: ['p(95)<1000'],
    checks: ['rate>0.99'],
  },
};

export default function () {
  const response = http.get(`${BASE_URL}/`, {
    tags: {
      endpoint: 'dashboard-home',
    },
  });

  check(response, {
    'status is 200': (r) => r.status === 200,
  });
}

<img width="2695" height="1716" alt="image" src="https://github.com/user-attachments/assets/6fb5b958-daa1-4d63-8c71-d459179be6d6" />
