# FROM python:3.7-slim
FROM ubuntu:18.04
MAINTAINER Pampa Nie "nxg@lohosoft.com"

RUN rm /etc/apt/sources.list
COPY ./sources.list /etc/apt
RUN apt-get update
RUN apt-get install -y libc-bin binutils
RUN apt install -y python3.7 python3-pip
# COPY ./get-pip.py /
# RUN python3.7 get-pip.py

# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# Install pycrypto so --key can be used with PyInstaller
RUN pip3 install pycrypto pyinstaller -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com


ARG USER_ID
ARG GROUP_ID

# update mark
RUN echo "2020031901" >> /dev/null

COPY requirements.txt /
RUN pip3 install -r /requirements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com

COPY src/ /app
WORKDIR /app

# Create a user group 
# RUN addgroup $GROUP_ID
 
# # Create a user under group
# RUN adduser -S -D -h /app $USER_ID $GROUP_ID

# # Chown all the files to the app user.
# RUN chown -R $USER_ID:$GROUP_ID /app

# # Switch to user
# USER $USER_ID

# Open the mapped port
#EXPOSE 3000

# This will generate the bundle in a subdirectory called dist.
RUN pyinstaller main.py --onefile

CMD [ "/bin/bash" ]

# CMD ["python3", "main.py"]