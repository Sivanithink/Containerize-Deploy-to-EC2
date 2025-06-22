###Github Actions Take home assignmnet Containerize & Deploy to EC2
## Step-1 The Application Stack
- created app.js and dockerfile and got package.json by  running npm init
- ![Screenshot (172)](https://github.com/user-attachments/assets/647a07ed-1c82-4da3-bbe4-23f008fcffe1)
## Step-2 The Full CI/CD Workflow
- Create the file: .github/workflows/cicd-pipeline.yml
## Step-3 Launching the ec2
- While Creating the security group  we allow incoming traffic on port:22 for SSH and port:3000 for App
![image](https://github.com/user-attachments/assets/88ac0f2b-a12a-457a-b023-fc83b6e55ff8)
- Launched the instance 
![Screenshot (163)](https://github.com/user-attachments/assets/d3b1222d-a185-47f4-8c1a-30f3b77de29f)
- Installed docker inside the EC2
![Screenshot (161)](https://github.com/user-attachments/assets/5fd8c101-6a19-448b-8d2a-5bc33c42d5b4)
## Step-4 Github secrets
- Created 3 repository Secrets EC2_HOST, EC2_SSH_KEY,EC2_USERNAME
![Screenshot (164)](https://github.com/user-attachments/assets/36bb505c-b3b4-487b-8f59-c20b99fc822e)
![image](https://github.com/user-attachments/assets/37a017fe-f67f-4895-934c-6732db39d327)
## Step-5 pushed the entire files to git repo
![Screenshot 2025-06-22 123417](https://github.com/user-attachments/assets/a439266f-617b-4ad2-9ac9-a7c58775129e)

## Step-6 initially not working and resolved 
![Screenshot (166)](https://github.com/user-attachments/assets/4b956cb6-9659-4bfe-92fe-98b6fcbf0e01)

-the error was the the cicd-pipeline.yml was saved as cicd-pipeline.yml.txt 
![Screenshot 2025-06-22 124129](https://github.com/user-attachments/assets/6fe10608-7434-41be-b55b-cfb4e6e52766)
- renamed to cicd-pipeline.yml
-initiallty it was like this app.listen(PORT, () => { which mean the app is listening to only the local host inside the container and  which cannot be accesed by the outside the EC2 instance even the port 3000 is  open so changed to app.listen(PORT, '0.0.0.0', () =>
![Screenshot (167)](https://github.com/user-attachments/assets/9ab48a2d-1898-4603-8f80-3d0794b366ea)
- although it was done but not able get the output in http://43.205.191.188:3000/ because
- added packages: write permission and included the docker/metadata-action@v5 to generate proper tags and labels.
- Used correct tag :main instead of :latest while pulling the image. using docker pull ghcr.io/sivanithink/containerize-deploy-to-ec2:main
- Generated a classic Personal Access Token (PAT) with write:packages, then logged in echo echo ghp_SlIJsCBNjJfUZ1Fxl0NyjHFkh7bf5O3rF*** | docker login ghcr.io -u Sivanithink --password-stdin
![Screenshot (170)](https://github.com/user-attachments/assets/352cfee4-5def-4ecc-84da-6d2a59cd28a1)
