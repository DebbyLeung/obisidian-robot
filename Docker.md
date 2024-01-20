pull image
```
docker pull helloworld
```
docker compose detached
```
docker-compose up -d
```

Example of Dockerfile
```
# base image from external can include (cuda/ubuntu/python/...)
FROM pytorch/pytorch:latest

# send cli - Install dependencies
RUN pip install jupyter transformers[torch] sentencepiece
  
# Set the working directory
WORKDIR /app


# Expose the container's port
EXPOSE 1234

# Start the Jupyter notebook server
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=1234", "--allow-root"]
```
build image
```
docker build -t chatglm . #location of Dockerfile
```

run image
```
# p= expose port, v= mount volume [IMAGE]
docker run --gpus all -p 1234:1234 -v C:\Users\stebb\OneDrive\Documents\GitHub\nlp_tut:/app chatglm:latest 
```