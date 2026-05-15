
```bash
kubectl apply -f ingress.yaml
```

- After applying ingress.yaml, if incase any issue, we can check the ALB controller logs

<img width="915" height="102" alt="image" src="https://github.com/user-attachments/assets/b453ccfa-5e4a-4d14-9c25-d3ad17c48622" />

<img width="929" height="420" alt="image" src="https://github.com/user-attachments/assets/5831082e-d381-452c-ae80-afa87de4822e" />

- If you try to access with the address, it should not work. It should work only if you use `example.com`
- But we didn't bought this domain `example.com`, so we will bypass the laptop hosts file. In linux we need to edit in `/etc/hosts `, in windows we can edit `/system32/etc/host` location. please check the chatgpt.

<img width="930" height="233" alt="image" src="https://github.com/user-attachments/assets/49240d5c-9381-4ba9-8be7-e681fda509fd" />

- Now if you hit `example.com` you are able to view the website.

<img width="592" height="189" alt="image" src="https://github.com/user-attachments/assets/98860ffe-d786-46a6-a5b9-8cfb6955547a" />

<img width="941" height="295" alt="image" src="https://github.com/user-attachments/assets/f7a12931-80da-4703-94b8-27f87a17c775" />
