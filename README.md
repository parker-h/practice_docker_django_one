# practice_docker_django_one
practice using docker, github, and django

Without Docker Compose.yaml and working outside of the Container:
	1. Activate virtual env
		a. Python -m venv <name of virtual env>
	2. Activate virtual enviorment
		a. .\env\Scripts\activate
	3. Install Django into virtual enviorment
		a. Python -m pip install django
	4. Updragde pip in virtual envoirment
		a. python -m pip install --upgrade pip
	5. Create django project (creates project core)
		a. Django-admin startproject <name> . 
	6. Create "Dockerfile"
		a. Add:
			i. FROM - import image
				1) Python:3.8.2-slim-buster
			ii. WORKDIR - create work directory in image
				1) /app
			iii. COPY - copy requirements.txt into image files
				1) Requirements.txt /app/
			iv. RUN - install dependencies from requirements.txt
				1) Pip install -r requirements.txt 
			v. COPY - copy source code into working directory on image
				1) .  /app/
			vi. CMD - start app in container
				1) ["python3", "manage.py", "runserver", "0.0.0.:8000]
	7. Create .dockerignore
		a. Add you virtual enviorment folder and anything else you don’t want to add to container
	8. Build simple hello world app in django
		a. Create a views.py file in core project folder
		b. In urls.py add: 
			i. from . import views
		c. In urls.py in urlpatterns add:
			i. path('', views.home)
		d. In views add:
		
		from django.shortcuts import render
		
		def home(request):
		    return render(request, 'index.html')
		e. Create a templates folder, and inside that folder add an index.html
			i. Add <h1>whatever you want</h1> in index.html
		f. In settings add 'core' as an "INSTALLED_APPS"
		g. Check to see if it works with "python manage.py runserver"
		h. Generate a requirements.txt file
			i. Pip freeze > requirements.txt
		i. Now build your container
			i. Docker build --tag <name> . (the dot is to use the files in the working directory)
			ii. Use "docker image ls" to see you newly created image
			iii. Now run image and create container
				1) Docker run -p 8000:8000 <name>
					a)        host machine port
					b)        container port
![image](https://user-images.githubusercontent.com/91643406/135483589-2d24fc75-3141-45fd-be8f-7f7573715e46.png)
