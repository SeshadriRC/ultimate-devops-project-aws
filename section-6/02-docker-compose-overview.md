
<img width="1727" height="907" alt="image" src="https://github.com/user-attachments/assets/649fbb91-70d8-4c77-88ff-934eb6086b17" />

# Docker compose Overview in simple words

## **1. Services**  
- Services define **containers** in the Docker Compose setup.  
- Each service represents a different part of an application (e.g., database, backend, frontend).  

### **What Goes Into Services?**  
- **Image**: The Docker image to use.  
- **Build**: If no image exists, specify how to build it.  
- **Ports**: Expose container ports.  
- **Environment**: Define environment variables.  
- **Depends_on**: Set service dependencies.  

---

## **2. Networks**  
- Networks allow **containers to communicate** with each other.  
- Containers in the same network **can talk** using service names.  

### **What Goes Into Networks?**  
- **Driver**: Defines the network type (e.g., bridge, overlay).  
- **Attachable**: Allows external containers to join.  

---

## **3. Volumes**  
- Volumes store **persistent data** outside the container.  
- Even if a container stops, the data remains.  

### **What Goes Into Volumes?**  
- **Named Volumes**: Shared storage between containers.  
- **Bind Mounts**: Maps a host directory to a container path.  

---

## **Summary**  
- **Services** define containers and how they run.  
- **Networks** enable communication between containers.  
- **Volumes** store data that persists beyond container restarts.  

With Docker Compose, you can **easily manage multi-container applications**! 🚀  

### Practicals

```bash
# Run the containers, -d is for detached mode
docker compose up -d    

# Stop the containers
docker compose down
```
