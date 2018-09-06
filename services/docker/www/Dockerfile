FROM ubuntu:latest

# Install Flask app dependencies.
RUN apt-get update -y
RUN apt-get install -y libmysqlclient-dev build-essential python-dev python-pip ansible
RUN pip install flask flask-sqlalchemy mysql-python

# Install playbook and run it.
COPY playbook.yml /etc/ansible/playbook.yml
COPY index.py.j2 /etc/ansible/index.py.j2
COPY templates /etc/ansible/templates
RUN mkdir -m 755 /opt/www
RUN ansible-playbook /etc/ansible/playbook.yml --connection=local

EXPOSE 80
