FROM centos:7

##安装python
RUN yum install python -y && yum -y install epel-release && yum install wget vim openssl-devel readline-devel python-devel python-pip -y   && wget https://www.python.org/ftp/python/3.5.3/Python-3.5.3.tar.xz &&    xz -d Python-3.5.3.tar.xz && tar xf Python-3.5.3.tar  && cd Python-3.5.3 && ./configure --prefix=/usr/local/python-3.5.3 --enable-optimizations && make -j 4 && make install && ln -sf /usr/local/python-3.5.3/bin/python3 /usr/bin/python3  && ln -sf /usr/local/python-3.5.3/bin/pip3 /usr/bin/pip3

##安装jupyter
##sha1:c1ebae9ce1b5:0c25328cd843b9f57b2043de1bb55f464d023939  [123456]
RUN pip install jupyter && mkdir -p /data/jupyter/ && jupyter-notebook --config=/data/jupyter/jupyter_notebook_config.py --generate-config && cd /data/jupyter/&& sed -i "s/#c.NotebookApp.ip = 'localhost'/c.NotebookApp.ip = '*'/" jupyter_notebook_config.py && sed -i "s%#c.NotebookApp.notebook_dir = u''%c.NotebookApp.notebook_dir = u'/data/jupyter'%g" jupyter_notebook_config.py&& sed -i "s/#c.NotebookApp.password = u''/c.NotebookApp.password = u'sha1:c1ebae9ce1b5:0c25328cd843b9f57b2043de1bb55f464d023939'/" jupyter_notebook_config.py

##配置Python3.5.3版本
RUN pip3 install ipykernel  && python3 -m ipykernel install --name python3 --display-name "Python3.5.3" && jupyter-kernelspec list

EXPOSE 8888

CMD jupyter-notebook