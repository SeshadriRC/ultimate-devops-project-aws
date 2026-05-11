# Developer - DevOps Collaboration in understanding build steps

- Video of the lecture on udemy is self explanatory. No additional notes is required.


### Learned from the video

- This project contains 21 microservices.
- In `src` folder we can see all the microservices.
- We are planning to containerize the microservice which written in popular programming language.
- We can identify using colour code in the architecture. use the architecture link which given in starting of the section to see it clearly. Just we are selecting one microservice for each programming language.
<img width="1705" height="1000" alt="image" src="https://github.com/user-attachments/assets/ad0f496a-d99d-4b29-9afb-9bacd8662882" />

- Java -> Ad service
- Go -> product catalog service
- Python -> Recommendation service

- We shud not directly start containerizing the microservice, first we need to navigate to each microservice folder and go through the `readme.md`. If any doubt we can check with the developer.
- Every programming language has a dependency file. For example, Python has a dependency file which is requirements.txt. Similarly, Java has a dependency file. If you're using Maven, the dependencies are written in `Pom.xml`.If you're using Gradle, the dependencies are defined in `Gradle` files.

- Similarly for go, there is a file called `Go.mod` where the complete dependencies are mentioned.
- In this video abhishek just ran go based application locally in EC2 by following the readme.md file of product catalog service
- It should show the output like below
<img width="1872" height="801" alt="image" src="https://github.com/user-attachments/assets/bf11a582-65f4-4546-974b-c9f5bfa80883" />

- Install the go locally before executing the command.


<img width="1289" height="208" alt="image" src="https://github.com/user-attachments/assets/12910ea6-bea0-4a35-b30a-8d9e88756f94" />

<img width="1301" height="454" alt="image" src="https://github.com/user-attachments/assets/61f7cd46-465d-4c01-b85b-d2f31499b66a" />

<img width="1348" height="185" alt="image" src="https://github.com/user-attachments/assets/ffee6531-42b5-47b5-98d0-4b79e7974303" />

```
-o means: It tells Go what filename to create after building the application.
```
