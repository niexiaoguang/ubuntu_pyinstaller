FROM ubuntu:16.04
MAINTAINER Pampa Nie "nxg@lohosoft.com"

RUN rm /etc/apt/sources.list
COPY ./sources.list /etc/apt
RUN apt-get update
# for pyinstaller 
RUN apt-get install -y libc-bin binutils

RUN apt-get install -y gcc gdb binutils make git dstat sysstat htop curl wget libjpeg-dev net-tools libffi-dev bzip2 libssl-dev sqlite3 libsqlite3-dev

# RUN http_proxy='http://10.0.2.2:1087' curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

COPY ./install_pyenv /
RUN chmod +x ./install_pyenv
RUN ./install_pyenv

RUN echo 'export PATH="/root/.pyenv/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc
RUN echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

RUN /bin/bash -c "source ~/.bashrc"
RUN pyenv install 3.7.0 -v
RUN pyenv rehash
RUN pyenv versions
RUN pyenv global 3.7.0


# RUN ln -s /usr/local/bin/python3 /usr/bin/python3
# Install pycrypto so --key can be used with PyInstaller
RUN pip install pycrypto pyinstaller -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com


ARG USER_ID
ARG GROUP_ID

# update mark
RUN echo "2020031901" >> /dev/null

COPY requirements.txt /
RUN pip install -r /requirements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com

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