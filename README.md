
Today 1:17 PM

movie-picture-pipeline.zip
Zip Archive
see im getting this error here what should i change here ..

064d5bb9-dc18-478b-9bb1-1614d52355d1.png
c9dc04dd-3d81-4bc2-937e-9c35aba8881d.png
1d249b3b-6260-4f95-9c0e-d6ad48171b2a.png
see these are things i did

here why im getting access denied ..

see

help me to complete my project setup step by step one after another once i complete at present i stuck at..the stage shown in the image..

done with the old issue now we have new issue 


see this new issue

see this


see i fixed the account id issue 

{
    "Status": "CREATE_FAILED",
    "Health": {
        "issues": [
            {
                "code": "NodeCreationFailure",
                "message": "Unhealthy nodes in the kubernetes cluster",
                "resourceIds": [
                    "i-035089865e7d5de99"
                ]
            }
        ]
    },
    "Instances": [
        "t3.small"
    ],
    "Desired": 1
}
~ $ 

437ad773-2877-40d3-a94d-bc3026413ac0.png
fda8c140-2b03-48f4-93b7-8cacd9ba845e.png

see this

 $ kubectl get deployment backend -o yaml | grep -A3 -B3 IMAGE_PLACEHOLDER
  annotations:
    deployment.kubernetes.io/revision: "4"
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"name":"backend","namespace":"default"},"spec":{"replicas":1,"selector":{"matchLabels":{"app":"backend"}},"template":{"metadata":{"labels":{"app":"backend"}},"spec":{"containers":[{"command":["python","-m","flask","run","--host=0.0.0.0","--port=5000"],"image":"IMAGE_PLACEHOLDER","imagePullPolicy":"Always","name":"backend","ports":[{"containerPort":5000}]}]}}}}
  creationTimestamp: "2026-08-19T08:50:18Z"
  generation: 4
  name: backend
--
        - run
        - --host=0.0.0.0
        - --port=5000
        image: IMAGE_PLACEHOLDER
        imagePullPolicy: Always
        name: backend
        ports:
~ $ kubectl get deployment backend -o jsonpath='{.spec.template.spec.containers[0].image}{"\n"}'
IMAGE_PLACEHOLDER
~ $ 



success

see


what is this bullshit


movie-picture-pipeline(1).zip
Zip Archive
check this zip file and analyze and guide me step by step to succeeded in setting up my project as mentioned in as project rubric


nothing coming

Perfect. ✅ This is exactly what we wanted.

Your frontend container now has:

REACT_APP_MOVIE_API_URL=http://98.92.82.236:30647
So the frontend is configured to call your working backend NodePort.

Final verification
Open this in your browser:

Frontend URL:

http://98.92.82.236:32093
You should now see the movie list:

Top Gun: Maverick

Sonic the Hedgehog

A Quiet Place

If the movies appear, then your main application deployment is working end-to-end:

Browser
   ↓
Frontend NodePort :32093
   ↓
React frontend
   ↓
Backend NodePort :30647
   ↓
Flask /movies
   ↓
Movie data ✅
Also verify the backend one more time
You already proved this works:

http://98.92.82.236:30647/movies
That is your Backend API URL for the rubric.

What I want you to do now
Just open:

http://98.92.82.236:32093
If you see all 3 movies, send me a screenshot.

Then I'll give you the final rubric checklist, item-by-item, showing exactly what is ✅ completed and whether anything still needs fixing before submission.


62395634-5deb-4aeb-8eb6-94ee772c8929.png
backend url

Yes — that is expected. Your backend URL is:

http://98.92.82.236:30647
When you open the root / path, Flask returns:

404 Not Found

because your backend apparently does not have a / route.

Use the API endpoint instead
Open:

http://98.92.82.236:30647/movies
You should see:

{
  "movies": [
    {
      "id": "123",
      "title": "Top Gun: Maverick"
    },
    {
      "id": "456",
      "title": "Sonic the Hedgehog"
    },
    {
      "id": "789",
      "title": "A Quiet Place"
    }
  ]
}
You already proved this with curl, so your backend API is working. ✅

Your two URLs
Backend API:

http://98.92.82.236:30647/movies
Frontend:

http://98.92.82.236:32093
Don't worry about the 404 at the backend root. For your rubric, the important requirement is that the Backend API returns the list of movies, and /movies does exactly that.

Now open the frontend URL:

http://98.92.82.236:32093
and check whether the three movies appear.



README(1).md
File
change this ealme file into simple and clear way

Yes. I simplified the README substantially while keeping the important project information: application structure, local commands, CI/CD workflows, Kubernetes deployment, AWS/EKS setup, verification, GitHub Secrets, and cleanup. The original describes the frontend/backend structure and CI/CD deliverables in detail. 


Download the simplified README:

Download README_simple.md

I also kept the README aligned with your actual project rather than making it unnecessarily long. 


README_simple.md
Document


Library
/
README_simple.md


Movie Picture Pipeline
A simple CI/CD project for a Movie Picture application.

Frontend: React

Backend: Python Flask

Docker: Application containers

GitHub Actions: CI/CD

AWS ECR: Docker image registry

AWS EKS + Kubernetes: Deployment

Project Structure
movie-picture-pipeline/
├── .github/workflows/
│   ├── frontend-ci.yaml
│   ├── frontend-cd.yaml
│   ├── backend-ci.yaml
│   └── backend-cd.yaml
├── setup/
└── starter/
    ├── frontend/
    └── backend/
Application
The frontend displays movies from the Flask backend.

Backend API:

GET /movies
Example response:

{
  "movies": [
    {"id": "123", "title": "Top Gun: Maverick"},
    {"id": "456", "title": "Sonic the Hedgehog"},
    {"id": "789", "title": "A Quiet Place"}
  ]
}
Frontend
Run locally:

cd starter/frontend
npm ci
npm start
Build and run with Docker:

docker build --build-arg REACT_APP_MOVIE_API_URL=http://localhost:5000 -t mp-frontend:latest .
docker run -p 3000:3000 mp-frontend:latest
Open:

http://localhost:3000
Backend
Run locally:

cd starter/backend
pipenv install
pipenv run serve
Test the API:

curl http://localhost:5000/movies
Tests and Linting
Frontend
cd starter/frontend
npm ci
CI=true npm test
npm run lint
Backend
cd starter/backend
pipenv install
pipenv run test
pipenv run lint
GitHub Actions
Frontend CI — frontend-ci.yaml
Runs on pull requests to main

Can be run manually

Runs lint and tests in parallel

Builds only when lint and tests pass

Backend CI — backend-ci.yaml
Runs on pull requests to main

Can be run manually

Runs lint and tests in parallel

Builds only when lint and tests pass

Frontend CD — frontend-cd.yaml
Runs when frontend changes are pushed to main

Can be run manually

Runs lint and tests

Builds the Docker image with REACT_APP_MOVIE_API_URL

Pushes the image to Amazon ECR

Deploys to EKS

Backend CD — backend-cd.yaml
Runs when backend changes are pushed to main

Can be run manually

Runs lint and tests

Builds the Docker image

Pushes the image to Amazon ECR

Deploys to EKS

Docker images are tagged with the Git commit SHA.

Kubernetes
Manifests:

starter/frontend/k8s/
starter/backend/k8s/
Apply frontend:

cd starter/frontend/k8s
kustomize build | kubectl apply -f -
Apply backend:

cd starter/backend/k8s
kustomize build | kubectl apply -f -
Check the deployment:

kubectl get pods
kubectl get services
Verify the Application
Backend:

http://<BACKEND-IP>:<NODEPORT>/movies
Frontend:

http://<FRONTEND-IP>:<NODEPORT>
The backend /movies endpoint should return the movie list, and the frontend should display it.

AWS / EKS
Create the AWS infrastructure:

cd setup/terraform
terraform apply
View the Terraform outputs:

terraform output
Configure kubectl:

aws eks update-kubeconfig --name <CLUSTER_NAME> --region <AWS_REGION>
GitHub Secrets
AWS credentials must be stored in GitHub Secrets and must not be written directly in workflow files.

Required secrets:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_SESSION_TOKEN
Cleanup
AWS resources can cost money. When finished:

cd setup/terraform
terraform destroy
